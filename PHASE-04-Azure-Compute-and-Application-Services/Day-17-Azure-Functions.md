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

## 🧪 HANDS-ON DEMO #1 — Create Your First Azure Function

We will see all steps in the video 


