# Day 5 — Azure Networking Deep Dive

---


## 1. Network working concepts 

```text
Internet
   ↓
NSG
   ↓
Azure VM
   ↓
SSH / RDP
```

---

# 2. What Is a Network Security Group?

**NSG** is used to control network traffic to and from Azure resources.

Introduce:

* Inbound security rules
* Outbound security rules
* Source
* Destination
* Port
* Protocol
* Action
* Priority

Explain the basic concept:

```text
Internet
   │
   │ Incoming Traffic
   ▼
┌──────────────┐
│     NSG      │
│ Allow / Deny │
└──────┬───────┘
       │
       ▼
   Azure VM
```
NSG rules are evaluated based on **priority**, with a lower numerical priority evaluated before a higher numerical priority.

---

# 3. Inbound Rules

> **Inbound = Traffic coming INTO your Azure resource.**

Example:

```text
Internet
    │
    ├── TCP 22 ──→ SSH
    │
    ├── TCP 80 ──→ HTTP
    │
    └── TCP 443 ─→ HTTPS
```

Examples:

| Port | Protocol | Purpose |
| ---- | -------- | ------- |
| 22   | TCP      | SSH     |
| 80   | TCP      | HTTP    |
| 443  | TCP      | HTTPS   |
| 3389 | TCP      | RDP     |

You should **not blindly open every port to the Internet**.

For example, instead of:

```text
Source: Any
Port: 22
Action: Allow
```

a safer approach is to restrict SSH access to a known source IP when appropriate.

---

# 4. Outbound Rules

> **Outbound = Traffic leaving your Azure resource.**

Example:

```text
Azure VM
   │
   ├──→ Internet
   │
   ├──→ Database
   │
   └──→ Other Azure Services
```
outbound rules control traffic leaving the resource or network interface/subnet where the NSG is associated.

simple example:

```text
VM → Internet → Allow
VM → Database → Allow
VM → Unwanted Destination → Deny
```

---

# 5. NSG Association

An NSG can be associated with:

* Subnet
* Network Interface (NIC)

```text
VNet
│
├── Subnet
│     │
│     └── NSG
│
└── VM
      │
      └── NIC
            │
            └── NSG
```

**NSG rules can apply at different points in the network path**.

---

# 6. Application Security Groups (ASG)

An Azure Application Security Group (ASG) is a logical object used to group virtual machines (VMs) based on their application function or role, rather than their IP addresses.
Instead of writing Network Security Group (NSG) rules that explicitly list individual IP addresses, you assign VMs to an ASG and then use that ASG as the source or destination in your NSG rules.
## Why ASGs Matter (The Problem They Solve)
Without ASGs, if you have a web application with three web servers, your database security rule in an NSG would look like this:

* Allow Traffic from: 10.0.0.4, 10.0.0.5, 10.0.0.6 to Database

If you scale up your application and add a fourth web server (10.0.0.7), you have to manually update the NSG rule to include the new IP address. This is tedious and prone to human error.
With ASGs, you create an ASG called AsgWebServers. You attach all web VMs to it. Your NSG rule becomes:

* Allow Traffic from: AsgWebServers to Database

When you add a new web server, you simply label it as part of AsgWebServers. The security rule automatically applies to it without you touching the NSG.

Suppose you have:

```text
Web Servers
Web-VM1
Web-VM2
Web-VM3

Database Servers
DB-VM1
DB-VM2
```

Instead of managing individual IP addresses in NSG rules, you can logically group NICs using **Application Security Groups**.

Conceptually:

```text
ASG-Web
   │
   ├── Web-VM1
   ├── Web-VM2
   └── Web-VM3

ASG-DB
   │
   ├── DB-VM1
   └── DB-VM2
```

Then your security policy can express the intended application relationship, such as:

```text
ASG-Web
    │
    │ Allow required application traffic
    ▼
ASG-DB
```

why ASGs are useful in larger environments.

---

# 7. Public vs Private Access

This is a critical concept.

### Public Access

```text
Internet
   ↓
Public IP
   ↓
Azure VM
```

The resource is reachable through a public endpoint, subject to security controls.

### Private Access

```text
Azure VNet
   ↓
Private IP
   ↓
Azure VM
```

The resource is accessed privately within the Azure network or through connected networks.

> "যতটা সম্ভব sensitive resources-কে public Internet থেকে directly expose না করে private networking ব্যবহার করা ভালো।"

* Private IP
* Public IP
* Private access
* Public access

---

# 8. Azure Bastion

Azure Bastion as a secure management option.

Concept:

```text
Your Browser
      │
      ▼
Azure Portal
      │
      ▼
Azure Bastion
      │
      ▼
Private IP
      │
      ▼
Azure VM
```

> "Azure Bastion ব্যবহার করলে Azure Portal থেকে browser-based SSH বা RDP connection করা যায়, এবং VM-এর জন্য direct public IP ব্যবহার করার প্রয়োজন কমে যায়।"

### Without Bastion

```text
Internet
   ↓
Public IP
   ↓
VM
```

### With Bastion

```text
Browser
   ↓
Azure Bastion
   ↓
Private IP
   ↓
VM
```

---

# HANDS-ON DEMO — Secure an Azure VM Using NSG

## Step 1 — Create a VM

```text
Azure Portal
   ↓
Virtual Machines
   ↓
Your VM
   ↓
Networking
```

Identify:

* Public IP
* Private IP
* NIC
* NSG
* Inbound port rules

---

## Step 2 — Review Existing NSG Rules

Open the NSG and show:

* Inbound rules
* Outbound rules
* Priority
* Source
* Destination
* Service
* Action

---

## Step 3 — Create an Inbound Rule

For example, if your VM is running a web server, create:

```text
Source: Internet
Destination: VM
Protocol: TCP
Destination Port: 80
Action: Allow
Priority: 100
```

Then test:

```text
Browser
   ↓
Public IP
   ↓
Port 80
   ↓
Azure VM
```

If the web server is running, viewers should see the website.

---

## Step 4 — Demonstrate SSH Security

If you need SSH access:

```text
Port: 22
Protocol: TCP
```

Instead of allowing SSH from everywhere, we should allow only trusted IP range like our office or home pc.

For example:

```text
Source:
My IP Address
```

rather than:

```text
Any
```

---

## Step 5 — Demonstrate Deny Behavior

Create a rule that blocks a test port.

For example:

```text
Port: 8080
Action: Deny
```

test the connection.

> "এখন NSG rule-এর কারণে traffic blocked হবে।"

---

## Step 6 — Demonstrate Azure Bastion

```text
Azure Portal
    ↓
Bastion
    ↓
Connect
    ↓
SSH / RDP
    ↓
VM Private IP
```

you can manage the VM without relying on a direct public IP connection.

---

# Final Hands-On Architecture

```text
                  Internet
                     │
                     ▼
              ┌─────────────┐
              │     NSG     │
              │             │
              │ Inbound     │
              │ Outbound    │
              └──────┬──────┘
                     │
                     ▼
              Azure Virtual
                 Network
                     │
                ┌────┴────┐
                │         │
                ▼         ▼
             Subnet     Subnet
                │
                ▼
             Azure VM
                │
                ▼
              Private IP

```

> **"আজ আমরা Azure Networking-এর একটি গুরুত্বপূর্ণ অংশ শিখলাম। আমরা NSG ব্যবহার করে inbound এবং outbound traffic control করলাম, ASG সম্পর্কে জানলাম, public এবং private access বুঝলাম এবং Azure Bastion ব্যবহার করে কীভাবে secure VM management করা যায় সেটাও দেখলাম।"**

---
