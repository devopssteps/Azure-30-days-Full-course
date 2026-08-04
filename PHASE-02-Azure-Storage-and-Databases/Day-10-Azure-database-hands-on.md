# Azure Database Tutorial (Complete Guide + Hands-On Azure MySQL Demo)

## 🎯 What You Will Learn

* Azure Database Overview
* Types of Azure Databases
* Azure SQL Database
* Azure Database for MySQL
* Azure Database for PostgreSQL
* Azure Cosmos DB
* Azure Managed Instance
* Database Backup & High Availability
* Hands-On Create Azure MySQL Database
* Connect Azure MySQL from Local PC
* Azure Database Cost Optimization
* Azure Database Interview Questions

---

# 1. Azure Database Overview

Azure provides fully managed database services.

Benefits:

✅ No OS management

✅ Automatic backups

✅ High Availability

✅ Automatic patching

✅ Scaling

✅ Security

---

## Database Service Comparison

| Database Type | Azure Service                 | AWS Equivalent |
| ------------- | ----------------------------- | -------------- |
| MySQL         | Azure Database for MySQL      | RDS MySQL      |
| PostgreSQL    | Azure Database for PostgreSQL | RDS PostgreSQL |
| SQL Server    | Azure SQL Database            | RDS SQL Server |
| Managed SQL   | Azure SQL Managed Instance    | RDS            |
| NoSQL         | Azure Cosmos DB               | DynamoDB       |
| Cache         | Azure Cache for Redis         | ElastiCache    |

---

# 2. Azure SQL Database

Managed Microsoft SQL Server.

Best for:

* .NET Applications
* Enterprise Applications
* ERP Systems

Features:

* Auto Backup
* Auto Scaling
* HA Built-in
* Geo Replication

---

# 3. Azure Database for MySQL

Managed MySQL service.

Best for:

* PHP Applications
* WordPress
* Laravel
* E-commerce Websites

Features:

* Automatic Backups
* Point-in-Time Restore
* SSL Encryption
* High Availability

---

# 4. Azure Database for PostgreSQL

Managed PostgreSQL service.

Best for:

* Modern Applications
* GIS Workloads
* Analytics

---

# 5. Azure Cosmos DB

Globally distributed NoSQL database.

Supports:

* JSON Documents
* MongoDB API
* Cassandra API
* Gremlin API

Use Cases:

* Social Media Apps
* Gaming
* IoT

---

# 6. Azure Database Architecture

```text
Application
      │
      ▼
Azure Database
      │
      ▼
Storage
      │
      ▼
Automatic Backup
```

---

# 7. Hands-On Demo: Create Azure MySQL Database

---

## Step 1: Login Azure Portal

Go to:

### [Microsoft Azure Portal](https://portal.azure.com?utm_source=chatgpt.com)

---

## Step 2: Search MySQL

Search:

```text
Azure Database for MySQL
```

Click:

```text
Azure Database for MySQL Flexible Server
```

---

## Step 3: Click Create

Choose:

```text
Flexible Server
```

Recommended for production and learning.

---

# Step 4: Basics Configuration

### Subscription

Select your Azure subscription.

---

### Resource Group

Create:

```text
azure-mysql-rg
```

---

### Server Name

Must be globally unique.

Example:

```text
devopsstepsmysql001
```

---

### Region

Choose:

```text
Southeast Asia
```

or nearest region.

---

### MySQL Version

Choose:

```text
MySQL 8.0
```

---

### Workload Type

For learning:

```text
Burstable
```

---

### Compute Size

Choose:

```text
Standard_B1ms
```

Lowest-cost option.

---

### Admin Username

```text
azureadmin
```

---

### Password

Example:

```text
StrongPassword@123
```

(Create your own strong password.)

---

Click:

```text
Next: Networking
```

---

# Step 5: Networking Configuration

### Connectivity Method

Choose:

```text
Public Access
```

This allows connection from your laptop.

---

### Allow Azure Services

