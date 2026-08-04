# Wazuh Manager Configuration Notes

## Overview

This document describes the configuration and role of the Wazuh Manager deployed on the SOC laboratory server.

The Wazuh Manager is the central component responsible for receiving, analyzing, and managing security events collected from connected agents.

## Wazuh Manager Role

The Wazuh Manager provides:

- Agent management.
- Security event analysis.
- Alert generation.
- Log processing.
- Communication with Wazuh agents.

## Deployment Environment

The Wazuh Manager is installed on:

```
Operating System: Ubuntu Server
Role: SIEM Manager
```

## Architecture

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

## Main Components

The Wazuh deployment contains:

### Wazuh Manager

Responsible for:

- Receiving events from agents.
- Applying detection rules.
- Generating alerts.

### Wazuh Indexer

Responsible for:

- Storing collected events.
- Indexing security data.
- Allowing fast searches.

### Wazuh Dashboard

Responsible for:

- Displaying alerts.
- Monitoring agents.
- Analyzing security events.

## Installation

The Wazuh server was deployed using the official installation assistant.

Installation command:

```bash
sudo bash ./wazuh-install.sh -a
```

The installation deployed the required Wazuh components automatically.

## Service Verification

The status of Wazuh services can be checked using:

```bash
systemctl status wazuh-manager
```

Additional verification can include checking:

- Wazuh Indexer status.
- Wazuh Dashboard availability.
- Agent connectivity.

## Agent Management

The Wazuh Manager manages connected endpoints.

Current monitored endpoint:

| Agent | Role |
|-------|------|
| Apache1 | Web server monitoring endpoint |

## Log Monitoring

The Wazuh Manager receives and analyzes events from Apache1.

Monitored information includes:

- System activity.
- Authentication events.
- Service events.
- Security-related logs.

## Configuration Files

Main Wazuh Manager configuration file:

```
/var/ossec/etc/ossec.conf
```

Rules and detection configurations are stored in:

```
/var/ossec/ruleset/
```

## Troubleshooting Commands

Check Wazuh Manager status:

```bash
systemctl status wazuh-manager
```

Restart Wazuh Manager:

```bash
systemctl restart wazuh-manager
```

Check running services:

```bash
systemctl --type=service | grep wazuh
```

## Current Status

The Wazuh Manager is operational and successfully receives events from the Apache1 Wazuh agent.

The current deployment provides centralized security monitoring for the SOC laboratory environment.