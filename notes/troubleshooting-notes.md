# Troubleshooting Notes

## Problem 1

No Sysmon Event ID 3 events

### Cause

Sysmon NetworkConnection logging disabled.

### Resolution

Verify Sysmon configuration includes:

NetworkConnect

Restart Sysmon if configuration changes are applied.

---

## Problem 2

No events visible in Wazuh

### Cause

Agent not forwarding logs.

### Resolution

Verify:

Get-Service WazuhSvc

Restart agent if necessary.

---

## Problem 3

Sysmon service not running

### Resolution

Verify:

Get-Service Sysmon64

Restart service if stopped.

---

## Problem 4

Invoke-WebRequest fails

### Possible Causes

- Internet unavailable
- DNS issue
- Firewall restriction

### Resolution

Verify connectivity using:

Test-NetConnection example.com -Port 443

---

## Problem 5

No HTTPS events after traffic generation

### Resolution

Generate additional traffic:

Invoke-WebRequest https://example.com

Refresh Threat Hunting after a few seconds.

---

## Problem 6

Port 443 filter returns no results

### Resolution

Increase event history:

Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -FilterXPath "*[System[(EventID=3)]]" -MaxEvents 100

---

## Problem 7

Threat Hunting search returns no data

Verify search fields:

data.win.system.eventID:3

or

data.win.eventdata.destinationPort:443

Adjust the time range to include the event timestamp.

---

## Validation Checklist

✓ Sysmon running

✓ Wazuh Agent running

✓ HTTPS request completed successfully

✓ TCP connectivity verified

✓ Sysmon Event ID 3 generated

✓ Wazuh Threat Hunting event available

✓ Network metadata reviewed

✓ Investigation completed
