# **1. Install Azure Functions Core Tools v4 in WSL (Ubuntu)**

Recommended for your Windows + WSL setup

## **Step 1 — Open Ubuntu in WSL**

Open your Ubuntu terminal from Windows Terminal or VS Code.

Check your Ubuntu version:

```
lsb_release -a
```

Check your Linux architecture:

```
uname -m
```

For the Microsoft APT instructions below, the expected architecture is `x86_64` (AMD64).

Update Ubuntu:

```
sudo apt update
sudo apt upgrade -y
```

Install the required packages:

```
sudo apt install -y curl gnupg apt-transport-https lsb-release
```

## **Step 2 — Add Microsoft's package signing key**

Run:

```
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc \
| gpg --dearmor \
| sudo tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null
```

This adds Microsoft's signing key so Ubuntu can verify the packages.

## **Step 3 — Add Microsoft's package repository**

Run:

```
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
```

This automatically detects your Ubuntu release codename.

For example:

- Ubuntu 22.04 → jammy
- Ubuntu 24.04 → noble

## **Step 4 — Install Azure Functions Core Tools v4**

Update the package list:

```
sudo apt update
```

Install:

```
sudo apt install azure-functions-core-tools-4
```

Installation complete

These commands follow Microsoft's documented Ubuntu installation method.&#x20;

Microsoft Learn+1



## **Step 5 — Verify installation**

Run:

```
func --version
```

You should see a version:

```
4.16.1
```

Also check:

```
func --help
```
