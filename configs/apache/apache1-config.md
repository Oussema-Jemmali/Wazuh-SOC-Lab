# Apache1 Configuration

## Overview

Apache1 is one of the web servers deployed in the SOC laboratory environment.

It has two main roles:

- Provide web service behind HAProxy.
- Act as a monitored endpoint through the Wazuh agent.

Apache1 is connected to the internal network through the GNS3 topology and communicates with the Wazuh Server for security monitoring.

## Server Role

Apache1 provides:

- HTTP web service.
- Backend service for HAProxy.
- Security event collection through Wazuh agent.

## Installed Components

The main components installed on Apache1 are:

| Component | Purpose |
|-----------|---------|
| Apache2 | Web server service |
| Wazuh Agent | Security monitoring |

## Apache Installation

Apache web server was installed using:

```bash
sudo apt update
sudo apt install apache2 -y
```

After installation, the service was started and enabled:

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

## Apache Service Verification

The Apache service status can be checked using:

```bash
sudo systemctl status apache2
```

A successful installation shows that the Apache service is active and running.

## Web Page Configuration

The default Apache web page was modified to identify Apache1 during HAProxy testing.

The web files are located in:

```
/var/www/html/
```

Example:

```
/var/www/html/index.html
```

The page contains information identifying the server as Apache1.

## HAProxy Integration

Apache1 is configured as a backend server in HAProxy.

Traffic flow:

```
Client
   |
   v
pfSense HAProxy
   |
   v
Apache1
```

HAProxy monitors Apache1 availability through health checks.

## Wazuh Agent Integration

Apache1 runs the Wazuh agent to send security events to the Wazuh Server.

The agent monitors:

- System activity.
- Authentication events.
- Service status.
- Log files.

Communication flow:

```
Apache1
   |
   |
Wazuh Agent
   |
   |
Wazuh Manager
```

## Testing

Apache1 was tested by:

- Accessing the web service through HAProxy.
- Verifying backend availability.
- Stopping Apache service to test HAProxy failover.

Failure simulation:

```bash
sudo systemctl stop apache2
```

Expected behavior:

- HAProxy detects Apache1 as unavailable.
- Traffic is redirected to Apache2.

## Current Status

Apache1 is successfully integrated into the SOC laboratory as:

- A production-like web server.
- A HAProxy backend server.
- A Wazuh monitored endpoint.