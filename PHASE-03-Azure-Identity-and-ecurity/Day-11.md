# Day 11 — Microsoft Entra ID

In this video we learn the following topics:
 * What is Microsoft Entra ID?
 * Architecture of Microsoft Entra ID
 * What is a Tenant?
 * Users
 * Groups
 * Authentication vs Authorization
 * MFA — Multi-Factor Authentication
 * What is SSO?

# 1. What is Microsoft Entra ID?

**Microsoft Entra ID** is Microsoft's cloud-based identity and access management service.

It helps organizations manage:

* Users
* Groups
* Applications
* Devices
* Authentication
* Authorization
* Access policies
* Identity security

Previously, Microsoft Entra ID was called **Azure Active Directory (Azure AD)**.

> Azure AD

while the current name is:

> Microsoft Entra ID

---

# 2. Architecture to Show Microsoft Entra ID

```text
                    Microsoft Entra ID
                           │
                    ┌──────┴──────┐
                    │             │
                  Users         Groups
                    │             │
                    └──────┬──────┘
                           │
                    Authentication
                           │
                     ┌─────┴─────┐
                     │           │
                    MFA         SSO
                     │           │
                     └─────┬─────┘
                           │
                     Authorization
                           │
                           ▼
                  Azure Resources
```
---

# Hands on MFA demo
We will create a user and login to that user and after put the username and password it will ask for the code so we need to put the code and we are using Authy for our MFA and URL is : https://www.authy.com/
