---
title: "Secure Your Kali Linux with UFW: Uncomplicated Firewall Setup"
date: 2024-09-26
draft: false
tags: ["Kali Linux", "Firewall", "UFW", "Linux Security", "Network Security", "Cybersecurity", "System Hardening", "Penetration Testing"]
categories: ["Cybersecurity", "Linux Security", "System Hardening", "Network Defense"]
author: "Kelvin Kiplagat"
summary: "A step-by-step guide to configuring UFW (Uncomplicated Firewall) on Kali Linux to enhance security and protect against unauthorized access."
---


# Secure Your Kali Linux with UFW: Uncomplicated Firewall Setup

### Secure Your Kali Linux with UFW: Uncomplicated Firewall Setup

<figure id="e7bc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*zP2yzRZmqi07lzIy32e9xQ.png"
class="graf-image" data-image-id="1*zP2yzRZmqi07lzIy32e9xQ.png"
data-width="854" data-height="285" data-is-featured="true" />
</figure>

1.  **Introduction**

In today's world, securing your system and network from unauthorized
access is critical, and firewalls play an essential role in that
defense. UFW (Uncomplicated Firewall) is a user-friendly tool designed
to manage firewall rules easily, especially for those who are not
familiar with more complex firewalls like `iptables`{.markup--code
.markup--p-code}. While Kali Linux is a powerful platform used primarily
by penetration testers and security professionals, it's equally
important to safeguard it with a proper firewall.

In this guide, I will take you step by step through configuring UFW on
Kali Linux. Although UFW might seem technical at first, by the end of
this tutorial, you'll see that it's actually a simple yet powerful tool
you can use to improve your network security.

#### 2. Installing UFW on Kali Linux 

Before diving into configuring UFW, we first need to ensure it is
installed on your Kali Linux system, as it doesn't come pre-installed.

Step 1: Update Your System\
Before installing UFW, it's always a good practice to ensure your system
is up to date:\
*sudo apt update /sudo apt upgrade:*\
expected output

<figure id="2df6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Y5Fcj_-W1QPwp2q0xMWu5g.png"
class="graf-image" data-image-id="1*Y5Fcj_-W1QPwp2q0xMWu5g.png"
data-width="1062" data-height="217" />
</figure>

Step 2: Install UFW\
To install UFW, run the following command in your terminal:\
*sudo apt install ufw:*

expected output

<figure id="ae66" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*0ff-hDZSkWQh4gXyMncZEw.png"
class="graf-image" data-image-id="1*0ff-hDZSkWQh4gXyMncZEw.png"
data-width="994" data-height="91" />
<figcaption>already the newest version</figcaption>
</figure>

Step 3: Verify UFW Installation\
Once UFW is installed, you can check its version to ensure everything is
set up correctly:\
*sudo ufw version:*

expected output

<figure id="3bd2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*i7H3F543XoxYYlLdo9MEMQ.png"
class="graf-image" data-image-id="1*i7H3F543XoxYYlLdo9MEMQ.png"
data-width="1074" data-height="72" />
</figure>

This will display the installed version of UFW and confirm that it's
ready to use.

Step 4: Check UFW Status\
After installation, UFW may not be enabled by default. You can check the
status with:\
*sudo ufw status:*

<figure id="ec93" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*GHLHB0Ry4gj0uQnpwdkzOA.png"
class="graf-image" data-image-id="1*GHLHB0Ry4gj0uQnpwdkzOA.png"
data-width="1054" data-height="274" />
</figure>

This will likely show if the firewall is *inactive* or *active*

#### 3. Basic UFW Configuration

Now that UFW is installed, it's time to configure it with some basic
rules. UFW's default settings can be restrictive, so we'll walk through
setting up essential rules to allow your system to function securely.

Step 1: Set Default Policies\
UFW allows you to set default policies for incoming and outgoing
traffic. By default, it will allow outgoing connections and deny
incoming ones, which is a secure starting point.

To set these default rules:\
*sudo ufw default deny incoming:*

