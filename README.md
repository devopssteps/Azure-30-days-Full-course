# **Azure in 30 Days — Learn Microsoft Azure from Zero to Cloud & DevOps**

# Course Outline
---

# 📅 PHASE 1 — Azure Fundamentals

## Day 1 — Introduction to Azure & Cloud Computing

**Topics:**

* What is Cloud Computing?
* IaaS vs PaaS vs SaaS
* Public vs Private vs Hybrid Cloud
* What is Microsoft Azure?
* Azure vs AWS
* Azure Regions & Availability Zones
* Azure Portal Overview
* Create Azure Free Account
* Azure CLI Introduction
* Azure Cloud Shell

---

## Day 2 — Azure Resource Groups & Subscriptions

* Azure Subscription
* Resource Groups
* Azure Resources
* Management Groups
* Azure hierarchy
* Azure Portal vs CLI
* Create Resource Group
* Delete Resources
* Azure Cost Management

🎯 Hands-on:

**Create and manage Azure resources using Portal + CLI**

---

## Day 3 — Azure Virtual Machines

* What is Azure VM?
* VM sizes
* Images
* OS disks
* Data disks
* SSH vs RDP
* Public IP
* Network Interface
* Create Linux VM
* Create Windows VM

🎯 Hands-on:

**Launch an Ubuntu VM and connect using SSH**

---

## Day 4 — Azure Virtual Network

* What is VNet?
* Subnets
* CIDR
* Private IP
* Public IP
* NIC
* NSG
* Route Tables

🎯 Hands-on:

**Build your first Azure VNet**

---

## Day 5 — Azure Networking Deep Dive

* Network Security Groups
* Inbound Rules
* Outbound Rules
* Application Security Groups
* Public vs Private Access
* Azure Bastion

🎯 Hands-on:

**Secure an Azure VM using NSG**

---

# 📅 PHASE 2 — Azure Storage & Databases

## Day 6 — Azure Storage Account

* What is Azure Storage?
* Storage Account
* Storage tiers
* Redundancy
* LRS
* ZRS
* GRS
* RA-GRS

🎯 Hands-on:

**Create and configure Storage Account**

---

## Day 7 — Azure Blob Storage

* Containers
* Blob types
* Upload/download files
* Public vs Private access
* Blob lifecycle
* Access tiers

🎯 Hands-on:

**Host a static website using Azure Blob Storage**

🔥 This is a great video because viewers see a real result.

---

## Day 8 — Azure Files & Storage Security

* Azure Files
* File Shares
* SMB
* Mount Azure Files
* Storage Access Keys
* SAS Tokens
* Shared Access Signature

🎯 Hands-on:

**Mount Azure File Share on Linux VM**

---

## Day 9 — Azure Managed Disks & Backup

* Managed Disks
* Snapshots
* Disk types
* Azure Backup
* Recovery Services Vault

🎯 Hands-on:

**Backup and restore Azure VM**

---

## Day 10 — Azure Database Services

* Azure SQL Database
* Azure Database for PostgreSQL
* Azure Database for MySQL
* Cosmos DB overview
* SQL vs NoSQL

🎯 Hands-on:

**Create Azure SQL Database and connect to it**

---

# 📅 PHASE 3 — Azure Identity & Security

## Day 11 — Microsoft Entra ID

Formerly Azure Active Directory.

* Users
* Groups
* Tenants
* Authentication
* Authorization
* MFA
* SSO

🎯 Hands-on:

**Create users and groups**

---

## Day 12 — Azure RBAC

* What is RBAC?
* Owner
* Contributor
* Reader
* Scope
* Role Assignment

🎯 Hands-on:

**Give different permissions to users**

---

## Day 13 — Managed Identity

🔥 Very important for Cloud and DevOps.

* What is Managed Identity?
* System-assigned identity
* User-assigned identity
* Why avoid passwords?

🎯 Hands-on:

**Azure VM → Azure Storage without access keys**

---

## Day 14 — Azure Key Vault

* Secrets
* Keys
* Certificates
* Key Vault security
* Managed Identity + Key Vault

🎯 Hands-on:

**VM retrieves secrets from Key Vault**

---

# 📅 PHASE 4 — Azure Compute & Application Services

## Day 15 — Azure App Service

* What is Azure App Service?
* Web Apps
* App Service Plans
* Deployment Slots
* Environment Variables
* Scaling

🎯 Hands-on:

**Deploy a web application to Azure App Service**

---

## Day 16 — App Service Deployment

* GitHub deployment
* ZIP deployment
* Azure CLI deployment
* Application settings
* Logs

🎯 Hands-on:

**Deploy application from GitHub to Azure**

---

## Day 17 — Azure Functions

