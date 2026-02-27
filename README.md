# Dashi

Dashi is a lightweight static website served by Nginx inside a Debian LXC container running on Proxmox VE.

This project powers a personal dashboard designed to fit my specific needs and preferences.

⚠️ This entire project was purely vibe-coded.
It works.
But you should still read everything carefully before deploying.

Use at your own risk.

---

# 🧠 What This Is

- A personal dashboard
- Fully self-hosted
- Running on Debian inside Proxmox LXC
- Served by Nginx
- Version controlled with Git
- Synced to GitHub

No frameworks.
No Docker.
No orchestration.
Just raw infrastructure and vibes.

---

# 🌐 Important: Internet Requirement

This HTML file loads external libraries via CDN, including:

- React (via CDN)
- ReactDOM (via CDN)
- Google Fonts

Because of this:

- ✅ The server or client must have internet access
- ❌ The site will NOT work fully offline
- ❌ If CDN access is blocked, the page may fail to render properly

If offline capability is required, dependencies must be self-hosted locally.

---

# 🏗️ Infrastructure Stack

- Proxmox VE
- Debian (LXC container)
- Nginx
- Git
- GitHub

---

# 🚀 Full Deployment Guide (From Zero)

## 1️⃣ Create Debian LXC in Proxmox

1. Download Debian template  
   Node → Local → CT Templates → Templates → Download Debian

2. Create container:
   - Hostname: `dashi`
   - Template: Debian
   - Disk: 8GB+
   - CPU: 1+
   - RAM: 512MB+
   - Network: DHCP or Static IP
   - Start after creation

---

## 2️⃣ Enter the Container

From Proxmox shell:

```bash
pct enter <CTID>
```

Example:
```bash
pct enter 101
```

---

## 3️⃣ Update Debian

```bash
apt update
apt upgrade -y
```

---

## 4️⃣ Install Nginx

```bash
apt install nginx -y
systemctl enable nginx
systemctl start nginx
systemctl status nginx
```

At this point, visiting:

```
http://<container-ip>
```

Should show the default Nginx page.

---

## 5️⃣ Deploy This Repository

Install Git:

```bash
apt install git -y
```

Go to web root:

```bash
cd /var/www/html
```

Remove default page:

```bash
rm index.nginx-debian.html
```

Clone this repository directly into the web root:

```bash
git clone https://github.com/yourusername/dashi.git .
```

If the directory is not empty:

```bash
git clone https://github.com/yourusername/dashi.git
cp dashi/index.html /var/www/html/
```

---

## 6️⃣ Verify Deployment

Open:

```
http://<container-ip>
```

You should now see the Dashi dashboard.

If it works:
You are now self-hosting your own dashboard.

---

# 🔄 Updating the Dashboard

If the repo lives inside `/var/www/html`:

```bash
cd /var/www/html
git pull
```

Done.

---

# 📁 Project Structure

```
/var/www/html
│── index.html
```

Simple.
Intentional.
Custom.

---

# ⚠️ Important Disclaimer

This project is tailored to personal needs and preferences.

It has:
- No production hardening
- No firewall configuration guidance
- No SSL setup
- No reverse proxy
- No security tuning

Before exposing this server to the public internet:
- Configure a firewall
- Set up SSL (Let's Encrypt or reverse proxy)
- Disable root SSH login
- Audit configurations

You are responsible for your infrastructure.

Deploy thoughtfully.

---

# 🎯 Purpose

Dashi exists to provide a clean, self-hosted dashboard tailored to my workflow, preferences, and daily needs.

It prioritizes:
- Simplicity
- Control
- Customization
- Independence from third-party hosting platforms

This is infrastructure built to serve me.

---

# 👤 Author

phdalandan

Built with:
- Debian
- Nginx
- Proxmox
- And vibes
