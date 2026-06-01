# 🎯 🔥 Azure Storage (Hands-On)
👉 **Azure Storage (Blob Storage + Upload + Static Website Hosting)**
---

# 🧠 1. What is Azure Storage?

👉 Azure Storage = service to store:

* Files
* Images
* Backups
* Static websites

👉 Equivalent of AWS S3

---

# 📦 2. Blob Storage (Core Concept)

👉 **Blob Storage** = object storage for unstructured data

✔ Use cases:

* Website hosting
* Image storage
* Logs & backups

---

# 💻 🧪 3. HANDS-ON: Create Storage Account

Go to
**Microsoft Azure Portal**

---

## 🔹 Steps:

1. Search → **Storage Accounts**
2. Click **Create**

---

## Fill details:

* Resource Group: `devops-rg`
* Storage name: `devopsstorage123` (unique)
* Region: nearest
* Performance: Standard
* Redundancy: LRS

👉 Click **Create**

⏳ Wait 1–2 minutes

---

> “Storage Account is the entry point for all storage services in Azure.”

---

# 📁 4. Create Container (Blob Storage)

---

## 💻 Steps:

1. Go to Storage Account
2. Click **Containers**
3. Click **+ Container**

---

## Settings:

* Name: `mycontainer`
* Access level: **Public (for demo)**

---

> “Container is like a folder where you store your files.”

---

# 📤 5. Upload Files

---

## 💻 Steps:

1. Open container
2. Click **Upload**
3. Select file (image / HTML)
4. Click Upload

---

## 🔗 Get URL:

👉 Click file → Copy URL

Example:

```text id="bloburl"
https://devopsstorage123.blob.core.windows.net/mycontainer/index.html
```

---

> “Now your file is publicly accessible via URL.”

---

# 🌐 6. Static Website Hosting (VERY IMPORTANT)

---

## 💻 Enable Static Website:

1. Go to Storage Account
2. Click **Static Website**
3. Enable it

---

## Configure:

* Index document: `index.html`
* Error document: `404.html`

---

## 📤 Upload Website Files:

👉 Upload into:

```text id="webcontainer"
$web
```

---

## 🌍 Access Website:

```text id="weburl"
https://<storage-name>.z13.web.core.windows.net
```

---

> “Now you have deployed a live website without any server — this is serverless hosting.”

---

# 🧠 Troubleshooting

---

## ❌ Website not loading?

✔ Check:

* Static website enabled
* File name = `index.html`
* Uploaded to `$web`

---

# 🧠 Summary

 - ✔ Created Storage Account
 - ✔ Uploaded files
 - ✔ Hosted static website

---

> “Azure Blob Storage allows you to host websites without managing servers.”

---
