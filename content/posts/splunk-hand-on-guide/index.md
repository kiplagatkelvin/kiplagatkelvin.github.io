---
title: "Threat Hunting with OSINT and Splunk: A Hands-on Guide"
author: "Kiplagatkelvin"
date: "2025-02-03"
summary: "Learn how to use OSINT tools like Shodan and analyze security logs in Splunk to detect and mitigate cyber threats."
categories: ["Cybersecurity", "Threat Hunting", "OSINT"]
tags: ["OSINT", "Splunk", "Threat Hunting", "Cybersecurity", "SIEM", "Kali Linux"]
readingTime: "8 min"
---




### Threat Hunting with OSINT and Splunk: A Hands-on Guide 

<figure id="2d80" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*5ED_nEsd13M1PN6zf2AtGQ.png"
class="graf-image" data-image-id="1*5ED_nEsd13M1PN6zf2AtGQ.png"
data-width="1118" data-height="571" data-is-featured="true" />
</figure>

### Introduction 
Cyber threats continue to evolve, and organizations must stay ahead of
attackers by using proactive security measures. One key approach is
**threat hunting**, which involves actively searching for threats within
a network rather than waiting for alerts.

In this hands-on activity, we will use **Open-Source Intelligence
(OSINT)** to gather threat data and then analyze security logs using
**Splunk** to detect suspicious activity. This guide will walk you
through the process using **Kali Linux**, demonstrating how to:

-   Perform **OSINT reconnaissance** using **Shodan**.
-   Use **Splunk** to ingest and analyze security logs.
-   Identify **suspicious activity** based on OSINT findings.
-   Propose **mitigation strategies** to strengthen cybersecurity
    defenses.

Let's get started!

### Variables Needed 

Before beginning, we must define key **variables** for our analysis:

-   **Target IP or Device Type** --- Identify a specific IP address,
    device type, or service to investigate.
-   **Threat Intelligence Indicators** --- Suspicious IPs, default
    credentials, exposed services, or vulnerable systems.
-   **Security Logs** --- Firewall logs, authentication logs, or
    network traffic logs to analyze.
-   **Splunk Queries** --- Search patterns to detect malicious
    activity.

### Tools Used 

To complete this activity, we will use the following tools:

### 1. OSINT Tool: Shodan

-   **Shodan**
    ([https://www.shodan.io](https://www.shodan.io){.markup--anchor
    .markup--li-anchor data-href="https://www.shodan.io" rel="noopener"
    target="_blank"}) is a search engine that scans and indexes
    Internet-connected devices.
-   Helps identify **exposed services, open ports, and
    vulnerabilities**.

### 2. Security Information and Event Management (SIEM) Tool: Splunk 

