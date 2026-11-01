# Day-16: App Service Deployment

```sh
GitHub → Azure App Service → Automatic Deployment → Live Website
```
```sh
       GitHub
          │
          │ git push
          ▼
   Azure App Service
          │
          │ Deployment
          ▼
    Live Web App 🚀
```


# HANDS-ON DEMO

## 1️⃣ Start With the Application
We will use our previous website

## 2️⃣ Push Application to GitHub

Create a GitHub repository:

```text id="3w9r7k"
azure-app-service-demo
```

Then:

```bash id="b3k8f1"
git init
git add .
git commit -m "Initial Azure App Service application"
git branch -M main
git remote add origin https://github.com/<username>/azure-app-service-demo.git
git push -u origin main
```

```text id="p5v2r0"
GitHub
 └── azure-app-service-demo
       ├── package.json
       ├── server.js
       └── README.md
```
---

## 3️⃣ GitHub → Azure App Service

This should be the **main demo**.

Go to:

```text
Azure Portal
   ↓
App Services
   ↓
Your Web App
   ↓
Deployment Center
```

Choose GitHub as the source.

Depending on the current Azure portal UI, you'll select/configure:

```text id="c8m1z4"
Source
  ↓
GitHub

Organization
  ↓
Repository
  ↓
Branch: main
```
Azure may configure the deployment workflow for you.

---
## 4️⃣ Trigger the Deployment

Now make a small change.

For example:

```text id="f2d8w7"
Hello from Azure!
```

Change it to:

```text id="f2d8w7"
Hello from Azure App Service!
```

Then:

```bash id="r6k3v9"
git add .
git commit -m "Update application message"
git push origin main
```

```text id="z7q4s2"
GitHub
   │
   │ Push
   ▼
Deployment
   │
   ▼
Azure App Service
   │
   ▼
Live Application
```

Refresh the browser.

🎉 The updated application should appear.
---
> **"এখন লক্ষ্য করুন, আমরা Azure Portal-এ গিয়ে manually কোনো file upload করিনি। শুধু GitHub-এ code push করেছি এবং configured deployment process-এর মাধ্যমে Azure App Service নতুন version deploy করেছে।"**

---
## Hands-on Demo : Understand scaling in App Service
This is an important topic for cloud and DevOps engineers.

Azure App Service supports two types of scaling.

Scale Up (Vertical Scaling)

Increase the compute capacity of the App Service Plan.

For example:
 - B1 → B2
 - More CPU and memory.
 - Higher pricing tier.

Scale Out (Horizontal Scaling)

Increase the number of instances running your application.

For example:
Before scaling
```
Instance 1
Web application
```
After scaling out
```
Instance 1                 Instance 2               Instance 3
Web app                    Web app                  Web app
```
Three application instances share incoming traffic.	

### Practical scaling exercise
 1. Open your App Service.
 2. Select Scale up (App Service plan).
 3. Observe available pricing tiers.
 4. Select Scale out (App Service plan).
 5. Observe the instance count.
 6. If you have a paid tier that supports scaling, increase the instance count to 2.

Important: Free F1 cannot scale out. Basic, Standard and Premium tiers have different scaling limits.

---
## Hands-on Demo : Configure application settings and environment variables
This is especially important for DevOps engineers.

Suppose your application connects to a database. You should not hardcode database credentials in Python source code.

Instead, use App Service application settings.

Azure Portal procedure:
 1. Open your Web App.
 2. Go to Settings → Environment variables (or Configuration, depending on portal layout).
 3. Select App settings.
 4. Click Add.
 5. Add the following:

| Name                   | Value                                            |
| --------------------   | ------------------------------------------------ | 
| APP_ENV                | Production  |
| DATABASE_HOST          | mydatabase.database.windows.net  | 
| DATABASE_NAME            | studentdb | 

Now Save and allow the application to restart.

Now modify your Python code:
```sh
import os

@app.route("/config")
def config():
    environment = os.environ.get("APP_ENV", "Development")

    return {
        "environment": environment
    }
```
Browse:

https://YOUR-APP-NAME.azurewebsites.net/config

Expected output:
```sh
{
  "environment": "Production"
}
```
For real database passwords, use Azure Key Vault references with App Service Managed Identity rather than placing credentials directly in application settings. 

---
## Hands-on Demo : Monitor application logs

A DevOps engineer needs to understand what happens when an application fails.

Let's enable application logging.

Run:
```sh
az webapp log config \
  --resource-group $RG \
  --name $APP \
  --web-server-logging filesystem
```
Then run:
```sh
az webapp log tail \
  --resource-group $RG \
  --name $APP
```
Open your website and refresh it several times.
 * You can observe application and web-server logs.

Alternatively, use Azure Portal:
 * App Service → Monitoring → Log stream

We can investigate with the following some issues:
 - HTTP 500 errors.
 - Application startup failures.
 - Dependency installation errors.
 - Application crashes.
 - HTTP request failures.

Microsoft documentation: Enable diagnostic logging in Azure App Service.
```sh
https://learn.microsoft.com/en-us/azure/app-service/troubleshoot-diagnostic-logs?WT.mc_id=MVP_344197&utm_source=chatgpt.com
```
---

## Azure App Service vs Azure Virtual Machine
This comparison is particularly useful for your students.
| Feature                   | Azure VM                     | Azure App Service                                            |
| -----------------------   | ---------------------------- | ------------------------------------------------ | 
| Service model             | IaaS                         | PaaS                             |             
| OS management             | You manage                   | Microsoft manages  |  
| Web server management     | You manage                   | Platform managed           | 
| Application deployment    | Manual/automated             |Built-in deployment                           |             
| OS patching               | You manage                   | Microsoft manages platform  |  
| Scaling                   | VM scaling                   | App Service scaling           | 
| Custom domain             | Yes                          |Yes                        |             
| HTTPS                     | Configure/manage             | Built-in HTTPS support  |  
| Infrastructure access     | Full VM access               | Limited platform access           | 











