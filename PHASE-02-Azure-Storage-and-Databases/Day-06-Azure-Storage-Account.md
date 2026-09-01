# 1. What is Azure Storage?

Azure Storage is Microsoft's cloud storage service for storing structured and unstructured data securely and at scale.

Examples:

* Images
* Videos
* PDFs
* Logs
* Backups
* Virtual Machine disks
* Static websites

---

# 2. Storage Account

A Storage Account is the top-level container that provides a unique namespace for Azure Storage services.

Diagram:

```text
Azure Subscription
        │
        ▼
Resource Group
        │
        ▼
Storage Account
        │
 ┌──────┼───────────┐
 │      │           │
 ▼      ▼           ▼
Blob   Files      Queues
                (and more)
```

Storage Account can contain multiple storage services.

---

# 3. Storage Services

```text
Storage Account
│
├── Blob Storage
├── Azure Files
├── Queue Storage
├── Table Storage
└── Managed Disks
```

Blob Storage will be covered in the next lesson.

---

# 4. Storage Performance Tiers

### Standard

* HDD-based
* Low cost
* General purpose

### Premium

* SSD-based
* High performance
* Low latency

---

# 5. Access Tiers

### Hot

Frequently accessed data.

Examples:

* Website images
* Application files

---

### Cool

Occasionally accessed data.

Examples:

* Monthly reports
* Backups

---

### Archive

Rarely accessed data.

Examples:

* Compliance
* Old backups

Simple comparison:

| Tier    | Cost to Store | Access Speed | Retrieval Cost |
| ------- | ------------- | ------------ | -------------- |
| Hot     | Higher        | Fast         | Lower          |
| Cool    | Lower         | Fast         | Higher         |
| Archive | Lowest        | Slow         | Highest        |

---

# 6. Storage Redundancy

---

## LRS

```text
Datacenter

Disk A
Disk B
Disk C
```

Three copies within one data center.

Advantages:

* Lowest cost
* Protects against disk failures

---

## ZRS

```text
Zone 1
   │
Zone 2
   │
Zone 3
```

Three availability zones in the same region.

---

## GRS

```text
Primary Region
      │
      │ Replication
      ▼
Secondary Region
```

If an entire region fails, data exists in another Azure region.

---

## RA-GRS

Same as GRS, but the secondary region can also be used for read access.

```text
Primary Region
       │
       │
Secondary Region
       ▲
       │
 Read Access
```

---

# 7. When Should We Use Each?

| Redundancy | Best Use Case                         |
| ---------- | ------------------------------------- |
| LRS        | Development/Test                      |
| ZRS        | Production within one region          |
| GRS        | Disaster Recovery                     |
| RA-GRS     | High availability + Disaster Recovery |

This table makes the concept easy to remember.

---

# 🧪 Hands-on Demo

---

## Step 1

Azure Portal

↓

Storage Accounts

↓

Create

---

## Step 2

Choose:

* Subscription
* Resource Group
* Storage Account Name
* Region

Explain the naming rules.

---

## Step 3

Choose Performance

Show:

* Standard
* Premium

Choose **Standard** for the demo.

---

## Step 4

Choose Redundancy

Open the dropdown.

Explain every option before selecting one.

Choose **LRS** first.

---

## Step 5

Review + Create

Wait for deployment.

---

## Step 6

Explore Storage Account

Open:

* Overview
* Configuration
* Networking
* Data Protection
* Access Keys
* Shared Access Signatures (brief overview)
* Containers

---

## Step 7

Create a Blob Container

Example:

```text
images
```

Upload:

* image.jpg
* pdf.pdf

Explain that Blob Storage is inside the Storage Account.

---

## Step 8

Change Access Tier

Show:

Hot

↓

Cool

Explain when you would use each.

---

## Step 9

Monitor Storage

Open:

Monitoring

↓

Metrics

Show:

* Transactions
* Capacity
* Availability

---

# Azure CLI Demo

Login

```bash
az login
```

List subscriptions

```bash
az account list --output table
```

Create Storage Account

```bash
az storage account create \
  --name mystorageaccount12345 \
  --resource-group azure30days-rg \
  --location eastus \
  --sku Standard_LRS
```

Show details

```bash
az storage account show \
  --name mystorageaccount12345 \
  --resource-group azure30days-rg
```

List Storage Accounts

```bash
az storage account list --output table
```

Delete (optional cleanup)

```bash
az storage account delete \
  --name mystorageaccount12345 \
  --resource-group azure30days-rg \
  --yes
```

**Tip:** Remind viewers that the storage account name must be **globally unique**, use only lowercase letters and numbers, and typically be between **3 and 24 characters**.

---

# Final Architecture

```text
User
   │
   ▼
Storage Account
   │
   ├── Blob Storage
   ├── Azure Files
   ├── Queue Storage
   ├── Table Storage
   └── Managed Disks

Replication

LRS
ZRS
GRS
RA-GRS
```

---
