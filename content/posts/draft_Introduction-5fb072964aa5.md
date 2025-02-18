<div>

# Introduction {#introduction .p-name}

</div>

::: {.section .p-summary field="subtitle"}
Cyber threats continue to evolve, and organizations must stay ahead of
attackers by using proactive security measures. One key approach is...
:::

::: {.section .e-content field="body"}
::: {#b030 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
###   {#5f05 .graf .graf--h3 .graf--empty .graf--leading .graf--title name="5f05"}

###   {#1b29 .graf .graf--h3 .graf--empty .graf-after--h3 name="1b29"}

### Introduction {#1c66 .graf .graf--h3 .graf-after--h3 name="1c66"}

Cyber threats continue to evolve, and organizations must stay ahead of
attackers by using proactive security measures. One key approach is
**threat hunting**, which involves actively searching for threats within
a network rather than waiting for alerts.

In this hands-on activity, we will use **Open-Source Intelligence
(OSINT)** to gather threat data and then analyze security logs using
**Splunk** to detect suspicious activity. This guide will walk you
through the process using **Kali Linux**, demonstrating how to:

-   [Perform **OSINT reconnaissance** using **Shodan**.]{#dc71}
-   [\
    ]{#6c68}
-   [Use **Splunk** to ingest and analyze security logs.]{#26c8}
-   [\
    ]{#2896}
-   [Identify **suspicious activity** based on OSINT findings.]{#0814}
-   [\
    ]{#4a0c}
-   [Propose **mitigation strategies** to strengthen cybersecurity
    defenses.]{#d2b7}
-   [\
    ]{#53cc}

Let's get started!

### Variables Needed {#317d .graf .graf--h3 .graf-after--p name="317d"}

Before beginning, we must define key **variables** for our analysis:

-   [**Target IP or Device Type** --- Identify a specific IP address,
    device type, or service to investigate.]{#b12a}
-   [\
    ]{#2d59}
-   [**Threat Intelligence Indicators** --- Suspicious IPs, default
    credentials, exposed services, or vulnerable systems.]{#4db9}
-   [\
    ]{#b816}
-   [**Security Logs** --- Firewall logs, authentication logs, or
    network traffic logs to analyze.]{#0a7d}
-   [\
    ]{#77d5}
-   [**Splunk Queries** --- Search patterns to detect malicious
    activity.]{#fbf9}
-   [\
    ]{#cfe4}

### Tools Used {#3a61 .graf .graf--h3 .graf-after--li name="3a61"}

To complete this activity, we will use the following tools:

### 1. OSINT Tool: Shodan {#9bad .graf .graf--h3 .graf-after--p name="9bad"}

-   [**Shodan**
    ([https://www.shodan.io](https://www.shodan.io){.markup--anchor
    .markup--li-anchor data-href="https://www.shodan.io" rel="noopener"
    target="_blank"}) is a search engine that scans and indexes
    Internet-connected devices.]{#dd78}
-   [\
    ]{#25c7}
-   [Helps identify **exposed services, open ports, and
    vulnerabilities**.]{#17ee}
-   [\
    ]{#f09f}

### 2. Security Information and Event Management (SIEM) Tool: Splunk {#09ac .graf .graf--h3 .graf-after--li name="09ac"}

-   [**Splunk** (https://www.splunk.com) is a powerful **SIEM** that
    collects, analyzes, and visualizes security logs.]{#c905}
-   [\
    ]{#0260}
-   [We will use **Splunk Free** or **Splunk Cloud** for this
    exercise.]{#395d}
-   [\
    ]{#b486}

### 3. Kali Linux {#91ac .graf .graf--h3 .graf-after--li name="91ac"}

-   [Kali Linux includes essential tools for **OSINT, penetration
    testing, and log analysis**.]{#a790}
-   [\
    ]{#478a}
-   [We will install and run **Shodan CLI** on Kali.]{#1937}
-   [\
    ]{#3497}

### Step 1: Gather Threat Intelligence Using Shodan {#4374 .graf .graf--h3 .graf-after--li name="4374"}

### 1.1 Install and Configure Shodan CLI on Kali Linux {#b9d4 .graf .graf--h3 .graf-after--h3 name="b9d4"}

1.  [Open **Kali Linux Terminal**.]{#6a01}
2.  [\
    ]{#46fb}
3.  [Install Shodan CLI:]{#4a14}

``` {#2e2c .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`pip install shodan`{.markup--code .markup--li-code}]{#7879}

``` {#15a6 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#f111 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#6eb1}
2.  [Initialize Shodan with your API key (sign up at
    [Shodan.io](https://www.shodan.io){.markup--anchor
    .markup--li-anchor data-href="https://www.shodan.io" rel="noopener"
    target="_blank"} and get your API key):]{#4a03}

``` {#50bb .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`shodan init YOUR_API_KEY`{.markup--code .markup--li-code}]{#528a}

``` {#9050 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#8b2a .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#93f6}

### 1.2 Perform an OSINT Search {#4973 .graf .graf--h3 .graf-after--li name="4973"}

Run Shodan searches to identify exposed and vulnerable systems:

-   [**Search for SSH services on port 22**:]{#e90b}

``` {#d956 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`shodan search "port:22"`{.markup--code .markup--li-code}]{#0443}

``` {#a9f5 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#f4b9 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#9ca6}
-   [**Find devices with default passwords**:]{#0e7a}

``` {#f032 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`shodan search "default password"`{.markup--code
    .markup--li-code}]{#9dd6}

``` {#57be .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#4b87 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#7cb6}
-   [**Identify vulnerable Apache servers**:]{#ae9a}

``` {#724b .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`shodan search "Apache vuln:CVE-2023-25690"`{.markup--code
    .markup--li-code}]{#f0f1}

``` {#aec1 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#f80e .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#9226}

### 1.3 Document the Findings {#2e12 .graf .graf--h3 .graf-after--li name="2e12"}

-   [Take screenshots of **Shodan search results**.]{#6413}
-   [\
    ]{#276b}
-   [Summarize:]{#89de}
-   [\
    ]{#b5a4}
-   [**Type of exposed devices**]{#8c04}
-   [\
    ]{#0223}
-   [**Potential risks**]{#5ec8}
-   [\
    ]{#6793}
-   [**How attackers could exploit these systems**]{#c8d1}
-   [\
    ]{#4c9a}
-   [\
    ]{#1c38}

### Step 2: Collect and Analyze Data Using Splunk {#3794 .graf .graf--h3 .graf-after--li name="3794"}

### 2.1 Install or Access Splunk {#84be .graf .graf--h3 .graf-after--h3 name="84be"}

#### Option 1: Install Splunk Free on Kali Linux {#119f .graf .graf--h4 .graf-after--h3 name="119f"}

1.  [Download Splunk from [Splunk
    Download](https://www.splunk.com/en_us/download/splunk-enterprise.html){.markup--anchor
    .markup--li-anchor
    data-href="https://www.splunk.com/en_us/download/splunk-enterprise.html"
    rel="noopener" target="_blank"}.]{#0d90}
2.  [\
    ]{#a773}
3.  [Install it using:]{#47b2}

``` {#3a55 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`dpkg -i splunk-*.deb`{.markup--code .markup--li-code}]{#4716}

``` {#0325 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#5251 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#2034}
2.  [Start Splunk and set an admin password:]{#160f}

``` {#1fdc .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`/opt/splunk/bin/splunk start`{.markup--code
    .markup--li-code}]{#ac49}

``` {#1e76 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#0be7 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#2699}
2.  [Open Splunk's web interface:]{#1b67}

``` {#2c22 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [[`http://127.0.0.1:8000`{.markup--code
    .markup--li-code}](http://127.0.0.1:8000){.markup--anchor
    .markup--li-anchor data-href="http://127.0.0.1:8000" rel="noopener"
    target="_blank"}]{#dd2b}

``` {#e780 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#9856 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#e032}

#### Option 2: Use Splunk Cloud {#2e11 .graf .graf--h4 .graf-after--li name="2e11"}

-   [Register for a **Splunk Cloud** free trial at Splunk Cloud.]{#149c}
-   [\
    ]{#b09a}
-   [Upload security logs for analysis.]{#85b1}
-   [\
    ]{#d2ef}

### 2.2 Ingest Security Logs into Splunk {#b514 .graf .graf--h3 .graf-after--li name="b514"}

-   [Collect logs from **firewall, authentication, or network
    traffic**:]{#4858}

``` {#b5e6 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo tail -f /var/log/auth.log sudo cat /var/log/syslog sudo tcpdump -i eth0 -w capture.pcap`{.markup--code
    .markup--li-code}]{#53d8}

``` {#77a6 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#4c7b .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#2a6e}
-   [Upload these logs into **Splunk**.]{#0641}
-   [\
    ]{#fb43}

### 2.3 Hunt for Suspicious Activity {#40f5 .graf .graf--h3 .graf-after--li name="40f5"}

Use Splunk to analyze security logs and detect threats:

-   [**Find failed SSH login attempts**:]{#7f89}

``` {#0c8e .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`index=auth | search "Failed password"`{.markup--code
    .markup--li-code}]{#c1fa}

``` {#e136 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#5061 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#a689}
-   [**Detect access to known malicious IPs** (replace with OSINT
    findings):]{#0db2}

``` {#3bca .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`index=firewall | search src_ip=192.168.1.100`{.markup--code
    .markup--li-code}]{#5ec7}

``` {#d1bb .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#d971 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#5f96}
-   [**Look for privilege escalation attempts**:]{#9955}

``` {#f790 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`index=linux_logs | search "sudo su" OR "sudo -i"`{.markup--code
    .markup--li-code}]{#fce2}

``` {#4607 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#3cf5 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [\
    ]{#5d66}

### 2.4 Document the Findings {#d5d4 .graf .graf--h3 .graf-after--li name="d5d4"}

-   [Take screenshots of **Splunk search results**.]{#a011}
-   [\
    ]{#3d25}
-   [Summarize **suspicious activities** found.]{#6eb4}
-   [\
    ]{#bdee}

### Step 3: Mitigation and Remediation {#6a77 .graf .graf--h3 .graf-after--li name="6a77"}

### 3.1 Mitigation Steps {#377d .graf .graf--h3 .graf-after--h3 name="377d"}

1.  [**Block malicious IPs** using iptables:]{#7bda}

``` {#953c .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo iptables -A INPUT -s <malicious_ip> -j DROP`{.markup--code
    .markup--li-code}]{#8d09}

``` {#27bf .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#aa95 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#6494}
2.  [**Update security patches**:]{#97f0}

``` {#e4c3 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo apt update && sudo apt upgrade -y`{.markup--code
    .markup--li-code}]{#dfdc}

``` {#e594 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#9d81 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#b95c}
2.  [**Harden SSH security**:]{#147b}

``` {#f4fe .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo nano /etc/ssh/sshd_config`{.markup--code
    .markup--li-code}]{#2c0c}

``` {#c7d5 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#67c1 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#e13d}

-   [Change **Port 22** → Custom Port]{#d5bd}
-   [\
    ]{#9829}
-   [Disable **root login** (`PermitRootLogin no`{.markup--code
    .markup--li-code}).]{#fef4}
-   [\
    ]{#70be}

1.  [\
    ]{#f5e3}
2.  [**Enable firewall rules**:]{#3025}

``` {#6a7e .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo ufw deny from <malicious_ip> sudo ufw enable`{.markup--code
    .markup--li-code}]{#35b8}

``` {#8648 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#1def .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#7871}

### Conclusion {#a787 .graf .graf--h3 .graf-after--li name="a787"}

This hands-on activity demonstrates the importance of combining **OSINT
and SIEM tools** to detect cyber threats. By using **Shodan** for
reconnaissance and **Splunk** for log analysis, we can identify
potential security risks and implement measures to mitigate them.

Would you like to see more in-depth **Splunk queries** or additional
**OSINT tools**? Let me know in the comments! 🚀
:::
:::
:::
:::

[View original.](https://medium.com/p/5fb072964aa5)

Exported from [Medium](https://medium.com) on February 13, 2025.
