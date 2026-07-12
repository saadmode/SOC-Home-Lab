# SPL Queries Used

These are the SPL queries I used during my investigation to analyze the failed login events (Event ID 4625).

---

## 1. View All Failed Login Events

This query displays every failed login event collected during the investigation.

```spl
index=* EventCode=4625
```

---

## 2. Count Total Failed Login Attempts

This query counts how many failed login events were recorded.

```spl
index=* EventCode=4625
| stats count as "Failed Login Attempts"
```

**Result:** 11 failed login attempts.

---

## 3. Check Failure Reasons

This query groups the events by the reason why the login failed.

```spl
index=* EventCode=4625
| stats count by Failure_Reason
```

**Result:** All events showed **"Unknown user name or bad password."**

---

## 4. Identify Logon Type

This query shows the type of logon used during the failed authentication attempts.

```spl
index=* EventCode=4625
| stats count by Logon_Type
```

**Result:** All events were **Logon Type 2 (Interactive)** because the incorrect password was entered directly on the Windows login screen.

---

## 5. View Login Activity Over Time

This query creates a timeline of the failed login events.

```spl
index=* EventCode=4625
| timechart span=1m count
```

## 6.  Display Failed Login Event Details

This query retrieves all failed login events (Event ID 4625) and displays the key fields needed during the investigation.

```spl
index=* EventCode=4625
| table _time Account_Name Account_Domain Failure_Reason Logon_Type Source_Network_Address Workstation_Name host
```

**Purpose**

- Shows the timestamp of each failed login.
- Identifies the targeted account.
- Displays the reason the login failed.
- Shows the logon type.
- Displays the source network address.
- Identifies the affected workstation and host.

**Result**

The query returned **11 failed login events**. All events had the failure reason **"Unknown user name or bad password"**, **Logon Type 2 (Interactive)**, and a **Source Network Address of 127.0.0.1**, confirming that the failed login attempts were generated locally during the lab.



This helped me see when the failed login attempts occurred and whether they happened within a short period.