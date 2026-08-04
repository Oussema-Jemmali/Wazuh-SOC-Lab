# Testing and Validation

## Overview

Testing was performed to validate the functionality of the SOC laboratory components.

The main objectives were:

- Verify HAProxy load balancing functionality.
- Confirm automatic failover when a web server becomes unavailable.
- Verify communication between the Wazuh agent and Wazuh server.

## Test Environment

The validation was performed using the following components:

- pfSense with HAProxy.
- Apache1 web server with Wazuh agent.
- Apache2 web server.
- Wazuh Server.

## Test 1: HAProxy Backend Availability

### Objective

Verify that HAProxy can communicate with both Apache backend servers.

### Procedure

1. Started Apache1 service.
2. Started Apache2 service.
3. Accessed the web service through HAProxy.
4. Checked the HAProxy backend status.

### Expected Result

Both Apache servers should appear as available backend servers.

### Result

HAProxy successfully detected both Apache servers as active.

Status:

PASS

---

# Test 2: Apache1 Failure Simulation

## Objective

Verify that HAProxy maintains service availability when Apache1 becomes unavailable.

## Procedure

1. Confirmed that Apache1 and Apache2 were running.
2. Accessed the service through HAProxy.
3. Stopped the Apache service on Apache1.

Command used:

```bash
sudo systemctl stop apache2
```

4. Checked HAProxy backend health status.
5. Accessed the service again.

## Expected Result

HAProxy should detect Apache1 failure and redirect traffic to Apache2.

## Result

After stopping Apache1:

- HAProxy marked Apache1 as unavailable.
- Apache2 remained available.
- Web service continued working successfully.

Status:

PASS

## Failover Flow

Before failure:

```
                HAProxy

                   |
        ______________________
       |                      |
       v                      v
    Apache1                Apache2
      UP                     UP
```

After Apache1 failure:

```
                HAProxy

                   |
                   |
                   v

                Apache2
                  UP
```

The test confirmed that HAProxy provides automatic failover.

---

# Test 3: Wazuh Agent Connectivity

## Objective

Verify communication between Apache1 and the Wazuh server.

## Procedure

1. Installed the Wazuh agent on Apache1.
2. Registered Apache1 with the Wazuh Manager.
3. Started the Wazuh agent service.
4. Checked the Wazuh Dashboard.

## Expected Result

Apache1 should appear as an active Wazuh agent.

## Result

The Apache1 endpoint was successfully displayed in the Wazuh Dashboard.

Status:

PASS

---

# Test 4: Network Connectivity

## Objective

Verify communication between laboratory components.

## Tests Performed

Connectivity was verified between:

- pfSense and internal servers.
- Apache servers and Wazuh server.
- Wazuh agent and Wazuh Manager.

## Result

All required communication paths were operational.

Status:

PASS

---

# Validation Summary

| Test | Result |
|------|--------|
| HAProxy backend detection | PASS |
| Apache1 failure simulation | PASS |
| Apache2 service continuity | PASS |
| Wazuh agent connection | PASS |
| Network communication | PASS |

## Conclusion

The implemented SOC laboratory successfully demonstrates:

- High availability using HAProxy.
- Web service failover.
- Centralized monitoring using Wazuh.
- Integration between network infrastructure and security monitoring components.