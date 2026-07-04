# wazuh-sysmon-network-connection-monitoring
## Overview

This lab demonstrates how to monitor outbound network connections using Sysmon Event ID 3 and investigate the generated telemetry inside the Wazuh Threat Hunting dashboard.

The objective is to simulate legitimate HTTPS traffic, verify that Sysmon captures the network activity, and confirm that Wazuh successfully ingests and displays the corresponding events for investigation.

---

## Lab Objectives

- Generate outbound HTTPS network traffic
- Capture Sysmon Network Connection events (Event ID 3)
- Verify event collection in Wazuh
- Perform Threat Hunting searches
- Investigate network metadata
- Map activity to MITRE ATT&CK

---

## Technologies Used

- Wazuh SIEM
- Sysmon
- Windows 11
- PowerShell
- Windows Event Viewer

---

## Lab Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh |
| Endpoint Monitoring | Sysmon |
| Shell | PowerShell |
| Event Source | Microsoft-Windows-Sysmon |

---

## MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Application Layer Protocol | T1071 |
| Web Protocols | T1071.001 |
| Network Service Discovery (Observation) | T1046 |

---

## Lab Steps

### Step 1
Verify Sysmon service

```
Get-Service Sysmon64
```

---

### Step 2
Verify Wazuh Agent

```
Get-Service WazuhSvc
```

---

### Step 3
Generate HTTPS traffic

```
Invoke-WebRequest https://example.com
```

---

### Step 4
Verify TCP connectivity

```
Test-NetConnection example.com -Port 443
```

---

### Step 5
View recent Sysmon Network Connection events

```
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -FilterXPath "*[System[(EventID=3)]]" -MaxEvents 20
```

---

### Step 6
Filter HTTPS traffic

```
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -FilterXPath "*[System[(EventID=3)]]" -MaxEvents 50 | Where-Object {$_.Message -match "443"}
```

---

### Step 7
Search inside Wazuh Threat Hunting

Search for:

```
data.win.system.eventID:3
```

or

```
data.win.eventdata.destinationPort:443
```

---

### Step 8
Review Event Details

Investigate:

- Process Image
- Source IP
- Destination IP
- Destination Port
- Protocol
- Process ID
- User
- Timestamp

---

## Detection Summary

| Event |
|------|
| Sysmon Event ID 3 |
| Outbound HTTPS Connection |
| Destination Port 443 |
| Network Telemetry Successfully Logged |
| Event Successfully Ingested by Wazuh |

---

## Learning Outcomes

- Understand Sysmon Event ID 3
- Monitor outbound HTTPS traffic
- Perform Threat Hunting using Wazuh
- Investigate network telemetry
- Correlate endpoint activity with SIEM data
- Practice SOC investigation workflow
