# Investigation Notes

## Lab Summary

This investigation focused on acquiring and preparing Windows ShimCache (Application Compatibility Cache) artifacts for offline forensic analysis.

The investigation reconstructed the artifact acquisition workflow by creating a sample executable, verifying the ShimCache registry location, exporting the SYSTEM registry hive, and attempting offline analysis using AppCompatCacheParser.

---

## Analyst Methodology

1. Create investigation workspace.
2. Create a sample executable.
3. Execute the executable.
4. Verify the ShimCache registry key.
5. Export the SYSTEM registry hive.
6. Attempt offline parsing.
7. Identify parser dependency.
8. Preserve collected evidence.
9. Document findings.

---

## Investigation Scenario

A sample executable was created and executed to generate execution artifacts.

The investigation aimed to determine:

- Whether the ShimCache registry location existed.
- Whether the SYSTEM hive could be exported.
- Whether the exported hive could be parsed offline.
- Whether evidence acquisition completed successfully.
- Whether parser errors affected evidence preservation.

---

## Evidence Collected

### Evidence 1 – Sample Executable

Collected:

- DemoApp.exe

Finding:

Successfully created and executed for the investigation.

---

### Evidence 2 – ShimCache Registry

Command Used

```powershell
Get-Item "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache"
```

Finding:

Confirmed the ShimCache registry key exists.

---

### Evidence 3 – SYSTEM Hive Export

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

## DFIR Analysis

The investigation demonstrated the standard forensic workflow for ShimCache acquisition. Although offline parsing was unsuccessful due to a missing dependency, evidence collection completed successfully, preserving the registry hive for future analysis.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Discovery | File and Directory Discovery | T1083 |
| Collection | Data from Local System | T1005 |

---

## Analyst Observations

- ShimCache resides within the SYSTEM registry hive.
- Registry verification confirmed the artifact location.
- SYSTEM hive acquisition completed successfully.
- Offline analysis depends on external parsing tools.
- Missing .NET runtime prevented parser execution but did not affect evidence collection.

---

## Conclusion

The investigation successfully demonstrated ShimCache evidence acquisition by verifying the registry location, exporting the SYSTEM hive, and preparing it for offline forensic analysis. Although parser execution failed because the .NET runtime was unavailable, the collected evidence remained intact and suitable for future analysis.
