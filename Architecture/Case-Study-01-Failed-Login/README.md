# Failed Login Investigation Using Splunk

## Overview

I created this lab to practice how a SOC Analyst investigates failed login attempts in Windows using Splunk.

To generate the logs, I locked my Windows 10 virtual machine and entered the wrong password several times. These failed logins created Windows Security Event ID 4625, which was forwarded to Splunk using the Universal Forwarder.

The goal of this project was to learn how to search for failed login events, understand what the logs mean, and investigate basic authentication activity.

## Lab Setup

- Windows 10 Virtual Machine
- Splunk Enterprise
- Splunk Universal Forwarder
- Sysmon
- Windows Security Logs

## Attack Simulation

I locked the Windows VM and intentionally entered the wrong password 11 times.

After waiting for the logs to reach Splunk, I searched for Event ID 4625 and confirmed that all failed login attempts were recorded.

## Investigation

During the investigation, I looked at:

- Total failed login attempts
- Failure reason
- Logon type
- Timeline of the events
- Event details

The investigation showed that all failed logins were generated from the local machine because I entered the incorrect password directly on the Windows login screen.

## What I Learned

This project helped me understand how Windows records failed authentication events and how Splunk can be used to investigate them.

I also learned how to write basic SPL queries to analyze Windows Security logs and identify failed login activity.

## Skills Practiced

- Splunk SPL
- Windows Event Log Analysis
- Event ID 4625 Investigation
- Authentication Log Analysis
- Basic SOC Investigation