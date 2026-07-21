# Network Connection Investigation Using Splunk

## Overview

I created this lab to practice how a SOC Analyst investigates network connection events in Windows using Splunk.

To generate the logs, I used PowerShell to send web requests to Google, GitHub, and Microsoft by running the `Invoke-WebRequest` command. These actions generated Sysmon Event ID 3 (Network Connection), which was forwarded to Splunk using the Universal Forwarder.

The goal of this project was to learn how to investigate outbound network connections, identify the process responsible for the connection, and analyze the destination IP addresses and ports.

## Lab Setup

- Windows 10 Virtual Machine
- Splunk Enterprise
- Splunk Universal Forwarder
- Sysmon
- PowerShell

## Attack Simulation

I generated outbound network traffic by executing the following PowerShell commands:

```powershell
Invoke-WebRequest https://www.google.com

Invoke-WebRequest https://github.com

Invoke-WebRequest https://www.microsoft.com
```

After waiting for the logs to reach Splunk, I searched for Sysmon Event ID 3 and confirmed that the network connection events were successfully recorded.

## Investigation

During the investigation, I looked at:

- All network connection events
- PowerShell network connections
- Destination IP addresses
- Destination ports
- Timeline of network activity
- Detailed event information

The investigation confirmed that PowerShell successfully established outbound HTTPS connections to external websites and that Sysmon recorded the activity.

## What I Learned

This project helped me understand how Sysmon records outbound network connections and how Splunk can be used to investigate network activity.

I also learned how to identify the process responsible for a connection, review destination IP addresses and ports, and analyze network events using SPL queries.

## Skills Practiced

- Splunk SPL
- Sysmon Event ID 3 Investigation
- Network Connection Analysis
- PowerShell Activity Investigation
- Basic SOC Investigation