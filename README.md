# 🌧️ WSL-DOCKER: How to Use WSL and Docker on Windows or Linux for Cybersecurity Labs

This guide shows how to:

* Set up **WSL** (Windows Subsystem for Linux)
* Install **Docker** on Windows (with WSL2)
* Run real **security tools** like Suricata, Zeek, Wazuh, or Elastic Stack
* Simulate traffic, malware, DNS abuse, and port scans for detection practice

---

## 📁 GitHub Repository Structure

```
WSL-Docker-Cyberlab/
├── README.md                 # Main setup and usage guide
├── docker-compose.yml       # Sample file for multi-container setups (optional)
├── /labs                    # Lab instructions or test scenarios
│   ├── metasploitable.md    # Setup and test with Metasploitable2
│   └── zeek-analysis.md     # PCAP-based threat detection using Zeek
├── /pcaps                   # Sample PCAP files for testing
│   └── example.pcap
├── /scripts                 # Bash or PowerShell scripts to automate setup
├── /screenshots             # Visual setup guides or tool output screenshots
└── /pdf                     # Exported documentation in PDF format
    └── WSL_Docker_Cyberlab_Guide.pdf
```

---

## Why Use WSL and Docker?

* Run Linux tools on Windows without VirtualBox
* Easily reset and manage isolated cybersecurity labs
* Lightweight, professional-grade test environments
* Practice blue team and threat hunting skills safely

---

## For Windows Users

### 1. Enable Required Features

Open **PowerShell as Administrator** and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**Then restart your computer.**

---

### 2. Install WSL and Ubuntu

After reboot, run:

```powershell
wsl --install
```

> This will auto-install Ubuntu (default is Ubuntu 22.04) and set up WSL 2.

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

You're now ready to:

* Pull and run SIEM/security tools like Suricata, Zeek, Wazuh, ELK
* Build custom incident detection labs
* Practice log analysis and alerting like a real SOC

---

## Example: Run Suricata

```bash
docker pull jasonish/suricata
docker run --rm -it --net=host --cap-add=NET_ADMIN jasonish/suricata -i eth0
```

---

## Example: Run Wazuh All-in-One Stack

```bash
git clone https://github.com/wazuh/wazuh-docker.git
cd wazuh-docker
docker compose -f generate-indexer-certs.yml run --rm generator
docker compose up -d
```

Access Wazuh Web UI:

```
https://localhost
Username: admin
Password: SecretPassword (or see .env file)
```

---

## Example: Run Elastic Stack (ELK)

```bash
docker pull sebp/elk
docker run -d -p 5601:5601 -p 9200:9200 -p 5044:5044 --name elk sebp/elk
```

Access Kibana at:

```
http://localhost:5601
```

---

## Example: Run Zeek for Passive Traffic Analysis

```bash
docker pull blacktop/zeek
```

Run Zeek to analyze a pcap file:

```bash
docker run -v $PWD:/pcap blacktop/zeek -r /pcap/example.pcap
```

> You can also mount a live interface or use `--net=host` for live analysis if supported.

Zeek will output detailed connection logs, DNS queries, HTTP activity, and more.

---

## Example: Run Metasploitable2 to Simulate Attacks

1. Download the Metasploitable2 VM: [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/)
2. Run it in **VirtualBox** or **VMware** on the same host
3. From WSL or another container, scan and test it using tools like:

```bash
nmap -A <metasploitable-ip>
```

You can simulate attacks and detect them using Suricata, Zeek, or Wazuh in real time.

---

## Forward Windows Logs to ELK or Wazuh

1. Install **Winlogbeat** from Elastic on your Windows host.
2. Edit `winlogbeat.yml` to point to your ELK or Wazuh server.
3. Start the service:

```powershell
Start-Service winlogbeat
```

This will stream Windows Event Logs directly into your SIEM!

---

