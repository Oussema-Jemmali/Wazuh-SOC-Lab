# Wazuh Server Installation

## Overview

The Wazuh server was deployed on an Ubuntu Server virtual machine to provide centralized security monitoring for the SOC laboratory.

The Wazuh platform acts as the Security Information and Event Management (SIEM) solution, collecting and analyzing security events from monitored endpoints.

## Wazuh Server Role

The Wazuh server is responsible for:

- Receiving security events from agents.
- Analyzing collected logs.
- Generating security alerts.
- Providing a centralized monitoring dashboard.

## Deployment Architecture

The Wazuh deployment contains the following components:

```
             Wazuh Agent
                 |
                 |
                 v
          Wazuh Manager
                 |
        __________________
       |                  |
       v                  v
Wazuh Indexer       Wazuh Dashboard
```

## System Preparation

Before installing Wazuh, the Ubuntu Server machine was prepared by:

- Updating system packages.
- Verifying network connectivity.
- Assigning a static IP address.
- Ensuring communication with laboratory devices.

System update command:

```bash
sudo apt update && sudo apt upgrade -y
```

## Wazuh Installation

The Wazuh installation was performed using the official installation assistant.

The installation command used:

```bash
sudo bash ./wazuh-install.sh -a
```

The `-a` option performs an all-in-one installation containing:

- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.

## Wazuh Manager Configuration

The Wazuh Manager is the main component responsible for:

- Managing agents.
- Receiving events.
- Applying detection rules.
- Generating alerts.

The manager was configured to accept communication from Wazuh agents deployed on monitored machines.

## Wazuh Dashboard

The Wazuh Dashboard provides a web-based interface used for:

- Monitoring agents.
- Viewing alerts.
- Searching security events.
- Analyzing collected data.

## Verification

After installation, the Wazuh services were checked to verify that all components were running correctly.

Verification includes:

- Accessing the Wazuh Dashboard.
- Checking Wazuh Manager status.
- Confirming that required services are active.

Example verification:

```bash
systemctl status wazuh-manager
```

## Network Communication

The Wazuh server communicates with agents through the configured Wazuh communication channels.

The communication flow is:

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

## Installation Result

The Wazuh server was successfully deployed and ready to receive security events from connected agents.

The final deployment provides centralized monitoring for the SOC laboratory environment.