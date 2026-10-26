# Day-14: Azure Key Vault

This video will cover the following topics:
 * Key vault Architecture
 * What is Azure Key Vault?
 * What are Secrets?
 * What are Keys?
 * What are Certificates?
 * Why Not Store Secrets in Code?
 * Key Vault Security
 * Managed Identity + Key Vault
 * HANDS-ON DEMO

## Architecture:

```text
        Azure VM
            │
            │ Managed Identity
            ▼
     Microsoft Entra ID
            │
            │ Authorization
            ▼
       Azure Key Vault
            │
            ▼
          Secret
```


---
# 1️⃣ What is Azure Key Vault?

**Azure Key Vault is a cloud service for securely storing and controlling access to sensitive information such as secrets, cryptographic keys, and certificates.**

Examples:

```text
Azure Key Vault
      │
 ┌────┼─────────┐
 ▼    ▼         ▼
Secrets Keys  Certificates
```

---
# 2️⃣ What are Secrets?

A **secret** can contain sensitive information such as:

* Database passwords
* API keys
* Application secrets
* Connection strings
* Tokens

Example:

```text
DatabasePassword
    ↓
MySuperSecretPassword
```
---

# 3️⃣ What are Keys?

Keys are used for cryptographic operations.

The Key Vault can manage cryptographic keys used for things such as:

* Encryption
* Signing
* Key management

For beginners:

> **Secret = Sensitive value**

> **Key = Cryptographic key**

---

# 4️⃣ What are Certificates?

Certificates are used for things such as:

* TLS/SSL
* Application authentication
* Secure communications

Architecture:

```text
Key Vault
 │
 ├── Secrets
 ├── Keys
 └── Certificates
```

---

# 5️⃣ Why Not Store Secrets in Code?

This is a bad practice:

```text
Application
   │
   ▼
config.py

DB_PASSWORD="MyPassword123"
```

Problems:

❌ Secret can leak into Git

❌ Developers may see production credentials

❌ Difficult to rotate

❌ Credentials can appear in logs/configuration

Instead:

```text
Application
    │
    ▼
Managed Identity
    │
    ▼
Key Vault
    │
    ▼
Secret
```

---

# 6️⃣ Key Vault Security

The main security concepts:

### Authentication

**Who is requesting access?**

Microsoft Entra ID identifies the user/workload.

### Authorization

**What is that identity allowed to do?**

Azure RBAC 

---

# 7️⃣ Managed Identity + Key Vault

We learn this connects from our previous lesson.

our previous video:

**Managed Identity**

Now:

**Managed Identity + Key Vault**

Architecture:

```text
                 Azure VM
                    │
                    │
             Managed Identity
                    │
                    ▼
             Microsoft Entra ID
                    │
                    │ Authentication
                    ▼
               Azure Key Vault
                    │
                    │ Authorization
                    ▼
                  Secret
```

> **Managed Identity tells Azure who the VM is.**

> **RBAC tells Azure what the VM can access.**

> **Key Vault stores the sensitive value.**

This is a very important lesson.

---

# 🧪 HANDS-ON DEMO

## Goal

Our final demo should look like:

```text
Azure VM
   │
   │ Managed Identity
   ▼
Microsoft Entra ID
   │
   │ Key Vault Secrets User
   ▼
Azure Key Vault
   │
   ▼
Demo Secret
```
The VM retrieves the secret without having a Key Vault password or access key stored inside it.

---

# Step 1 — Create Key Vault

Azure Portal:

```text
Azure Portal
    ↓
Key Vaults
    ↓
Create
```

Example:

```text
Key Vault Name:

azure-demo-kv-XXXX
```

Choose:

* Subscription
* Resource Group
* Region
* Appropriate pricing tier

For this demo, we use the simplest configuration.

---

# Step 2 — Configure Access Model

During creation, use the **Azure role-based access control (RBAC)** authorization model.

```text
Key Vault
    │
    ▼
Access Control (IAM)
    │
    ▼
Azure RBAC
```

