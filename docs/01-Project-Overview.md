# Project Overview

## Project Title

Wazuh SOC Lab with pfSense Firewall and HAProxy Load Balancing

## Introduction

This project consists of designing and implementing a virtual Security Operations Center (SOC) laboratory environment using Wazuh SIEM, pfSense firewall, HAProxy load balancer, Apache web servers, and GNS3 network simulation.

The objective of this project is to create a realistic infrastructure where network security, service availability, and security monitoring are integrated together.

The laboratory simulates a small enterprise environment containing a firewall, web servers, and a centralized SIEM platform for monitoring and analyzing security events.

## Project Objectives

The main objectives of this project are:

- Deploy a Wazuh SIEM platform for centralized security monitoring.
- Configure pfSense as a firewall and network gateway.
- Implement HAProxy as a load balancer to provide service availability.
- Deploy multiple Apache web servers behind HAProxy.
- Configure Apache1 as a monitored endpoint using the Wazuh agent.
- Simulate the complete infrastructure using GNS3 and VirtualBox.
- Validate high availability by testing web server failover.

## Project Architecture

The laboratory is composed of the following components:

- pfSense:
  - Firewall
  - Router
  - HAProxy load balancer

- Apache1:
  - Web server
  - Wazuh monitored endpoint

- Apache2:
  - Secondary web server
  - High availability backend server

- Wazuh Server:
  - SIEM platform
  - Log collection and analysis server

## Technologies Used

| Technology | Role |
|------------|------|
| Wazuh | Security Information and Event Management (SIEM) |
| pfSense | Firewall and network gateway |
| HAProxy | Load balancing and high availability |
| Apache2 | Web server services |
| Ubuntu Server | Operating system for Linux servers |
| GNS3 | Network simulation platform |
| VirtualBox | Virtual machine virtualization |

## Implemented Features

The project includes:

- Virtual network topology creation using GNS3.
- pfSense firewall deployment.
- HAProxy frontend and backend configuration.
- Load balancing between Apache1 and Apache2.
- Wazuh server installation and configuration.
- Wazuh agent deployment on Apache1.
- High availability testing through Apache service failure simulation.

## Testing Scenario

The main validation scenario performed in this project:

1. Both Apache servers are running behind HAProxy.
2. Client requests are forwarded through HAProxy.
3. Apache1 service is stopped intentionally.
4. HAProxy detects Apache1 as unavailable.
5. Traffic continues through Apache2 successfully.

This confirms that the implemented load balancing and failover mechanism is working correctly.

## Project Scope

This SOC laboratory demonstrates practical skills in:

- Network security architecture
- Firewall administration
- SIEM deployment
- Security monitoring
- Reverse proxy and load balancing
- Linux server administration
- Infrastructure troubleshooting

## Future Improvements

Possible extensions of this project include:

- Adding Suricata IDS/IPS integration.
- Deploying additional Wazuh agents.
- Adding Windows endpoint monitoring with Sysmon.
- Implementing automated attack simulations.
- Creating custom Wazuh detection rules.
- Integrating additional monitoring dashboards.