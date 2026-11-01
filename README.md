# TechNova IT Support — Ticket #1043

## Windows 11 — Print Spooler Service Troubleshooting

**Ticket Status:** Service Restored  
**Priority:** Medium  
**Category:** Windows Services / Printing  
**Environment:** Windows 11 Pro — PC01  
**Lab Type:** Simulated IT Support Incident

---

## 1. Incident Description

An employee named Ana reported that she was unable to print documents from her Windows 11 workstation.

The IT Support team was assigned to investigate the Windows Print Spooler service, identify the issue, and restore normal service operation.

**Objective:** Diagnose and recover a stopped Windows service using Services, PowerShell, and Windows Event Viewer.

## 2. Lab Environment

| Component | Configuration |
|---|---|
| Company | TechNova Solutions (Simulated) |
| Workstation | PC01 |
| Operating System | Windows 11 Pro |
| Virtualization | VMware Workstation |
| Affected Service | Print Spooler |
| Service Name | Spooler |
| Startup Type | Automatic |

## 3. Troubleshooting Procedure

### Step 1 — Inspect the Service

Opened the Windows Services console using:

`services.msc`

Located Print Spooler and verified that its initial status was Running and its startup type was Automatic.

### Step 2 — Simulate the Incident

Stopped the Print Spooler service to simulate a printing-related service failure.

Confirmed that the service status changed to Stopped.

### Step 3 — Diagnose Using PowerShell

Opened PowerShell with administrative privileges and executed:

`Get-Service -Name Spooler`

The command confirmed that Print Spooler was stopped.

### Step 4 — Restore the Service

Executed the following command:

`Start-Service -Name Spooler`

Then verified the service status:

`Get-Service -Name Spooler`

The service returned to the Running state.

### Step 5 — Investigate Windows Event Logs

Opened Windows Event Viewer using:

`eventvwr.msc`

Navigated to:

**Windows Logs → System**

Searched for Event ID 7036, which is associated with service state changes.

No matching Event ID 7036 records were found.

Further investigation using PowerShell identified Event ID 7040 records from Service Control Manager, confirming that service startup configuration changes were being recorded.

The System event log was confirmed to be enabled and operational.

### Step 6 — Final Service Verification

Executed:

`Get-Service -Name Spooler | Select-Object Name, Status, StartType`

**Verified Result:**

| Name | Status | StartType |
|---|---|---|
| Spooler | Running | Automatic |

## 4. Root Cause and Findings

The simulated incident was caused by manually stopping the Print Spooler service.

PowerShell confirmed the stopped state, and the service was successfully restored using Start-Service.

The absence of Event ID 7036 in the available System logs was observed but not established as a separate system fault.

## 5. Resolution

**Service Recovery: Successful**

- Confirmed the service was stopped.
- Restored the service using PowerShell.
- Verified the Running state.
- Confirmed the Automatic startup configuration.
- Investigated relevant Windows event logs.

**Validation Limitation:** A physical or virtual printer test was not performed. Therefore, successful end-to-end printing was not verified.

## 6. Screenshots and Evidence

The following evidence will be added:

1. Print Spooler in the Stopped state.
2. PowerShell diagnosis confirming the stopped service.
3. Final PowerShell verification showing Running and Automatic.

## 7. Technical Skills Demonstrated

- Windows 11 troubleshooting
- Windows Services administration
- PowerShell service management
- Windows Event Viewer
- Service Control Manager event analysis
- Incident simulation and recovery
- Technical documentation
- Post-resolution verification

## 8. Lessons Learned

Windows services can be managed through both the graphical Services console and PowerShell.

Service recovery should always be followed by verification of the actual service status.

Event logs provide useful diagnostic information, but missing events should not be treated as proof of a specific fault without additional evidence.

---

**TechNova Solutions — Hands-on IT Support Portfolio**  
**Ticket #1043 | Print Spooler Service Troubleshooting**
