---
title: "On-Path Attacks with Ettercap"
date: 2025-02-16
draft: false
tags: ["Cybersecurity", "MITM Attack", "Ettercap", "Network Security", "ARP Spoofing", "Penetration Testing"]
categories: ["Cybersecurity", "Network Security", "Penetration Testing"]
author: "Kelvin Kiplagat"
summary: "A hands-on guide to performing On-Path Attacks using Ettercap, covering ARP spoofing, traffic interception, and security implications."
canonical_url: "https://medium.com/@kiplagatkelvin034"
---

# Lab --- On-Path Attacks with Ettercap
### Lab --- On-Path Attacks with Ettercap 

<figure id="6d99" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*H4idexQNDHxPC2x0cGoRpg.png"
class="graf-image" data-image-id="1*H4idexQNDHxPC2x0cGoRpg.png"
data-width="1210" data-height="625" />
</figure>

### Introduction

**What is an On-Path Attack?**

In the world of cybersecurity, on-path attacks --- also known as
Man-in-the-Middle (MITM) attacks --- are among the most powerful methods
for intercepting, modifying, or stealing data over a network. Through
these attacks, an adversary places themselves "between" two
communicating hosts, gaining the ability to capture information without
needing to directly compromise the devices themselves.

<figure id="e913" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*VDWKKYBfSTo8EHMsN26V1A.png"
class="graf-image" data-image-id="1*VDWKKYBfSTo8EHMsN26V1A.png"
data-width="1093" data-height="576" />
</figure>

**Why Ettercap?**

In this lab, we're using *Ettercap*, a well-known network security tool,
to perform an on-path attack within a controlled environment. This
process will help you understand how network traffic can be intercepted
and manipulated, and will highlight the importance of network security
measures, especially encryption.

**Lab Objectives**

This guide covers three key stages in the on-path attack:

