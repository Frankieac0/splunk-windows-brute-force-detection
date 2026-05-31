# Splunk Windows Brute Force Detection Project

## Project Overview

This project demonstrates the creation of a brute force detection solution using Splunk and Windows Security Event Logs.

The goal of the project is to identify failed authentication attempts, detect potential brute force attacks, and generate alerts for suspicious login activity.

---

## Tools Used

- Splunk Enterprise
- Windows Security Event Logs
- Windows 11
- GitHub

---

## Data Source

Windows Security Logs

Key Event ID:

- EventCode 4625 (Failed Login Attempts)

---

## Detection Queries

### Failed Login Events

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
```

### Failed Login Attempts by Account Name

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name
| sort - count
```

### Failed Login Attempts by Computer Name

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by ComputerName
| sort - count
```

### Brute Force Detection Threshold

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name ComputerName
| where count > 5
```

---

## Dashboard Components

1. Failed Login Events Over Time
2. Failed Login Attempts by Account Name
3. Failed Login Attempts by Computer Name

---

## Alert Configuration

A scheduled alert was created to detect excessive failed login attempts.

Trigger Condition:

- More than 5 failed login attempts
- Scheduled execution every 5 minutes

---

## Skills Demonstrated

- SIEM Monitoring
- Splunk Search Processing Language (SPL)
- Windows Event Log Analysis
- Brute Force Detection
- Dashboard Creation
- Alert Configuration
- Security Monitoring

---

## Author

Frank Coleman

Cybersecurity Student | SOC Analyst Candidate
## Project Evidence

### Windows Security Logs Successfully Ingested

See screenshot:
screenshots/queries/Raw Windows Security Events Successfully Ingested into Splunk.png

### Failed Login Events Filtered by EventCode 4625

See screenshot:
screenshots/queries/Windows Security Failed Authentication Events Filtered by EventCode 4625.png

### Failed Login Attempts by Account Name

See screenshot:
screenshots/queries/Failed Login Attempt Counts by Account Name in Splunk.png

### Correlated Failed Login Attempts by Account Name and Host

See screenshot:
screenshots/queries/Correlated Failed Login Attempts by Account Name and Host.png

### Detection Threshold Exceeded

See screenshot:
screenshots/queries/Failed Login Attempts Exceeding Brute Force Detection Threshold.png

### Alert Configuration

See screenshots:

screenshots/queries/Initial Scheduled Alert Configuration for Brute Force Detection.png

screenshots/queries/Final Configuration of Scheduled Brute Force Detection Alert.png

screenshots/queries/Successful Creation of Brute Force Login Detection Alert in Splunk.png
