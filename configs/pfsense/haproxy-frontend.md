# HAProxy Frontend Configuration

## Overview

The HAProxy frontend configuration defines how HAProxy receives incoming client connections and forwards them to the configured backend servers.

In this SOC laboratory, the frontend is configured on pfSense and acts as the entry point for HTTP traffic before it is distributed to Apache1 and Apache2.

## Frontend Role

The frontend is responsible for:

- Listening for incoming client requests.
- Defining the listening address and port.
- Forwarding traffic to the HAProxy backend.
- Applying frontend rules before sending requests to backend servers.

## Traffic Flow

The request flow is:

```
Client
   |
   v
HAProxy Frontend
   |
   v
HAProxy Backend
   |
   |
   +------------+
   |            |
   v            v
Apache1      Apache2
```

## Frontend Configuration

The frontend configuration contains the following elements:

## Listen Address

The frontend listens on the configured pfSense interface.

Example:

```
Interface: LAN
```

## Listening Port

The frontend receives HTTP requests on:

```
Port: 80
```

## Default Backend

The frontend forwards incoming requests to the configured HAProxy backend pool.

Backend:

```
Apache Backend Pool
```

## Request Processing

When a client sends an HTTP request:

1. The request reaches pfSense.
2. HAProxy frontend receives the connection.
3. HAProxy checks the configured backend.
4. The request is forwarded to an available Apache server.

## Normal Operation

When both Apache servers are available:

```
              Client

                |
                v

          HAProxy Frontend

                |
                v

          HAProxy Backend

          _____________
         |             |
         v             v
      Apache1       Apache2
        UP            UP
```

## Failover Operation

When Apache1 becomes unavailable:

```
              Client

                |
                v

          HAProxy Frontend

                |
                v

          HAProxy Backend

                |
                v

             Apache2
               UP
```

HAProxy automatically forwards traffic to the available backend server.

## Testing

The frontend configuration was validated by:

1. Accessing the web service through the HAProxy frontend address.
2. Confirming that requests reach Apache servers.
3. Stopping Apache1 service.
4. Verifying that Apache2 continues serving requests.

## Result

The HAProxy frontend successfully provides:

- Centralized HTTP traffic management.
- Connection forwarding to backend servers.
- Integration with HAProxy load balancing.
- High availability access to web services.