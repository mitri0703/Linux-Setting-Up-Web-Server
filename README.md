# Project 6 – Linux Web Server Setup (Apache on Ubuntu ARM)

![Apache](https://img.shields.io/badge/Apache2-Web%20Server-D22128?style=flat&logo=apache&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Domain](https://img.shields.io/badge/Domain-Linux%20%7C%20Apache%20%7C%20Web%20Server%20%7C%20Systems%20Admin-blueviolet)

---

## Overview

This project builds and configures an **Apache web server** on Ubuntu 24.04 ARM running in a Parallels VM on Apple Silicon Mac. It demonstrates Linux system administration, Apache deployment, service validation, and custom HTML hosting — documented with terminal output and browser evidence at each step.

---

## Environment

| Tool | Purpose |
|------|---------|
| Ubuntu 24.04 ARM | Host OS for Apache web server |
| Apache2 | HTTP web server |
| Parallels Desktop | VM environment on Apple Silicon Mac |
| Terminal | Linux CLI for installation and configuration |
| Firefox | Browser-based service validation |
| HTML | Custom hosted content |
| GitHub | Documentation and version control |

---

## Project Steps

### 🟢 Step 1 — System Update & Package Install

**Actions Taken:**
1. Deployed Ubuntu 24.04 ARM in Parallels Desktop
2. Ran `sudo apt update && sudo apt upgrade -y` to update all system packages
3. Installed Apache2 using `sudo apt install apache2 -y`
4. Confirmed package dependencies resolved and service symlinks created

**Key Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 -y
```

![System Update and Apache Install](Project%20Screenshots/01-apt-update-apache-install.png)
*apt upgrade completing — Apache2 installed and service symlinks created on Ubuntu 24.04 ARM*

---

### 🔵 Step 2 — Apache Service Validation

**Actions Taken:**
1. Ran `sudo systemctl status apache2` to verify service health
2. Confirmed: **active (running)** since Apr 14 23:18:18 EDT
3. Verified Apache2 service enabled and preset correctly
4. Confirmed Main PID assigned and worker processes running

**Key Command:**
```bash
sudo systemctl status apache2
```

![Apache Service Status](Project%20Screenshots/02-apache-service-status.png)
*apache2.service confirmed active (running) — enabled, 3 worker processes, 5.1M memory*

---

### 🟡 Step 3 — Default Apache Page (Localhost Test)

**Actions Taken:**
1. Opened Firefox and navigated to `http://localhost`
2. Confirmed Apache2 Ubuntu Default Page loaded — **"It works!"**
3. Validated Apache was serving HTTP traffic on port 80 before customization

![Apache Default Page](Project%20Screenshots/03-apache-default-page.png)
*Apache2 Ubuntu Default Page confirming web server is operational at http://localhost*

---

### 🔴 Step 4 — Custom HTML Deployment & Final Validation

**Actions Taken:**
1. Replaced default Apache landing page using terminal redirection:
```bash
sudo tee /var/www/html/index.html
```
2. Wrote custom HTML content to `/var/www/html/index.html`
3. Performed hard browser refresh to clear cache
4. Validated custom page loaded successfully at `http://localhost`

**Final Output:**
> **Linux Web Server Project Complete**
> Apache is successfully running on Ubuntu 24.04 ARM.
> Built in Parallels VM on Apple Silicon Mac.

![Custom HTML Page Live](Project%20Screenshots/04-custom-html-page-live.png)
*Custom HTML page live at http://localhost — confirming full Apache deployment and content hosting*

---

## Problems Solved

| Issue | Root Cause | Resolution |
|-------|-----------|------------|
| AMD64 vs ARM64 ISO mismatch | Downloaded wrong Ubuntu image for Apple Silicon | Downloaded correct Ubuntu ARM64 desktop image |
| Parallels VM creation errors | Incorrect VM configuration workflow | Corrected Parallels setup for ARM architecture |
| Apache default page cache | Browser serving cached default page after HTML replacement | Performed hard refresh to clear browser cache |
| Default index not replaced | File permission issue with direct edit | Used `sudo tee` via terminal to overwrite `/var/www/html/index.html` |

---

## Screenshot Naming Reference

| File Name | Description |
|-----------|-------------|
| `01-apt-update-apache-install.png` | apt upgrade completing — Apache2 installed with symlinks |
| `02-apache-service-status.png` | systemctl status apache2 — active (running) confirmed |
| `03-apache-default-page.png` | Apache2 default page at http://localhost — "It works!" |
| `04-custom-html-page-live.png` | Custom HTML page live — project completion confirmed |

---

## Skills Demonstrated

| Skill | How It Was Applied |
|-------|--------------------|
| Linux System Administration | Managed packages, services, and file system via CLI on Ubuntu ARM |
| Apache Web Server Deployment | Installed, configured, and validated Apache2 on Ubuntu 24.04 |
| Service Management | Used systemctl to verify Apache service health and enable on boot |
| Browser Cache Validation | Diagnosed and resolved cached page issue with hard refresh |
| HTML Deployment | Wrote and hosted custom HTML content via terminal file redirection |
| VM Networking & Compatibility | Resolved Apple Silicon ARM64 compatibility issues in Parallels |
| Service Troubleshooting | Diagnosed Apache install output and confirmed correct symlink creation |

---

## Lessons Learned

**Architecture matters before you download anything.** The first obstacle was an AMD64 vs ARM64 ISO mismatch — the wrong Ubuntu image won't boot on Apple Silicon hardware at all. Verifying the target architecture before provisioning a VM is a step that gets skipped until it causes a failure. It shouldn't be.

**`systemctl status` is the fastest way to confirm a service is real.** The Apache default page loading in a browser is encouraging — but `systemctl status apache2` showing active (running) with a PID and worker processes is the actual confirmation that the service is healthy and will survive a reboot. Browser output can be cached. Service status can't be faked.

**Browser cache is a silent troubleshooter's trap.** After replacing the default Apache index file, the browser still showed the old page. Nothing in the terminal suggested a problem — the file was overwritten, Apache was running, the path was correct. A hard refresh cleared it immediately. In production, this exact scenario causes unnecessary escalations. Checking the cache should be step one before investigating the server.

---

## Repository Structure

```text
Project-8-Linux-Web-Server/
├── Project Screenshots/
│   ├── 01-apt-update-apache-install.png
│   ├── 02-apache-service-status.png
│   ├── 03-apache-default-page.png
│   └── 04-custom-html-page-live.png
├── PROJECT_DOCUMENTATION.md
└── README.md
```

---

## References

- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/2.4/)
- [Ubuntu Server Guide](https://ubuntu.com/server/docs)
- [systemd Service Management](https://www.freedesktop.org/software/systemd/man/systemctl.html)
