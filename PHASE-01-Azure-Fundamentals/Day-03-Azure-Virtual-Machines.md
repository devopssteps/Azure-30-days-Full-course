# Day-3: Azure Virtual Machines (Hands-On)

---

# 1. What is Azure VM?

👉 A **Virtual Machine (VM)** is a cloud server you can create in minutes
<br>
👉 Same concept as AWS EC2

💡 You control:

* OS
* CPU/RAM
* Networking

---

# 2. HANDS-ON: Launch Azure VM

Go to
**Microsoft Azure Portal**

---

## 🔹 Step-by-Step

### 1. Search → **Virtual Machines**

Click **Create → Azure Virtual Machine**

---

### 2. Basic Settings

* Resource Group: `devops-rg`
* VM Name: `myvm`
* Region: nearest (e.g., East US / Southeast Asia)
* Image: **Ubuntu 22.04 LTS**
* Size: **B1s** (free tier friendly)

---

### 3. Authentication

👉 Choose:

* SSH Public Key

Paste your key OR generate new

---

### 4. Inbound Ports

✔ Allow:

* SSH (22)
* HTTP (80)

---

### 5. Click **Create**

Wait 1–2 minutes

---

> “This is how you launch a server in Azure in just a few clicks.”

---

# 3. Get Public IP

👉 After deployment:

* Go to VM
* Copy **Public IP**

---

# 4. SSH into VM (VERY IMPORTANT)

---

## Command:

```bash
ssh azureuser@<public-ip>
```

---

👉 Example:

```bash
ssh azureuser@20.123.45.67
```

---

> “Now we are connecting to our cloud server using SSH — just like AWS EC2.”

---

# 5. Install Nginx (Real Demo)

---

## Commands:

```bash
sudo apt update
sudo apt install nginx -y
```

---

## Start Nginx:

```bash
sudo systemctl start nginx
```

---

## Check status:

```bash
sudo systemctl status nginx
```

---

# 6. Test in Browser

👉 Open:

```text
http://<public-ip>
```

 - ✔ You will see:
 - 👉 Nginx default page 

---

> “Now your web server is live on the internet — this is a real cloud deployment.”

---

# Troubleshooting (VERY IMPORTANT)

---

## ❌ If not working:

 - ✔ Check port 80 open
 - ✔ Check NSG rules
 - ✔ Restart nginx

---

## Fix:

```bash
sudo systemctl restart nginx
```

---

# Summary

 - ✔ Created VM
 - ✔ Connected using SSH
 - ✔ Installed Nginx
 - ✔ Accessed via browser

---

> “Now you know how to launch and manage a real cloud server in Azure.”

---
