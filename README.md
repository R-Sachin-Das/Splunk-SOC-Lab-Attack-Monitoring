# Splunk SIEM Security Monitoring & Attack Analysis Lab

## Objective
This project demonstrates the implementation of a centralized Security Information and Event Management (SIEM) pipeline using Splunk Enterprise to monitor, parse, and analyze endpoint security events. The lab involves simulating real-world network reconnaissance from an attacking machine (Kali Linux) against a targeted Windows host to validate real-time detection engineering workflows.

## Skills & Technologies Demonstrated
* **SIEM Management:** Splunk Enterprise (Data Ingestion, Indexing, Search Processing Language)
* **Operating Systems:** Kali Linux, Windows 11 / Windows Server
* **Network & Security Auditing:** Nmap, Windows Event Log Subsystem (Security & System Channels)
* **Technical Troubleshooting:** Network boundary debugging (Windows Firewall configuration), syntax query optimization, data model field extraction mapping.

## Environment Architecture
* **SIEM Platform:** Splunk Enterprise 10.4.0
* **Attacking Node:** Kali Linux VM (Subnet: 10.0.5.x)
* **Target Endpoint:** Windows VM configured with active Security Log Auditing

## Phase-by-Phase Implementation

### Phase 1: Splunk Search Processing Language (SPL) Optimization
Configured tailored SPL queries to transition searches out of high-overhead real-time streaming into stabilized historical indexing, successfully isolating baseline operational records.
* Optimized Query: `index=main EventCode=1 | table _time, LogName, SourceName, Message`

### Phase 2: Live Attack Simulation & Firewall Debugging
Executed active network reconnaissance (Nmap port sweeps) from the Kali endpoint. Diagnosed and resolved local packet drop boundaries by modifying target firewall rules to safely permit ICMP and TCP traffic streams in an isolated sandbox.

### Phase 3: Field Alias Extraction & Forensic Analysis
Identified and resolved blank field extraction anomalies by mapping Splunk’s native event aliases (`user`, `Logon_Type`, `Security_ID`) to parse Windows Security Log events.
* Advanced Forensic Query: `index=main sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625) | table _time, EventCode, user, Logon_Type, Security_ID`
* Successfully captured and analyzed automated background elevation tasks (`Logon_Type 5` running under `NT AUTHORITY\SYSTEM` with `SID S-1-5-18`).

## Lab Artifacts
*[Insert your best Splunk dashboard screenshots here]*
