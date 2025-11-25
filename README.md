# Wazuh Threat Detection Proof of Concept (POC)

## Overview

This project demonstrates a complete Wazuh-based threat detection setup using a virtualized environment.
The goal was to deploy a Wazuh monitoring infrastructure, configure agent-based monitoring on multiple endpoints, and simulate a real-world attack scenario to verify detection capabilities.

This POC includes:

* Full Wazuh Server setup (Manager, Indexer, Dashboard)
* Deployment of two monitored endpoints
* Successful agent registration and connectivity
* Execution of an SSH brute-force attack
* Detection, alert generation, and analysis through Wazuh

---

## Lab Architecture

| Component       | OS         | IP Address     | Role                        |
| --------------- | ---------- | -------------- | --------------------------- |
| Wazuh Server    | Wazuh OVA  | 192.168.52.134 | Manager, Indexer, Dashboard |
| Kali Endpoint   | Kali Linux | 192.168.52.130 | Attacker and Wazuh Agent    |
| Debian Endpoint | Debian 13  | 192.168.52.133 | Victim and Wazuh Agent      |

---

## Objectives

1. Deploy Wazuh Manager, Indexer, and Dashboard
2. Install and register Wazuh agents on two endpoints
3. Validate connectivity between server and endpoints
4. Simulate a security attack
5. Collect and analyze security alerts
6. Produce a final POC report

---

## Setup Summary

* Wazuh OVA imported into VMware
* Agents installed on both Debian and Kali endpoints
* Agents successfully registered using `agent-auth`
* Dashboard confirmed active with two connected agents
* System logs, connectivity tests, and services verified

---

## Attack Simulation: SSH Brute Force

To test Wazuh’s detection capability, an SSH brute-force attack was launched from the Kali machine targeting the Debian endpoint.

### Command Used:

```
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.52.133
```

### Outcome:

* Numerous authentication failures generated on the Debian endpoint
* Wazuh captured and categorized the events
* Alerts were visible in the Wazuh Dashboard under Threat Hunting
* High severity warnings were logged
* MITRE ATT&CK techniques were mapped (e.g., T1110 Brute Force)

---

## Results and Observations

* Wazuh successfully monitored both endpoints
* The brute-force attack triggered multiple alerts related to failed authentication
* Wazuh Dashboard displayed event counts, severity levels, and attack details
* The system correlated activity with MITRE ATT&CK techniques
* Endpoint integrity and security insights were visible in real time

---

## Project Report

Full completed report with diagrams, screenshots, event logs, and findings is available here:

[Wazuh_POC_Report_Sheeza_Alam_Khan_Final.pdf](Wazuh_POC_Report_Sheeza_Alam_Khan_Final.pdf)



---

## Conclusion

This Wazuh POC demonstrates a successful implementation of centralized security monitoring, attack simulation, and alert detection.
The environment effectively identifies brute-force authentication attempts and provides analysts with detailed insights using Wazuh’s dashboard, rules, and MITRE mappings.

This project can serve as a foundation for more advanced SIEM scenarios, log correlation, and incident response automation.

