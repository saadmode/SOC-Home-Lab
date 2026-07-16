# Case Study 4: Suspicious PowerShell Execution Investigation

## Objective

The purpose of this investigation was to monitor PowerShell process creation events on a Windows 10 virtual machine using Sysmon and Splunk. The goal was to understand how PowerShell executions are logged, identify the command line used, determine the parent process, and practice investigating PowerShell activity as a SOC Analyst.

# Lab Environment

* **Host Machine:** Windows 10
* **SIEM:** Splunk Enterprise
* **Log Forwarder:** Splunk Universal Forwarder
* **Monitoring Tool:** Sysmon
* **Target System:** Windows 10 Virtual Machine

# Scenario

During routine monitoring, PowerShell was executed several times using different command-line arguments to simulate system reconnaissance activity. The objective was to investigate the PowerShell executions, determine how they were launched, identify the parent process, review the command line, and verify the user account responsible for the activity.

# Investigation Steps

### Step 1 – Search for PowerShell Process Creation Events

I first searched for all PowerShell process creation events recorded by Sysmon.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
```

This displayed all PowerShell process creation events.

### Step 2 – Display Important Investigation Fields

Next, I displayed the most useful information for each event.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
| table _time Image ParentImage CommandLine User
```

This allowed me to review:

* Event time
* Executed process
* Parent process
* Full command line
* User account

### Step 3 – Check Parent Processes

To understand how PowerShell was started, I grouped the events by parent process.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by ParentImage
```

This identified which application launched PowerShell.

### Step 4 – Check User Activity

I reviewed which user executed PowerShell.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by User
```

This identified the user account responsible for the activity.

### Step 5 – Review Command Lines

I examined the PowerShell command lines executed during the investigation.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
| stats count by CommandLine
```

This showed the different PowerShell commands executed during testing.

### Step 6 – Create a Timeline

Finally, I created a timeline to visualize when the PowerShell executions occurred.

**SPL Query**

```spl
index=* EventCode=1 Image="*powershell.exe"
| timechart count
```

The timeline clearly showed the execution activity over time.

# Findings

During the investigation I confirmed that:

* Sysmon successfully recorded PowerShell process creation events.
* Splunk collected all PowerShell execution logs.
* The parent process responsible for launching PowerShell was identified.
* The executed command lines were successfully captured.
* The user account responsible for the activity was identified.
* PowerShell reconnaissance activity could be investigated using simple SPL queries.

# What I Learned

This case study improved my understanding of PowerShell process monitoring using Sysmon and Splunk. I learned how to investigate process creation events, review command-line arguments, identify parent-child process relationships, and determine which user executed the commands. These investigation techniques are commonly used by SOC analysts during endpoint monitoring and threat hunting.

# Conclusion

This investigation demonstrated how Sysmon and Splunk can be used together to monitor PowerShell activity on Windows systems. By analyzing process creation events, command lines, parent processes, and user accounts, I was able to investigate PowerShell executions and understand how suspicious command-line activity can be identified during security monitoring.