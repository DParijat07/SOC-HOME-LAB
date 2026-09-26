# 🔐 Authentication Simulations

## 1. Overview

This section documents controlled authentication-related security simulations performed inside the SOC Home Lab.

Authentication events are useful for SOC practice because failed and repeated login attempts can generate observable security telemetry across Windows and Linux systems.

The simulations in this section are designed to validate whether the laboratory monitoring environment can:

* Generate authentication telemetry
* Collect authentication events
* Detect suspicious authentication patterns
* Generate SIEM alerts where applicable
* Support analyst investigation
* Provide evidence for validation

---

# 2. Simulation Scope

The initial authentication simulations include:

| ID      | Simulation                  | Target           | Primary Telemetry          |
| ------- | --------------------------- | ---------------- | -------------------------- |
| SIM-001 | SSH Authentication Attempts | Metasploitable 2 | Linux authentication logs  |
| SIM-002 | SSH Brute-Force Simulation  | Metasploitable 2 | Linux authentication logs  |
| SIM-003 | Windows Failed Logon        | Windows 7        | Windows Security Event Log |

Additional authentication scenarios may be added later.

---

# 3. Simulation Architecture

```text id="4l2m5w"
                  Kali Linux
                Attack Simulator
                       │
                       │
             Authentication Activity
                       │
          ┌────────────┴────────────┐
          │                         │
          ▼                         ▼
   Metasploitable 2             Windows 7
       Linux                    Windows
          │                         │
          ▼                         ▼
   auth/system logs          Security Events
          │                         │
          └────────────┬────────────┘
                       │
                       ▼
                  SIEM Layer
                 ┌─────────┐
                 │ Wazuh   │
                 │ Splunk  │
                 └────┬────┘
                      │
                      ▼
                SOC Investigation
```

---

# 4. Simulation Workflow

Every authentication simulation follows:

```text id="4d7q2m"
Define Objective
      ↓
Prepare Target
      ↓
Verify SIEM Monitoring
      ↓
Generate Controlled Authentication Activity
      ↓
Verify Source Log
      ↓
Check Wazuh / Splunk
      ↓
Investigate Event
      ↓
Capture Evidence
      ↓
Document Result
```

---

# 5. SIM-001 — SSH Authentication Attempts

## Objective

Generate controlled SSH authentication activity against the authorized Linux target and verify that the resulting authentication events are visible to the SOC monitoring environment.

## Target

**Metasploitable 2**

## Source

**Kali Linux**

## Expected Telemetry

Primary source:

```text id="1vl7ub"
/var/log/auth.log
```

Expected information may include:

* Timestamp
* Source IP
* Authentication result
* Username
* SSH-related information

## Validation Flow

```text id="8d1r2v"
Kali
  ↓
SSH Authentication Attempt
  ↓
Metasploitable 2
  ↓
/var/log/auth.log
  ↓
Wazuh / Splunk
  ↓
Event Investigation
```

## Status

🟡 Planned

---

# 6. SIM-002 — SSH Brute-Force Simulation

## Objective

Generate repeated controlled SSH authentication failures against the authorized Linux target and investigate how the monitoring environment represents the activity.

## Target

**Metasploitable 2**

## Source

**Kali Linux**

## Expected Telemetry

Repeated authentication failures should generate multiple Linux authentication events.

The investigation should examine:

* Source IP
* Target account
* Number of attempts
* Time interval
* Authentication result
* Related Wazuh alert information
* Relevant Splunk search results

## MITRE ATT&CK Reference

Potential technique:

**T1110 — Brute Force**

The specific sub-technique, if applicable, will be determined from the actual simulation and documented evidence.

## Validation Flow

```text id="4x7w9p"
Repeated SSH Authentication Attempts
                ↓
         Linux auth.log
                ↓
        Wazuh / Splunk
                ↓
        Alert / Search
                ↓
        Analyst Triage
                ↓
        Evidence
```

## Status

🟡 Planned

---

# 7. SIM-003 — Windows Failed Logon

## Objective

Generate controlled failed authentication activity against the Windows endpoint and verify that the corresponding Windows Security Event is collected by the SOC monitoring environment.

## Target

**Windows 7**

## Source

Authorized laboratory activity

## Expected Telemetry

A failed Windows authentication may generate:

```text id="l2c8nq"
Event ID 4625
```

The actual event should be verified from the Windows Event Viewer and SIEM rather than assumed.

## Investigation Fields

Potentially useful fields include:

* Timestamp
* Account name
* Source address
* Logon type
* Failure reason
* Authentication package
* Computer name

The exact fields available depend on the generated event and collection method.

## Validation Flow

```text id="v5v1r0"
Controlled Failed Logon
        ↓
Windows Security Event
        ↓
Event ID 4625
        ↓
Wazuh / Splunk
        ↓
Search / Alert
        ↓
Investigation
```

## Status

🟡 Planned

---

# 8. Evidence Requirements

For each completed authentication simulation, collect evidence showing:

### Source Activity

Proof that the simulation was performed.

### Source Log

Proof that the target system generated the expected telemetry.

### SIEM Visibility

Proof that the event reached Wazuh and/or Splunk.

### Investigation

Proof that relevant event fields were analyzed.

### Result

A concise statement of whether the expected telemetry and detection behavior were observed.

---

# 9. Evidence Structure

Authentication evidence should be organized under the central evidence directory.

Example:

```text id="2w1c8f"
06-EVIDENCE/
└── Authentication/
    ├── SIM-001/
    ├── SIM-002/
    └── SIM-003/
```

The exact evidence structure may be adjusted to match the final repository architecture.

---

# 10. Simulation Validation Checklist

```text id="j4z8y2"
[ ] Target confirmed as authorized lab system
[ ] SIEM monitoring verified
[ ] Simulation objective defined
[ ] Authentication activity generated
[ ] Source log verified
[ ] Expected event identified
[ ] Wazuh visibility checked
[ ] Splunk visibility checked
[ ] Relevant fields analyzed
[ ] MITRE ATT&CK mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

# 11. Important Distinction

An authentication simulation and a successful detection are separate outcomes.

For example:

```text id="y2w6q1"
SSH Brute Force Performed
          ↓
Authentication Logs Generated
          ↓
Logs Collected
          ↓
Events Visible in SIEM
          ↓
Detection Rule / Search
          ↓
Alert or Investigative Finding
```

Each stage should be validated separately.

A simulation should **not** be marked as a successful detection merely because the attack activity was performed.

---

# 12. Current Status

| Simulation                            | Status     |
| ------------------------------------- | ---------- |
| SIM-001 — SSH Authentication Attempts | 🟡 Planned |
| SIM-002 — SSH Brute-Force             | 🟡 Planned |
| SIM-003 — Windows Failed Logon        | 🟡 Planned |

Status will be updated only after the simulations are actually performed and validated.

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Generate the activity, verify the source telemetry, verify SIEM visibility, investigate the result, and preserve evidence.**

This ensures that every authentication simulation becomes a **defensible piece of practical SOC experience**, rather than simply a list of commands performed in a home lab.
