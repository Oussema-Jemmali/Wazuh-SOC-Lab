# Future Improvements

## Overview

The current SOC laboratory successfully demonstrates the integration of network security, service availability, and centralized security monitoring.

This environment can be extended with additional security technologies and automation features to make it closer to a real enterprise SOC infrastructure.

## IDS/IPS Integration

### Suricata Deployment

Integrate Suricata IDS/IPS into the network architecture to provide:

- Network traffic inspection.
- Intrusion detection.
- Malicious activity detection.
- Security event generation.

Suricata alerts can be forwarded to Wazuh for centralized analysis.

---

## Additional Wazuh Agents

Deploy additional Wazuh agents on more infrastructure components.

Possible monitored endpoints:

- Apache2 server.
- pfSense firewall.
- Windows endpoint.
- Additional Linux servers.

Benefits:

- Wider security visibility.
- Centralized monitoring of the entire environment.
- More realistic SOC operations.

---

## Windows Endpoint Monitoring

Add a Windows machine with:

- Wazuh agent.
- Sysmon integration.

This would allow monitoring of:

- Process execution.
- User activity.
- Authentication events.
- Suspicious behaviors.

---

## Security Attack Simulation

Introduce controlled security testing scenarios to validate detection capabilities.

Examples:

- Failed SSH login attempts.
- Web server attacks.
- Suspicious command execution.
- Privilege escalation simulations.

The generated events can be analyzed through Wazuh alerts.

---

## Custom Wazuh Rules

Create custom detection rules adapted to the laboratory environment.

Examples:

- Detect specific Apache events.
- Detect suspicious authentication attempts.
- Generate alerts for abnormal activities.

Benefits:

- Improved detection accuracy.
- Better understanding of SIEM rule creation.

---

## Automation with Ansible

Use Ansible to automate deployment and configuration tasks.

Possible automation tasks:

- Installing Wazuh agents.
- Configuring Apache servers.
- Deploying security tools.
- Applying system configurations.

Benefits:

- Faster deployment.
- Repeatable infrastructure.
- Reduced manual configuration.

---

## Monitoring and Visualization Improvements

Integrate additional visualization tools such as:

- Grafana dashboards.
- Additional performance monitoring tools.

Possible monitored metrics:

- CPU usage.
- Memory consumption.
- Network traffic.
- Service availability.

---

## HTTPS and Secure Communication

Improve security by implementing encrypted communication.

Possible enhancements:

- TLS certificates for HAProxy.
- HTTPS frontend configuration.
- Secure communication between components.

---

## High Availability Improvements

Extend the current HAProxy implementation with additional redundancy.

Possible improvements:

- Multiple HAProxy nodes.
- pfSense high availability configuration.
- Additional backend servers.

---

## Cloud Integration

Extend the laboratory into a hybrid environment by integrating:

- Cloud virtual machines.
- Cloud security monitoring.
- Additional network segments.

---

## Final Goal

The future objective is to evolve this laboratory into a complete enterprise-like SOC platform including:

- Network monitoring.
- Endpoint detection.
- Intrusion detection.
- Automated response.
- Threat simulation.
- Security operations workflows.