1.  [Launching Ettercap and exploring its capabilities.]{#b20c}
2.  [Performing an on-path attack using ARP spoofing.]{#9c94}

3.Using Wireshark to monitor and analyze the ARP spoofing process.

### Topology {#3652 .graf .graf--h3 .graf-after--p name="3652"}

<figure id="45ee" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*98LyAjwe6qwyQTQ394uwJA.jpeg"
class="graf-image" data-image-id="1*98LyAjwe6qwyQTQ394uwJA.jpeg"
data-width="720" data-height="371" />
</figure>

Attached is the topology I will be using for illustration.

### Part 1: Launch Ettercap and Explore Its Capabilities {#a317 .graf .graf--h3 .graf-after--p name="a317"}

In this attack, you will use ARP spoofing to redirect traffic on the
local virtual network to your Kali Linux system at 10.6.6.1. ARP
spoofing is often used to impersonate the default gateway router to
capture all traffic entering or leaving the local IP network. Because
your lab environment uses an internal virtual network, instead of
spoofing the default gateway, you will use ARP spoofing to redirect
traffic that is destined for a local server with the address 10.6.6.13.

1.  [Load Kali Linux using the username kali and the password kali. Open
    a terminal session from the menu bar at the top of the
    screen.]{#527f}
2.  [The target host in this lab is the Linux device at 10.6.6.23. To
    view the network from the target perspective, and initiate traffic
    between the target and the server, use *SSH* to log in to this host.
    The username is labuser and the password is *Cisco123.*]{#4cbd}

The user of the *10.6.6.23* host is communicating with the server at
*10.6.6.13*. The on-path attacker at *10.6.6.1* (your Kali VM) will
intercept and relay traffic between these hosts.

Note: The password will not display on the screen.

*(kali㉿Kali)-\[\~\]\
\# ssh -l labuser 10.6.6.23*

<figure id="402a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*vUAyKdoZYL013bxVlmjM1g.png"
class="graf-image" data-image-id="1*vUAyKdoZYL013bxVlmjM1g.png"
data-width="643" data-height="508" />
</figure>

3\. Because you are creating an on-path attack that uses ARP spoofing,
you will be monitoring the ARP mappings on the victim host. The attack
will cause changes to those mappings.

Use the command *ip neighbor* to view the current ARP cache on the
target computer. Note: The hostname *gravemind* maybe different for your
Kali VM environment.

*labuser@gravemind:/\$ ip neighbor*

<figure id="8374" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*3UyThYuhpZVcsNZB4fqJCA.png"
class="graf-image" data-image-id="1*3UyThYuhpZVcsNZB4fqJCA.png"
data-width="621" data-height="241" />
</figure>

#### Step 2: Load Ettercap GUI interface to begin scanning. {#b626 .graf .graf--h4 .graf-after--figure name="b626"}

1.  [Open a new terminal session from the menu bar in Kali Linux. Do not
    close the SSH-terminal that is running the session with
    10.6.6.23.]{#631e}
2.  [Use the **ettercap -h** command to view the help file for the
    Ettercap application.]{#eeab}

*(kali㉿Kali)-\[\~\]\
\$ ettercap -h*

<figure id="39a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*WNJnVYuFbE2xJSLfrDTZSw.png"
class="graf-image" data-image-id="1*WNJnVYuFbE2xJSLfrDTZSw.png"
data-width="651" data-height="486" />
</figure>

3\. In this part, you will use a GUI interface to access Ettercap. Start
Ettercap GTK+ graphical user interface using the **ettercap -G**
command. Most Ettercap functions require root permissions, so use the
**sudo** command to obtain the required permissions.

*(kali㉿kali)-\[\~\]\
\# sudo ettercap -G*

<figure id="e020" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*PuJHhzRryEr0tDCiDxJ0bw.png"
class="graf-image" data-image-id="1*PuJHhzRryEr0tDCiDxJ0bw.png"
data-width="961" data-height="625" />
</figure>

1.  [The Ettercap GUI opens in a new window. You are sniffing traffic on
    an internal, virtual network. The default setup is to scan using
    interface eth0. Change the sniffing interface to **br-internal**,
    which is the interface that is configured on the 10.6.6.0/24 virtual
    network, by changing the value in the **Setup \> Primary**
    **Interface** dropdown.]{#1ee6}

<figure id="9847" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*PY8HkU6vru3pJg9LTmvjcQ.png"
class="graf-image" data-image-id="1*PY8HkU6vru3pJg9LTmvjcQ.png"
data-width="822" data-height="493" />
</figure>

2\. Click the **checkbox** icon at the top right of the Ettercap screen
to continue. A message appears at the bottom of the screen indicating
that Unified sniffing has started.

### Part 2: Perform the On-Path (MITM) Attack {#c545 .graf .graf--h3 .graf-after--p name="c545"}

### Step 1: Select the Target Devices. {#7cb4 .graf .graf--h3 .graf-after--h3 name="7cb4"}

1.  [In the Ettercap GUI window, open the Hosts List window by clicking
    the Ettercap menu (three dots icon). Select the Hosts entry and then
    Hosts List. Click the Scan for Hosts icon (magnifying glass) at top
    left in the menu bar. A list of the hosts that were discovered on
    the 10.6.6.0/24 network appears in the Host List window.]{#53dd}

<figure id="a504" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*vq3MrWTcy8wJpdxboLG76w.png"
class="graf-image" data-image-id="1*vq3MrWTcy8wJpdxboLG76w.png"
data-width="816" data-height="462" />
</figure>

***At least one of the MAC addresses should be familiar.***

1.  [Define the source and destination devices for the attack. To do so,
    click the IP address 10.6.6.23 in the window to highlight the target
    user host. Click the Add to Target 1 button at the bottom of the
    Host List window. This defines the user's host as Target 1.]{#122d}

<figure id="6fc5" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*H6UgH-EhtH8iayiXBPBdRw.png"
class="graf-image" data-image-id="1*H6UgH-EhtH8iayiXBPBdRw.png"
data-width="817" data-height="286" />
</figure>

2\. Click the IP address of the destination web server at 10.6.6.13 to
highlight the line. Click the Add to Target 2 button at the bottom of
the host window.

<figure id="b4bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*TDLWFTXZMrvTXDDQKbzdXA.png"
class="graf-image" data-image-id="1*TDLWFTXZMrvTXDDQKbzdXA.png"
data-width="820" data-height="319" />
</figure>

Any IP/MAC address specified as a Target 1 will have all its traffic
diverted through the attacking computer that is running Ettercap. In
this lab, the attacking computer is the Kali Linux machine at 10.6.6.1.
All other computers on the subnet, other than the targets, will
communicate normally.

1.  [Click the MITM icon on the menu bar (the first circular icon on top
    right). Select **ARP Poisoning**... from the dropdown menu. Verify
    that **Sniff remote connections** is selected. Click OK.]{#c54b}

<figure id="3161" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*kXg1c8iI6dkdNoxvNaLISQ.png"
class="graf-image" data-image-id="1*kXg1c8iI6dkdNoxvNaLISQ.png"
data-width="811" data-height="478" />
</figure>

Verify that **Sniff remote connections** is selected. Click OK.

<figure id="c240" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*l4cAJMJuTcpXD5Y9YyGsJQ.png"
class="graf-image" data-image-id="1*l4cAJMJuTcpXD5Y9YyGsJQ.png"
data-width="802" data-height="475" />
</figure>

2\. The MITM exploit is started. If sniffing does not start immediately,
click the Start option (play button) at left in the top menu.

n/b snifing has already started...

<figure id="c097" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*cZ1fpNvBXhGp7cxwtBXHOg.png"
class="graf-image" data-image-id="1*cZ1fpNvBXhGp7cxwtBXHOg.png"
data-width="823" data-height="208" />
</figure>

### Step 2: Perform the ARP spoofing attack. {#086d .graf .graf--h3 .graf-after--figure name="086d"}

1.  [Return to the terminal window that is running the SSH session with
    the target user host at 10.6.6.23. Repeat the ping to
    10.6.6.13]{#c800}

*labusergravemind:/\$ ping -c 5 10.6.6.13*

<figure id="b4af" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*N3h4MvYCVdAC4huwiA2gEw.png"
class="graf-image" data-image-id="1*N3h4MvYCVdAC4huwiA2gEw.png"
data-width="652" data-height="217" />
</figure>

2\. Use the ***ip neighbor*** command to view the ARP table on 10.6.6.23
again. Note the MAC address listed for 10.6.6.13.

***ip neighbor***

<figure id="d744" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*RVuuRkszuMepaiD9BUF_qw.png"
class="graf-image" data-image-id="1*RVuuRkszuMepaiD9BUF_qw.png"
data-width="757" data-height="85" />
</figure>

### Part 3: Use Wireshark to Observe the ARP Spoofing Attack {#0b24 .graf .graf--h3 .graf-after--figure name="0b24"}

### Step 1: Select the Target Devices and Perform the MITM attack using the CLI {#116c .graf .graf--h3 .graf-after--h3 name="116c"}

In this step, you will use the command line interface in Ettercap to
perform ARP spoofing and write a .pcap file that can be opened in
Wireshark. Refer to the help information for Ettercap to interpret the
options used in the commands.

1.  [Return to the terminal session that is connected via SSH to
    10.6.6.23. Ping the IP addresses 10.6.6.11 and 10.6.6.13. 10.6.6.11
    is another host on the LAN that we will verify is unaffected by the
    attack. Then, use the **ip neighbor** command to find the MAC
    addresses associated with the IP addresses of the two
    systems.]{#5702}

*labuser@gravemind:/\$ ping -c 5 10.6.6.11*

<figure id="540e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*kINL-aTQpna3QU0o9ow5Xg.png"
class="graf-image" data-image-id="1*kINL-aTQpna3QU0o9ow5Xg.png"
data-width="637" data-height="207" />
</figure>

*labuser@gravemind:/\$ ping -c 5 10.6.6.13*

<figure id="e7ba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ytG4l_9hs_gIkpR7O5SMtQ.png"
class="graf-image" data-image-id="1*ytG4l_9hs_gIkpR7O5SMtQ.png"
data-width="634" data-height="198" />
</figure>

*labuser@gravemind:/\$ ip neighbor*

<figure id="0211" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*stpxUTYrMJ51WCW7sCrv3g.png"
class="graf-image" data-image-id="1*stpxUTYrMJ51WCW7sCrv3g.png"
data-width="633" data-height="88" />
</figure>

**Note**: To find the MAC of 10.6.6.23, go to the SSH session terminal
and enter the **ip address** command. Determine the MAC address of the
interface that is addressed on the 10.6.6.0/24 network.

2\. In a terminal window, enter the command as follows to save the pcap
file in the current working directory:

***(kali@kali)-\[\~\]\$sudo ettercap -T -q -i br-internal \--write
mitm-saved.pcap \--mitm arp /10.6.6.23// /10.6.6.13//***

below is the output

<figure id="e4a5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*O_T7AlYmSnNjD7EGaTqQ_g.png"
class="graf-image" data-image-id="1*O_T7AlYmSnNjD7EGaTqQ_g.png"
data-width="660" data-height="441" />
</figure>

<figure id="ec10" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*MmeiUrO8kx41cR2JTRZ48g.png"
class="graf-image" data-image-id="1*MmeiUrO8kx41cR2JTRZ48g.png"
data-width="637" data-height="448" />
</figure>

### Explanation:

1.  [**`sudo`{.markup--code .markup--li-code}**:Executes the command
    with root privileges (required for Ettercap to function properly,
    especially when working with network interfaces).]{#1542}
2.  [**`ettercap`{.markup--code .markup--li-code}**:This is the name of
    the tool used for network sniffing and man-in-the-middle (MITM)
    attacks, including ARP poisoning.]{#65c4}
3.  [**`-T`{.markup--code .markup--li-code}**:Specifies the **Text
    mode**. This mode runs Ettercap in a terminal with text-based output
    instead of the graphical interface.]{#812e}
4.  [**`-q`{.markup--code .markup--li-code}**:Enables **Quiet mode**,
    meaning Ettercap will suppress unnecessary output, showing only
    essential information.]{#3e0f}
5.  [**`-i br-internal`{.markup--code .markup--li-code}**:Specifies the
    **network interface** to use for the attack. In this case,
    `br-internal`{.markup--code .markup--li-code} is likely a network
    bridge interface, which is common in virtualized environments or
    when using tools like Docker or VirtualBox. This is the interface
    through which the attack will operate.]{#21dc}
6.  [**`--write mitm-saved.pcap`{.markup--code .markup--li-code}**:Tells
    Ettercap to **save** the captured traffic into a file called
    `mitm-saved.pcap`{.markup--code .markup--li-code}. This is useful
    for later analysis of the network traffic that was
    intercepted.]{#f31b}
7.  [**`--mitm arp`{.markup--code .markup--li-code}**:This specifies the
    type of **man-in-the-middle attack** to use, which in this case is
    **ARP poisoning (ARP spoofing)**. It allows the attacker to
    intercept and possibly alter the communication between two devices
    by poisoning the ARP cache of both devices.]
8.  [**`/10.6.6.23//`{.markup--code .markup--li-code}** and
    **`/10.6.6.13//`{.markup--code .markup--li-code}**:These are the
    **target IP addresses** of the two devices involved in the ARP
    spoofing attack. The syntax `/IP_ADDRESS//`{.markup--code
    .markup--li-code} is used by Ettercap to specify the target
    IPs.]

-   [`10.6.6.23`{.markup--code .markup--li-code} is the victim device's
    IP (the one you want to intercept traffic from).]
-   [`10.6.6.13`{.markup--code .markup--li-code} is the device you want
    to manipulate or monitor (the target device).]

#### What this command does: {#395f .graf .graf--h4 .graf-after--li name="395f"}

-   [The command starts an **ARP poisoning attack** on the network
    interface `br-internal`{.markup--code .markup--li-code}, between the
    devices with IP addresses `10.6.6.23`{.markup--code
    .markup--li-code} and `10.6.6.13`{.markup--code
    .markup--li-code}.]
-   [It intercepts the communication between these two devices and saves
    the network traffic in a file called `mitm-saved.pcap`{.markup--code
    .markup--li-code}.]
-   [During the attack, Ettercap manipulates the ARP tables of both
    devices to route their traffic through the attacker's machine,
    enabling the attacker to inspect, manipulate, or inject packets into
    the communication stream.]

### Step 2: Open Wireshark to view the Saved PCAP file.

1.  [In the Kali terminal window, start Wireshark with the
    **mitm-saved.pcap** file that you created with Ettercap.]{#e06f}

***wireshark mitm-saved.pcap***

<figure id="75ef" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*wP9rpcmTfWVNrpt1PiHQnA.png"
class="graf-image" data-image-id="1*wP9rpcmTfWVNrpt1PiHQnA.png"
data-width="1912" data-height="825" />
</figure>

duplicate ip address have been detected

<figure id="6d25" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*JpRiFhPxRCDdYQ47qFur6g.png"
class="graf-image" data-image-id="1*JpRiFhPxRCDdYQ47qFur6g.png"
data-width="1918" data-height="475" />
</figure>

2\. The Ettercap attack computer first broadcasts ARP requests to obtain
the actual MAC addresses for the two target hosts, 10.6.6.23 and
10.6.6.11. The attacking machine then begins to send ARP responses to
both target hosts using its own MAC for both IP addresses. This causes
the two target hosts to address the Ethernet frames to the attacker's
computer, which enables it to collect data as an on-path attacker.

**Mitigating On-Path Attacks**

On-path attacks, where an attacker intercepts and manipulates
communication between two parties, can be mitigated through a
combination of technical and organizational measures:

Technical Measures:

**Encryption:**

End-to-End Encryption: Ensures that only the intended recipients can
decrypt the data, even if it's intercepted.

Transport Layer Security (TLS): Protects communication channels,
particularly for web traffic.

**Virtual Private Networks (VPNs):**

Create encrypted tunnels between devices, making it difficult for
attackers to intercept traffic.

**Network Segmentation:**

Dividing networks into smaller segments can limit the attack surface and
prevent lateral movement.

Intrusion Detection Systems (IDS) and Intrusion Prevention Systems
(IPS):

Monitor network traffic for malicious activity and can block suspicious
connections.

**Firewall Configuration:**

Configure firewalls to block unnecessary traffic and enforce strict
access controls.

**DNS Security:**

Use DNSSEC to validate the authenticity of DNS records and prevent DNS
poisoning attacks.

**Web Application Firewalls (WAFs):**

Protect web applications from attacks like cross-site scripting (XSS)
and SQL injection.

**Regular Security Audits and Vulnerability Scanning:**

Identify and address vulnerabilities that could be exploited by
attackers.

**Organizational Measures:**

Employee Training:

Educate employees about the risks of on-path attacks and how to
recognize and avoid them.

Teach them to be cautious of phishing attempts and to verify the
authenticity of websites and emails.

**Strong Password Policies:**

Enforce strong, unique passwords for all accounts to prevent
unauthorized access.

**Multi-Factor Authentication (MFA):**

Add an extra layer of security by requiring users to provide multiple
forms of verification.

Incident Response Plan:

Have a plan in place to respond to security incidents, including on-path
attacks.

**Stay Informed:**

Keep up-to-date with the latest security threats and vulnerabilities.

**Additional Considerations:**

Be Wary of Public Wi-Fi: Avoid using public Wi-Fi for sensitive
activities, as it's more susceptible to on-path attacks.

Verify Website Authenticity: Ensure you're accessing legitimate websites
by checking the URL and using HTTPS.

Use Security-Conscious Browsers: Consider using browsers with built-in
security features like ad-blockers and tracking protection.

Stay Updated: Keep your operating systems, applications, and security
software up-to-date with the latest patches.

By combining these technical and organizational measures, you can
significantly reduce the risk of successful on-path attacks and protect
your sensitive information.

### Conclusion

**In this lab, i have successfully demonstrated the potential impact of
on-path attacks using the Ettercap tool.** By manipulating the ARP
protocol, we were able to intercept and potentially modify network
traffic between two devices. This hands-on experience highlights the
importance of understanding network security principles and implementing
robust security measures to protect against such attacks.

**Key Takeaways:**

-   **ARP Poisoning:** A powerful technique that can be used to
    compromise network security.
-   **Ettercap:** A versatile tool for network analysis and security
    testing.
-   **Wireshark:** A valuable tool for analyzing network traffic and
    identifying security threats.

**Recommendations for Future Work:**

-   **Advanced Techniques:** Explore more advanced techniques, such as
    DNS spoofing and HTTP injection.
-   **Real-World Scenarios:** Analyze real-world attack scenarios and
    how they can be mitigated.
-   **Security Best Practices:** Implement best practices for network
    security, such as strong password policies, regular security audits,
    and up-to-date software.

By understanding the principles of on-path attacks and the tools used to
execute them, we can take proactive steps to enhance network security
and protect sensitive information.


By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [November 8, 2024](https://medium.com/p/dfc854138809).

[Canonical
link](https://medium.com/@kiplagatkelvin034/lab-on-path-attacks-with-ettercap-dfc854138809){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
