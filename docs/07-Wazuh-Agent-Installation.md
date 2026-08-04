# Wazuh Agent Installation

## Overview

The Wazuh agent was installed on Apache1 to enable security monitoring and log collection from the web server.

Apache1 acts as both a web server and a monitored endpoint connected to the Wazuh SIEM platform.

## Wazuh Agent Role

The Wazuh agent is responsible for:

- Collecting system and security events.
- Monitoring endpoint activity.
- Forwarding logs to the Wazuh Manager.
- Allowing centralized security analysis.

## Agent Deployment Architecture

The communication flow between Apache1 and the Wazuh server is:

```
              Apache1 Server

                    |
                    |
                    v

              Wazuh Agent

                    |
                    |
                    v

            Wazuh Manager

                    |
                    |
                    v

            Wazuh Dashboard
```

## Installation Preparation

Before installing the agent, Apache1 was prepared by:

- Updating system packages.
- Verifying network connectivity with the Wazuh server.
- Confirming that the server has a valid IP address.

System update command:

```bash
sudo apt update && sudo apt upgrade -y
```

## Agent Installation

The Wazuh agent package was installed on Apache1.

The installation process includes:

1. Installing the Wazuh agent package.
2. Configuring the Wazuh Manager address.
3. Registering the agent.
4. Starting the Wazuh agent service.

## Agent Configuration

The agent was configured to communicate with the Wazuh Manager.

The configuration defines:

- Wazuh Manager IP address.
- Agent identity.
- Communication settings.

The agent configuration file is:

```
/var/ossec/etc/ossec.conf
```

## Agent Registration

After installation, Apache1 was registered with the Wazuh Manager.

The registration process allows the Wazuh Manager to:

- Identify the endpoint.
- Receive events from the agent.
- Apply monitoring rules.

## Starting the Agent

The Wazuh agent service was started after configuration.

Command:

```bash
sudo systemctl start wazuh-agent
```

The service status was verified using:

```bash
sudo systemctl status wazuh-agent
```

## Verification

The agent status was checked from the Wazuh Dashboard.

Successful communication is confirmed when:

- Apache1 appears in the agent list.
- The agent status is active.
- Events are received from the endpoint.

## Monitoring Capabilities

The Wazuh agent on Apache1 provides monitoring for:

- System activity.
- Service status.
- Authentication events.
- Log files.
- Security-related events.

## Installation Result

Apache1 was successfully integrated into the SOC environment as a monitored endpoint.

The Wazuh agent allows the Wazuh server to collect and analyze security information from the web server.