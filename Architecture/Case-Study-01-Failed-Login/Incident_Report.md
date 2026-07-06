# Incident Report

## Summary

While testing my home SOC lab, I simulated multiple failed login attempts on a Windows 10 virtual machine.

The objective was to generate Windows Security Event ID 4625 and investigate the events using Splunk.

## Timeline

The failed login attempts occurred within a few minutes and were successfully forwarded to Splunk.

## Findings

- Event ID: 4625
- Total Failed Logins: 11
- Failure Reason: Unknown user name or bad password
- Logon Type: 2 (Interactive)
- Source Address: 127.0.0.1
- Host: DESKTOP-CTNJBF0

## Analysis

The logs confirmed that Windows created an Event ID 4625 for every failed login attempt.

The source address was 127.0.0.1 because the incorrect passwords were entered directly on the Windows virtual machine instead of from another device.

Logon Type 2 indicates that the login attempt happened locally through the Windows login screen.

Since this was a lab exercise, the activity was expected and used to practice log analysis.

## Conclusion

This investigation showed how failed login events can be detected and analyzed in Splunk.

The project helped me become more familiar with Windows authentication logs and basic SOC investigation techniques.