# WSL-DOCKER-
🐧 How to Use WSL and Docker on Windows or Linux for Cybersecurity Labs

This guide shows how to:

* Set up **WSL** (Windows Subsystem for Linux)
* Install **Docker** on Windows (with WSL2)
* Run real **security tools** like Suricata, Zeek, or Kali Linux
* Simulate traffic, malware, DNS abuse, and port scans for detection practice

---

## 💻 Why Use WSL and Docker?

* Run Linux tools on Windows without VirtualBox
* Easily reset and manage isolated cybersecurity labs
* Lightweight, professional-grade test environments
* Practice blue team and threat hunting skills safely

---

## 🪟 For Windows Users

### 1. Enable Required Features

Open **PowerShell as Administrator** and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

➡️ **Then restart your computer.**

---

### 2. Install WSL and Ubuntu

After reboot, run:

```powershell
wsl --install
```

> ✅ This will auto-install Ubuntu (default is Ubuntu 22.04) and set up WSL 2.

If not, you can manually install Ubuntu:

* Open **Microsoft Store**
* Search for **Ubuntu 22.04**
* Install and launch it
* Set your **Linux username** and **password**

---

### 3. Install Docker Desktop for Windows

1. Download Docker: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. During setup:

   * Choose **WSL 2 backend**
   * Enable integration with your **Ubuntu distro**
3. After installation, open **Ubuntu** and test Docker:

```bash
docker --version
```

---

✅ You're now ready to:

* Pull and run SIEM/security tools like Suricata, Zeek, Wazuh, ELK
* Build custom incident detection labs
* Practice log analysis and alerting like a real SOC

---

## 🔒 Example: Run Suricata

```bash
docker pull jasonish/suricata
docker run --rm -it --net=host --cap-add=NET_ADMIN jasonish/suricata -i eth0
```

---

