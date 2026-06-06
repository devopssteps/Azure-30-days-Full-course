# 🎯 🔥 Azure CLI + PowerShell (Hands-On Tutorial)

👉 Topics Covered:

* Azure CLI Basics
* Azure PowerShell Basics
* Automation Commands
* Real DevOps Use Cases

---

# 🧠 1. What is Azure CLI?

👉 Azure CLI = command-line tool to manage Azure resources

💡 Used for:

* Automation
* Scripting
* CI/CD pipelines
* Infrastructure management

👉 Similar to AWS CLI

---

> “Instead of clicking manually in portal, DevOps engineers automate everything using CLI.”

---

# 💻 🧪 2. Install Azure CLI (Ubuntu/Linux)

### Azure CLI install URL:
https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
---

## 🔹 Install Command

```bash id="azcliinstall"
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

---

## 🔍 Verify Installation

```bash id="azversion"
az version
```

---

# 🔐 3. Login to Azure

---

## Command

```bash id="azlogin"
az login
```

### 👉 Browser opens for authentication, type the code then type your username and password
<br>
👉 Type 1 and Enter when you see the message "Select a subscription and tenant (Type a number or Enter for no changes): 1"
---

## Show Current Account

```bash id="azaccount"
az account show
```

---

# 📦 4. Azure CLI Basic Commands

---

## List Resource Groups

```bash id="azgroup"
az group list --output table
```

---

## Create Resource Group

```bash id="azgroupcreate"
az group create --name devops-rg --location eastus
```

---

## List VMs

```bash id="azvmlist"
az vm list --output table
```
## Create a blob storage
```sh
az storage account create \
  --resource-group rg2 \
  --name rajivsiddiqui2011 \
  --location eastus \
  --sku Standard_LRS
```
## Delete a blob storage
```sh
az storage account delete \
  --resource-group rg2 \
  --name rajivsiddiqui2011 \
  --yes
```
---

# 🖥️ 5. Create VM Using CLI (Hands-On)

---

## Command

```bash id="azvmcreate"
az vm create \
  --resource-group devops-rg \
  --name myvm \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys
```

---

# 🌐 Open HTTP Port

```bash id="azopenport"
az vm open-port \
  --resource-group devops-rg \
  --name myvm \
  --port 80
```

---

# 🔌 SSH into VM

```bash id="azssh"
ssh azureuser@<public-ip>
```

---

# 🌍 Install Nginx

```bash id="aznginx"
sudo apt update
sudo apt install nginx -y
```

---

> “With just a few commands, we deployed a complete cloud server.”

---

# ⚡ 6. Azure PowerShell Basics

👉 PowerShell is another automation tool from Microsoft

---

# 💻 Install PowerShell (Ubuntu)

```bash id="psinstall"
sudo snap install powershell --classic
```

---

## Start PowerShell

```powershell id="psstart"
pwsh
```

---

# 🔐 Connect Azure

```powershell id="pslogin"
Connect-AzAccount
```

---

# 📦 PowerShell Commands

## List Resource Groups

```powershell id="psgroup"
Get-AzResourceGroup
```

---

## Create Resource Group

```powershell id="psgroupcreate"
New-AzResourceGroup -Name devops-rg2 -Location eastus
```

---

# 🤖 7. Automation Basics 

👉 Save commands into script

---

## Bash Script Example

```bash id="bashscript"
#!/bin/bash

az group create --name devops-rg --location eastus
```

---

## Run Script

```bash id="runscript"
bash deploy.sh
```

---

> “Automation saves time and removes manual errors.”

---

# 🧠 8. Real DevOps Use Cases

 - ✔ CI/CD pipelines
 - ✔ Infrastructure provisioning
 - ✔ Kubernetes automation
 - ✔ Scheduled scripts

---

# 🧠 Summary

 - ✔ Azure CLI = Linux-friendly automation
 - ✔ PowerShell = Microsoft automation tool
 - ✔ Automation = core DevOps skill

---

> “CLI and automation are mandatory skills for every DevOps engineer.”

---