```text
Yes
```

---
### Allow all

```text
Firewall rule name - Any name like AllowAll_2026-6-2_19-49-34
Start IP address - 0.0.0.0
End IP address - 255.255.255.255
```

### Add Client IP

Click:

```text
Add Current Client IP Address
```

Azure automatically detects your IP.


---

Click:

```text
Review + Create
```

---

# Step 6: Create Database

Click:

```text
Create
```

Deployment usually takes:

```text
5-10 minutes
```

---

# 🎉 Azure MySQL Database Created

---

# Step 7: Get Connection Information

Navigate:

```text
Resource
      ↓
Overview
```

Copy:

### Server Name

Example:

```text
devopsstepsmysql001.mysql.database.azure.com
```

---

# Step 8: Create Database

Open:

```text
Query Editor
```

Create database:

```sql
CREATE DATABASE devopsdb;
```

---

# Create Table

```sql
USE devopsdb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
);
```

---

# Insert Data

```sql
INSERT INTO users(name)
VALUES('Rajiv');
```

---

# Verify

```sql
SELECT * FROM users;
```

Output:

```text
1 Rajiv
```

---

# Connect Azure MySQL from Local PC

---

## Option 1: Using MySQL Workbench

Download:

### [MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=chatgpt.com)

Install normally.

---

# Create New Connection

Open MySQL Workbench.

Click:

```text
+
New Connection
```

---

# Connection Details

### Connection Name

```text
Azure MySQL
```

---

### Hostname

```text
devopsstepsmysql001.mysql.database.azure.com
```

---

### Port

```text
3306
```

---

### Username

```text
azureadmin
```

or

```text
azureadmin@devopsstepsmysql001
```

(depending on server configuration)

---

### Password

Use the password created earlier.

---

Click:

```text
Test Connection
```

---

# Common Error

```text
Can't connect to MySQL server
```

Usually caused by firewall rules.

---

# Fix Firewall

Azure Portal:

```text
Networking
      ↓
Firewall Rules
```

Add:

```text
Your Current IP
```

Save.

---

# 🎉 Connection Successful

---

# Option 2: Connect Using MySQL CLI

Install MySQL Client.

Run:

```bash
mysql -h devopsstepsmysql001.mysql.database.azure.com \
-u azureadmin \
-p
```

Enter password.

---

# Show Databases

```sql
SHOW DATABASES;
```

---

# Use Database

```sql
USE devopsdb;
```

---

# View Data

```sql
SELECT * FROM users;
```

---

# Backup and Restore

Azure automatically performs:

* Daily backups
* Point-in-Time Restore
* Geo Backup (optional)

---

# High Availability

Enable:

```text
High Availability
```

Options:

* Same Zone
* Zone Redundant

Provides automatic failover.

---

# Cost Optimization

For learning:

### Use

```text
Burstable B1ms
```

### Disable HA

```text
Off
```

### Stop unused resources

Delete databases after lab completion.

---

# Azure MySQL vs Install MySQL on VM

| Feature    | Azure MySQL | MySQL on VM |
| ---------- | ----------- | ----------- |
| Patching   | Automatic   | Manual      |
| Backup     | Automatic   | Manual      |
| HA         | Built-in    | Manual      |
| Scaling    | Easy        | Difficult   |
| Management | Low         | High        |
| Cost       | Higher      | Lower       |

---

# Real-World Recommendation

### Production

Use:

```text
Azure Database for MySQL
```

---

### Learning

Use:

```text
MySQL on Azure VM
```

if budget is limited.

---

# Interview Questions

### What is Azure Database for MySQL?

A fully managed MySQL service in Azure.

---

### Difference between Azure SQL and Azure MySQL?

Azure SQL uses Microsoft SQL Server; Azure MySQL uses the MySQL engine.

---

### What is Point-in-Time Restore?

Restore a database to a specific time using backups.

---

### Why use Managed Database?

Less operational overhead, automatic backups, patching, and scaling.

---
