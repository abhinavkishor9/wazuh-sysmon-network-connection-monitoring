# Investigation Notes

## Incident Summary

Generated outbound HTTPS traffic from the Windows endpoint using PowerShell.

Sysmon successfully logged the network connection, and Wazuh ingested the event for Threat Hunting analysis.

---

## Investigation Timeline

### Initial Validation

Verified:

- Sysmon service running
- Wazuh Agent running

---

### Activity Generated

PowerShell executed:

Invoke-WebRequest https://example.com

A successful HTTP 200 response confirmed outbound network communication.

---

### Connectivity Test

PowerShell executed:

Test-NetConnection example.com -Port 443

Result:

TCP connection successful

---

### Endpoint Detection

Observed:

Sysmon Event ID 3

Event Description:

Network connection detected

---

### Wazuh Investigation

Threat Hunting search returned:

- Destination Port
- Destination Address
- Process Image
- Process ID
- User
- Timestamp

---

## Evidence Collected

- Sysmon Event ID 3
- HTTPS Traffic
- Destination Port 443
- Successful TCP Connection
- Wazuh Alert
- Endpoint Metadata

---

## MITRE ATT&CK

Technique:

T1071

Sub-technique:

T1071.001

---

## Severity

Low

The observed activity represents expected outbound HTTPS communication and serves as a validation of endpoint telemetry collection.

---

## Conclusion

The endpoint successfully generated outbound HTTPS traffic, Sysmon recorded the network connection, and Wazuh displayed the event in Threat Hunting. This validates the end-to-end monitoring pipeline for network connection events.
