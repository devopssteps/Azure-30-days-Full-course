# 1. What is Azure Blob Storage?

Azure Blob Storage is an object storage service for storing unstructured data such as:

* Images
* Videos
* PDFs
* HTML/CSS/JavaScript files
* Backups
* Log files

Examples:

```text
Blob Storage

images/
videos/
documents/
backup.zip
website/
```

Blob Storage is optimized for massive amounts of unstructured data.

---

# 2. Blob Storage Hierarchy

```text
Azure Storage Account
        │
        ▼
Container
        │
        ▼
Blob
```

Example:

```text
Storage Account (mywebsite)
     │
Container (images)
     │
Blob
logo.png
banner.jpg
index.html
```

---

# 3. What is a Container?

A container is similar to a folder that organizes blobs.

Example:

```text
Storage Account

mycompany

├── images
├── videos
├── website
└── backup
```

---

# 4. Blob Types

Three blob types.

---

## Block Blob

Used for:

* Images
* Videos
* Documents
* Website files

Most common type.

---

## Append Blob

Used for:

* Logging
* Monitoring
* Audit files

New data is appended to the end.

---

## Page Blob

Used for:

* Azure VM disks
* Random read/write workloads

Azure Managed Disks are based on Page Blobs.

---

# 5. Upload & Download Files

Show:

Portal

↓

Storage Account

↓

Container

↓

Upload

Upload:

```text
index.html

style.css

logo.png
```

We can also downloading a file.

---

# 6. Public vs Private Access

## Private

```text
Internet

   ❌

Blob
```

Only authorized users can access.

---

## Public

```text
Internet

   │

Public URL

   │

Blob
```

Anyone with the URL can access, depending on the configured access level.

---

# 7. Blob Access Tiers

## Hot

Frequently accessed.

Examples:

Website images

---

## Cool

Occasionally accessed.

Example:

Monthly backups

---

## Cold (if available in your selected region/account type)

Infrequently accessed data with different cost characteristics than Cool.

---

## Archive

Rarely accessed.

Examples:

Compliance data

Historical backups

---

Comparison:

| Tier    | Storage Cost | Retrieval Speed                  | Typical Use             |
| ------- | ------------ | -------------------------------- | ----------------------- |
| Hot     | Higher       | Fast                             | Active content          |
| Cool    | Lower        | Fast                             | Backup/Reports          |
| Cold    | Lower        | Slower access characteristics    | Long-term inactive data |
| Archive | Lowest       | Retrieval required before access | Long-term archival      |

---

# 8. Blob Lifecycle Management

Lifecycle policies automatically move blobs based on age.

Example:

```text
Day 1

Hot

↓

After 30 Days

Cool

↓

After 180 Days

Archive

↓

After 365 Days

Delete
```

Lifecycle policies help reduce storage costs.

---

# 🧪 Hands-on Demo

---

# Step 1

Azure Portal

↓

Storage Account

↓

Capabilities
↓

Static Website

↓

Enable Static Website

↓

type the file name like index.html and error.html

↓

Click Save

↓

Now we can see the URL of the website as follows just copy the URL and pest it in browser, But it will not show and page because we did not upload file.
```text
https://your-storage-account.zXX.web.core.windows.net
```
---

# Step 2
Now click container

↓

We can see new container created name $web

↓

Get in the container and upload your index.html, image, and other file as you want


---


# Step 3

Now open the browser and refresh the URL which we get before and now we can see the website like as follows 

```text
https://your-storage-account.zXX.web.core.windows.net
```

---

# Step 4

Update Website

Edit:

```html
<h1>Welcome to Azure Blob Storage</h1>
```

Upload again.

Refresh browser.

Changes are reflected.

---

# Step 5

Public vs Private Demo

Create another container.

Keep it Private.

Try opening a blob URL.

Access is denied.

How access can be granted securely when needed.

---

# Step 6

Azure CLI Demo

Login:

```bash
az login
```

Create Storage Account:

```bash
az storage account create \
  --name mystorageaccount12345 \
  --resource-group azure30days-rg \
  --location eastus \
  --sku Standard_LRS
```

Create Container:

```bash
az storage container create \
  --name website \
  --account-name mystorageaccount12345 \
  --auth-mode login
```

Upload a file:

```bash
az storage blob upload \
  --account-name mystorageaccount12345 \
  --container-name website \
  --name index.html \
  --file index.html \
  --auth-mode login
```
Delete the container - if we enable static website from browser we are not able to delete the container we need to delete it from cli
```bash
az storage container delete --name "\$web" --account-name <YourStorageAccountName> --auth-mode login
```
List blobs:

```bash
az storage blob list \
  --account-name mystorageaccount12345 \
  --container-name website \
  --output table \
  --auth-mode login
```

---

# Final Architecture

```text
User
   │
   ▼
Azure Storage Account
        │
        ▼
Blob Container
        │
        ├── index.html
        ├── style.css
        ├── logo.png
        └── script.js
        │
        ▼
Azure Static Website
        │
        ▼
Public URL
```

---
