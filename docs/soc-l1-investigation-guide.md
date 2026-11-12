# SOC L1 Investigation Guide

This guide uses only the lab’s recorded components and outcomes. It is intended as a repeatable practice workflow, not a claim that every exercise generated a dedicated alert.

## Triage sequence

### 1. Establish scope

- Identify the alert time range and the system under review.
- In this lab, the monitored endpoint is Wazuh Agent `003` at `192.168.1.11` (dashboard name `ubuntu`).
- Distinguish endpoint events from monitoring-server events. The monitoring VM is `Soc-Monitoring`; its bridged address is `192.168.1.9`.
- Check that the dashboard time picker includes the exercise. The project screenshots do not establish a timezone, so preserve their displayed time unless corroborating records establish one.

### 2. Review the alert

In Wazuh **Threat Hunting**, constrain the search to the expected agent, time window, and relevant rule. Recorded rule IDs:

| Rule ID | Recorded meaning in this lab | Initial analyst check |
|---|---|---|
| `100100` | Custom SSH brute-force rule, level 10 | Review authentication context and event grouping; the final record does not retain the exact XML or correlation thresholds |
| `550` | FIM checksum change | Confirm the monitored path (`/etc/soc-vt-test.txt`) and whether the change was expected |
| `87103` | VirusTotal lookup returned no records | Report reputation as unknown/no record, not clean |
| `533` | Listening-port state changed | Treat as host change evidence; do not label it a reverse-shell detection without process/session evidence |
| `86601` | Suricata rule present in integrated event pipeline | Inspect the underlying Suricata signature and endpoint/network fields before assigning meaning |

### 3. Search telemetry, not just alerts

For Zeek and other raw records, switch to **Discover** and `wazuh-archives-*`. Archive records may be useful even when no alert was raised. Inspect the event structure first; if the indexed schema contains the Zeek field, a starting filter is:

```text
data.id.orig_h:"192.168.1.11"
```

Add a destination address or port only after confirming it in the event. The project record does not preserve Kali’s IP or a listener port. Avoid assuming all records in a broad archive view belong to the endpoint; the retained screenshot includes monitoring-server events.

### 4. Correlate and qualify

Compare timestamps, agent identity, source/destination addresses, ports, protocol, and the controlled test notes. A nearby timestamp can establish association for further investigation, but not causation or attack type. For a stronger reverse-shell conclusion, seek direct process context and a corresponding network flow; the retained Rule `533` evidence is only a port-state change.

### 5. Write a defensible case note

Use four short sections:

1. **Observed:** quote the rule, agent, timestamp, and fields actually visible.
2. **Context:** state the controlled exercise or business activity that aligns with the event, if known.
3. **Assessment:** explain what the evidence supports and your confidence.
4. **Next step:** identify the additional event or owner confirmation needed to resolve uncertainty.

Do not state “malware detected” from a VirusTotal no-record response, “attack detected” from a generic Suricata pipeline rule, or “reverse shell confirmed” from Rule `533` alone.

## Project evidence available

The original repository retains three screenshots: a Rule `533` port-change detail, a Rule `533` Threat Hunting list, and a populated archive view. The archive screenshot’s visible rows are monitoring-server records and do not isolate the shell-related flow. Dedicated screenshots for Rules `550`, `87103`, and `100100`, Suricata ingestion, and terminal activity are not retained. See [the original evidence gallery](https://github.com/alen97mathew-gif/intelligent-soc-platform#evidence-gallery).


