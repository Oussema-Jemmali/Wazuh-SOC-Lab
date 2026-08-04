# 🛡️ Wazuh SOC Lab  
### Security Operations Center Laboratory with Wazuh SIEM, pfSense Firewall & HAProxy High Availability

<p align="center">

<img src="assets/logo.png" width="180">

</p>

<p align="center">
A virtual SOC infrastructure designed to simulate enterprise security monitoring, network protection, and highly available web services.
</p>

<p align="center">

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-blue)
![pfSense](https://img.shields.io/badge/Firewall-pfSense-orange)
![HAProxy](https://img.shields.io/badge/Load%20Balancer-HAProxy-green)
![GNS3](https://img.shields.io/badge/Network-GNS3-purple)
![Linux](https://img.shields.io/badge/Platform-Linux-yellow)

</p>

---

# 📌 Project Overview

The **Wazuh SOC Lab** is a cybersecurity infrastructure project that combines:

- Security Information and Event Management (SIEM)
- Firewall protection
- Load balancing
- Web server availability
- Network simulation

The objective is to build a realistic enterprise-like environment where security events can be collected, analyzed, and monitored while maintaining service availability.

The entire infrastructure was simulated using **GNS3** and **VirtualBox**.

---

# 🏗️ Architecture

<p align="center">

<img src="assets/architecture.png" width="700">

</p>


The laboratory contains:

| Component | Role |
|-----------|------|
| pfSense | Firewall, Router, HAProxy Load Balancer |
| Apache1 | Web Server + Wazuh Agent |
| Apache2 | Secondary Web Server |
| Wazuh Server | SIEM Platform |

---

# 🌐 Network Topology

```
                         Internet
                            |
                         pfSense
                  Firewall + HAProxy
                            |
                         Switch
          _________________|_________________
         |                 |                |
      Apache1           Apache2       Wazuh Server
   (Wazuh Agent)      (Web Server)      (SIEM)
```

---

# ⚙️ Implemented Features

## 🔥 pfSense Firewall

Implemented:

- Network gateway configuration
- Firewall management
- Internal network connectivity
- HAProxy package integration

---

## ⚖️ HAProxy Load Balancing

Configured:

- Frontend listener
- Backend pool
- Apache1 and Apache2 servers
- Health monitoring

HAProxy provides:

- Traffic distribution
- Backend availability checking
- Automatic failover

---

## 🖥️ Apache Web Servers

Two Apache servers were deployed:

### Apache1

Role:

- Primary web server
- Wazuh monitored endpoint

### Apache2

Role:

- Backup web server
- High availability backend

---

## 🛡️ Wazuh SIEM Deployment

Configured:

- Wazuh Server
- Wazuh Dashboard
- Wazuh Agent on Apache1

The platform provides:

- Log collection
- Security event analysis
- Endpoint monitoring
- Alert generation

---

# 🧪 Testing & Validation

## HAProxy Failover Test

A high availability test was performed:

### Scenario

1. Apache1 and Apache2 were running.
2. Client accessed the service through HAProxy.
3. Apache service was stopped on Apache1.
4. HAProxy detected Apache1 failure.
5. Traffic continued through Apache2.

Result:

```
Apache1  → DOWN

Apache2  → ACTIVE

Service  → AVAILABLE
```

✅ HAProxy successfully maintained service availability.

---

# 🧰 Technologies Used

| Technology | Purpose |
|------------|---------|
| Wazuh | SIEM and security monitoring |
| pfSense | Firewall and routing |
| HAProxy | Load balancing |
| Apache2 | Web services |
| Ubuntu Server | Linux infrastructure |
| GNS3 | Network simulation |
| VirtualBox | Virtualization |

---

# 📂 Repository Structure

```
Wazuh-SOC-Lab/

├── README.md
├── LICENSE
├── .gitignore

├── docs/
│   ├── 01-Project-Overview.md
│   ├── 02-Lab-Architecture.md
│   ├── 03-GNS3-Setup.md
│   ├── 04-pfSense-Configuration.md
│   ├── 05-HAProxy-Configuration.md
│   ├── 06-Wazuh-Server-Installation.md
│   ├── 07-Wazuh-Agent-Installation.md
│   ├── 08-Testing-and-Validation.md
│   ├── 09-Troubleshooting.md
│   └── 10-Future-Improvements.md

├── configs/
│   ├── pfsense/
│   │   ├── haproxy-backend.md
│   │   └── haproxy-frontend.md
│   │
│   ├── wazuh/
│   │   ├── ossec.conf
│   │   ├── agent.conf
│   │   └── manager-notes.md
│   │
│   └── apache/
│       ├── apache1-config.md
│       └── apache2-config.md

├── screenshots/

└── assets/
    ├── architecture.png
    └── logo.png
```

---

# 🎯 Skills Demonstrated

This project demonstrates practical knowledge in:

### Cybersecurity

- SIEM deployment
- Security monitoring
- Log analysis
- Endpoint monitoring

### Network Security

- Firewall configuration
- Network segmentation
- Traffic management
- High availability design

### Infrastructure

- Linux administration
- Virtualization
- Network simulation
- Service deployment

---

# 🚀 Future Improvements

Planned enhancements:

- Add Suricata IDS/IPS integration
- Add Windows endpoint monitoring with Sysmon
- Create custom Wazuh detection rules
- Add attack simulation scenarios
- Automate deployment using Ansible
- Integrate additional security monitoring tools

---

# 👤 Author

**Oussema Jemmali**

Cybersecurity Engineering Student / SOC Enthusiast

Focus areas:

- Network Security
- SIEM
- Firewall Administration
- Infrastructure Security

---

# 📜 License

This project is licensed under the MIT License.