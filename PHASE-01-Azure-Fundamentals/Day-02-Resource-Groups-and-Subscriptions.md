# Day 2: Azure Resource Groups & Subscriptions

![Resource and Subscription](https://github.com/devopssteps/Azure-30-days-Full-course/blob/main/PHASE-01-Azure-Fundamentals/azure_hierarchy_structure.jpg) 

# 1. Real-World Example

### 🏢 Think of Azure like a large company

```text
Microsoft Azure
       │
       ▼
Management Group
       │
       ▼
Azure Subscription
       │
       ▼
Resource Group
       │
       ├── VM
       ├── Storage Account
       ├── Database
       ├── VNet
       └── Public IP
```
---

# 2. What Is an Azure Resource?

Start from the bottom because it is easiest to understand.

An **Azure Resource** is an individual service or component that you create and manage in Azure.

Examples:

* Virtual Machine
* Storage Account
* Virtual Network
* Azure SQL Database
* Public IP
* Network Interface
* Key Vault
* App Service

For example:

```text
Resource Group: Production-RG
       │
       ├── Web-VM
       ├── Production-VNet
       ├── Production-Storage
       ├── Production-SQL
       └── Production-KeyVault
```

> "এই প্রতিটি individual component হলো Azure Resource."

### Important concept

Resources are created inside a **Resource Group**.

---

# 3. What Is a Resource Group?

An **Azure Resource Group** is a logical container used to organize and manage related Azure resources.

For example:

```text
Production-RG
│
├── Web Server VM
├── Database
├── Storage
├── VNet
└── Key Vault
```

You can also organize resources by application:

```text
Ecommerce-App-RG
│
├── Frontend
├── Backend
├── Database
└── Storage
```

Or by environment:

```text
Dev-RG
Test-RG
Staging-RG
Production-RG
```

### Important point

A Resource Group is **not a physical server or data center**.

It is a **logical management boundary**.

---

# 4. What Is an Azure Subscription?

An Azure Subscription is a **billing and management boundary** for Azure resources.

A subscription is associated with:

* Billing
* Costs
* Resource limits
* Access control
* Resource management

Example:

```text
Company
│
├── Production Subscription
│      └── Production Resources
│
├── Development Subscription
│      └── Development Resources
│
└── Testing Subscription
       └── Testing Resources
```

> "একটি Organization-এর business requirement অনুযায়ী একাধিক Azure Subscription থাকতে পারে। যেমন Production-এর জন্য একটি Subscription এবং Development-এর জন্য আরেকটি Subscription."

---

# 5. Management Groups

Management Groups allow you to organize multiple Azure subscriptions.

Example:

```text
Management Group
│
├── Production Subscription
│
├── Development Subscription
│
├── Testing Subscription
│
└── Security Subscription
```

This becomes especially useful for **large organizations**.

For example, you can apply Azure policies and governance at the Management Group level.

---

# 6. Azure Hierarchy — VERY IMPORTANT

```text
Microsoft Entra Tenant
        │
        ▼
Management Groups
        │
        ▼
Subscriptions
        │
        ▼
Resource Groups
        │
        ▼
Resources
```

### Level 1 — Tenant: Your Microsoft Entra ID / Azure identity boundary.

### Level 2 — Management Group: Used to organize multiple subscriptions.

### Level 3 — Subscription: Billing and management boundary.

### Level 4 — Resource Group: Logical container for related resources.

### Level 5 — Resources: Actual Azure services.

> **"Management Groups organize Subscriptions, Subscriptions contain Resource Groups, and Resource Groups contain Resources."**


---

# 7. Azure Portal vs Azure CLI

## Azure Portal

Graphical User Interface.

You can:

* Create resources
* Configure resources
* View billing
* Manage users
* Monitor resources

Good for beginners and visual management.

---

## Azure CLI

Command-line interface.

Example:

```bash
az login
```

List subscriptions:

```bash
az account list --output table
```

Show current subscription:

```bash
az account show --output table
```

List Resource Groups:

```bash
az group list --output table
```

Create Resource Group:

```bash
az group create \
  --name demo-rg \
  --location eastus
```

Delete Resource Group:

```bash
az group delete \
  --name demo-rg \
  --yes
```

> "Production environment এবং automation-এর ক্ষেত্রে CLI খুবই গুরুত্বপূর্ণ, কারণ আমরা command line এবং scripts ব্যবহার করে infrastructure manage করতে পারি।"

We can access azure by the following way:

* Azure Portal
* Azure CLI
* Azure PowerShell
* ARM/Bicep
* Terraform

We will cover **Terraform later in the course**.

---

# 🧪 8. HANDS-ON LAB — Create Resource Group Using Portal

Now start the practical demonstration.

Go to:

**Azure Portal → Resource Groups → Create**

Choose:

### Subscription

Select your Azure subscription.

### Resource Group

Enter:

```text
azure30days-rg
```

### Region

For example:

```text
East US
```

Then:

**Review + Create → Create**

> "আমরা এখন একটি Resource Group তৈরি করেছি। এখন এই Resource Group-এর ভিতরে বিভিন্ন Azure Resources তৈরি করতে পারব।"

---

# 🧪 9. Create Resource Group Using Azure CLI

Open **Azure Cloud Shell** or your local terminal.

Login:

```bash
az login
```

Check subscriptions:

```bash
az account list --output table
```

Set the correct subscription if you have multiple subscriptions:

```bash
az account set --subscription "YOUR_SUBSCRIPTION_NAME"
```

Create Resource Group:

```bash
az group create \
  --name azure30days-cli-rg \
  --location eastus
```

Verify:

```bash
az group show \
  --name azure30days-cli-rg
```

List all Resource Groups:

```bash
az group list --output table
```

---

# 🧪 10. Create an Azure Resource Inside Resource Group

Now create a simple Storage Account.

First, create a unique storage account name.

Example:

```text
azure30daysstorage123
```

Storage Account names must be globally unique and generally use lowercase letters and numbers.

Command:

```bash
az storage account create \
  --name azure30daysstorage123 \
  --resource-group azure30days-cli-rg \
  --location eastus \
  --sku Standard_LRS
```

Verify:

```bash
az storage account show \
  --name azure30daysstorage123 \
  --resource-group azure30days-cli-rg
```

Now explain:

```text
Subscription
     │
     ▼
azure30days-cli-rg
     │
     ▼
Storage Account
```

This gives your viewers a real understanding of the relationship between:

**Subscription → Resource Group → Resource**

---

# 🧪 11. Delete Resources

Now demonstrate Azure resource lifecycle.

You can delete only the Storage Account:

```bash
az storage account delete \
  --name azure30daysstorage123 \
  --resource-group azure30days-cli-rg \
  --yes
```

Or delete the entire Resource Group:

```bash
az group delete \
  --name azure30days-cli-rg \
  --yes
```

### Important warning

> "Resource Group delete করলে সাধারণত Resource Group-এর ভিতরের resources-গুলোও delete হয়ে যাবে। তাই Production environment-এ এই command খুব সাবধানে ব্যবহার করতে হবে।"

---

# 💰 12. Azure Cost Management

Now introduce cost management.

Go to:

**Azure Portal → Cost Management + Billing**

* Cost analysis
* Budgets
* Cost alerts
* Billing scope
* Spending monitoring

**Cost Management → Cost Analysis**

> "Cloud শেখার সময় cost management খুব গুরুত্বপূর্ণ। কারণ resource create করলে usage অনুযায়ী charge হতে পারে।"

**Cost Management → Budgets → Create**

Set:

* Subscription
* Budget amount
* Alert threshold
* Email notification

### Practical advice

> "Azure Free Account ব্যবহার করলেও সব resources সবসময় free নয়। তাই কোনো lab শেষ হলে unnecessary resources delete করে দিন এবং Cost Management regularly check করুন।"

---

# Final Practical Architecture

```text
Azure
│
└── Subscription
      │
      ├── azure30days-rg
      │       │
      │       ├── Storage Account
      │       ├── VM
      │       └── VNet
      │
      └── another-rg
              │
              └── Other Resources
```

> "আজকে আমরা Azure-এর hierarchy বুঝলাম এবং Portal ও Azure CLI ব্যবহার করে Resource Group তৈরি করলাম। এরপর Resource Group-এর ভিতরে Azure Resource তৈরি করলাম এবং সবশেষে Resource delete করা ও Cost Management সম্পর্কে জানলাম।"

---

