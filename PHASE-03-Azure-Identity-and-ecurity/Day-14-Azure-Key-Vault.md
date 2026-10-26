# Day-14: Azure Key Vault

This video will cover the following topics:
 * Key vault Architecture
 * What is Azure Key Vault?
 * 

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



