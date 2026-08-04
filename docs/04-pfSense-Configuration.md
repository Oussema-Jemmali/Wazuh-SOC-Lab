# pfSense Configuration

## Overview

pfSense was deployed as the main network security device in the SOC laboratory.

It provides network routing, firewall protection, and hosts the HAProxy load balancing service used to distribute traffic between Apache web servers.

## pfSense Role

In this project, pfSense performs three main roles:

- Firewall
- Network gateway
- HAProxy load balancer

## Network Position

pfSense is connected to the internal laboratory switch with the following devices:

- Apache1 server
- Apache2 server
- Wazuh Server

The traffic flow is:

```
Client
  |
  v
pfSense
  |
  v
Switch
  |
  +---- Apache1
  |
  +---- Apache2
  |
  +---- Wazuh Server
```

## Initial Configuration

After installing pfSense, the following configurations were performed:

- Assigned network interfaces.
- Configured LAN connectivity.
- Verified communication with internal servers.
- Confirmed access to the pfSense web interface.

## Firewall Configuration

pfSense firewall rules were configured to control traffic between network components.

The firewall is responsible for:

- Allowing required communication.
- Blocking unauthorized traffic.
- Protecting internal services.

## HAProxy Installation

The HAProxy package was installed on pfSense to provide load balancing functionality.

HAProxy allows pfSense to:

- Receive client HTTP requests.
- Forward requests to backend web servers.
- Monitor server availability.

## HAProxy Integration

The HAProxy configuration contains two main sections:

### Frontend

The frontend defines:

- Listening address.
- Listening port.
- Incoming HTTP requests.

The frontend receives client connections and forwards them to the configured backend.

### Backend

The backend contains the available web servers:

- Apache1
- Apache2

HAProxy performs health checks to verify that backend servers are available.

## Backend Health Monitoring

HAProxy continuously checks the status of backend servers.

When a server is healthy:

```
HAProxy
   |
   +---- Apache1 (UP)
   |
   +---- Apache2 (UP)
```

When Apache1 becomes unavailable:

```
HAProxy
   |
   +---- Apache1 (DOWN)
   |
   +---- Apache2 (UP)
```

Traffic is automatically redirected to the available server.

## Verification

The pfSense configuration was validated by:

- Accessing the pfSense dashboard.
- Confirming HAProxy service availability.
- Checking backend server status.
- Testing traffic redirection during Apache1 failure.

## Configuration Result

The final pfSense deployment successfully provides:

- Network security control.
- HAProxy load balancing.
- High availability for Apache services.
- Central point for traffic management.