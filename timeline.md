# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 09:00 | Created investigation workspace | PowerShell |
| 09:05 | Created DemoApp.exe | File System |
| 09:10 | Executed sample executable | Start-Process |
| 09:15 | Verified ShimCache registry key | PowerShell |
| 09:20 | Exported SYSTEM registry hive | reg save |
| 09:25 | Attempted offline ShimCache parsing | AppCompatCacheParser |
| 09:30 | Identified missing .NET runtime | Parser Output |
| 09:35 | Preserved exported evidence | SYSTEM.hiv |
| 09:40 | Removed lab artifacts | PowerShell |
| 09:45 | Documented investigation | Documentation |

---

# Investigation Flow

Investigation Started

↓

Created Investigation Workspace

↓

Created Demo Executable

↓

Executed Demo Application

↓

Verified ShimCache Registry

↓

Exported SYSTEM Hive

↓

Attempted Offline Parsing

↓

Identified Missing .NET Runtime

↓

Preserved Evidence

↓

Removed Lab Artifacts

↓

Investigation Completed

---

# Summary

The investigation demonstrated the acquisition workflow for Windows ShimCache artifacts by verifying the registry location, exporting the SYSTEM registry hive, and preparing it for offline forensic analysis. Although AppCompatCacheParser could not process the hive due to a missing .NET runtime dependency, the evidence collection process was completed successfully, preserving the SYSTEM hive for future forensic examination.
