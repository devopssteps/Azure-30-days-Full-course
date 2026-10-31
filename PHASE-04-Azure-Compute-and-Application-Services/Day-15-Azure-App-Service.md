# Day 15: Azure App Service – Complete Hands-on Tutorial

## 1. What is Azure App Service?
Azure App Service is a Platform as a Service (PaaS) offering that allows developers to host web applications and REST APIs without managing the underlying virtual machines, operating systems, or web servers.

One important concept:

With an Azure VM, you manage the operating system and web server. With Azure App Service, Microsoft manages the underlying infrastructure, and you focus on your application.

### Azure App Service supports:
*	.NET applications
*	Java applications
*	Node.js applications
*	Python applications
*	PHP applications
*	Custom containers using Docker

### It can host:
*	Websites
*	Web applications
*	REST APIs
*	Backend services

### Real-world example:
Suppose you develop an e-commerce application.

A customer opens your website: https://www.myshop.com
The application runs on Azure App Service. Customers can browse products, log in, and place orders without you managing an EC2-style or Azure VM-based web server.

## 2. Understand Azure App Service architecture
There are two important components:

### A. App Service Plan
This defines the compute resources used by your application.
It determines:
*	CPU and memory capacity.
*	Number of instances.
*	Pricing tier.
*	Scaling capabilities.
*	Operating system.

### B. App Service (Web App)
This is the actual application that hosts your website or API.
One App Service Plan can host multiple Web Apps, and those applications share the plan's compute resources.

For example:
| App Service Plan     | Web Apps    |
| -------------------- | ----------- | 
| devopssteps-plan     | frontend-app  |
|                      | backend-api  | 
|                      | student-portal | 
|                      | company-website           |


## 3. Hands-on Demo 1: Create your first Azure Web App
Beginner practical lab
Our objective is to create a web application using Azure App Service and access it through a public URL.

### Step 1: Open Azure Portal

Go to Azure Portal.

Search for:

App Services

Click Create → Web App.

### Step 2: Configure the Web App
Use the following configuration:

| Setting                   | Value                                            |
| --------------------      | ------------------------------------------------ | 
| Subscription              | Your Azure subscription  |
| Resource Group            | devopssteps-rg  | 
| Name                      | devopssteps-webapp-2026 | 
| Publish                   | Code          |
| Runtime stack             | Python 3.12 (or an available supported version)  |
| Operating System          | Linux  | 
| Region                    | Your nearest available Azure region | 
| Pricing Plan              | Free F1, if available          |
	
Note: Web App names must be globally unique. If the name is unavailable, add a random suffix.		
	
### Step 3: Create the App Service Plan
In the Pricing Plan section, select an available plan.

Understand the tiers:	
| Tier                   | Purpose                                            |
| --------------------   | ------------------------------------------------ | 
| Free F1                | Learning and testing  |
| Basic B1               | Basic production workloads  | 
| Standard S1            | Production, scaling and deployment slots | 
| Premium v3             | Higher-performance production workloads	          |

Free and paid tiers have different limitations. Do not use Free F1 for a production application.

### Step 4: Review and create
 1. Click Review + Create.
 2. Wait for validation.
 3. Click Create.
 4. Wait for deployment to finish.
 5. Click Go to resource.

### Step 5: Open your website
Find the Default Domain under Overview.

It will look like:
 * https://devopssteps-webapp-2026.azurewebsites.net
 * Open it in your browser.
 * Expected result
Your Azure Web App should respond through its public URL.	

# 4. Hands-on Demo 2: Deploy your own Python application
Now let's deploy a real application. This is more useful for your DevOps students because they will understand how application code gets deployed to PaaS.

Since you use WSL Ubuntu, we can perform this demo from your Ubuntu terminal.
### Step 1: Create a Python application
Open WSL Ubuntu:
```sh
mkdir azure-appservice-demo
cd azure-appservice-demo
```
Create app.py:
```sh

from flask import Flask
import os

app = Flask(__name__)

@app.route("/")
def home():
    return """
    <html>
    <head>
        <title>DevOps Steps</title>
    </head>
    <body style="text-align:center; font-family:Arial;">
        <h1>Welcome to DevOps Steps!</h1>
        <h2>Azure App Service Demo</h2>
        <p>My Python application is running on Azure.</p>
        <p>Deployment: Successful!</p>
    </body>
    </html>
    """

@app.route("/health")
def health():
    return {"status": "healthy"}

if __name__ == "__main__":
    app.run()
```

### Step 2: Create requirements.txt
```sh
Flask
gunicorn
```

Your project structure should look like this:
```sh
azure-appservice-demo/
│
├── app.py
└── requirements.txt
```

### Step 3: Test your application locally
Install dependencies:
```sh
pip install -r requirements.txt
```
Run:
```sh
gunicorn --bind 0.0.0.0:8000 app:app
```
Open:
```sh
http://localhost:8000
```
You should see your website

Stop the application using Ctrl+C.

### Step 4: Connect to Azure from WSL
If Azure CLI is already installed:
```sh
az login
```
Check your subscription:
```sh
az account show
```
If you have multiple subscriptions, select the correct one:
```sh
az account set --subscription "YOUR-SUBSCRIPTION-ID"
```
Set your resource details:
```sh
RG="devopssteps-rg"
APP="devopssteps-webapp-2026"
```

### Step 5: Enable build automation
Because this is a Python application, Azure needs to install the dependencies during deployment.

Run:
```sh
az webapp config appsettings set \
  --resource-group $RG \
  --name $APP \
  --settings SCM_DO_BUILD_DURING_DEPLOYMENT=true
```
### Step 6: Configure the startup command
```sh
az webapp config set \
  --resource-group $RG \
  --name $APP \
  --startup-file "gunicorn --bind=0.0.0.0 --timeout 600 app:app"
```
### Step 7: Create ZIP package
From inside the azure-appservice-demo directory:
```sh
zip -r app.zip app.py requirements.txt
```

### Step 8: Deploy the application
```sh
az webapp deploy \
  --resource-group $RG \
  --name $APP \
  --src-path app.zip \
  --type zip
```
Azure will upload the ZIP file, build the Python application, install dependencies and deploy it.

Python ZIP deployments use build automation; make sure the ZIP contains the application files at its root, not inside another enclosing directory. 

### Step 9: Browse your application
```sh
echo "https://${APP}.azurewebsites.net"
```
Open the URL.

Also test your health endpoint:
```sh
https://YOUR-APP-NAME.azurewebsites.net/health
```
Expected response:
```sh
{
  "status": "healthy"
}
```
You have now deployed a Python application to Azure without creating or managing a VM.
