# Lab Architecture

## Overview

The SOC laboratory architecture is designed to simulate a small enterprise network environment containing security monitoring, firewall protection, and highly available web services.

The infrastructure is composed of four main components connected through a virtual switch inside GNS3:

- pfSense firewall
- Apache1 web server with Wazuh agent
- Apache2 web server
- Wazuh Server

The objective of this architecture is to combine network security, service availability, and centralized security monitoring.

## Network Topology

```
                         Internet
                            |
                         pfSense
                  (Firewall + HAProxy)
                            |
                         Switch
          _________________|_________________
         |                 |                |
      Apache1           Apache2       Wazuh Server
   (Wazuh Agent)      (Web Server)      (SIEM)
```

## Component Description

## pfSense Firewall

### Role

pfSense is the main network security device in the laboratory.

### Responsibilities

- Act as the network gateway.
- Control traffic between networks.
- Provide firewall filtering.
- Host HAProxy service.
- Distribute HTTP traffic between backend servers.

### Services Configured

- Firewall rules.
- HAProxy frontend.
- HAProxy backend.
- Backend health monitoring.

---

## Apache1 Server

### Role

Apache1 is the primary web server and a monitored endpoint.

### Responsibilities

- Host the Apache web service.
- Receive traffic from HAProxy.
- Generate system and service logs.
- Send security events to the Wazuh server through the Wazuh agent.

### Security Monitoring

The Wazuh agent installed on Apache1 allows:

- System monitoring.
- Log collection.
- Security event analysis.
- Agent status tracking.

---

## Apache2 Server

### Role

Apache2 acts as the secondary web server in the HAProxy backend pool.

### Responsibilities

- Provide web service availability.
- Receive traffic when Apache1 becomes unavailable.
- Maintain service continuity during failures.

---

## Wazuh Server

### Role

The Wazuh server provides centralized security monitoring.

### Responsibilities

- Receive logs from Wazuh agents.
- Analyze security events.
- Generate alerts.
- Display monitoring information through the Wazuh dashboard.

### Main Components

The deployment includes:

- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.

---

## Traffic Flow

The normal traffic flow is:

```
Client Request
       |
       v
    pfSense
       |
       v
    HAProxy
       |
       |
  _______________
 |               |
 v               v
Apache1       Apache2
```

HAProxy checks backend availability and forwards requests only to healthy servers.

---

## Security Monitoring Flow

The security event flow is:

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

The Wazuh agent collects events from Apache1 and sends them to the Wazuh server for analysis.

---

## High Availability Design

The HAProxy configuration provides service continuity.

When Apache1 is operational:

```
HAProxy
   |
   |
Apache1 + Apache2
```

When Apache1 fails:

```
HAProxy
   |
   |
Apache2
```

HAProxy automatically removes the failed server from the backend pool and redirects requests to the available server.

## Architecture Benefits

This design provides:

- Centralized security monitoring.
- Firewall protection.
- Service availability.
- Load balancing.
- Realistic SOC infrastructure simulation.
- Practical experience with enterprise security components.