# File Creation Investigation Using Splunk

## Overview

I created this lab to practice how a SOC Analyst investigates file creation activity on a Windows system using Splunk and Sysmon.

To generate the logs, I created several files inside a test folder on my Windows 10 virtual machine. I also renamed one file and created a file named **malware.exe** (a renamed text file) to simulate a suspicious executable.

The goal of this project was to learn how file creation events are recorded by Sysmon, how to search for them in Splunk, and how to identify the process and user responsible for creating the files.

## Lab Setup

* Windows 10 Virtual Machine
* Splunk Enterprise
* Splunk Universal Forwarder
* Sysmon

## Activity Performed

I created a folder named **C:\SOC-Lab** and generated file activity by:

* Creating multiple test files
* Renaming one of the files
* Creating a file named **malware.exe** for testing
* Waiting for the events to be forwarded to Splunk

After the logs reached Splunk, I searched for **Sysmon Event ID 11** to verify that the file creation events were successfully recorded.

## Investigation

During the investigation, I looked at:

* All file creation events
* Files created inside the **SOC-Lab** folder
* The process that created each file
* The user account responsible for the activity
* The timeline of file creation events
* Executable files created during the test

The investigation confirmed that all file creation events were successfully collected by Splunk. I was able to identify the files, the process that created them, and the associated user account using simple SPL queries.

## What I Learned

This project helped me understand how Sysmon logs file creation events and how Splunk can be used to investigate endpoint activity.

I also learned how to filter logs, analyze important event fields, and identify potentially suspicious files during an investigation.

## Skills Practiced

* Splunk SPL
* Sysmon Log Analysis
* File Creation Investigation
* Windows Event Log Analysis
* Endpoint Investigation
* Basic SOC Investigation
