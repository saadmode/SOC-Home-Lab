# Case Study 7: File Creation Investigation

## Objective

The purpose of this investigation was to monitor file creation events on a Windows 10 virtual machine using Sysmon and Splunk. The goal was to understand how file creation events are logged, identify which process created the files, and practice investigating this activity as a SOC analyst.


# Lab Environment

* **Host Machine:** Windows 10
* **SIEM:** Splunk Enterprise
* **Log Forwarder:** Splunk Universal Forwarder
* **Monitoring Tool:** Sysmon
* **Target System:** Windows 10 Virtual Machine


# Scenario

During routine monitoring, several new files were created inside a folder named **C:\SOC-Lab**. One of the files was named **malware.exe**, which could look suspicious during an investigation. My task was to use Splunk to review the logs, identify the files that were created, and determine which process and user were responsible.


# Investigation Steps

### Step 1 – Search for File Creation Events

I first searched for all Sysmon file creation events.

**SPL Query**

```spl
index=* EventCode=11
```

This showed all file creation events collected by Sysmon.


### Step 2 – Filter the Investigation Folder

Since Windows creates many files in the background, I filtered the search to only show events related to my test folder.

**SPL Query**

```spl
index=* EventCode=11 TargetFilename="*SOC-Lab*"
```

This made it much easier to focus only on the files created during the test.


### Step 3 – View Important Information

Next, I displayed only the most useful fields.

**SPL Query**

```spl
index=* EventCode=11
| table _time TargetFilename Image User
```

This allowed me to quickly see:

* The time of the event
* The file name
* The process that created the file
* The user account involved


### Step 4 – Check Which Processes Created Files

To understand which applications were creating files, I grouped the events by process.

**SPL Query**

```spl
index=* EventCode=11
| stats count by Image
```

This provided a summary of the processes responsible for file creation.


### Step 5 – Check User Activity

I also checked which user account created the files.

**SPL Query**

```spl
index=* EventCode=11
| stats count by User
```

This helped identify the user associated with the activity.


### Step 6 – Create a Timeline

Finally, I created a timeline to see when file creation events occurred.

**SPL Query**

```spl
index=* EventCode=11
| timechart count
```

The timeline showed the file creation activity over time and made it easy to identify when the test actions happened.


# Findings

During the investigation I confirmed that:

* File creation events were successfully collected by Sysmon.
* The files created inside **C:\SOC-Lab** appeared in Splunk.
* Splunk recorded the process responsible for creating each file.
* The user account responsible for the activity was also recorded.
* The test file named **malware.exe** appeared in the logs like any other newly created file. Although it was only a renamed text file, a SOC analyst would normally investigate any unexpected executable file.


# What I Learned

This case study helped me understand how Sysmon records file creation events and how Splunk can be used to investigate them. I also learned how to filter large amounts of log data, display only useful information, and identify the process and user responsible for file creation. These are common tasks performed by SOC analysts during endpoint investigations.


# Conclusion

This investigation demonstrated how Splunk and Sysmon can be used together to monitor file creation activity on Windows systems. By using simple SPL searches, I was able to identify newly created files, determine which process created them, and review the associated user account. This project improved my understanding of endpoint monitoring and basic incident investigation using a SIEM.
