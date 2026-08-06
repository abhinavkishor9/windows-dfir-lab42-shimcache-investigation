# Troubleshooting Notes

## Issue 1

Parser failed to execute.

### Cause

.NET Runtime was required. It wasn't installed.

### Resolution

Install the required .NET Desktop Runtime before running AppCompatCacheParser.

---

## Issue 2

Parser displayed "Failed to resolve hostfxr.dll".

### Cause

Missing .NET runtime libraries.

### Resolution

Download and install the appropriate x64 .NET runtime from Microsoft.

---

## Issue 3

SYSTEM hive export failed.

### Cause

PowerShell or Command Prompt was not running as Administrator.

### Resolution

Launch as Administrator. Then we execute:

```cmd
reg save HKLM\SYSTEM C:\ShimCacheLab\SYSTEM.hiv
```

---

## Issue 4

Registry key not found.

### Cause

Incorrect registry path.

### Resolution

Verify the path:

```powershell
Get-Item "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache"
```

---

## Issue 5

Demo executable did not launch.

### Cause

Incorrect executable path.

### Resolution

Verify the file exists before executing:

```powershell
Get-ChildItem C:\ShimCacheLab
```

---


```powershell
Remove-Item C:\ShimCacheLab -Recurse -Force
```
