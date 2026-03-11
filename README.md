# Mini SIEM Brute Force Detection Lab

## Overview

This project demonstrates how a Security Information and Event Management (SIEM) platform can be used to detect and monitor brute-force login attempts using Splunk.

In this lab, authentication logs were ingested into Splunk Enterprise and analyzed using SPL (Search Processing Language) to identify repeated failed login attempts from a single IP address. Alerts and dashboards were then created to automatically detect and visualize suspicious authentication activity.

---

## Tools Used

* Splunk Enterprise
* SPL (Search Processing Language)
* Regex for IP extraction

---

## Lab Architecture

Authentication Logs → Splunk Indexing → SPL Detection Query → Alert Trigger → Security Monitoring Dashboard

---

## Detection Query

The following SPL query was used to detect repeated failed login attempts and identify attacker IP addresses:

```
index=main source="*auth_attack.log*" fail OR Failed
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort -count
```

This query performs the following steps:

* Searches authentication logs for failed login attempts
* Extracts the source IP address using regex
* Counts the number of attempts per IP
* Sorts results to identify the most active attacker

---

## Detection Results

The SIEM detected repeated failed login attempts from the following IP address:

```
163.27.187.39
23 failed login attempts
```

This activity represents a simulated brute-force login attack.

---

## Alert Configuration

An automated alert was configured in Splunk with the following parameters:

* Alert Name: Brute Force Login Detection
* Trigger Condition: Number of Results > 10
* Schedule: Runs hourly
* Action: Add to Triggered Alerts

This allows the SIEM to automatically