<figure id="7f66" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*_zhwqBZjYWBfE_mW1kez8Q.png"
class="graf-image" data-image-id="1*_zhwqBZjYWBfE_mW1kez8Q.png"
data-width="1059" data-height="79" />
<figcaption>expected output</figcaption>
</figure>

Deny incoming: Blocks all inbound traffic unless specified by additional
rules.

*sudo ufw default allow outgoing:*

<figure id="8cbd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ukWpDJXGQC4mlsCJALOYKQ.png"
class="graf-image" data-image-id="1*ukWpDJXGQC4mlsCJALOYKQ.png"
data-width="1062" data-height="66" />
</figure>

-   Allow outgoing: Permits all outbound traffic so your system can
    connect to external servers.

Step 2: Allow SSH Connections\
If you are using SSH to remotely connect to your Kali Linux system, it's
important to enable it, especially if you've just set UFW to block all
incoming traffic. To allow SSH (port 22):\
*sudo ufw allow ssh:*

<figure id="216a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*LexVGVItRnc6vc1FceiegQ.png"
class="graf-image" data-image-id="1*LexVGVItRnc6vc1FceiegQ.png"
data-width="1056" data-height="91" />
</figure>

you can see that SSH is allowed:

<figure id="7d4c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*0a7NNPpv-xS2AcGjE5FMvg.png"
class="graf-image" data-image-id="1*0a7NNPpv-xS2AcGjE5FMvg.png"
data-width="1057" data-height="291" />
</figure>

This ensures that even with a strict firewall, you can still remotely
access the machine via SSH.

Step 3: Enable UFW\
Now that the basic rules are set, it's time to enable UFW:\
*sudo ufw enable:*

<figure id="4e2d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Ft4ZjejAdhIati1Qm1CQCQ.png"
class="graf-image" data-image-id="1*Ft4ZjejAdhIati1Qm1CQCQ.png"
data-width="1066" data-height="73" />
<figcaption>expected output but if it is your first time you will be
prompted with a confirmation message. Type ‘y’ to proceed.</figcaption>
</figure>

You'll be prompted with a confirmation message. Type \`y\` to proceed.

Once enabled, UFW will begin enforcing your firewall rules immediately.
Be careful not to block yourself out of the system, especially if you're
connected remotely.

Step 4: Check UFW Status\
To verify that UFW is enabled and to check what rules are currently
active, run:\
*sudo ufw status verbose*

<figure id="dc8f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*qjkwXK83m_jACZHIBDRI0A.png"
class="graf-image" data-image-id="1*qjkwXK83m_jACZHIBDRI0A.png"
data-width="1066" data-height="370" />
</figure>

