# HAProxy Configuration

## Overview

HAProxy was configured on pfSense to provide load balancing and high availability for the Apache web services.

The objective is to distribute incoming HTTP requests between Apache1 and Apache2 and maintain service availability if one server becomes unavailable.

## HAProxy Role

In this project, HAProxy acts as a reverse proxy and load balancer.

Its responsibilities are:

- Receive incoming client HTTP requests.
- Forward requests to backend web servers.
- Monitor backend server availability.
- Remove unavailable servers automatically.

## HAProxy Architecture

The traffic flow is:

```
                Client
                   |
                   v
              HAProxy
             (pfSense)
                   |
          __________|__________
         |                     |
         v                     v
     Apache1               Apache2
  (Primary Server)    (Backup Server)
```

## Backend Configuration

The HAProxy backend contains the Apache servers that provide the web service.

Configured backend servers:

| Server | Role |
|--------|------|
| Apache1 | Primary web server and Wazuh monitored endpoint |
| Apache2 | Secondary web server for availability |

The backend configuration includes:

- Server IP addresses.
- Service port.
- Health check configuration.
- Server availability status.

## Backend Health Checks

HAProxy uses health checks to verify that backend servers are operational.

The health check process:

1. HAProxy sends periodic checks to backend servers.
2. If the server responds correctly, it remains available.
3. If the server stops responding, HAProxy marks it as unavailable.
4. Traffic is redirected to healthy servers.

## Frontend Configuration

The frontend is responsible for receiving client connections.

The frontend configuration defines:

- Listening interface.
- Listening port.
- Connection forwarding rules.
- Associated backend pool.

Traffic received by the frontend is forwarded to the configured backend servers.

## Load Balancing Process

Normal operation:

```
              HAProxy

                 |
       ___________________
      |                   |
      v                   v
 Apache1              Apache2
   UP                    UP
```

Both servers are available and can receive requests.

## Failover Testing

A failover test was performed to verify HAProxy behavior.

### Test Procedure

1. Started Apache1 and Apache2 services.
2. Accessed the web service through HAProxy.
3. Stopped the Apache service on Apache1.
4. Checked HAProxy backend status.
5. Tested web access again.

### Expected Result

HAProxy should detect Apache1 as unavailable and redirect traffic to Apache2.

### Result

After Apache1 failure:

```
              HAProxy

                 |
                 |
                 v

              Apache2
                UP
```

Apache2 continued serving requests successfully.

The test confirmed that HAProxy provides service continuity.

# HAProxy Logging Integration

## Enable Logging

HAProxy logging was enabled on pfSense to monitor backend availability.

The logs contain important events:

- Backend server UP
- Backend server DOWN
- Connection failures
- Health check results


Example event:

haproxy:
Server agil_web_servers_ipvANY/apache_vm1 is DOWN,
reason: Layer4 connection problem


These logs are forwarded to Wazuh through Syslog.

## HAProxy Benefits in This Lab

The HAProxy implementation provides:

- High availability.
- Automatic failover.
- Backend health monitoring.
- Centralized traffic management.
- Improved service reliability.