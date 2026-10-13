
# Day 11 — Azure RBAC Explained

In todays video we will learn the following topics.
 * What is Azure RBAC?
 * RBAC Architecture
 * What is a Role?
 * Owner
 * Contributor
 * Reader
 * Comparison table for owner vs Contributor vs Reader
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










