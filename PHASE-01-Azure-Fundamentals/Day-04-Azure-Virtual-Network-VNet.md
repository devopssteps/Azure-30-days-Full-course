# Azure Virtual Network (VNet) – Hands-On

---

# 1. What is VNet?

👉 **Virtual Network (VNet)** = your private network in Azure
👉 Equivalent of AWS VPC

💡 Used to:

* Isolate resources
* Control traffic
* Secure applications

---

# 2. CIDR (IP Addressing Basics)

👉 CIDR defines IP range of your network

Example:

```text
10.0.0.0/16
```

✔ Meaning:

* Total IPs ≈ 65,536

---

## Common CIDR Examples

| CIDR | IP Count |
| ---- | -------- |
| /16  | 65K      |
| /24  | 256      |
| /28  | 16       |

---

> “CIDR decides how big your network will be.”

---

# 3. Subnets

👉 Subnet = smaller network inside VNet

---

## Example:

* VNet: `10.0.0.0/16`
* Subnet1: `10.0.1.0/24` (Web)
* Subnet2: `10.0.2.0/24` (App)
* Subnet3: `10.0.3.0/24` (DB)

---

> “Subnets help us organize and secure different layers of application.”

---

# 4. HANDS-ON: Create VNet

Go to
**Microsoft Azure Portal**

---

## 🔹 Steps:

1. Search → **Virtual Networks**
2. Click **Create**

---

## Fill details:

* Name: `devops-vnet`
* Address space:

```text
10.0.0.0/16
```

---

## Add Subnets:

### Subnet 1:

* Name: `web-subnet`
* CIDR:

```text
10.0.1.0/24
```

---

### Subnet 2:

* Name: `app-subnet`
* CIDR:

```text
10.0.2.0/24
```

---

👉 Click **Create**

---

> “Now we have created a private network with multiple subnets.”

---

# 5. Deploy VM into Subnet

---

## Steps:

1. Go to **Virtual Machines**
2. Create VM
3. Select:

   * VNet: `devops-vnet`
   * Subnet: `web-subnet`

---

👉 This VM is now inside your private network

---

# 6. Architecture (Real DevOps Design)

---

## 3-Tier Architecture

```
Internet
   ↓
Public Subnet (Web)
   ↓
Private Subnet (App)
   ↓
Private Subnet (DB)
```

---

> “This architecture is used in real production environments.”

---

# 7. Security (Quick Mention)

👉 Use NSG:

* Allow HTTP (80)
* Allow SSH (22)

---

# Summary

 - ✔ VNet = private network
 - ✔ CIDR = IP range
 - ✔ Subnet = network segmentation
 - ✔ Architecture = secure design

---
> “Azure VNet is the backbone of secure and scalable cloud architecture.”

---
