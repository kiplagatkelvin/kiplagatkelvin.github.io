---
title: "Leveraging Nmap for Network Discovery and Vulnerability Assessment: A Comprehensive Lab Walkthrough"
author: "Kiplagatkelvin"
date: "2025-02-20"
tags: ["Nmap", "Network Discovery", "Vulnerability Assessment", "Cybersecurity", "Penetration Testing"]
categories: ["Cybersecurity", "Network Security", "Ethical Hacking"]
summary: "This lab walkthrough demonstrates how to use Nmap for network discovery, OS fingerprinting, and vulnerability assessment, essential for both red and blue teams."
cover:
  image: "https://cdn-images-1.medium.com/max/800/1*Ip4uwH0bAYjkDTPQEIDr6w.png" # Replace with an optimized local image if necessary
  alt: "Nmap scanning network for vulnerabilities"
  caption: "Using Nmap for network discovery and security assessment"
draft: false
---


# Leveraging Nmap for Network Discovery and Vulnerability Assessment: A Comprehensive Lab Walkthrough 


### Leveraging Nmap for Network Discovery and Vulnerability Assessment: A Comprehensive Lab Walkthrough 

<figure id="12a0" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*Ip4uwH0bAYjkDTPQEIDr6w.png"
class="graf-image" data-image-id="1*Ip4uwH0bAYjkDTPQEIDr6w.png"
data-width="1066" data-height="610" data-is-featured="true" />
</figure>

**Introduction**

Network security is an ongoing challenge, with new vulnerabilities and
attack vectors emerging constantly. Nmap, a network discovery and
auditing tool, is one of the most effective tools for cybersecurity
practitioners to probe network assets. This lab walkthrough will detail
how to use Nmap for discovering network hosts, fingerprinting operating
systems, and detecting exposed services --- skills essential for both
red and blue teams.

### Background / Scenario 

A Wireshark capture shows unusual activity on a machine on the 10.6.6.0
DMZ network. You've been asked to do some active recon on the machine to
determine what services it may be offering and if there are vulnerable
applications that could present security issues. The IP address of the
suspicious computer is 10.6.6.23. You have access to a Kali Linux system
on the 10.6.6.0 network.

#### scope 

In this lab setup, we'll be working within a virtualized cisco
environment using Kali Linux. Our target network is a typical corporate
configuration with a range of IP addresses from 10.6.6.0/24. This
walkthrough will explore multiple scan types, including discovery,
service identification, and NSE scripts for SMB enumeration.

<figure id="58cf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*VSEwSaW4sqCxFYm3hkoPVA.png"
class="graf-image" data-image-id="1*VSEwSaW4sqCxFYm3hkoPVA.png"
data-width="731" data-height="420" />
</figure>

**Environment Setup and Command Basics**

To begin, ensure your kali environment is ready for the scan. After
logging into your Kali instance, verify your network configuration:

This ensures your network interface is up, and you're connected to the
10.6.6.0/24 subnet. Next, check that Nmap is installed and up-to-date:

*nmap -V*

1.  Log into the Kali system with the username kali and the password
    kali*.* You are presented with the Kali desktop.
2.  Open a terminal window.
3.  Verify that Kali has an interface in the 10.6.6.0/24 network using
    the ifconfig command.
4.  Use the *nmap -V* command to verify that Nmap is installed and to
    display the Nmap version. The output will be similar to what is
    shown below.

<figure id="e909" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*l1mXnraHQVmmpdUCSWszmQ.png"
class="graf-image" data-image-id="1*l1mXnraHQVmmpdUCSWszmQ.png"
data-width="1672" data-height="124" />
</figure>

**Exploring Nmap Options**

Running *nmap -h* provides a comprehensive list of options and flags.
For quick reference, here's a summary of the core options we'll use in
this lab:

<figure id="6ccd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*H0y9EypHUeh2mrwhfFv9BA.png"
class="graf-image" data-image-id="1*H0y9EypHUeh2mrwhfFv9BA.png"
data-width="1270" data-height="322" />
</figure>

### **Part 1: Host Discovery and Initial Scans** 

### **Discovery Scan** 

To begin reconnaissance, let's discover active hosts within our network:

*nmap -sn 10.6.6.0/24*

<figure id="4c45" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*7qC8zCHCGFX3KaGsIQBivg.png"
class="graf-image" data-image-id="1*7qC8zCHCGFX3KaGsIQBivg.png"
data-width="1717" data-height="711" />
</figure>

