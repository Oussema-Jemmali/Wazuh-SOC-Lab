# HAProxy Backend Configuration

## Overview

The HAProxy backend configuration defines the pool of web servers that receive traffic from the HAProxy frontend.

In this SOC laboratory, the backend contains two Apache web servers:

- Apache1
- Apache2

HAProxy monitors the availability of each server and forwards traffic only to healthy backend nodes.

## Backend Role

The backend is responsible for:

- Defining available web servers.
- Performing server health checks.
- Managing backend availability.
- Providing failover capability.

## Backend Architecture

```
                HAProxy Backend

                       |
          ______________|______________
         |                             |
         v                             v
      Apache1                       Apache2
   Primary Server              Secondary Server
   Wazuh Agent                  Web Server
```

## Configured Backend Servers

| Server | Role | Status |
|--------|------|--------|
| Apache1 | Primary web server and Wazuh monitored endpoint | Active |
| Apache2 | Secondary web server | Active |

## Backend Configuration Parameters

The backend configuration includes:

### Server Address

Each Apache server is defined using its internal IP address.

Example:

```
Apache1: <Apache1-IP>
Apache2: <Apache2-IP>
```

### Service Port

The backend web service uses:

```
Port: 80
```

### Health Check

HAProxy health checks verify that backend servers are responding correctly.

The health check process:

1. HAProxy sends requests to backend servers.
2. Server responses are analyzed.
3. Available servers remain in the backend pool.
4. Failed servers are temporarily removed.

## Load Balancing Behavior

When both servers are available:

```
              HAProxy

                 |
        __________________
       |                  |
       v                  v
    Apache1            Apache2
      UP                 UP
```

Traffic can be forwarded to both backend servers.

## Failover Behavior

When Apache1 becomes unavailable:

```
              HAProxy

                 |
                 v

              Apache2
                UP
```

HAProxy automatically removes Apache1 from the backend pool and continues forwarding requests to Apache2.

## Validation

The backend configuration was tested by:

1. Starting Apache1 and Apache2.
2. Verifying both servers appear as available.
3. Stopping Apache1 service.
4. Checking HAProxy backend status.
5. Confirming Apache2 continues serving requests.

## Result

The HAProxy backend successfully provides:

- Backend server monitoring.
- Automatic failover.
- High availability for web services.
- Continuous service operation during server failure.