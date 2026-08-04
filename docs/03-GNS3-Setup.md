# GNS3 Setup

## Overview

GNS3 was used to simulate and connect the SOC laboratory infrastructure.

The purpose of using GNS3 is to create a realistic network environment where virtual machines can communicate through a controlled topology similar to an enterprise network.

The virtual infrastructure combines GNS3 with VirtualBox to run and connect the required machines.

## GNS3 Components

The following components were integrated into the GNS3 topology:

- pfSense firewall
- Apache1 Ubuntu Server
- Apache2 Ubuntu Server
- Wazuh Ubuntu Server
- Ethernet switch

## Virtual Machine Integration

The virtual machines were created and managed using VirtualBox, then connected inside GNS3.

The integration allows:

- Centralized network simulation.
- Virtual machine communication through GNS3 links.
- Realistic network traffic flow.
- Easier testing of firewall and load balancing configurations.

## Network Topology Creation

The topology was created using the following steps:

1. Created a new GNS3 project.
2. Added an Ethernet switch.
3. Imported VirtualBox virtual machines.
4. Added all required devices to the workspace.
5. Connected all devices to the switch.
6. Configured network interfaces.
7. Started all virtual machines.

## Device Connections

The final topology contains:

```
                         pfSense
                            |
                            |
                         Switch
          _________________|_________________
         |                 |                |
      Apache1           Apache2       Wazuh Server
   (Wazuh Agent)      (Web Server)      (SIEM)
```

## Network Interface Configuration

Each virtual machine was assigned a network interface connected to the GNS3 internal network.

The interfaces were configured to allow communication between:

- pfSense and internal servers.
- Apache servers and pfSense.
- Apache1 and Wazuh Server.

## Connectivity Verification

After connecting the devices, connectivity was verified using network tests.

The validation included:

- Checking IP address assignments.
- Testing connectivity between machines.
- Confirming communication between Wazuh agent and Wazuh server.
- Verifying access to Apache services through HAProxy.

## VirtualBox Adapter Configuration

During the integration process, VirtualBox network adapters were adjusted to allow GNS3 communication.

The configuration required:

- Assigning dedicated adapters for GNS3 connections.
- Avoiding conflicting network attachments.
- Ensuring each VM had the correct interface connected to the laboratory network.

## Troubleshooting

### Virtual Machine Not Connecting in GNS3

Problem:

VirtualBox adapters were already assigned and could not be connected through GNS3.

Solution:

- Reviewed VirtualBox adapter settings.
- Disabled unused adapters.
- Assigned the correct adapter for GNS3 integration.

---

### Communication Problems Between Devices

Problem:

Devices could not communicate after topology creation.

Solution:

- Verified IP configuration.
- Checked firewall rules.
- Confirmed that all devices were connected to the same internal network.