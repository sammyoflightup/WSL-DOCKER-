# WSL-DOCKER-
 How to Use WSL and Docker on Windows or Linux for Cybersecurity Labs
# 🐧 How to Use WSL and Docker on Windows or Linux for Cybersecurity Labs

This guide shows how to:

- Set up **WSL** (Windows Subsystem for Linux)
- Install **Docker** on both Windows and Linux
- Run real **security tools** like Suricata, Zeek, or Kali Linux
- Simulate network traffic and practice how to catch threats like malware, DNS abuse, and port scanning

---

## 💻 Why Use WSL and Docker?

- You can run Linux tools on Windows easily
- You don’t need VirtualBox or dual boot
- You can set up and delete labs without breaking your system
- It's how professionals build safe, isolated environments for testing and detection

---

## ✅ For Windows Users

### 1. Turn on needed features

Open **PowerShell as Administrator** and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
Then restart your computer.

### Install WSL and Ubuntu
