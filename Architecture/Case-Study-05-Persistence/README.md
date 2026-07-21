# Persistence Investigation Using Splunk

## Overview

I created this lab to practice how a SOC Analyst investigates Windows persistence mechanisms using Splunk and Sysmon.

To generate the logs, I created a Registry Run Key under **HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run** using the Windows **reg.exe** utility. The registry value, named **TestPersistence**, was configured to launch **Notepad** automatically whenever the user logs in.

The goal of this project was to understand how persistence techniques are recorded by Sysmon, how to investigate registry modifications in Splunk, and how to identify the process responsible for creating the persistence mechanism.

---

## Lab Setup

* Windows 10 Virtual Machine
* Splunk Enterprise
* Splunk Universal Forwarder
* Sysmon

---

## Activity Performed

I performed the following actions during the lab:

* Created a test folder named **C:\SOC-Lab**
* Added a Registry Run Key named **TestPersistence**
* Configured the Run Key to launch **C:\Windows\System32\notepad.exe**
* Verified the registry entry using **Registry Editor**
* Waited for the events to be forwarded to Splunk
* Removed the persistence entry after the investigation

---

## Investigation

During the investigation, I examined:

* Registry value modification events (Sysmon Event ID 13)
* The Registry Run Key location used for persistence
* The **reg.exe** process that created the registry value (Sysmon Event ID 1)
* Important event fields such as time, process, registry path, details, and user
* Registry events generated specifically by **reg.exe**

The investigation confirmed that the registry modification was successfully recorded by Sysmon and forwarded to Splunk. Using simple SPL queries, I was able to identify the registry path, the process responsible for creating the persistence entry, and the user account that performed the action.

---

## What I Learned

This project helped me understand one of the most common Windows persistence techniques used by attackers.

I learned how Registry Run Keys can be monitored using Sysmon, how registry modification events appear in Splunk, and how to identify the process responsible for creating persistence on a Windows endpoint.

---

## Skills Practiced

* Splunk SPL
* Sysmon Log Analysis
* Windows Registry Investigation
* Persistence Detection
* Endpoint Investigation
* Windows Event Log Analysis
* Basic SOC Investigation