The output from your `nmap -sn 10.6.6.0/24`{.markup--code
.markup--p-code} scan shows a ping sweep on the subnet
`10.6.6.0/24`{.markup--code .markup--p-code}, where Nmap performed a
scan to check for live hosts without scanning individual ports (since
`-sn`{.markup--code .markup--p-code} skips port scans). Here's a
breakdown of the results:

**Active Hosts**:Seven hosts are up, which includes:

-   `10.6.6.1`{.markup--code .markup--li-code} - This is likely the
    gateway or virtual switch/router, as it usually has
    the `.1`{.markup--code .markup--li-code} address in a
    subnet.
-   `10.6.6.11`{.markup--code .markup--li-code}
    (`webgoat.vm`{.markup--code .markup--li-code}) - A VM likely running
    the WebGoat application, a common testing tool for security
    training.
-   `10.6.6.12`{.markup--code .markup--li-code}
    (`juice-shop.vm`{.markup--code .markup--li-code}) - Probably running
    OWASP Juice Shop, an application used for practicing security
    attacks.
-   `10.6.6.13`{.markup--code .markup--li-code}
    (`dvwa.vm`{.markup--code .markup--li-code}) - Potentially hosting
    DVWA (Damn Vulnerable Web Application), another security training
    tool.
-   `10.6.6.14`{.markup--code .markup--li-code}
    (`mutillidae.vm`{.markup--code .markup--li-code}) - Likely running
    Mutillidae, another intentionally vulnerable application.]{#207c}
-   `10.6.6.23`{.markup--code .markup--li-code}
    (`gravemind.vm`{.markup--code .markup--li-code}) - Could be hosting
    another specific application, but the purpose isn't clear from this
    name alone.
-   `10.6.6.100`{.markup--code .markup--li-code} - No hostname
    information, possibly another device or VM on the network.

This command uses a "ping scan" to identify active hosts by sending ICMP
echo requests. Active IP addresses will respond, giving us a list of
targets. For this lab, assume that IP 10.6.6.23 has been identified as a
potentially vulnerable host.

#### **Default TCP Scan** 

Now that we've identified a target, let's investigate open ports using a
default TCP scan:

*nmap 10.6.6.23*

<figure id="f969" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*WUjWELCuLc0C0LIhxGaFNA.png"
class="graf-image" data-image-id="1*WUjWELCuLc0C0LIhxGaFNA.png"
data-width="1717" data-height="412" />
</figure>

<figure id="33f4" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*rTYWDHTQszLkVqzlcmotWA.png"
class="graf-image" data-image-id="1*rTYWDHTQszLkVqzlcmotWA.png"
data-width="1275" data-height="295" />
</figure>

Each of these open ports represents a potential access point for an
attacker, and understanding these services helps evaluate the security
posture of 10.6.6.23.

### **Part 2: Deepening Our Scan with OS and Version Detection** 

#### **Operating System Detection**

To better understand the host, we'll attempt to detect its operating
system:

*sudo nmap -O 10.6.6.23*

<figure id="63f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ouMn-CMzZfno8HUkdpyQKA.png"
class="graf-image" data-image-id="1*ouMn-CMzZfno8HUkdpyQKA.png"
data-width="1708" data-height="841" />
</figure>

This Nmap scan used the `-O`{.markup--code .markup--p-code} flag to
perform OS detection on `10.6.6.23`{.markup--code .markup--p-code}
(gravemind.vm), which successfully identified the host as running a
Linux operating system, specifically versions between **4.15** and
**5.8**. Here\'s a breakdown of the results:

-   **Open Ports**: Six TCP ports are open, supporting services like
    FTP, SSH, DNS, HTTP, and SMB (NetBIOS and Microsoft-DS).
-   **MAC Address**: Shows `02:42:0A:06:06:17`{.markup--code
    .markup--li-code}, which could be helpful for device identification,
    though it appears not associated with a known vendor.
-   **Device Type**: Classified as "general purpose," suggesting this
    is likely a standard server rather than a specialized device like a
    router or IoT equipment.
-   **OS Detection**: Nmap OS detection uses various fingerprints to
    estimate the operating system. Here, it accurately recognizes a
    Linux OS kernel within the 4.x to 5.x range.
-   **Network Distance**: Reported as "1 hop," indicating that the scan
    is likely being run within the same local network or subnet, as the
    device is just one step away in network terms.

These findings are useful for understanding the device type, its likely
OS environment, and potential vulnerabilities specific to Linux kernel
versions in the 4.x and 5.x series. If you'd like to dive deeper, we
could use further Nmap scripts or other tools to enumerate services in
detail or check for specific vulnerabilities on each open port.

#### **Service Version Detection** 

For a more granular look at the host's services, we'll probe specific
ports with version detection:

*nmap -v -p21 -sV -T4 10.6.6.23*

<figure id="7329" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*1Gp05Hw9WnbvuJGUSToe1Q.png"
class="graf-image" data-image-id="1*1Gp05Hw9WnbvuJGUSToe1Q.png"
data-width="1708" data-height="631" />
</figure>

In this Nmap scan, the command used `-v -p21 -sV -T4`{.markup--code
.markup--p-code} to gather detailed information on port **21** (FTP) for
the target `10.6.6.23`{.markup--code .markup--p-code}. Here's a
breakdown of the results:

-   **Verbose Mode (-v)**: Provides detailed output about each scan
    phase, showing steps as they happen.
-   **Specified Port (-p21)**: Limits the scan to only **port 21**
    (FTP) to focus on this service alone.
-   **Service Version Detection (-sV)**: Identifies the service version
    running on an open port. Here, it detects **vsftpd 3.0.3**, a common
    FTP server.
-   **Aggressive Timing Template (-T4)**: Speeds up the scan without
    compromising reliability, useful for a faster scan in non-intrusive
    environments.

**Scan Findings**:

-   **Port Status**: Port 21 is open, running FTP.
-   **Service and Version**: The FTP service is identified as **vsftpd
    3.0.3**.
-   **OS Information**: The service appears to run on a **Unix**-based
    operating system, inferred from the service response.

This level of detail can help determine if **vsftpd 3.0.3** has known
vulnerabilities or misconfigurations that could be exploited. Further
steps could include testing for default FTP credentials or checking if
anonymous login is allowed.

#### **Aggressive Scan with -A Option**

To combine these scans and maximize information retrieval, use an
aggressive scan:

*nmap -p21 -sV -A 10.6.6.23*

<figure id="f5cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*YgGB9SjEkw8DbPF2vKxwsQ.png"
class="graf-image" data-image-id="1*YgGB9SjEkw8DbPF2vKxwsQ.png"
data-width="1723" data-height="835" />
</figure>

Your Nmap scan indicates that the target host
(`gravemind.vm`{.markup--code .markup--p-code} at
`10.6.6.23`{.markup--code .markup--p-code}) is running an FTP server
(vsftpd 3.0.3) and allows anonymous access. Here's a brief breakdown of
the findings:

**Scan Summary of the above**

-   Host Status: Up (with low latency)
-   Open Port:
-   21/tcp (FTP):
-   Service: vsftpd 3.0.3
-   Anonymous Access: Allowed (FTP code 230)

Files Accessible via Anonymous FTP:

1.  `file1.txt`{.markup--code .markup--li-code} (16 bytes)
2.  `file2.txt`{.markup--code .markup--li-code} (16 bytes)
3.  `file3.txt`{.markup--code .markup--li-code} (29 bytes)
4.  `supersecretfile.txt`{.markup--code .markup--li-code} (26
    bytes)

#### FTP Server Info: 

-   Connected to `10.6.6.1`{.markup--code .markup--li-code}
-   Logged in as `ftp`{.markup--code .markup--li-code}
-   Transfer type: ASCII
-   Control and data connections are unencrypted (plain text)
-   Session timeout: 300 seconds

#### Potential Risks:

-   Anonymous FTP Access: Allows unauthorized users to access
    potentially sensitive files.
-   Plain Text Connections: No encryption, exposing data to
    interception.

#### Recommendations: 

-   Disable Anonymous FTP Access to prevent unauthorized file
    access.
-   Implement Secure FTP (SFTP/FTPS) to encrypt connections.
-   Regularly Review Files on the FTP server for sensitive
    information.

### **Part 3: Running NSE Scripts for SMB Enumeration** 

The Server Message Block (SMB) protocol is a network file sharing
protocol supported on Windows computers and by SAMBA on Linux. SMB
enables applications to read and write files or request services over a
network. Open public shares or shared devices such as print servers on a
network, can be accessed through SMB.

The earlier scan of open ports on the target computer indicates that the
SMB ports 139 and 445 are open. Find more information on these ports
using the -A and -p command options. The -A option executes several
functions including running the default scripts. Specify more than one
port to scan by listing them separately with a comma between them

*nmap -A -p139,445 10.6.6.23*

<figure id="493b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*oNANNfSjgoLqw-D8phvL0Q.png"
class="graf-image" data-image-id="1*oNANNfSjgoLqw-D8phvL0Q.png"
data-width="1702" data-height="837" />
</figure>

#### Results Summary 

-   **Host Status**:

The host (10.6.6.23) is up, with a low latency of 0.00045 seconds,
indicating it's reachable and responsive.

**Open Ports**:

**Port 139/tcp**:

-   **State**: Open
-   **Service**: NetBIOS Session Service (part of SMB)
-   **Version**: Samba smbd 3.X --- 4.X, indicating it supports SMB
    versions 3.x to 4.x.

**Port 445/tcp**:

-   **State**: Open
-   **Service**: NetBIOS Session Service
-   **Version**: Samba smbd 4.9.5-Debian, showing a specific version of
    the Samba service used to handle SMB requests.

#### Additional Information 

**Service Info**:

Host: GRAVEMIND

Workgroup: WORKGROUP

**Security Mode**:

-   The `smb-security-mode`{.markup--code .markup--li-code} section
    shows:

**Account Used**: `<blank>`{.markup--code .markup--p-code}, suggesting
no specific account was used for the scan.

**Authentication Level**: `user`{.markup--code .markup--p-code}, which
indicates that user-level access is required.

**Challenge Response**: Supported, meaning the service can use
challenge-response authentication.

**Message Signing**: Disabled, which is considered a security risk (as
it can expose SMB traffic to man-in-the-middle attacks).

**SMB2 Security Mode**:

Message signing is enabled but not required, which can also pose a
security risk.

**OS Discovery**:

-   Detected Operating System: Windows 6.1 (Samba 4.9.5-Debian),
    suggesting the system is running a version of Samba emulating a
    Windows environment.
-   Computer Name: GRAVEMIND
-   Domain Name: `<blank>`{.markup--code .markup--li-code}, indicating
    that the system is not part of a domain.

**Time Information**:

The SMB service provides the current date and time as well as system
time synchronization information.

#### Conclusion 

The scan reveals that the target machine is running Samba, likely
functioning as a file and print server. The presence of open SMB ports
with some security features disabled poses potential security risks,
making it essential to implement proper configurations to secure the
service

#### **Enumerating SMB Users**

Nmap contains the powerful Nmap Scripting Engine (NSE), which enables
the programming of various Nmap options and conditional actions to be
taken as a result of the responses. NSE has built-in scripts that
enumerate users, groups, and network shares. One of the more commonly
used scripts for SMB discovery is the smb-enum-users.nse script. Use the
Nmap NSE script with the command:

*nmap \--script smb-enum-users.nse -p139,445 10.6.6.23*

<figure id="91f5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*-9SB6-0fPb6RHWJtTR_TVg.png"
class="graf-image" data-image-id="1*-9SB6-0fPb6RHWJtTR_TVg.png"
data-width="1714" data-height="817" />
</figure>

**Results Summary**

-   **Host Status**:
-   The host (10.6.6.23) is up and responsive, with a latency of 0.0010
    seconds.
-   **Open Ports**:
-   **Port 139/tcp**: Open and associated with the NetBIOS Session
    Service.
-   **Port 445/tcp**: Open and associated with Microsoft Directory
    Services (another SMB-related service).

#### **User Enumeration Results** 

The script successfully enumerated user accounts on the SMB service.
Here are the details:

1.  **User: GRAVEMIND\\arbiter**

-   **RID**: 1001 (Relative Identifier, a unique number assigned to the
    user in the context of the domain)
-   **Flags**
-   **Account disabled**: Indicates that this user account is currently
    disabled.
-   **Password not required**: This suggests that a password is not
    required to log in to this account.
-   **Normal user account**: Indicates this account has standard user
    privileges, not elevated privileges.

1.  **User: GRAVEMIND\\masterchief**

-   **RID**: 1000.
-   **Flags**:
-   **Account disabled**: This user account is also disabled.
-   **Password not required**: Similarly, a password is not required to
    log in to this account.
-   **Normal user account**: This is also a standard user
    account.

**Conclusion**

The enumeration reveals two user accounts on the target machine
(GRAVEMIND), both of which are disabled and configured to not require
passwords. This setup may indicate poor security practices, as disabled
accounts still being enumerated can present risks if an attacker can
enable them or exploit weaknesses in the SMB service.

Overall, the results highlight potential vulnerabilities in the
configuration of user accounts, making it crucial for system
administrators to regularly review and tighten security settings on SMB
services.

The output shows any usernames found on the SMB server, helping identify
potentially exposed accounts. Access to usernames can be useful for
brute force attacks, making it essential to secure user lists.

#### **Enumerating Shared Directories** 

To see if the host shares directories, A serious security concern is the
existence of publicly shared directories (folders). You can enumerate
the network shares using another NSE script, smb-enum-shares.nse. To
discover shared directories on the target computer. Use the Nmap share
enumeration script with the command:

*nmap --- script smb-enum-shares.nse -p445 10.6.6.23*

<figure id="bc6b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*u6BTmBxH02Va_7o1TXx_5w.png"
class="graf-image" data-image-id="1*u6BTmBxH02Va_7o1TXx_5w.png"
data-width="1720" data-height="768" />
</figure>

#### **Results Summary** 

-   **Host Status**:
-   The host (10.6.6.23) is up and responsive, with a latency of
    0.00087 seconds.
-   **Open Port**:
-   **Port 445/tcp**: Open and associated with Microsoft Directory
    Services (again, indicating an SMB service).

**Share Enumeration Results**

The script successfully identified three shared directories on the SMB
service:

1.  **Share: \\\\10.6.6.23\\IPC\$**

-   **Type**: STYPE_IPC_HIDDEN (Inter-Process Communication, typically
    hidden from normal enumeration).
-   **Comment**: IPC Service (Samba 4.9.5-Debian).
-   **Users**: 1 (indicating at least one user is connected).
-   **Max Users**: \<unlimited\> (indicating no limit on user
    connections).
-   **Path**: C:\\tmp (the file system path for this share).
-   **Anonymous Access**: READ/WRITE (indicating that anyone can access
    this share with read and write permissions).

1.  **Share: \\\\10.6.6.23\\print\$**

-   **Type**: STYPE_DISKTREE (a standard disk share).
-   **Comment**: Printer Drivers.
-   **Users**: 0 (indicating no current users are connected).
-   **Max Users**: \<unlimited\>.
-   **Path**: C:\\var\\lib\\samba\\printers.
-   **Anonymous Access**: READ/WRITE (indicating open access for any
    user).

1.  **Share: \\\\10.6.6.23\\workfiles**

-   **Type**: STYPE_DISKTREE.
-   **Comment**: Confidential Workfiles.
-   **Users**: 0.
-   **Max Users**: \<unlimited\>.
-   **Path**: C:\\var\\spool\\samba.
-   **Anonymous Access**: READ/WRITE.

**Conclusion**

The scan revealed three shares on the target SMB service, with two of
them (print\$ and workfiles) indicating that they allow anonymous access
with read/write permissions. This is a significant security risk, as it
enables any user to access, modify, or delete files in these shares
without authentication.

1.  **IPC\$**: Typically used for administrative purposes, but allowing
    anonymous access can lead to unauthorized access.
2.  **print\$**: Sharing printer drivers could expose sensitive
    information if unauthorized users access it.
3.  **workfiles**: The comment suggests that it contains confidential
    data, which should not be openly accessible.

Overall, the findings suggest that the SMB service on the target system
has misconfigured shares, making it crucial to review and tighten access
controls to prevent unauthorized access and potential data breaches.
Proper configurations should restrict anonymous access and enforce
authentication for sensitive shares.

If public or anonymous shares are enabled, unauthorized users might gain
read/write access to sensitive files. This is a serious risk, especially
in internal networks, where such shares can provide a foothold for
lateral movement.

**Reflection on Findings**

This lab demonstrates how Nmap provides critical insights into network
vulnerabilities. Key takeaways include:

-   **Nmap's Power in Recon**: Both blue and red teams benefit from
    Nmap's ability to map out network assets and assess their
    exposure.
-   **Security Implications of Open Ports and Services**: Each exposed
    service, such as FTP or SMB, has associated risks. Controlling
    access to these ports and implementing access restrictions can
    mitigate these vulnerabilities.
-   **Ethical and Practical Considerations**: While Nmap is an
    invaluable tool, its use should be governed by ethics and proper
    authorization, especially given its ability to expose sensitive
    details about a network.

By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [October 31, 2024](https://medium.com/p/89c85d1d3d6f).

[Canonical
link](https://medium.com/@kiplagatkelvin034/leveraging-nmap-for-network-discovery-and-vulnerability-assessment-a-comprehensive-lab-walkthrough-89c85d1d3d6f){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
