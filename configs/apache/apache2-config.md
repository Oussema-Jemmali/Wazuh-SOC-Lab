# Apache2 Configuration

## Overview

Apache2 is the secondary web server deployed in the SOC laboratory environment.

Its main purpose is to provide service availability and act as a backup backend server for HAProxy.

Apache2 does not currently run a Wazuh agent and is mainly used to validate high availability and failover functionality.

## Server Role

Apache2 provides:

- Secondary HTTP web service.
- HAProxy backend availability.
- Service continuity when Apache1 becomes unavailable.

## Installed Components

The main component installed on Apache2 is:

| Component | Purpose |
|-----------|---------|
| Apache2 | Web server service |

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

A successful installation confirms that the web server is active.

## Web Page Configuration

The default Apache web page was customized to identify Apache2 during HAProxy failover testing.

The website files are located in:

```
/var/www/html/
```

Example:

```
/var/www/html/index.html
```

The page contains information identifying the server as Apache2.

## HAProxy Integration

Apache2 is configured as a backend server in the HAProxy backend pool.

Traffic flow:

```
Client
   |
   v
pfSense HAProxy
   |
   v
Apache2
```

HAProxy continuously checks Apache2 availability.

## High Availability Role

Apache2 provides service continuity when Apache1 fails.

Normal operation:

```
              HAProxy

                 |
        __________________
       |                  |
       v                  v
    Apache1            Apache2
      UP                 UP
```

After Apache1 failure:

```
              HAProxy

                 |
                 v

              Apache2
                UP
```

## Testing

Apache2 was validated through HAProxy failover testing.

Test procedure:

1. Started Apache1 and Apache2.
2. Accessed the service through HAProxy.
3. Stopped Apache1 Apache service.
4. Verified that Apache2 continued serving requests.

Command used to stop Apache1:

```bash
sudo systemctl stop apache2
```

## Current Status

Apache2 is successfully integrated as:

- A backup web server.
- A HAProxy backend server.
- A high availability component of the SOC laboratory.