---
title: "Detecting Suspicious DNS Queries in Splunk"
date: 2025-03-15T21:37:00
draft: false
author: "Kelvin Kiplagat"
categories: ["Cybersecurity", "Splunk", "Threat Hunting"]
tags: ["DNS Analysis", "Splunk SIEM", "Threat Intelligence", "DNS Tunneling"]
summary: "An analysis of long DNS queries in Splunk and potential risks like DNS tunneling."
description: "This post explores the detection of unusually long DNS queries using Splunk, which may indicate DNS tunneling, malware command-and-control (C2) activity, or data exfiltration."
---



# Analyzing DNS Log Files Using Splunk SIEM

![image.png](image.png)

## Introduction

DNS (Domain Name System) logs are crucial for understanding network activity and identifying potential security threats. Splunk SIEM (Security Information and Event Management) provides powerful capabilities for analyzing DNS logs and detecting anomalies or malicious activities.

## Prerequisites

Before analyzing DNS logs in Splunk, ensure the following:

- Splunk instance is installed and configured.
- DNS log data sources are configured to forward logs to Splunk.

## Steps to Upload Sample DNS Log Files to Splunk SIEM

### 1. Prepare Sample DNS Log Files

- Obtain a sample DNS log file in a suitable format (e.g., `dns.log.gz`).([https://www.secrepo.com/maccdc2012/dns.log.gz](https://www.secrepo.com/maccdc2012/dns.log.gz))
- Ensure the log files contain relevant DNS events, including source IP, destination IP, domain, query type, response code, etc.
- Validate the log files to ensure they are formatted correctly and contain structured data for analysis.
- Save the sample log files in a directory accessible by the Splunk instance.

### 2. Upload Log Files to Splunk

- Log in to the Splunk web interface.
- Navigate to **Settings > Add Data**.
- Select **Upload** as the data input method.
- Choose the appropriate input source to match your log file format.

![image.png](image%201.png)

### 3. Choose File

- Click on **Select File** and choose the sample DNS log file `dns.log.gz`.
- Ensure that the correct file is uploaded to avoid data inconsistencies.

![image.png](image%202.png)

### 4. Set Source Type

- In the **Set Source Type** section, specify the source type as `dnslogs`.
- Ensure that the host is set to `kelvin` to track logs based on the originating system.
- Modify parsing options if needed to match the log file structure.

![image.png](image%203.png)

### 5. Review Settings

- Review other settings such as **index**, **host**, and **sourcetype**.
- Ensure the settings are configured correctly to match the sample DNS log file.
- Adjust **timestamp recognition** and **field extraction** settings if necessary.

![image.png](image%204.png)

### 6. Click Upload

- Once all settings are configured, click on the **Review** button.
- Verify the extracted fields and confirm the expected data format.
- Click **Submit** to upload the sample DNS log file to Splunk.

![image.png](image%205.png)

### 7. Verify Upload

- After uploading, navigate to the search bar in the Splunk interface.
- Run a search query to verify that the uploaded DNS events are visible:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs"
    ```
    
- Check if logs appear correctly and troubleshoot missing or malformed entries.

![image.png](image%206.png)

## Steps to Analyze DNS Log Files in Splunk SIEM

### 1. Search for DNS Events

- Open the Splunk interface and navigate to the search bar.
- Enter the following search query to retrieve DNS events:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs"
    ```
    
- Filter logs based on date, source IP, or specific DNS query types to refine search results.

![image.png](image%207.png)

### 2. Extract Relevant Fields

- Identify key fields in DNS logs such as **source IP, destination IP, domain, query type, response code**, etc.
- Use regex to search for common DNS-related keywords in the raw event data:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
    ```
    
- Ensure proper field extractions to facilitate detailed analysis.

![image.png](image%208.png)

### **Key Observations from the Splunk Results:**

1. **Filtered DNS Logs**
    - The results show DNS-related logs filtered from `dns.log.gz`, coming from **host "kelvin"** with `sourcetype="dnslogs"`.
    - The query successfully extracts DNS queries and responses based on the regex filter.
2. **Fields in the Logs:**
    - **Source & Destination IPs** → Example: `192.168.202.141` communicating with `192.168.207.4` on **port 53**.
    - **Query Type & Response Code** → Common responses include **NXDOMAIN** (Non-Existent Domain).
    - **Protocol** → Most queries use **UDP (User Datagram Protocol)**.
    - **Domain Queries** → Includes lookups like `dns.msftncsi.com`.
3. **NXDOMAIN Responses:**
    - **NXDOMAIN** indicates a **failed DNS lookup** (requested domain does not exist).
    - Could be normal or a sign of:
        - **Misconfigured DNS settings**
        - **Malicious activity (e.g., command-and-control domain lookups**

### 3. Identify Anomalies

- Look for unusual patterns or anomalies in DNS activity.
- Query to identify spikes:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | stats count by domain
    ```
    

![image.png](image%209.png)

**Findings:**

1. **High Number of Empty Domains (`(empty)`)**
    - 2,719 occurrences.
    - Could indicate **malformed DNS queries**, **corrupt logs**, or **network scanning attempts**.
2. **Suspicious Binary-like String (`\x00\x00\x00...`)**
    - 10,181 occurrences.
    - This might be **encoded data**, potentially **DNS tunneling** or **malicious traffic**.
    - Could indicate an **attempt to bypass security measures** by hiding payloads in DNS queries.
3. **Unusual Domains:**
    - **`s4yj3z+ahnzaa.=connect.rssfeeds.com`** and **`s6fgaabadbrmdcwnzb...=auth.rssfeeds.com`**
        - These contain **randomized alphanumeric prefixes**, possibly **algorithmically generated domains** (DGA).
        - DGAs are commonly used by **malware for command-and-control (C2) communication**.
    - **`../nessus`**
        - Could be related to vulnerability scanning or an attempt to exploit directory traversal.
    - **`0-jf-w.channel.facebook.com`**
        - Likely a legitimate request to Facebook services.
    - **`0.0.0.0.in-addr.arpa`**
        - Reverse DNS lookup for 0.0.0.0, possibly related to **misconfigured network settings**.

### 4. Find the Top DNS Sources

- Use the `top` command to count the occurrences of each query type:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | top domain
    ```
    

![image.png](image%2010.png)

is designed to retrieve the most frequently queried domains from the DNS log file (`dns.log.gz`) and display them in descending order based on their frequency.

### What to Expect from This Query:

1. **Most Queried Domains**
    - The results show the top domains that devices in your network have attempted to resolve via DNS.
    - The domain with the highest count is `44.206.168.192.in-addr.arpa`, indicating reverse DNS lookups.
2. **Count Column**
    - This indicates how many times each domain was queried.
    - Example: `creativecommons.org` was queried `1889` times.
3. **Percent Column**
    - This shows the percentage of total queries that each domain represents.

### Possible Insights:

- **Commonly Accessed Websites:**
    - Domains like `www.php.net`, `splunk.com`, `api.twitter.com`, and `facebook.com` suggest user activity related to development, social media, and analytics.
- **Suspicious Activity Detection:**
    - If unexpected domains appear frequently (e.g., unusual or unknown domains), they could indicate malware, beaconing, or C2 (Command and Control) activity.
- **Reverse Lookups (`in-addr.arpa`)**
    - The presence of `in-addr.arpa` domains suggests reverse DNS lookups, which could indicate system or service-level network activities.
- Identify the most frequently queried domains and their request origins:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | stats count by domain, src_ip | sort -count
    ```
    

![image.png](image%2011.png)

### **Key Findings from the Results**

- **Top Queried Domain:** `44.206.168.192.in-addr.arpa`
    - **(4148 requests from `192.168.202.83`)**
    - This indicates a **reverse DNS lookup** happening frequently from this internal IP.
- **Frequent API Calls:**
    - `api.twitter.com` (1440 requests)
    - `api.facebook.com` (1430 requests)
    - These suggest that users or applications on `192.168.202.103` are actively communicating with social media platforms.
- **Security & Admin-related Domains:**
    - `www.splunk.com` (1024 requests) → Possibly internal monitoring or updates.
    - `fs-1.one.ubuntu.com` (612 requests) → Ubuntu cloud services, maybe for system updates.
- **Possible Open-source Intelligence (OSINT) or Development Activity:**
    - `creativecommons.org`, `www.php.net`, `www.dokuwiki.org`
    - These are common for developers or research-related browsing.
1. **Potential Anomalies or Risks**
    - **Unusual Reverse DNS Lookups (`in-addr.arpa`)**
        - If unexpected, this could indicate an attacker **probing** or trying to **enumerate** internal IPs.
    - **Data Exfiltration via API Calls?**
        - High request counts to `api.twitter.com` & `api.facebook.com` could mean **automated tools or scripts** posting data.
        - Could indicate **data leaks** if unauthorized.
    - **Tunneling or Unknown Domains:**
        - If any **unknown domain** appears frequently from a single `src_ip`, it may be worth investigating for **C2 communication**.

### 5. Detect Fast Flux DNS Activity

- Look for domains with rapidly changing IP addresses, which could indicate a botnet:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | stats dc(src_ip) as unique_ips by domain | where unique_ips > 10
    ```
    

![image.png](image%2012.png)

    ****

**key findings**

**Suspicious Null/Encoded Domain: `\x00\x00\x00...`**

- **Possible Causes:**
    - **Malformed DNS Query:** Could be due to a **misconfigured** or malicious system.
    - **DNS Exfiltration / Tunneling:** Some malware hides data in DNS queries.
    - **Encoding Issue:** The data could be **binary**, indicating an application attempting to resolve an unusual domain.
    
    **. Reverse DNS Lookups (`.in-addr.arpa`)**
    
    - These entries represent **reverse DNS lookups** where an IP is being resolved into a hostname.
    - The high number of unique IPs querying different `.arpa` domains could indicate:
        - **Normal network behavior** (internal IP lookups).
        - **Potential reconnaissance activity** (an attacker probing internal IPs).
        - **Misconfigured DNS settings** leading to excessive reverse lookups.

### 6. Monitor for DNS Tunneling

- Detect DNS tunneling attempts by filtering high-frequency requests to unusual domains:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | stats count by domain | where count > 1000
    ```
    

![image.png](image%2013.png)

retrieved **domains with more than 1000 queries**.

### **Observations**

1. **High Volume of Reverse DNS Lookups**
    - **Domain:** `44.206.168.192.in-addr.arpa` (1507 queries)
    - **Meaning:** This is a **reverse DNS lookup**, resolving the IP `192.168.206.44` back to a hostname.
    - **Possible Causes:**
        - Normal network behavior (e.g., internal system resolving IPs).
        - **Reconnaissance activity**: Attackers often perform reverse lookups to map internal networks.
    

- Identify long suspicious domain names indicative of encoded data:
    
    ```
    source="dns.log.gz" host="kelvin" sourcetype="dnslogs" | eval domain_length=len(domain) | where domain_length > 50
    ```
    

Investigate if these queries originate from unauthorized sources.

![image.png](image%2014.png)

### **Key Findings from the Query Output**

1. **Total Events Matched**:
    - You filtered **430 events** from a total of **122,130** records.
    - This means that **430 DNS queries** had domains longer than **50 characters**.
2. **Suspicious DNS Queries?**
    - Some of the domain names appear **long and encoded**, which could indicate:
        - **DNS Tunneling** 🕵️‍♂️ (Data exfiltration via DNS)
        - **Randomized Malware Domains** 🚨 (Command & Control Servers)
        - **Legitimate but long subdomains** (e.g., CDNs, analytics tools)
3. **Highlighted Fields in Your Screenshot:**
    - `dst_ip`: Shows the destination IPs being queried.
    - `dst_port`: Includes **UDP 53**, meaning **DNS queries** are happening over the standard DNS protocol.
    - `flags`: Includes `NXDOMAIN` (indicating **non-existent domains**).
    - Some results show **PTR and SRV record lookups**, which are normal but could also be used for **reconnaissance**.

### Conclusion

Analyzing DNS log files using Splunk SIEM enables security professionals to detect and respond to potential security incidents effectively. By understanding DNS activity and identifying anomalies, organizations can enhance their overall security posture and protect against various cyber threats.

Feel free to customize these steps according to your specific use case and requirements.
