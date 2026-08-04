# Troubleshooting

## Overview

During the implementation of the SOC laboratory, several configuration and integration issues were encountered.

This document describes the main problems, their causes, and the solutions applied.

---

# GNS3 and VirtualBox Integration Issues

## Problem

Virtual machines imported from VirtualBox were not always connecting correctly inside GNS3.

Some adapters were already assigned, preventing GNS3 from creating the required connections.

## Cause

The VirtualBox network adapters were conflicting with GNS3 interfaces.

## Solution

The following actions were performed:

- Reviewed VirtualBox network adapter configuration.
- Disabled unused adapters.
- Assigned the correct adapter for GNS3 communication.
- Verified that each virtual machine was connected to the correct network.

## Result

All virtual machines were successfully integrated into the GNS3 topology.

---

# Network Connectivity Issues

## Problem

Some machines could not communicate with each other after creating the topology.

## Possible Causes

- Incorrect IP configuration.
- Wrong network interface assignment.
- Firewall rules blocking traffic.
- Incorrect GNS3 connections.

## Solution

The following checks were performed:

- Verified IP addresses.
- Tested connectivity using ping.
- Checked pfSense interface configuration.
- Reviewed firewall rules.

Example command:

```bash
ping <destination-ip>
```

## Result

Network communication between required components was restored.

---

# HAProxy Backend Not Available

## Problem

HAProxy did not detect Apache servers correctly as available backend servers.

## Possible Causes

- Incorrect backend IP addresses.
- Wrong service ports.
- Apache service not running.
- Health check failure.

## Solution

The following configurations were verified:

- Backend server addresses.
- HTTP service availability.
- Apache service status.
- HAProxy backend configuration.

Apache service verification:

```bash
sudo systemctl status apache2
```

## Result

HAProxy successfully detected the backend servers.

---

# HAProxy Failover Not Working

## Problem

Traffic was not redirected correctly when a backend server failed.

## Possible Causes

- Incorrect health check configuration.
- Backend server still considered available.
- Configuration not applied.

## Solution

The following steps were performed:

- Verified HAProxy health checks.
- Restarted HAProxy service after configuration changes.
- Confirmed backend server status from the HAProxy dashboard.

## Result

HAProxy successfully removed the unavailable server and redirected traffic to the available backend.

---

# Wazuh Agent Connection Problem

## Problem

Apache1 agent was not appearing as active in the Wazuh Dashboard.

## Possible Causes

- Incorrect Wazuh Manager address.
- Agent service not running.
- Network communication issue.

## Solution

The following checks were performed:

Verify agent service:

```bash
sudo systemctl status wazuh-agent
```

Restart agent:

```bash
sudo systemctl restart wazuh-agent
```

Verify network communication between Apache1 and Wazuh Server.

## Result

Apache1 successfully connected to the Wazuh Manager.

---

# Wazuh Server Resource Management

## Problem

The Wazuh server consumed significant system resources during operation.

## Cause

SIEM platforms require memory and CPU resources for:

- Log indexing.
- Event analysis.
- Dashboard services.

## Solution

Resource usage was monitored and unnecessary services were limited when required.

## Result

The Wazuh environment remained operational with available resources.

---

# General Troubleshooting Approach

When facing issues in the laboratory, the following methodology was applied:

1. Identify the affected component.
2. Check service status.
3. Verify network connectivity.
4. Review configuration files.
5. Check logs.
6. Apply corrections.
7. Retest functionality.

## Conclusion

The troubleshooting process helped ensure proper integration between:

- GNS3 network simulation.
- pfSense firewall.
- HAProxy load balancing.
- Apache web servers.
- Wazuh monitoring platform.