-   **Splunk** (https://www.splunk.com) is a powerful **SIEM** that
    collects, analyzes, and visualizes security logs.
-   We will use **Splunk Free**

**3. Kali Linux**

-   Kali Linux includes essential tools for **OSINT, penetration
    testing, and log analysis**.

### Step 1: Gather Threat Intelligence Using Shodan 

### 1.1 Access Shodan Online 

1.  Open **Firefox** or any browser.
2.  Navigate to [**Shodan.io**](https://www.shodan.io){.markup--anchor
    .markup--li-anchor data-href="https://www.shodan.io" rel="noopener"
    target="_blank"}.

<figure id="1df3" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*I1U_mOtk_s7EWvTimjpOkA.png"
class="graf-image" data-image-id="1*I1U_mOtk_s7EWvTimjpOkA.png"
data-width="1897" data-height="934" />
</figure>

**3. Create an account** (if you haven't already).

<figure id="8204" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*z7yez3eG62cSg6IKFNVINA.png"
class="graf-image" data-image-id="1*z7yez3eG62cSg6IKFNVINA.png"
data-width="1918" data-height="901" />
</figure>

### 1.2 Perform an OSINT Search 

Use Shodan's search bar to look for exposed and vulnerable systems:

#### **Search for SSH services on port 22**: 

``` {#fe03 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
port:22
```

it displays more open port : 22

<figure id="0a13" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Esm-HLpJ7rjaJbeOjAC9Qg.png"
class="graf-image" data-image-id="1*Esm-HLpJ7rjaJbeOjAC9Qg.png"
data-width="1906" data-height="933" />
</figure>

<figure id="3339" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*CePsHyDGJrIf7jwsPekZKw.png"
class="graf-image" data-image-id="1*CePsHyDGJrIf7jwsPekZKw.png"
data-width="498" data-height="816" />
</figure>

united states was leading in term of open port :22 with 20 million
results then followed by Germany ,china and the list continue by...

i checked on the shodan report and vulnerability section is where i was
paying attention to:

<figure id="759e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*0l-mQLct8PT9WhoRTz6aEw.png"
class="graf-image" data-image-id="1*0l-mQLct8PT9WhoRTz6aEw.png"
data-width="1918" data-height="955" />
</figure>

#### **SSH Services on Port 22 (port:22):** 

-   **Type of Exposed Devices:** A wide variety of devices expose SSH
    (Secure Shell) services on port 22. This could include servers (web
    servers, database servers, file servers), routers, firewalls,
    network devices, and even embedded systems. The prevalence of SSH on
    port 22 is because it's the standard port for remote
    administration.
-   **Potential Risks:** Exposing SSH directly to the internet carries
    significant risks:
-   **Brute-Force Attacks:** Attackers can attempt to guess usernames
    and passwords to gain access.
-   **Vulnerability Exploitation:** If the SSH server software has
    known vulnerabilities, attackers can exploit them to gain
    control.
-   **Man-in-the-Middle Attacks:** If SSH is misconfigured or weak
    ciphers are used, attackers might intercept communication and steal
    credentials or manipulate data.

**How Attackers Could Exploit These Systems:**

**Gaining Initial Access:** Once an attacker gains access via SSH, they
can pivot to other systems on the network.

**Data Breaches:** Attackers can steal sensitive data stored on the
compromised server.

**Malware Installation:** Attackers can install malware, such as
ransomware or backdoors, to maintain persistence or disrupt operations.

**Denial-of-Service (DoS) Attacks:** Compromised systems can be used as
part of a botnet for DDoS attacks.

-   **Find devices with default passwords**:

i was curious to check devices with default password.

``` {#d21e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
default password
```

<figure id="523a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*7SRAqJXgBcMS-OI3HoDVmg.png"
class="graf-image" data-image-id="1*7SRAqJXgBcMS-OI3HoDVmg.png"
data-width="1918" data-height="841" />
</figure>

<figure id="7035" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*aME1J3Kn0vlnycOlifBWDw.png"
class="graf-image" data-image-id="1*aME1J3Kn0vlnycOlifBWDw.png"
data-width="1870" data-height="825" />
</figure>

shodan report states that the vulnerabilties were 17

<figure id="1e74" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*5XDWNBDToBCUcCYPyM0j5A.png"
class="graf-image" data-image-id="1*5XDWNBDToBCUcCYPyM0j5A.png"
data-width="1908" data-height="781" />
</figure>

#### **Devices with Default Passwords (default password):** 

**Type of Exposed Devices:** Devices using default passwords are often
IoT devices (routers, cameras, smart home devices), embedded systems,
and older network equipment. These devices are often overlooked in terms
of security updates and configuration.

**Potential Risks:** Using default passwords is extremely risky.
Attackers can easily find default credentials online or use automated
tools to scan for devices with these weaknesses.

#### **How Attackers Could Exploit These Systems:** 

**Easy Access:** Default credentials provide trivial access to the
device, bypassing any other security measures.

**Device Hijacking:** Attackers can take control of the device for
malicious purposes, like including it in a botnet.

**Data Theft:** If the device stores or processes data, attackers can
access it.

**Network Compromise:** A compromised device on the network can be a
stepping stone to other, more critical systems.

#### **Identify vulnerable Apache servers**: 

``` {#9957 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
product:apache httpd
```

<figure id="8620" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*LOI5syhjW2kao5LBQNbryQ.png"
class="graf-image" data-image-id="1*LOI5syhjW2kao5LBQNbryQ.png"
data-width="1918" data-height="949" />
</figure>

shodan report vulnerabity section:

<figure id="6470" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*cZzMkvSmgX2CsXVRwngz9Q.png"
class="graf-image" data-image-id="1*cZzMkvSmgX2CsXVRwngz9Q.png"
data-width="1911" data-height="931" />
</figure>

### **Vulnerable Apache Servers (product:apache httpd):** 

**Type of Exposed Devices:** Web servers running the Apache HTTPD
software.

**Potential Risks:** Apache, like any software, can have
vulnerabilities. These vulnerabilities can range from information
disclosure to remote code execution.

#### **How Attackers Could Exploit These Systems:** 

**Remote Code Execution (RCE):** The most severe vulnerabilities allow
attackers to execute arbitrary code on the server, potentially giving
them complete control.

**Local File Inclusion (LFI):** Attackers might be able to read
sensitive files on the server.

-   **Cross-Site Scripting (XSS):** Attackers can inject malicious
    scripts into web pages served by the vulnerable Apache server,
    potentially targeting users.
-   **Denial-of-Service (DoS):** Exploits might cause the server to
    crash or become unavailable.

### Step 2: Collect and Analyze Data Using Splunk 

### 2.1 Install or Access Splunk 

#### Option 1: Install Splunk Free on Kali Linux 

1.  Download Splunk from [Splunk
    Download](https://www.splunk.com/en_us/download/splunk-enterprise.html){.markup--anchor
    .markup--li-anchor
    data-href="https://www.splunk.com/en_us/download/splunk-enterprise.html"
    rel="noopener" target="_blank"}.

### Breakdown of the Command: 

``` {#4e23 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
wget -O splunk.deb "https://download.splunk.com/products/splunk/releases/latest/linux/splunk-latest-linux-2.6-amd64.deb"
```

<figure id="b0fb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*IrD8nh9kxDzuK_7oLlycEQ.png"
class="graf-image" data-image-id="1*IrD8nh9kxDzuK_7oLlycEQ.png"
data-width="1915" data-height="414" />
</figure>

<figure id="0e51" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*d-Dco176O0QZv1MOAxJ2dg.png"
class="graf-image" data-image-id="1*d-Dco176O0QZv1MOAxJ2dg.png"
data-width="1915" data-height="244" />
</figure>

2\. Install it using:

``` {#a497 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
dpkg -i splunk-splunk-9.4.0-6b4ebe426ca6-linux-amd64.deb
```

<figure id="5416" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*ruaPDvpwYKRLmXKm4qE4Jw.png"
class="graf-image" data-image-id="1*ruaPDvpwYKRLmXKm4qE4Jw.png"
data-width="1918" data-height="412" />
</figure>

3\. Start Splunk and set an admin password:

``` {#592d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo /opt/splunk/bin/splunk start -accept-license
```

<figure id="cbdd" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*qe8YIxxt6AMyMv_4g_PlxQ.png"
class="graf-image" data-image-id="1*qe8YIxxt6AMyMv_4g_PlxQ.png"
data-width="1885" data-height="310" />
</figure>

4\. Open Splunk's web interface:

``` {#9446 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
http://127.0.0.1:8000
```

<figure id="dea4" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*k0Z23UIyXSlXyDfO6vVUcQ.png"
class="graf-image" data-image-id="1*k0Z23UIyXSlXyDfO6vVUcQ.png"
data-width="1918" data-height="987" />
</figure>

already logged in:

<figure id="cf94" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*uUCMtU2gmtWWRMG421_3Ww.png"
class="graf-image" data-image-id="1*uUCMtU2gmtWWRMG421_3Ww.png"
data-width="1918" data-height="981" />
</figure>

### 2.2 Ingest Security Logs into Splunk 

-   Collect logs from **firewall, authentication, or network
    traffic**:

``` {#4f41 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo tail -f /var/log/auth.log sudo cat /var/log/syslog && sudo tcpdump -i eth0 -w capture.pcap
```

it us began capturing the file and we are creating a traffic

<figure id="bcd8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ICEcpY76GwgGe2qjfG2B_Q.png"
class="graf-image" data-image-id="1*ICEcpY76GwgGe2qjfG2B_Q.png"
data-width="1917" data-height="451" />
</figure>

#### Monitor `/var/log/auth.log`{.markup--code .markup--h4-code} with `tail -f`

``` {#f2d9 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo tail -f /var/log/auth.log
```

<figure id="3183" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*qcM-Z5nNOSd6vI2Sf8SZPw.png"
class="graf-image" data-image-id="1*qcM-Z5nNOSd6vI2Sf8SZPw.png"
data-width="1906" data-height="364" />
</figure>

This will continuously display the last few lines of
`/var/log/auth.log`{.markup--code .markup--p-code} and update the output
as new entries are added.

#### Collect logs from a network or endpoints

Ingest Security Logs:

``` {#f73f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo tail -f /var/log/auth.log   # View authentication logs
sudo cat /var/log/syslog         # View system logs
sudo tcpdump -i eth0 -w capture.pcap   # Capture network traffic
```

-   Upload logs into **Splunk**.

to ingest data to splunk the data we had earlier on generated we go
**setting** and then **data input** then **Choose the Data Type**:

<figure id="cf59" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Wqxc9PA8j0QPmT_ItazSAA.png"
class="graf-image" data-image-id="1*Wqxc9PA8j0QPmT_ItazSAA.png"
data-width="1917" data-height="856" />
</figure>

-   Select the type of input you want to configure. For example, if
    you're uploading a log file from your local machine, choose **Files
    & Directories**.
-   If you're collecting logs directly from a network or a server, you
    can choose other inputs like **TCP/UDP** or **HTTP Event
    Collector**.

**below image display adding data.**

<figure id="926e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*twaD1zs-DGqpVQZdV9eONQ.png"
class="graf-image" data-image-id="1*twaD1zs-DGqpVQZdV9eONQ.png"
data-width="1906" data-height="676" />
</figure>

### 2.3 Hunt for Suspicious Activity 

Use Splunk to analyze security logs and detect threats:

-   Go to **Search & Reporting**.
-   Run a search query to verify the logs are ingested
-   **Find failed SSH login attempts**:

``` {#4493 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
index=auth | search "Failed password"
```

<figure id="4b96" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*9aUuIx-xcs5pfAsGoXdpCw.png"
class="graf-image" data-image-id="1*9aUuIx-xcs5pfAsGoXdpCw.png"
data-width="1918" data-height="856" />
</figure>

**. Look for privilege escalation attempts**:

``` {#a9fb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
index=linux_logs | search "sudo su" OR "sudo -i"
```

<figure id="f981" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*y6KBwuyXgnfgeG3bFcD7Dg.png"
class="graf-image" data-image-id="1*y6KBwuyXgnfgeG3bFcD7Dg.png"
data-width="1912" data-height="787" />
</figure>

### Step 3: Mitigation and Remediation 

### 3.1 Mitigation Steps 

1.  **Block malicious IPs** using iptables:

``` {#d696 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
sudo iptables -A INPUT -s <malicious_ip> -j DROP
```

<figure id="8164" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*-WBgkOezZkOJqFL_J_HQMQ.png"
class="graf-image" data-image-id="1*-WBgkOezZkOJqFL_J_HQMQ.png"
data-width="1743" data-height="943" />
</figure>

Your **iptables** rule has been successfully added! 🎉

The output confirms that **traffic from**
**`192.168.1.100`{.markup--code .markup--p-code}** **is now being
dropped** because:

✅ The rule appears in the **INPUT chain**\
✅ **Packets (pkts) and bytes (bytes) count is 0** --- This means the
blocked IP **hasn't tried to connect yet**

**2. Update security patches**

``` {#d01f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
sudo apt update && sudo apt upgrade -y
```

obviously update the patch daily if you can

<figure id="0671" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*vaBQKvEKlOgjEu-9ZX5IYg.png"
class="graf-image" data-image-id="1*vaBQKvEKlOgjEu-9ZX5IYg.png"
data-width="1723" data-height="877" />
</figure>

**3. Harden SSH security**:

``` {#8efa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo nano /etc/ssh/sshd_config
```

<figure id="1520" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*uvMNAEtgAdfbQHWmi6VkWg.png"
class="graf-image" data-image-id="1*uvMNAEtgAdfbQHWmi6VkWg.png"
data-width="1744" data-height="984" />
</figure>

4\. Change **Port 22** → Custom Port

Always **pick a port above 1024** (e.g., `2200`{.markup--code
.markup--p-code}, `2222`{.markup--code .markup--p-code},
`2525`{.markup--code .markup--p-code}) to avoid conflicts with system
services.

-   Locate this line:

``` {#d331 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#Port 22
```

-   Remove the `#`{.markup--code .markup--li-code} and change
    `22`{.markup--code .markup--li-code} to a custom port (e.g.,
    `2200`{.markup--code .markup--li-code} or any unused port above
    `1024`{.markup--code .markup--li-code}).

``` {#32ef .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
plaintext Port 2200
```

<figure id="0741" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*gv7PxiQv6VNwt9oVbseJUQ.png"
class="graf-image" data-image-id="1*gv7PxiQv6VNwt9oVbseJUQ.png"
data-width="1740" data-height="931" />
</figure>

### Conclusion

This hands-on activity demonstrates the importance of combining **OSINT
and SIEM tools** to detect cyber threats. By using **Shodan** for
reconnaissance and **Splunk** for log analysis, we can identify
potential security risks and implement measures to mitigate them.

Would you like to see more in-depth **Splunk queries** or additional
**OSINT tools**? Let me know in the comments! 🚀




By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [February 3, 2025](https://medium.com/p/13907a7e2765).

[Canonical
link](https://medium.com/@kiplagatkelvin034/threat-hunting-with-osint-and-splunk-a-hands-on-guide-13907a7e2765){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
