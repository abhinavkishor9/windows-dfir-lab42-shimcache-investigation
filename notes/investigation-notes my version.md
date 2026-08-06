# Investigation Notes

## Lab Summary

In this investigation we have demonstrated acquiring and preparing Windows ShimCache (Application Compatibility Cache) artifacts for offline forensic analysis.

We created a sample executable, verified the ShimCache registry location using PowerShell , and using Command Prompt, we exported the SYSTEM registry hive, and attempted to parse SYSTEM hive using AppCompatCacheParser.

---

## Analyst Methodology

1. Create investigation folder.
2. Create a sample executable.(.txt file)
3. Execute the .txt file
4. Verify the ShimCache registry key.
5. Export the SYSTEM registry hive.
6. Attempt offline parsing.
7. Identify parser dependency.(.NET required)

---

## Investigation Scenario

Suppose an attacker executes:

**DemoApp.exe**

Later, the executable is deleted to hide evidence.

Investigators need to answer:

- Was the executable ever present on the system?
- Was it executed?
- Where was it located?
- Can evidence still be recovered after deletion?

ShimCache may still contain information about the executable, allowing investigators to identify previously executed applications even if the original file no longer exists.

---

## Evidence Collected

### Evidence 1 

Collected:

- DemoApp.exe. Copied notepad.exe into it.

Finding:

Successfully created and executed excutable.

---

### Evidence 2 

Command Used

```powershell
Get-Item "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache"
```

Finding:

ShimCache registry key is verified. It exists.

---

### Evidence 3 

Command Used

```cmd
reg save HKLM\SYSTEM C:\ShimCacheLab\SYSTEM.hiv
```

Finding:

Successfully exported the SYSTEM registry hive for offline analysis.

---

### Evidence 4 – Offline Parsing Attempt

Tool Used

- AppCompatCacheParser

Finding:

Parser could not execute because the required .NET runtime was not installed.

---


## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Discovery | File and Directory Discovery | T1083 |
| Collection | Data from Local System | T1005 |

---
