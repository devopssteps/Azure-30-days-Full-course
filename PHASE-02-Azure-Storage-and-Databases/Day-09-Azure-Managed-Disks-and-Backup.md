## 1. Real disaster recovery scenario. 


> **"ধরুন আপনার Azure Virtual Machine-এ গুরুত্বপূর্ণ Data রয়েছে। হঠাৎ ভুল করে একটি গুরুত্বপূর্ণ File Delete হয়ে গেল, অথবা পুরো VM Crash করল। তখন কী করবেন? আজকের ভিডিওতে আমরা Azure Managed Disks, Snapshots এবং Azure Backup ব্যবহার করে একটি Virtual Machine Backup ও Restore করে দেখব—সম্পূর্ণ Hands-on Demo সহ।"**


```text
Azure VM
     │
     ▼
Managed Disk
     │
     ▼
Azure Backup
     │
     ▼
Recovery Services Vault
     │
     ▼
Restore VM
```

---

# 2. What is Azure Managed Disk?

Azure Managed Disk is a fully managed block storage service for Azure Virtual Machines.

Every Azure VM stores its operating system and data on managed disks.

---

# 3. Azure Managed Disk Architecture

```text
Azure VM
     │
     ▼
Managed Disk
     │
 ┌───┴────┐
 │         │
OS Disk  Data Disk
```

* OS Disk → Operating System
* Data Disk → Application Data

---

# 4. Types of Azure Managed Disks

| Disk Type      | Best Use Case                                  |
| -------------- | ---------------------------------------------- |
| Standard HDD   | Development/Test                               |
| Standard SSD   | Web Apps                                       |
| Premium SSD    | Production                                     |
| Premium SSD v2 | High-performance databases                     |
| Ultra Disk     | Mission-critical workloads with very high IOPS |


### Standard HDD

* Lowest cost
* Development

### Standard SSD

* Better performance
* General workloads

### Premium SSD

* Production
* Databases

### Premium SSD v2

* Improved performance and flexible provisioning

### Ultra Disk

* Very high IOPS
* Low latency

---

# 5. Snapshots

A Snapshot is a point-in-time copy of a managed disk.

```text
VM

↓

Managed Disk

↓

Snapshot
```

Example:

Before updating a server:

Take Snapshot

↓

Install Application

↓

If failure

↓

Restore Snapshot

---

# 6. Azure Backup

Azure Backup is a managed backup service.

Features:

* Automated backup
* Scheduled backup
* Restore
* Encryption
* Long-term retention

---

# 7. Recovery Services Vault

The Recovery Services Vault stores:

* VM Backups
* Recovery Points
* Backup Policies

Architecture:

```text
Azure VM
     │
     ▼
Azure Backup
     │
     ▼
Recovery Services Vault
```

---

# 🧪 Hands-on Demo

## Step 1

Azure Portal

↓

Virtual Machines

↓

Choose VM

Show:

* OS Disk
* Data Disk

---

## Step 2

Open Managed Disk

Explain:

* Size
* Type
* Encryption
* Performance

---

## Step 3

Create Snapshot

Disk

↓

Create Snapshot

Name:

```text
vm-before-update
```

Choose:

* Standard HDD (for demo cost savings)
* Same Region

Create.

---

## Step 4

Create Recovery Services Vault

Portal

↓

Recovery Services Vault

↓

Create

Choose:

* Subscription
* Resource Group
* Region

Deploy.

---

## Step 5

Enable Azure Backup

Recovery Vault

↓

Backup

Choose:

```text
Azure

Virtual Machine
```

Select:

Your VM

Create Backup Policy.

---

## Step 6

Backup Now

Click:

```text
Backup Now
```

Choose retention.

Start Backup.

```text
Backup Job

Running

↓

Completed
```

---

## Step 7

We can see how we get a Failure

SSH into the Linux VM.

Create a test file:

```bash
echo "Azure Backup Demo" > /home/azureuser/demo.txt
```

Verify:

```bash
cat /home/azureuser/demo.txt
```

Delete it:

```bash
rm /home/azureuser/demo.txt
```

"The file is gone. Now let's recover the VM from backup."

---

## Step 8

Restore VM

Recovery Services Vault

↓

Backup Items

↓

Virtual Machine

↓

Restore VM

Choose:

Latest Recovery Point

Restore.

The available restore options (e.g., create a new VM or restore disks, depending on the scenario).

---

## Step 9

Verify Recovery

SSH into the restored VM (or inspect the restored disks, depending on the restore option you used).

Show that the system has been restored to the selected recovery point and explain what was recovered.

---

# Azure CLI Demo

Login

```bash
az login
```

List disks

```bash
az disk list --output table
```

Create Snapshot

```bash
az snapshot create \
  --resource-group azure30days-rg \
  --source myVM_OsDisk \
  --name vm-snapshot-demo
```

List Snapshots

```bash
az snapshot list --output table
```

---

# Final Architecture

```text
Azure VM
     │
     ▼
Managed Disk
     │
     ├─────────────┐
     ▼             ▼
 Snapshot     Azure Backup
                    │
                    ▼
       Recovery Services Vault
                    │
                    ▼
              Restore Azure VM
```

---
