# Day 17: Azure Function 

## 1. What is Serverless Computing?

### Traditional application

```text
User
 ↓
Load Balancer
 ↓
VM
 ↓
Operating System
 ↓
Web Server
 ↓
Application
```

You have to think about:

* VM
* OS
* Patching
* Server availability
* Scaling
* Infrastructure

Serverless:

```text
User
 ↓
Azure Function ⚡
 ↓
Your Code
```
Azure manages much of the underlying infrastructure.
> **"Serverless doesn't mean there are literally no servers. It means you don't manage the underlying servers directly."**

## ⚡ 2. What is Azure Functions?

> **Azure Functions is a serverless compute service that lets you run event-driven code without having to manage the underlying server infrastructure.**

Simple architecture:

```text
Event
  │
  ▼
Azure Function
  │
  ▼
Your Code
```

Events can include:

```text
HTTP Request
Timer
Queue Message
Blob Event
Event
```
---
# 3. Function App vs Function

### Function App

The container/environment that hosts your functions and their configuration.

```text
Function App
    │
    ├── Function 1
    ├── Function 2
    └── Function 3
```

### Function

The individual piece of code that performs a task.

Example:

```text
Function App
     │
     ├── helloFunction
     ├── processOrder
     └── sendReport
```


> **Function App = Application/container**

> **Function = Individual serverless function**

---

## 4. What is a Trigger?

A **trigger** determines how a function is invoked.

```text
Trigger
   ↓
Function
   ↓
Code
```

Examples:

```text
HTTP Trigger
Timer Trigger
Queue Trigger
Blob Trigger
Event Trigger
```

In this video, we will focus on http trigger:

### HTTP Trigger

```text
Browser / Client
       │
       ▼
HTTP Trigger
       │
       ▼
Azure Function
```

### Timer Trigger

```text
Schedule
   │
   ▼
Timer Trigger
   │
   ▼
Azure Function
```
---

# 🔗 5. What are Bindings?

> **Bindings provide a way for Azure Functions to connect to other services and data sources with less boilerplate code.**

Concept:

```text
Function
   │
   ├── Input Binding
   │
   └── Output Binding
```

For example:

```text
Blob Storage
     │
     ▼
Input Binding
     │
     ▼
Function
     │
     ▼
Output Binding
     │
     ▼
Queue / Storage
```

---
# 1. Serverless vs VM

|                   | Azure VM              | Azure Functions              |
| ----------------- | --------------------- | ---------------------------- |
| Server management | You manage it         | Azure manages infrastructure |
| OS                | You manage            | Managed platform             |
| Scaling           | You configure         | Platform-dependent/managed   |
| Billing model     | Resource uptime/usage | Execution/plan dependent     |
| Best for          | Full server control   | Event-driven workloads       |
| Deployment        | Application + server  | Function code                |

---
# Comparison Azure App Service vs Azure Functions    
| Feature          | Azure App Service                                | Azure Functions                                                                           |
| ---------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| Main purpose     | Host websites and web applications               | Run individual tasks or functions                                                         |
| Application type | Full web application, REST API, backend          | Event-driven code, background jobs, lightweight APIs                                      |
| Execution        | Application is hosted continuously               | Code executes when triggered                                                              |
| Trigger          | Usually receives HTTP requests                   | HTTP, timer, queue, blob, Event Grid, etc.                                                |
| Scaling          | Scale the App Service Plan up or out             | Can automatically scale based on incoming events, depending on hosting plan               |
| Pricing          | Generally pay for the App Service Plan resources | Depends on hosting plan; consumption options charge based on execution and resource usage |
| Best suited for  | Websites, web portals, backend APIs              | Automation, scheduled tasks, event processing                                             |
| Typical example  | Hosting an e-commerce website                    | Sending an email when a new order arrives  

## 2. Practical examples

### Example A: Azure App Service — hosting a complete website

Imagine you develop an online shopping website using Python and Flask.

Your application might have:

- Home page
- Login and registration
- Product catalog
- Shopping cart
- Payment integration
- Admin dashboard
- Database connectivity

You deploy the complete application to Azure App Service.

When customers visit your website, App Service handles their HTTP requests and returns the appropriate pages or API responses.

Example: Your existing Python Flask application from the App Service lab is a good example of this use case.

### Example B: Azure Functions — executing a specific task

Imagine you have the same shopping website, but whenever a customer places an order, you want to send an email automatically.

The workflow:

1. Customer places an order.
2. Website saves the order in the database.
3. A message is sent to Azure Queue Storage.
4. An Azure Function is triggered by that message.
5. The function executes Python code.
6. Customer receives an order confirmation email.

You don't need to deploy another complete website to perform this task. You only need an Azure Function.

## 3. Common Azure Functions triggers

One of the most important concepts to teach your students is the Trigger.

A trigger determines when an Azure Function executes.

HTTP Trigger

Executes when someone sends an HTTP request to the function.

Example: An API endpoint that returns customer information.

Timer Trigger

Executes according to a schedule.

Example: Run a Python script every day at midnight to generate a report.

Queue Trigger

Executes when a new message arrives in Azure Queue Storage.

Example: Process customer orders in the background.

Blob Trigger

Executes when a blob is uploaded or updated.

Example: Automatically resize an uploaded image.

## 4. How does the pricing differ?

App Service: You select an App Service Plan, such as Basic, Standard or Premium. You generally pay for the provisioned plan resources, even when your website receives very little traffic.

Azure Functions: You choose a hosting plan. With Flex Consumption, billing is based on execution, memory consumption and any always-ready instances. Premium and Dedicated plans have different pricing models.

---
## Real life example, an online shopping application:

| Azure service        | Responsibility                              |
| -------------------- | ------------------------------------------- |
| Azure App Service    | Hosts the shopping website                  |
| Azure SQL Database   | Stores customer and order information       |
| Azure Functions      | Sends emails and processes background tasks |
| Azure Storage Queue  | Stores background processing messages       |
| Azure Key Vault      | Stores database credentials and secrets     |
| Application Insights | Monitors application performance            |

---
## 🧪 HANDS-ON DEMO #1 — Create Your First Azure Function

We will see all steps in the video 



