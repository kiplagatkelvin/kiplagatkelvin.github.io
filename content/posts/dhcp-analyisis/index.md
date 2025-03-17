---

title: "DHCP Log Analysis Using Splunk"
date: 2025-03-17
draft: false
author: "Kelvin Kiplagat"
description: "A step-by-step guide on analyzing DHCP logs using Splunk, including identifying multiple IP leases per client."
tags: ["Splunk", "DHCP Logs", "Log Analysis", "Cybersecurity"]
categories: ["SIEM", "Threat Hunting"]

---


# Analyzing DHCP Log Files Using Splunk SIEM

![image.png](image.png)

## Introduction

Dynamic Host Configuration Protocol (DHCP) log files contain valuable information about IP address assignments, lease durations, client requests, and server responses. Analyzing DHCP logs using Splunk SIEM enables network administrators to monitor IP address usage, detect anomalies, identify unauthorized devices, and troubleshoot network issues effectively.

## Project Overview

In this project, we will upload sample DHCP log files to Splunk SIEM and perform various analyses to gain insights into IP address assignments within the network.

## Prerequisites

Before starting the project, ensure the following:

- Splunk instance is installed and configured.
- DHCP log data sources are configured to forward logs to Splunk.
- DHCP log files are available in a structured format (e.g., `dhcp.log.gz`).([https://www.secrepo.com/maccdc2012/dhcp.log.gz](https://www.secrepo.com/maccdc2012/dhcp.log.gz))
- Splunk sourcetype is defined as `KELVINDHCPLOGS`.

---

## Steps to Upload Sample DHCP Log Files to Splunk SIEM

### 1. Prepare Sample DHCP Log Files

- Obtain sample DHCP log files in a suitable format.([https://www.secrepo.com/maccdc2012/dhcp.log.gz](https://www.secrepo.com/maccdc2012/dhcp.log.gz))
- Ensure the log files contain relevant DHCP events, including timestamps, IP address assignments, lease durations, client identifiers, etc.
- Save the sample log files in a directory accessible by the Splunk instance.

![image.png](image%201.png)

### 2. Upload Log Files to Splunk

- Log in to the Splunk web interface.
- Navigate to **Settings > Add Data**.
- Select **Upload** as the data input method.

![image.png](image%202.png)

### 3. Choose File

- Click **Select File** and choose the sample DHCP log file (`dhcp.log.gz`).

![image.png](image%203.png)

### 4. Set Source Type

- In the **Set Source Type** section, specify the source type for the uploaded log file.
- Choose the appropriate source type for DHCP logs (`KELVINDHCPLOGS`).

![image.png](image%204.png)

### 5. Review Settings

- Review settings such as **index**, **host**, and **sourcetype**.
- Ensure the settings match the sample DHCP log file.

![image.png](image%205.png)

### 6. Click Upload

- Click **Review**, verify settings, then click **Submit** to upload the log file to Splunk.

![image.png](image%206.png)

### 7. Verify Upload

- Navigate to the search bar in the Splunk interface.
- Run the following query to verify that DHCP events are visible:
    
    ```
    source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
    ```
    

---

![image.png](image%207.png)

## Steps to Analyze DHCP Log Files in Splunk SIEM

### 1. Search for DHCP Events

Run the following search query to retrieve DHCP events:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
```

![image.png](image%208.png)

### 2. Extract Relevant Fields

Identify key fields in DHCP logs such as:

- **timestamp** → Log timestamp (epoch format).
- **client_identifier** → Unique client ID (random string).
- **leased_ip** → Assigned IP address.
- **dest_port** → Destination port (DHCP client, usually 68).
- **dhcp_server_ip** → DHCP server IP address.
- **source_port** → Source port (DHCP server, usually 67).
- **mac_address** → Client's MAC address.
- **dhcp_requested_ip** → IP address requested in the DHCP lease process.
- **lease_time** → Duration of lease in seconds.
- **transaction_id** → Unique transaction ID of the DHCP request.

Use Splunk's field extraction capabilities or regular expressions:

```
| rex field=_raw "(?P<leased_ip>\d+\.\d+\.\d+\.\d+)"
```

![image.png](image%209.png)

now the filleds have been extracted correctly

![image.png](image%2010.png)

### 3. Analyze IP Address Assignments

Determine the distribution of IP address assignments:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| stats count by leased_ip
```

is **counting the number of times each IP address has been leased** in the last 24 hours.

![image.png](image%2011.png)

### key findings:

1. **High DHCP Lease Activity**
    - **192.168.202.115** (20 times), **192.168.202.102** (18 times), **192.168.202.101** (17 times), and **192.168.202.113** (16 times) were leased frequently.
    - These may be **high-traffic or persistent devices** (e.g., workstations, servers, or IoT devices).
2. **Possible Device Renewals or Reassignments**
    - The presence of IPs leased multiple times suggests **frequent renewals or DHCP lease expirations**.
    - If unexpected, check the **DHCP lease duration settings** on the DHCP server.
3. **Low or Single-Time Leases**
    - **192.168.202.103, 192.168.202.111, 192.168.202.118** → These IPs were leased only **once** in 24 hours.
    - Could indicate **transient devices** (e.g., guests, mobile devices, or temporary systems).

### **Further Analysis**

**Identify MAC Addresses of These Leases**

Modify your query to include MAC addresses:

```
spl
CopyEdit
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| stats count by leased_ip, mac_address

```

This will help correlate **specific devices** to IPs.

![image.png](image%2012.png)

### **Identifying Device Types**

**VMware MAC Addresses Detected**

- **00:0c:29:** is a VMware OUI (Organizationally Unique Identifier).
- Suggests **virtual machines** are being assigned IPs dynamically.

### **Investigate DHCP Lease Patterns**

- **Frequent Leases**
    - 192.168.202.115 (20 leases) and 192.168.202.102 (18 leases) → Possible DHCP **renewal issues** or a misconfigured device.
    - Suggest checking DHCP **lease time settings**.
- **Low Lease Counts**
    - IPs like **192.168.202.103, 192.168.202.111, 192.168.202.118** have **only 1 lease** → These may be **temporary guest devices**.

Identify the top 10 most leased IP addresses:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| top limit=10 leased_ip
```

![image.png](image%2013.png)

my observation 

- **Most frequently leased IP:** `192.168.202.75` (assigned **33 times** in 24 hours).
- **Frequent clients:** Devices using `192.168.202.141`, `192.168.202.115`, and `192.168.202.91` are also active.
- **Presence of `255.255.255.255`:**
    - This is a **broadcast address** used when a device is requesting an IP.
    - Could indicate frequent **DHCP Discover requests** (e.g., devices joining the network).

### 4. Detect Anomalies

Look for unusual IP assignment patterns over time:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| timechart span=1h count by leased_ip
```

![image.png](image%2014.png)

Here are some observations:

1. **Time-Based Analysis**: The logs are displayed in hourly intervals.
2. **Mostly Zero Activity**: From **10:00 AM on March 16, 2025, to 1:00 AM on March 17, 2025**, all recorded values are `0`, indicating no DHCP activity.
3. **Spike in Activity**: At **2:00 AM on March 17, 2025**, DHCP activity is recorded across multiple IP addresses.
4. **Significant DHCP Requests**: The highest recorded count at `2:00 AM` is `134` under the "OTHER" column, with other IP addresses showing varying counts.
5. **No Further Activity**: After 2:00 AM, activity drops back to `0` at 3:00 AM and 4:00 AM.

### **Possible Interpretations**

- **Scheduled Event or Attack?**
    - If the sudden spike at 2:00 AM wasn't expected, it could indicate **unauthorized activity**, such as a rogue device performing mass DHCP requests.
    - If this was a known event (e.g., system updates, maintenance), it might be **normal network behavior**.
- **Potential Anomalies**
    - Investigate why **only 2:00 AM saw activity** while the rest of the log is empty.
    - The "OTHER" column has **134** requests, which is significantly higher than other IPs—this could indicate **an anomaly** or **a misconfigured device**.
    - Cross-check with **firewall logs, IDS/IPS alerts, or endpoint logs** to see if this event aligns with other suspicious activity

Detect unauthorized or unknown DHCP clients:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| stats dc(client_identifier) AS unique_clients BY mac_address
```

![image.png](image%2015.png)

you have a list of unique `client_identifier` counts per `mac_address`.

### **Interpretation of Your Results**

- Each row represents a **unique MAC address**.
- The `unique_clients` column shows the **number of distinct client identifiers** associated with that MAC address.
- If `unique_clients > 1`, it means **multiple clients are using the same MAC address**, which could indicate:
    - **Shared devices** (e.g., virtual machines, NAT devices).
    - **DHCP spoofing or MAC cloning**.
    - **Reassigned DHCP leases**.

Identify possible rogue DHCP servers by monitoring unexpected DHCP offers:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS" DHCPMessageType=OFFER
| stats count by host
```

![image.png](image%2016.png)

successfully counted the number of DHCP log events (333) for the host **"kelvin"** from the source `dhcp.log.gz`.
This groups the logs **by host** and counts the total number of events per host.

Since i have  only have one host (`kelvin`), it returns a single row.

### 5. Monitor IP Address Usage

Monitor IP address lease activity over time:

```
source="dhcp.log.gz" host="kelvin" sourcetype="KELVINDHCPLOGS"
| timechart span=1h count by leased_ip
```

![image.png](image%2017.png)

- **Observations:**
    - Almost all IP addresses had **zero leases** for most of the observed period.
    - **Between 02:00 and 03:00 on March 17, 2025**, there was noticeable activity:
        - `192.168.202.101` = 17 leases
        - `192.168.202.102` = 18 leases
        - `192.168.202.112` = 16 leases
        - `192.168.202.113` = 16 leases
        - `192.168.202.115` = 20 leases
        - `192.168.202.141` = 32 leases
        - `192.168.202.157` = 11 leases
        - `192.168.202.75` = 33 leases
        - `192.168.202.91` = 18 leases
        - `255.255.255.255` = 134 leases (This might indicate a broadcast DHCP lease request)

### **Possible Explanations for the Sudden Spike**

1. **DHCP Renewal Burst**:
    - Multiple clients might have attempted to renew their IP leases simultaneously.
    - This could happen if the DHCP lease time expired around that period.
2. **Network Anomaly or Attack**:
    - A rogue device or **DHCP starvation attack** could be attempting to exhaust available IPs.
    - The high number of **broadcast (255.255.255.255) requests** might indicate excessive DHCP discover requests.
3. **Planned System Restart or Maintenance**:
    - A DHCP server reboot could trigger all devices to renew their leases.
    

**Conclusion**

Analyzing DHCP log files using Splunk SIEM provides valuable insights into IP address assignments within a network. By monitoring DHCP events, detecting anomalies, and correlating logs with other security data, organizations can:

- Improve network management.
- Identify unauthorized or rogue DHCP servers.
- Detect devices that frequently change IPs.
- Troubleshoot network and connectivity issues efficiently.

By leveraging Splunk’s powerful log processing capabilities, security teams can enhance visibility into network activity and prevent potential security incidents.
