# 🛡️ Wazuh SOC Lab

<h3 align="center">
Enterprise-like SOC Infrastructure Simulation using Wazuh SIEM, pfSense Firewall, HAProxy Load Balancing and GNS3
</h3>

<p align="center">
A cybersecurity laboratory designed to simulate a Security Operations Center (SOC) environment by integrating security monitoring, network protection, and high availability services.
</p>

<p align="center">

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-blue)
![pfSense](https://img.shields.io/badge/Firewall-pfSense-orange)
![HAProxy](https://img.shields.io/badge/Load%20Balancer-HAProxy-green)
![GNS3](https://img.shields.io/badge/Network%20Simulation-GNS3-purple)
![Linux](https://img.shields.io/badge/OS-Ubuntu%20Server-yellow)

</p>

---

# 📌 Project Overview

The **Wazuh SOC Lab** is a virtual cybersecurity infrastructure built to reproduce a simplified enterprise SOC environment.

The project combines:

- SIEM monitoring using Wazuh
- Network security using pfSense firewall
- High availability using HAProxy
- Web service deployment using Apache servers
- Network simulation using GNS3

The goal is to demonstrate how security monitoring and network services can be integrated into a centralized security architecture.

---

# 🏗️ Lab Architecture

<p align="center">

<img src="assets/architecture.png" width="750">

</p>


The infrastructure consists of:

| Component | Role |
|-----------|------|
| pfSense | Firewall, gateway and HAProxy load balancer |
| Apache1 | Web server + Wazuh monitored endpoint |
| Apache2 | Secondary web server for failover |
| Wazuh Server | SIEM platform for security monitoring |
| GNS3 | Network topology simulation |

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

# ⚙️ Implemented Components

## 🔥 pfSense Firewall

pfSense was deployed as the main network security component.

Implemented:

- Network routing
- Firewall management
- Internal network communication
- HAProxy package installation

Documentation:

```
docs/04-pfSense-Configuration.md
```

---

# ⚖️ HAProxy Load Balancing

HAProxy was configured on pfSense to provide high availability for Apache services.

Implemented:

- Frontend configuration
- Backend configuration
- Health checks
- Automatic failover

Architecture:

```
                 HAProxy

                    |
          ___________________
         |                   |
         v                   v

      Apache1             Apache2
       UP                  UP
```

During failure:

```
                 HAProxy

                    |
                    v

                 Apache2
                   UP
```

Documentation:

```
docs/05-HAProxy-Configuration.md

configs/pfsense/
├── haproxy-frontend.md
└── haproxy-backend.md
```

---

# 🖥️ Apache Web Servers

Two Apache servers were deployed as HAProxy backend nodes.

## Apache1

Role:

- Primary web server
- Wazuh monitored endpoint

Integrated with:

- Wazuh Agent

Configuration:

```
configs/apache/apache1-config.md
```

---

## Apache2

Role:

- Secondary web server
- Failover server

Configuration:

```
configs/apache/apache2-config.md
```

---

# 🛡️ Wazuh SIEM Deployment

The Wazuh platform was deployed on Ubuntu Server.

Components:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

The Wazuh agent was installed on Apache1 to collect security events.

Architecture:

```
Apache1

   |
   |
Wazuh Agent

   |
   |
Wazuh Manager

   |
   |
Wazuh Dashboard
```

Documentation:

```
docs/

06-Wazuh-Server-Installation.md
07-Wazuh-Agent-Installation.md
```

Configuration references:

```
configs/wazuh/

├── ossec.conf
├── agent.conf
└── manager-notes.md
```

---

# 🧪 Testing and Validation

## HAProxy Failover Test

A high availability test was performed.

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

The test confirmed successful automatic failover.

---

# 📸 Project Screenshots

Screenshots demonstrating the implementation:

```
screenshots/

├── gns3.png
├── haproxy-dashboard.png
├── backend-online.png
├── backend-failover.png
├── wazuh-agent.png
└── wazuh-dashboard.png
```

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
│
├── configs/
│   ├── pfsense/
│   ├── wazuh/
│   └── apache/
│
├── screenshots/
│
└── assets/
    └── architecture.png
```

---

# 🧰 Technologies Used

| Technology | Usage |
|------------|-------|
| Wazuh | SIEM and security monitoring |
| pfSense | Firewall and network security |
| HAProxy | Load balancing and failover |
| Apache2 | Web services |
| Ubuntu Server | Linux infrastructure |
| GNS3 | Network simulation |
| VirtualBox | Virtualization |

---

# 🚀 Future Improvements

Planned enhancements:

- Integrate Suricata IDS/IPS
- Add Windows endpoint monitoring with Sysmon
- Create custom Wazuh detection rules
- Add attack simulation scenarios
- Automate deployment using Ansible
- Expand the SOC monitoring environment

---

# 👤 Author

**Oussema Jemmali**

Cybersecurity Engineering Student

Areas of interest:

- SOC Operations
- Network Security
- SIEM Technologies
- Firewall Administration
- Infrastructure Security

---

# 📜 License

This project is licensed under the MIT License.