This will display the current status (\`active\` or \`inactive\`) and
list all allowed/denied services.

#### 4. Allowing and Denying Services in UFW

With UFW enabled and basic rules in place, it's important to fine-tune
the firewall by allowing or denying specific services and ports based on
your needs. Let's go over some common configurations.

Step 1: Allow Common Services\
UFW makes it easy to allow common services like HTTP, HTTPS, and SSH
with simple commands. Here's how to allow traffic for these services:

-   Allow HTTP (Port 80):\
    *sudo ufw allow http*

<figure id="3307" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*66DbrXxpEVexTaTItRWSLA.png"
class="graf-image" data-image-id="1*66DbrXxpEVexTaTItRWSLA.png"
data-width="1071" data-height="76" />
<figcaption>port 80 added,check below image to to see
the status</figcaption>
</figure>

<figure id="1d52" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*etfmi62p6-OCiSElK6qxzA.png"
class="graf-image" data-image-id="1*etfmi62p6-OCiSElK6qxzA.png"
data-width="1069" data-height="136" />
<figcaption>port 80 added already i hope we are good.</figcaption>
</figure>

n/b(i had to reset my ufw to show case how i added port 80

-   Allow HTTPS (Port 443)\
    *sudo ufw allow https*

<figure id="41a2" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*QkEo3iBtShi7wLDD_BRtng.png"
class="graf-image" data-image-id="1*QkEo3iBtShi7wLDD_BRtng.png"
data-width="1008" data-height="259" />
</figure>

-   Allow SSH (Port 22):\
     If you haven't already allowed SSH in the previous step, you can do
    it here:\
    *sudo ufw allow ssh*

<figure id="ccb3" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*AB01G-CoXPN_WglGgkNsww.png"
class="graf-image" data-image-id="1*AB01G-CoXPN_WglGgkNsww.png"
data-width="1066" data-height="288" />
</figure>

Step 2: Allow Custom Ports\
For applications running on non-standard ports, you can specify custom
ports. For example, if you have a web server running on port 8080, you
can allow it as follows:

-   Allow traffic on Port 8080:\
     *sudo ufw allow 8080/tcp*

<figure id="9df1" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*o4Tz1GQF95UZHqDe5e_-oQ.png"
class="graf-image" data-image-id="1*o4Tz1GQF95UZHqDe5e_-oQ.png"
data-width="1066" data-height="330" />
</figure>

Step 3: Denying Services\
To block a specific service or port, you can use the \`deny\` option.
For example, to block SSH access:

-   Deny SSH:\
    *sudo ufw deny SSH*

<figure id="4668" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*_7RfKncnG5GVsAjnYV3GXg.png"
class="graf-image" data-image-id="1*_7RfKncnG5GVsAjnYV3GXg.png"
data-width="1068" data-height="358" />
<figcaption>Check the SSH and you can see that the service
is denied.</figcaption>
</figure>

You can also block any custom port in a similar way. For instance, if
you want to block access to port 8080:\
\
*sudo ufw deny 8080/tcp*

<figure id="e52c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*2vBhrUkXqez8cu3ILEqCuQ.png"
class="graf-image" data-image-id="1*2vBhrUkXqez8cu3ILEqCuQ.png"
data-width="1068" data-height="360" />
</figure>

Step 4: Allowing Specific IP Addresses\
Sometimes, you might want to allow a specific IP or range of IPs to
access a service while blocking others. For example, to allow SSH from a
specific IP address (ex\`192.168.1.100\`):

-   Allow SSH from a Specific IP:\
    *sudo ufw allow from 192.168.1.100 to any port 22*

<figure id="0f84" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*cpMUpYpKro2s282PLR4iHA.png"
class="graf-image" data-image-id="1*cpMUpYpKro2s282PLR4iHA.png"
data-width="1510" data-height="322" />
<figcaption>ip address added successfully check the
output keenly.</figcaption>
</figure>

This ensures only connections from that IP address can access SSH.

Step 5: Viewing Active Rules

To see the current list of all active rules, run:\
*sudo ufw status numbered*

<figure id="8e02" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*GTg-zwSn21yyTvkigcw9uw.png"
class="graf-image" data-image-id="1*GTg-zwSn21yyTvkigcw9uw.png"
data-width="931" data-height="265" />
</figure>

This will display all the rules along with their respective numbers,
which will be useful when you want to delete a rule.

#### 5. Managing and Deleting UFW Rules

As you fine-tune your firewall settings, you might need to modify or
remove certain rules. UFW provides simple ways to list, delete, and
manage these rules.

Step 1: Listing UFW Rules\
To view all the active rules, use the following command:\
\
*sudo ufw status numbered*

<figure id="d249" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*GTg-zwSn21yyTvkigcw9uw.png"
class="graf-image" data-image-id="1*GTg-zwSn21yyTvkigcw9uw.png"
data-width="931" data-height="265" />
</figure>

This command will display each rule with a corresponding number, which
is useful for managing or deleting specific rules later.

Step 2: Deleting UFW Rules\
If you need to delete a specific rule, note the number from the list
displayed by \`sudo ufw status numbered\`. For example, if you want to
delete rule number 2, run:\
\
*sudo ufw delete 2*

<figure id="f80d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*enSYbuYg-zqUQIbILee8Sg.png"
class="graf-image" data-image-id="1*enSYbuYg-zqUQIbILee8Sg.png"
data-width="948" data-height="358" />
<figcaption>i have capture the image for you see that i will be deleting
number 2 which is port 443</figcaption>
</figure>

second image is when number 2 is deleted

<figure id="3991" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*0-f_w9to2pY_JQSYlIYYzg.png"
class="graf-image" data-image-id="1*0-f_w9to2pY_JQSYlIYYzg.png"
data-width="919" data-height="253" />
<figcaption>now number 2 was deleted and replaced by
SSH ,simply that</figcaption>
</figure>

You'll be asked to confirm the deletion. Once confirmed, the rule will
be removed.

Step 3: Resetting UFW\
If you want to reset UFW back to its default state and remove all custom
rules, use the following command:\
*sudo ufw reset*

<figure id="3072" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Z3nCr4oJxpBzJUu-PuSn5g.png"
class="graf-image" data-image-id="1*Z3nCr4oJxpBzJUu-PuSn5g.png"
data-width="930" data-height="273" />
<figcaption>i have done more of resetting my rules</figcaption>
</figure>

This command will disable UFW and delete all the existing rules, so use
it with caution if you've already spent time configuring specific rules.

Step 4: Disabling UFW\
If you need to temporarily turn off the firewall, you can disable UFW
without resetting it:\
*sudo ufw disable*

<figure id="7e73" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*PReLFGQRbfGDmm9Hk3sK7g.png"
class="graf-image" data-image-id="1*PReLFGQRbfGDmm9Hk3sK7g.png"
data-width="958" data-height="181" />
</figure>

This will stop enforcing the firewall rules until you enable it again.

Step 5: Re-Enabling UFW\
To turn UFW back on after disabling it, use:\
*sudo ufw enable*

<figure id="2f1b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*IwHW8zgjM1fB_IL8fv1iAw.png"
class="graf-image" data-image-id="1*IwHW8zgjM1fB_IL8fv1iAw.png"
data-width="940" data-height="124" />
<figcaption>i have enabled again</figcaption>
</figure>

Step 6: Modifying Rules\
If you need to change a rule, the easiest way is to delete the existing
rule and create a new one. For example, to modify an SSH rule from
\`allow\` to \`limit\`, you would:\
1. Delete the original rule:\
*sudo ufw allow ssh*

<figure id="764e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*2fH2xcNj1svgPDswBk94vA.png"
class="graf-image" data-image-id="1*2fH2xcNj1svgPDswBk94vA.png"
data-width="924" data-height="190" />
</figure>

2\. Add the modified rule (rate-limited SSH):\
*sudo ufw limit ssh*

<figure id="3dea" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*m0Hw_wb69c6HtKnmIfgisQ.png"
class="graf-image" data-image-id="1*m0Hw_wb69c6HtKnmIfgisQ.png"
data-width="958" data-height="196" />
</figure>

#### 6. Conclusion


UFW (Uncomplicated Firewall) is a powerful yet simple tool that enables
you to secure your Kali Linux system by managing incoming and outgoing
network traffic. Through this guide, we've covered everything from
installing UFW, setting default policies, and allowing or denying
services, to managing and deleting rules. By applying these steps, you
can effectively control access to your system, prevent unauthorized
connections, and enhance your overall security.

UFW's ease of use, combined with its ability to handle advanced
configurations like custom ports and specific IPs, makes it an essential
tool for anyone looking to strengthen their network defenses. Whether
you are securing your home lab or a professional environment, UFW's
simple commands can provide robust protection without the complexity of
other firewall solutions.

Now that you've mastered the basics of UFW, you're equipped to customize
your firewall setup further, automate security measures, and explore
advanced features. Stay secure and continue exploring more ways to
protect your systems!

### END 
By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [September 28, 2024](https://medium.com/p/5cdaa55eead9).

[Canonical
link](https://medium.com/@kiplagatkelvin034/secure-your-kali-linux-with-ufw-uncomplicated-firewall-setup-5cdaa55eead9){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
