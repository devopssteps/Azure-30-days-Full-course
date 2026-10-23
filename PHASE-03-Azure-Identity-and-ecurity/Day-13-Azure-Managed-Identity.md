# Day-13: Azure Managed Identity

### In this video we will learn the following topics
 * What is Managed Identity?
 * Why Avoid Access Keys?
 * Two Types of Managed Identity
 * User-Assigned Managed Identity
 * How Managed Identity Actually Works
 * HANDS-ON DEMO

### # 1️⃣ What is Managed Identity?
**Managed Identity allows an Azure resource to authenticate to supported Azure services without you having to manage credentials such as passwords, secrets, or storage access keys.**

Example:

```text
Traditional Approach

VM
 │
 ├── Storage Account Name
 ├── Access Key
 └── Password/Secret
          │
          ▼
       Storage
```

Problem:

* Credentials must be stored somewhere.
* Credentials can accidentally be exposed.
* Keys need rotation.
* Developers have to manage secrets.

With Managed Identity:

```text
Azure VM
    │
    ▼
Managed Identity
    │
    ▼
Microsoft Entra ID
    │
    ▼
Access Token
    │
    ▼
Azure Storage
```

No application-managed storage key is required for the demo.

---

# 2️⃣ Why Avoid Access Keys?

This is an important issue for secure our service.

Suppose you write:

```bash
export AZURE_STORAGE_KEY="xxxxxxxxxxxxxxxx"
```

Now you have a secret sitting in your environment.

Potential problems:

```text
Developer
   ↓
Secret
   ↓
Code / Environment / Pipeline
   ↓
Possible Exposure
```

With Managed Identity:

```text
VM
 ↓
Identity
 ↓
Token
 ↓
Storage
```

The Azure platform manages the identity credentials.

### Important clarification Of manage identity

> **"You don't have to create, store, or manage the credentials yourself; Azure handles the identity credentials and token acquisition."**

---

# 3️⃣ Two Types of Managed Identity

Azure has two major types.

## System-Assigned Managed Identity

The identity is tied to the Azure resource.

```text
VM
 │
 └── System-Assigned Identity
```

If you delete the VM, the system-assigned identity is also deleted.

### Good for:

* One specific VM
* One application
* Simple deployments

---
# 4️⃣ User-Assigned Managed Identity

This is an independent Azure resource.

```text
             User-Assigned Identity
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
         VM1       VM2       VM3
```

You can assign the same identity to multiple Azure resources.

### Good for:

* Multiple VMs
* Multiple applications
* Reusable identity
* Larger environments

---

# System vs User Assigned

| Feature                 | System-Assigned  | User-Assigned |
| ----------------------- | ---------------- | ------------- |
| Lifecycle               | Tied to resource | Independent   |
| Reusable                | ❌                | ✅             |
| Multiple resources      | Generally no     | ✅             |
| Deleted with resource   | ✅                | ❌             |
| Separate Azure resource | ❌                | ✅             |

# 5️⃣ How Managed Identity Actually Works

This is the architecture I recommend showing on screen:

```text
                  Azure VM
                     │
                     │
              Managed Identity
                     │
                     ▼
             Microsoft Entra ID
                     │
              Authentication
                     │
                     ▼
               Access Token
                     │
                     ▼
               Azure Storage
                     │
              Authorization
                     │
                     ▼
              Storage Data
```

Explanation:

### Authentication

**Who is this?**

Microsoft Entra ID establishes the identity.

### Authorization

**What can this identity do?**

Azure RBAC determines what the identity is allowed to do.

---

# 🧪 HANDS-ON DEMO

## Demo Architecture

```text
Azure VM
Ubuntu Linux
    │
    │ System-Assigned
    │ Managed Identity
    ▼
Microsoft Entra ID
    │
    │ RBAC
    ▼
Storage Account
    │
    ▼
Blob Container
```

Goal:

> **VM reads a Blob from Azure Storage without using a Storage Account access key.**

---

# Step 1 — Create Storage Account

Azure Portal:

```text
Storage Accounts
       ↓
Create
```

Example:

```text
Storage Account:
azuredemostorageXXXX
```

Choose:

* Subscription
* Resource Group
* Region
* Standard performance
* Locally redundant storage (for a simple demo)

Create the Storage Account.

---

# Step 2 — Create Blob Container

Open:

```text
Storage Account
      ↓
Data storage
      ↓
Containers
      ↓
+ Container
```

Create:

```text
managedidentity-demo
```

Keep public access disabled.

This is important because we want to demonstrate **identity-based private access**.

---

# Step 3 — Upload a Test File

Upload:

```text
demo.txt
```

Contents:

```text
Hello from Azure Managed Identity!
```

Your architecture is now:

```text
Storage Account
      │
      ▼
Container
      │
      ▼
demo.txt
```

---

# Step 4 — Create Azure VM

Create an Ubuntu Linux VM.

For Our demo, a small B-series VM is sufficient **if that SKU is available for your subscription and region**.

After deployment:

```text
Virtual Machine
       ↓
Identity
```

---

# Step 5 — Enable System-Assigned Identity

Go to:

```text
VM
 ↓
Identity
 ↓
System assigned
 ↓
Status: ON
 ↓
Save
```

Azure creates an identity associated with the VM.

Show viewers:

```text
System assigned identity
Status: ON

Object ID: xxxxxxxx
```

This is a very important moment in the demo.

---

# Step 6 — Give the VM Permission

Now connect Managed Identity with RBAC.

Go to:

```text
Storage Account
      ↓
Access Control (IAM)
      ↓
Add role assignment
```

Choose an appropriate **data-plane storage role** for your demonstration.

For example, if the VM only needs to read blobs:

```text
Storage Blob Data Reader
```

Then:

```text
Assign access to:
Managed identity

Select:
Your VM

Review + Assign
```

Our architecture becomes:

```text
VM
 │
 │ Managed Identity
 ▼
Entra ID
 │
 │ Storage Blob Data Reader
 ▼
Storage Account
 │
 ▼
Blob
```

### ⚠️ Important 

Don't use the generic **Reader** role for this demonstration and expect it to read blob contents.

The generic Reader role allows management-plane visibility, while **Storage Blob Data Reader** is a data-plane role designed to read blob data.

---

# Step 7 — Connect to the VM

SSH:

```bash
ssh azureuser@<VM-PUBLIC-IP>
```

> "এখন আমরা VM-এর ভিতরে আছি। লক্ষ্য করুন, এখানে কোনো Storage Account Access Key নেই।"

---

# Step 8 — Install Azure CLI

If necessary:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Check:

```bash
az --version
```

---

# Step 9 — Login Using Managed Identity

Run:

```bash
az login --identity
```

You should see the VM authenticate using its Managed Identity.

```text
No username
No password
No storage access key
```

The VM is using its Azure-managed identity.

---

# Step 10 — Get the Storage Account

You can use:

```bash
az storage account show \
  --name <storage-account-name> \
  --resource-group <resource-group-name>
```

---

# Step 11 — Read the Blob Without Access Key

Use Azure CLI with identity-based authorization.

For example:

```bash
az storage blob download \
  --account-name <storage-account-name> \
  --container-name managedidentity-demo \
  --name demo.txt \
  --file demo-downloaded.txt \
  --auth-mode login
```

Then:

```bash
cat demo-downloaded.txt
```

Expected:

```text
Hello from Azure Managed Identity!
```

🎉 **This is the main result you want viewers to see.**

---

# 🔥 Show This on Screen

Immediately after the successful command:

```text
                 SUCCESS!
                     ✅

Azure VM
   │
   │ Managed Identity
   ▼
Microsoft Entra ID
   │
   │ RBAC Permission
   ▼
Azure Storage
   │
   ▼
demo.txt

NO ACCESS KEY
NO PASSWORD
NO SECRET
```

---

# 🧪 Step 12 — Prove the Permission 

remove the:

**Storage Blob Data Reader**

role assignment.

Then run the same command again.

It should fail because the identity no longer has the necessary data-plane permission.

Then add the role back and run the command again.

```text
Permission Removed
       ↓
Access Denied ❌

Permission Added
       ↓
Access Granted ✅
```

This demonstrates the difference between:

**Authentication → Identity**

and

**Authorization → Permission**

---










