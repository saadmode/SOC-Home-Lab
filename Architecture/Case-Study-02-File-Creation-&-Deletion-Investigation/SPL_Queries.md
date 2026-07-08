# Case Study 7 - Splunk Searches

## 1. Show all Sysmon file creation events

```spl
index=* EventCode=11
```

Purpose:
Displays every file creation event collected by Sysmon.

---

## 2. Show only files created inside the SOC-Lab folder

```spl
index=* EventCode=11 TargetFilename="*SOC-Lab*"
```

Purpose:
Filters results to the investigation folder.

---

## 3. Display important investigation fields

```spl
index=* EventCode=11
| table _time TargetFilename Image User
```

Purpose:
Shows the event time, file name, process, and user.

---

## 4. Count file creation by process

```spl
index=* EventCode=11
| stats count by Image
```

Purpose:
Identifies which processes created files.

---

## 5. Count file creation by user

```spl
index=* EventCode=11
| stats count by User
```

Purpose:
Shows which user account created files.

---

## 6. Display file creation timeline

```spl
index=* EventCode=11
| timechart count
```

Purpose:
Visualizes file creation activity over time.

---

## 7. Search for executable files

```spl
index=* EventCode=11 TargetFilename="*.exe"
```

Purpose:
Finds executable files created on the system.

---

## 8. Investigate a specific executable

```spl
index=* EventCode=11 TargetFilename="*malware.exe*"
```

Purpose:
Reviews the event details for the simulated suspicious executable.
