# windows-dfir-lab42-shimcache-investigation

## Overview

ShimCache (AppCompatCache) is considered one of the most important Windows forensic artifacts because it can provide evidence that an executable existed on a system, even if the file has been deleted. It is widely used by professional DFIR analysts.

---

# Executive Summary

Windows has a feature called the Application Compatibility Framework.

Its purpose is simple:

Help old applications continue working on newer versions of Windows.

Suppose you install a program written for Windows XP on Windows 10.

Windows checks:

Is this program old?
Does it need compatibility fixes?
Should Windows apply special settings before launching it?

To speed up this process, Windows maintains a cache of applications it has examined.

That cache is called the:

ShimCache

or

Application Compatibility Cache (AppCompatCache).
Every time Windows evaluates an executable for compatibility, it records information inside the cache.

Think of ShimCache as:

Windows

↓

"I've seen this executable."

↓

Store basic information

↓

ShimCache

It is not designed for forensic investigations.

It exists for Windows compatibility.

Just like Amcache, forensic investigators later discovered that it contains valuable evidence.
Unlike Amcache, ShimCache is not a separate file.

It is stored inside the Windows Registry.

Location:

HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache

This Registry key contains binary data.

You cannot simply open it and read the contents.
Depending on the Windows version, ShimCache may contain:

Executable path
Executable name
File size
Last Modified Time
Compatibility information
ShimCache indicates that Windows processed or evaluated an executable.

It does not conclusively prove that the executable was successfully run.

Because of this:

Professional investigators correlate ShimCache with:

Prefetch
Amcache
BAM
SRUM
Event Logs

Never rely on ShimCache alone.


---

# Investigation Objectives

- Locate the ShimCache Registry artifact.
- Understand where Windows stores it.
- Generate executable activity.
- Parse ShimCache.
- Search for recently observed executables.
- Compare ShimCache with Amcache.
- Document forensic findings.

---


# Tools Used

- Windows 10 VM
-  PowerShell
-  Control Panel
-  AppCompatCacheParser (Eric Zimmerman)

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

1. Create investigation folder
2. Create and execute a sample executable.(.txt file)
3. Verify the ShimCache registry key.
4. Export the SYSTEM registry hive.
5. Attempt offline ShimCache parsing.
6. Identify parser dependency issue.


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

