# Day-15-Azure-App-Service.md


# 1️⃣ What is Azure App Service?
> **Azure App Service হলো Microsoft Azure-এর একটি managed platform যেখানে আমরা web application, REST API এবং backend application deploy এবং run করতে পারি, server infrastructure নিজে manage না করেই।**

Traditional approach:

```text
You
 │
 ├── VM
 ├── OS
 ├── Patching
 ├── Web Server
 ├── Runtime
 ├── Security
 └── Application
```

App Service:

```text
Azure
 │
 ├── Infrastructure
 ├── OS Management
 ├── Platform
 └── App Service
        │
        ▼
   Your Application
```

> **We focus more on the application; Azure manages much of the underlying platform infrastructure.**

---

# 2️⃣ Azure App Service Web Apps

**Web App** is the App Service resource where you deploy your web application.

Architecture:

```text
Azure Subscription
       │
       ▼
 Resource Group
       │
       ├──────────────┐
       ▼              ▼
App Service Plan   Other Resources
       │
       ▼
    Web App
       │
       ▼
Your Application
```

---
# 3️⃣ App Service Plan

**App Service** vs **App Service Plan**.

### App Service Plan

The plan provides the underlying compute resources for your App Service apps.

```text
App Service Plan
       │
 ┌─────┼─────┐
 ▼     ▼     ▼
Web1  Web2  Web3
```

Depending on the plan and configuration, multiple apps can share the same compute resources.

> **Web App = Application**

> **App Service Plan = Compute resources/platform environment where the app runs**

---

# 4️⃣ App Service Pricing / Tiers

For our demo, we show the available tiers in the current Azure portal rather than memorizing specific pricing.

```text
Development / Testing
        ↓
Basic
        ↓
Standard
        ↓
Premium
```

Exact tiers and features can change:

> "Azure pricing and available SKUs change over time, so always check the current pricing and regional availability before deploying."

---

# 5️⃣ Hands-On — Create App Service

Go to:

```text
Azure Portal
    ↓
App Services
    ↓
Create
    ↓
Web App
```

You'll see the configuration.

---
# Step 1 — Subscription

Select your Azure subscription.

Example:

```text
Subscription:
Pay-As-You-Go
```

---

# Step 2 — Resource Group

Create:

```text
azure-appservice-demo-rg
```

---

# Step 3 — Web App Name

Choose a globally unique name.

Example:

```text
devopssteps-demo-2026-xxx
```

Azure will provide a URL similar to:

```text
https://<your-app-name>.azurewebsites.net
```

---

# Step 4 — Deployment Options

Select **Code**

Choose the runtime matching your application.

For example:

```text
Runtime stack:
Node.js
```

or:

```text
Python
```

or:

```text
.NET
```
---

# Demo Application
Example:

```text
Node.js Web App
      │
      ▼
Azure App Service
      │
      ▼
Live Website
```

In the next video we will see how we can deploy form **GitHub → CI/CD → Azure App Service**
---
# 6️⃣ Create App Service Plan

Create:

```text
App Service Plan:
azure-demo-plan
```

Choose a low-cost suitable SKU for the demo.

Then create the Web App.

Wait for deployment to finish.

---
# 7️⃣ Test the Default Web App

Open:

```text
App Service
    ↓
Overview
    ↓
Default Domain
```

Open the URL.

You'll see your deployed application/default page depending on your deployment state.

> "এই URL-টাই Azure আমাদের application-এর জন্য public endpoint হিসেবে দিচ্ছে।"

---