* Serverless Computing
* Function Apps
* Triggers
* Bindings
* HTTP Trigger
* Timer Trigger

🎯 Hands-on:

**Build your first serverless Azure Function**

---

## Day 18 — Azure Load Balancer & Application Gateway

Compare:

* Azure Load Balancer
* Application Gateway
* Layer 4 vs Layer 7
* Health Probes
* SSL/TLS
* WAF

🎯 Hands-on:

**Deploy Application Gateway with Web Application Firewall**

---

# 📅 PHASE 5 — Containers & Kubernetes

## Day 19 — Docker on Azure

* Docker fundamentals
* Azure Container Registry
* Push Docker image
* Pull Docker image

🎯 Hands-on:

**Docker → ACR**

---

## Day 20 — Azure Container Instances

* What is ACI?
* Container deployment
* Environment variables
* Container networking

🎯 Hands-on:

**Deploy Docker container to Azure**

---

## Day 21 — Azure Container Apps

* Container Apps
* Serverless containers
* Revisions
* Scaling
* Environment

🎯 Hands-on:

**Deploy a containerized application**

---

## Day 22 — Azure Kubernetes Service (AKS)

🔥 One of your most important videos.

* What is Kubernetes?
* What is AKS?
* AKS architecture
* Control Plane
* Node Pools
* Pods
* Services

🎯 Hands-on:

**Create your first AKS cluster**

---

## Day 23 — Deploy Application on AKS

* kubectl
* Deployment
* Service
* LoadBalancer
* ConfigMap
* Secret

🎯 Hands-on:

**Deploy a Dockerized application to AKS**

---

# 📅 PHASE 6 — Azure DevOps & CI/CD

## Day 24 — Azure DevOps Introduction

* Azure DevOps overview
* Organizations
* Projects
* Repos
* Boards
* Pipelines
* Artifacts
* Test Plans

🎯 Hands-on:

**Create your first Azure DevOps project**

---

## Day 25 — Azure Repos & Git

* Git fundamentals
* Azure Repos
* Branches
* Pull Requests
* Merge
* Branch policies

🎯 Hands-on:

**Create Git repository and push application**

---

## Day 26 — Azure Pipelines CI/CD

🔥 High-value DevOps topic.

* CI vs CD
* YAML Pipeline
* Build Pipeline
* Release Pipeline
* Pipeline Agents

🎯 Hands-on:

**Git → Build → Test → Deploy**

---

## Day 27 — CI/CD with Docker + ACR + AKS

🔥 This should be one of your biggest videos.

Build:

**Developer → Git → Azure Pipeline → Docker Build → ACR → AKS**

🎯 Final result:

**Automatic deployment to Kubernetes**

---

# 📅 PHASE 7 — Infrastructure as Code & Monitoring

## Day 28 — Terraform on Azure

* Why Terraform?
* Terraform vs ARM
* AzureRM Provider
* Resource Group
* VNet
* VM
* Variables
* Outputs

🎯 Hands-on:

**Deploy Azure infrastructure using Terraform**

---

## Day 29 — Azure Monitor & Application Insights

* Azure Monitor
* Metrics
* Logs
* Log Analytics Workspace
* Application Insights
* Alerts

🎯 Hands-on:

**Monitor Azure VM and Application**

---

# 🏆 Day 30 — FINAL AZURE REAL-WORLD PROJECT

This should be the **big finale** of your entire course.

## 🔥 Project: Production-Style 3-Tier Application on Azure

### Architecture

```text
                    Internet
                       │
                       ▼
                Azure Application
                    Gateway
                    + WAF
                       │
                       ▼
                 Azure Web App
                    / AKS
                       │
                       ▼
              Azure SQL Database
                       │
                       ▼
               Azure Blob Storage


Developer
    │
    ▼
Azure Repos
    │
    ▼
Azure Pipeline
    │
    ├── Build
    ├── Test
    ├── Docker Build
    ├── Push to ACR
    │
    ▼
     AKS
    │
    ▼
Production


Terraform
    │
    ▼
Azure Infrastructure
```

### Project Technologies

* Azure VNet
* Subnets
* NSG
* Application Gateway
* WAF
* Azure VM
* Azure Container Registry
* Docker
* AKS
* Azure SQL
* Blob Storage
* Key Vault
* Managed Identity
* Azure Monitor
* Log Analytics
* Azure DevOps
* Azure Pipelines
* Terraform

### Final CI/CD

```text
Developer
    ↓
Git Push
    ↓
Azure Repos
    ↓
Azure Pipeline
    ↓
Build & Test
    ↓
Docker Image
    ↓
Azure Container Registry
    ↓
AKS Deployment
    ↓
Application Gateway
    ↓
Users
```

