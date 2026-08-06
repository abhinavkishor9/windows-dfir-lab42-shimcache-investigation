# windows-dfir-lab42-shimcache-investigation

## Overview

ShimCache (Application Compatibility Cache) is a Windows forensic artifact that records information about executable files processed by the operating system. During DFIR investigations, ShimCache helps analysts identify applications that existed or were executed on a system, making it valuable for malware investigations and incident response.

In this hands-on DFIR lab, a custom executable was created and executed before examining the ShimCache registry location, exporting the SYSTEM hive, and preparing it for offline analysis using AppCompatCacheParser.

---

# Executive Summary

This investigation demonstrates how ShimCache artifacts can be collected using native Windows tools without directly modifying forensic evidence. The SYSTEM registry hive was exported successfully, allowing offline analysis while preserving forensic integrity.

Although AppCompatCacheParser could not parse the hive because the required .NET runtime was missing, the investigation successfully demonstrated the proper acquisition workflow followed by professional DFIR analysts.

---

# Investigation Objectives

- Understand ShimCache forensic artifacts.
- Create and execute a sample executable.
- Verify the ShimCache registry key.
- Export the SYSTEM registry hive.
- Prepare evidence for offline forensic analysis.
- Understand parser dependencies.
- Document forensic findings.

---

# Skills Demonstrated

- Windows Registry Investigation
- ShimCache Artifact Collection
- Registry Hive Acquisition
- Host-Based DFIR
- PowerShell Registry Analysis
- Windows Forensic Artifact Preservation
- Offline Evidence Collection
- Evidence Documentation
- Incident Reporting

---

# Tools Used

- Windows 10
- Windows PowerShell
- Registry Editor
- reg.exe
- AppCompatCacheParser (Eric Zimmerman)

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Windows 10 |
| Investigation Type | Host-Based DFIR |
| Primary Artifact | ShimCache |
| Registry Hive | SYSTEM |
| Analysis Method | Offline Registry Analysis |
| Shell | Windows PowerShell |
| Privileges | Administrator |

---

# Investigation Workflow

1. Create investigation workspace.
2. Create and execute a sample executable.
3. Verify the ShimCache registry key.
4. Export the SYSTEM registry hive.
5. Attempt offline ShimCache parsing.
6. Identify parser dependency issue.
7. Preserve collected evidence.
8. Remove lab artifacts.

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1083 | File and Directory Discovery |
| T1059 | Command and Scripting Interpreter |
| T1005 | Data from Local System |
| T1112 | Modify Registry (Related Investigation) |

---

# Evidence Collected

- Demo executable
- ShimCache registry key
- Exported SYSTEM hive
- PowerShell outputs
- Parser execution output
- Error indicating missing .NET runtime

---

# Evidence Correlation

The investigation correlated multiple forensic artifacts:

- The demo executable was successfully created and executed.
- The ShimCache registry location was verified.
- The SYSTEM hive was exported successfully.
- Offline parsing was attempted using AppCompatCacheParser.
- The parser failure confirmed an environmental dependency rather than an acquisition issue.

---

# Investigation Findings

The investigation confirmed that ShimCache information resides within the SYSTEM registry hive and can be preserved through offline acquisition. Although parsing was unsuccessful because the required .NET runtime was not installed, the exported hive remained suitable for later forensic analysis once the dependency is resolved.

---

# Key Takeaway

ShimCache is one of the most valuable Windows execution artifacts for DFIR investigations. Properly exporting the SYSTEM hive enables investigators to perform offline analysis while preserving forensic evidence and avoiding changes to the live system.
