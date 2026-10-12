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
# Azure Tenant
An Azure Tenant is a single, dedicated, and isolated instance of Microsoft Entra ID (formerly Azure AD) that represents a specific organization.

## How It Works
* Your Private Cloud Space: When your organization signs up for a Microsoft cloud service (like Azure or Microsoft 365), Microsoft creates a dedicated tenant for you.
* Security Boundary: It acts as a secure container. Everything inside it—users, passwords, permissions, and connected applications—is completely isolated from every other company's tenant.
* The Analogy: Think of an Azure Tenant like an apartment in an apartment building. Microsoft owns the whole building, but your tenant is your specific apartment. Only people with your key (credentials) can get inside, and your neighbors cannot see or touch anything in your space.

## Key Things a Tenant Houses
* User Identities: All the employee accounts, guest accounts, and security groups for your company.
* Subscriptions: The billing accounts used to pay for Azure resources like Virtual Machines or databases.

---

# Hands on MFA demo
We will create a user and login to that user and after put the username and password it will ask for the code so we need to put the code and we are using Authy for our MFA and URL is : https://www.authy.com/

---
# SSO
Single Sign-On (SSO) is an authentication method that allows you to log in once with a single set of credentials (username and password) to access multiple independent software systems, applications, or websites. For example we are login to google one time and now we can access youtube or google drive and it will not asking the credentials again. 

------------------------------
### How It Works

* One Login: You enter your username and password a single time on a central login page.
* Seamless Access: The central system verifies your identity and automatically grants you access to all your connected apps without asking you to log in again.
* The Analogy: Think of SSO like a wristband at an amusement park. You show your ID and pay at the entrance to get the wristband. For the rest of the day, you just show that wristband to get on every ride, rather than buying a separate ticket for each one.

------------------------------
### Why People Use It

* Better Security: Users only have to remember one strong password instead of dozens of weak ones.
* Time Saving: It eliminates the frustration of logging into different tools repeatedly throughout the workday.
* Easy Offboarding: When an employee leaves a company, IT can disable their single SSO account to instantly block their access to all company apps at once.



