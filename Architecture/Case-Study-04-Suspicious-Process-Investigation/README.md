# Suspicious PowerShell Execution Investigation Using Splunk

## Overview

I created this lab to practice how a SOC Analyst investigates PowerShell process creation events using Splunk and Sysmon.

To generate the logs, I executed several PowerShell commands from Command Prompt to simulate command-line activity commonly seen during system reconnaissance.

The goal of this project was to understand how Sysmon records PowerShell executions, how Splunk collects these events, and how to investigate process creation activity using SPL queries.

## Lab Setup

* Windows 10 Virtual Machine
* Splunk Enterprise
* Splunk Universal Forwarder
* Sysmon

## Activity Performed

I generated PowerShell activity by executing commands such as:

* whoami
* hostname
* Get-Process
* Get-Service
* Get-LocalUser

After waiting for the logs to reach Splunk, I searched for Sysmon Event ID 1 to verify that the PowerShell process creation events were successfully recorded.

## Investigation

During the investigation, I reviewed:

* PowerShell process creation events
* Parent processes
* Command-line arguments
* User accounts
* Execution timeline
* Command frequency

The investigation confirmed that Sysmon successfully recorded the PowerShell executions and that Splunk provided detailed information for each process.

## What I Learned

This project helped me understand how PowerShell executions are monitored using Sysmon and Splunk.

I also learned how to investigate process creation events, analyze command lines, identify parent processes, and review user activity during an endpoint investigation.

## Skills Practiced

* Splunk SPL
* Sysmon Log Analysis
* PowerShell Investigation
* Process Creation Analysis
* Windows Endpoint Monitoring
* Basic SOC Investigation