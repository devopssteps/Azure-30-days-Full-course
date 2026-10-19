
# Day 11 — Azure RBAC Explained

In todays video we will learn the following topics.
 * What is Azure RBAC?
 * RBAC Architecture
 * What is a Role?
 * Owner
 * Contributor
 * Reader
 * Comparison table for owner vs Contributor vs Reader
 * Sample Customized role to allow user to create a VM only


# 1. What is Azure RBAC?

**RBAC = Role-Based Access Control**

Azure RBAC is used to control:

> **Who can access Azure resources, what they can do, and where they can do it.**

The three important questions are:

```text id="q8f0d1"
WHO?
 ↓
User / Group / Service Principal

WHAT?
 ↓
Role

WHERE?
 ↓
Scope
```
This is the core concept of RBAC.
---
# 8. Three Core Concepts of RBAC
simple formula: Who + What + Where = Access.
```sh
[ Who? ]                   [ What? ]                 [ Where? ]
Security Principal    +   Role Definition    +           Scope           = Access Granted
 (e.g., Jane the         (e.g., "Reader" -          (e.g., Only inside
    Student)              can view things)         "Lab-Resource-Group")
```
1. Security Principal (The "Who"): An identity requesting access. This can be a single User, a Group of people, or an application (Service Principal). 
2. Role Definition (The "What"): A collection of permissions. Azure has thousands of built-in roles, but beginners only need to know the big three:
	* 👀 Reader: Can look, but cannot touch or change anything.
	* 🛠️ Contributor: Can create, edit, or delete resources, but cannot grant access to others.
	* 👑 Owner: Has full control, including the power to grant or revoke access for others. 
3. Scope (The "Where"): The boundary where the access applies. Azure organizes resources like folders on a computer:
	* Subscription (The billing account) → Resource Group (A folder holding related items) → Resource (An individual VM or database).
	* Rule of Thumb: Inherited access flows downhill. If you are a Reader at the Subscription level, you are automatically a Reader for everything inside it.

Azure RBAC supports several scopes:

```text id="w8qkkn"
Management Group
       │
       ▼
Subscription
       │
       ▼
Resource Group
       │
       ▼
Resource
```

For example:

```text id="q7t9s2"
Rajiv
  │
  ▼
Contributor
  │
  ▼
Resource Group: Production
```

Rajiv can manage resources within that scope according to the role's permissions.

---
# 2. RBAC Architecture

Diagram:
```text id="6g2n9a"
Microsoft Entra ID
       │
       ▼
     User
       │
       ▼
Role Assignment
       │
       ├── Role
       │
       └── Scope
             │
             ▼
        Azure Resource
```

For example:

```text id="kq6nqk"
John
  │
  ▼
Contributor
  │
  ▼
Resource Group
  │
  ▼
Azure VM
```

Meaning:

**John can manage resources within that Resource Group according to the permissions included in the Contributor role.**

---
# 3. What is a Role?

A role is a collection of permissions.

Example:

```text id="1c7s4q"
Reader
   ↓
Can View

Contributor
   ↓
Can Manage

Owner
   ↓
Can Manage + Manage Access
```
---
# 4. Owner

Explain:

**Owner** has full management access to resources within the assigned scope and can also manage access.

Example:

```text id="7v4l3c"
Owner
 │
 ├── Create
 ├── Modify
 ├── Delete
 └── Assign Access
```

This is a powerful role.

**Security point:** Don't give Owner unnecessarily.

---
 # 5. Contributor

Contributor can manage resources but **cannot grant access to others** through Azure RBAC.

```text id="9w7g8k"
Contributor
 │
 ├── Create
 ├── Modify
 ├── Delete
 └── ❌ Manage Access
```

Example:

A developer may need to:

* Start/stop a VM
* Deploy resources
* Modify resources

but shouldn't be able to give themselves or others additional permissions.

---
# 6. Reader

Reader is mostly for viewing resources.

```text id="d8kh2s"
Reader
 │
 ├── View
 ├── Inspect
 └── ❌ Modify
```

Useful for:

* Auditors
* Managers
* Monitoring teams
* Support teams

---
# 7. Comparison

| Role        | View | Create/Modify/Delete | Assign Access |
| ----------- | ---: | -------------------: | ------------: |
| Reader      |    ✅ |                    ❌ |             ❌ |
| Contributor |    ✅ |                    ✅ |             ❌ |
| Owner       |    ✅ |                    ✅ |             ✅ |

---

# For creating VM, we need to give this permission 

```sh
"actions": [
                    "Microsoft.Compute/virtualMachines/*",
                    "Microsoft.Compute/disks/*",
                    "Microsoft.Compute/images/read",
                    "Microsoft.Compute/locations/*/read",
                    "Microsoft.Network/networkInterfaces/*",
                    "Microsoft.Network/publicIPAddresses/*",
                    "Microsoft.Network/networkSecurityGroups/*",
                    "Microsoft.Network/virtualNetworks/read",
                    "Microsoft.Network/virtualNetworks/subnets/read",
                    "Microsoft.Network/virtualNetworks/subnets/join/action",
                    "Microsoft.Resources/deployments/*",
                    "Microsoft.Resources/subscriptions/resourceGroups/read",
                    "Microsoft.Storage/storageAccounts/read",
                    "Microsoft.Resources/subscriptions/resourceGroups/write",
                    "Microsoft.Resources/subscriptions/resourceGroups/delete"
                ]
```