---
# Step 3 — Create a Secret

Open:

```text
Key Vault
   ↓
Objects
   ↓
Secrets
   ↓
Generate/Import
```

Create:

```text
Name:

DemoPassword
```

Value:

```text
DemoPassword-123!
```

---

# Step 4 — Create/Use Your Azure VM

We Use the VM from our previous Managed Identity demo.

Open:

```text
VM
 ↓
Identity
 ↓
System Assigned
 ↓
Status: On
```

If it's OFF:

```text
Status → ON
Save
```

---

# Step 5 — Give VM Permission to Read Secrets

Go to:

```text
Key Vault
    ↓
Access Control (IAM)
    ↓
Add Role Assignment
```

Select:

**Key Vault Secrets User**

Then:

```text
Assign access to:
Managed identity

Select:
Virtual Machine

Your VM
```

Then:

**Review + Assign**

---
# Step 6 — SSH Into VM

```bash
ssh azureuser@<VM-PUBLIC-IP>
```

> "Notice that we haven't copied the Key Vault secret or a Key Vault password into this VM."

---

# Step 7 — Install Azure CLI

If necessary:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Verify:

```bash
az --version
```

---
# Step 8 — Authenticate Using Managed Identity

Run:

```bash
az login --identity
```

The VM authenticates using its Managed Identity.

No username/password is required for the Azure CLI login.

---
# Step 9 — Retrieve the Secret

Run:

```bash
az keyvault secret show \
  --vault-name <KEY-VAULT-NAME> \
  --name DemoPassword \
  --query value \
  --output tsv
```

We should see:

```text
DemoPassword-123!
```

**This is the main moment of this demo.**

Immediately show:

```text
VM
 │
 │ Managed Identity
 ▼
Microsoft Entra ID
 │
 │ RBAC
 ▼
Azure Key Vault
 │
 ▼
DemoPassword
```

> **"আমরা VM-এর মধ্যে কোনো Key Vault password বা access key রাখিনি। VM তার Managed Identity ব্যবহার করে Key Vault থেকে Secret retrieve করেছে।"**

---
# 🔥 Step 10 — Prove RBAC Is Working

Remove the:

**Key Vault Secrets User**

role assignment.

Then run:

```bash
az keyvault secret show \
  --vault-name <KEY-VAULT-NAME> \
  --name DemoPassword \
  --query value \
  --output tsv
```

The request should fail because the VM no longer has the required permission.

Now add:

**Key Vault Secrets User**

again.

Run the command.

It should work again.

now we will see:

```text
Permission Removed
       ↓
Access Denied ❌

Permission Added
       ↓
Secret Retrieved ✅
```

This demonstrates the complete relationship between:

**Managed Identity + Microsoft Entra ID + RBAC + Key Vault**

---
# 🧠 Authentication vs Authorization

```text
VM
 │
 ▼
Managed Identity
 │
 ▼
Microsoft Entra ID
 │
 │
 │ Authentication
 ▼
"Who are you?"
 │
 ▼
RBAC
 │
 │ Authorization
 ▼
"What can you access?"
 │
 ▼
Key Vault Secret
```

---
# Azure CLI Commands

List Key Vaults:

```bash
az keyvault list --output table
```

List secrets:

```bash
az keyvault secret list \
  --vault-name <KEY-VAULT-NAME> \
  --output table
```

Retrieve secret:

```bash
az keyvault secret show \
  --vault-name <KEY-VAULT-NAME> \
  --name DemoPassword
```

```bash
--query value --output tsv
```

so the output clearly shows the secret value.

---

# 🏗️ Final Architecture of this demo

```text
                    Azure VM
                       │
                       │
               System-Assigned
               Managed Identity
                       │
                       ▼
               Microsoft Entra ID
                       │
                       │ Authentication
                       ▼
                  Azure RBAC
                       │
              Key Vault Secrets User
                       │
                       ▼
                 Azure Key Vault
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
          Secrets     Keys    Certificates
             │
             ▼
       Database Password
```

---


