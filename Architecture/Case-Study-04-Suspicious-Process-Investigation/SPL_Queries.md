# Case Study 4 - Splunk Searches

## 1. Show all PowerShell process creation events

```spl
index=* EventCode=1 Image="*powershell.exe"
```

Purpose:
Displays all PowerShell process creation events collected by Sysmon.

---

## 2. Display important investigation fields

```spl
index=* EventCode=1 Image="*powershell.exe"
| table _time Image ParentImage CommandLine User
```

Purpose:
Shows the event time, process, parent process, command line, and user.

---

## 3. Count executions by parent process

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by ParentImage
```

Purpose:
Identifies which application launched PowerShell.

---

## 4. Count executions by user

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by User
```

Purpose:
Shows which user account executed PowerShell.

---

## 5. Count command lines

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by CommandLine
```

Purpose:
Shows the different PowerShell commands executed.

---

## 6. Display execution timeline

```spl
index=* EventCode=1 Image="*powershell.exe"
| timechart count
```

Purpose:
Visualizes PowerShell activity over time.