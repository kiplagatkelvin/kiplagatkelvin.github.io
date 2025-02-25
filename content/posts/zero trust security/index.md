--
title: "A Practical Guide to Zero Trust Security: Implementing Network Segmentation with pfSense, MFA with Authy, and Continuous Monitoring Using Splunk"
author: "Kiplagatkelvin"
date: "2025-01-24"
tags: ["Zero Trust", "pfSense", "MFA", "Authy", "Splunk", "Cybersecurity", "Network Security"]
categories: ["Cybersecurity", "Network Security"]
summary: "Learn how to implement a basic Zero Trust Architecture using pfSense for network segmentation, Authy for MFA, and Splunk for continuous monitoring."



---



### A Practical Guide to Zero Trust **Security: Implementing Network Segmentation with pfSense, MFA with Authy, and Continuous Monitoring Using Splunk** 

<figure id="8998" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*CQUgkjyZ8JSRmqqz_hmPBQ.png"
class="graf-image" data-image-id="1*CQUgkjyZ8JSRmqqz_hmPBQ.png"
data-width="960" data-height="483" data-is-featured="true" />
</figure>

**Introduction**

The aim of this project was to implement a **basic Zero Trust
Architecture** as a practical demonstration of modern security
principles. Zero Trust operates under the philosophy of "never trust,
always verify," ensuring that every access request is validated and that
sensitive resources are segmented from general user access.

This activity involved three key components:

1.  **Network Segmentation**: Using **pfSense** to create isolated
    VLANs for general users and sensitive systems, with strict access
    controls.
2.  **Multi-Factor Authentication (MFA)**: Configuring **Authy** to
    secure system access with an additional layer of verification beyond
    passwords.
3.  **Continuous Monitoring**: Using **Splunk** to monitor network
    activity, detect anomalies, and establish real-time alerts for
    suspicious behavior.

By the end of this project, we will achieve:

-   A segmented network where general users are restricted from
    accessing sensitive systems.
-   Strong authentication mechanisms that prevent unauthorized
    access.
-   A monitoring system to track user and device activity for proactive
    threat detection.

This hands-on activity is designed not only to enhance your technical
skills in configuring security tools but also to provide a comprehensive
guide for others looking to implement a Zero Trust model. Each step is
documented with clear explanations, practical tests (e.g., ping
commands), and screenshots to ensure replicability.

**Step 1: Install and Configure pfSense**

The first step is setting up **pfSense** to implement **network
segmentation**, which is a cornerstone of Zero Trust Architecture.

**1. Install pfSense**

1.  **Download pfSense**:

-   Visit [pfSense Official Download
    Page](https://www.pfsense.org/download/){.markup--anchor
    .markup--li-anchor data-href="https://www.pfsense.org/download/"
    rel="noopener" target="_blank"}.
-   Choose the appropriate installer for your system.

<figure id="3343" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*hxnddSJ5Ta3FQBo2ewXPjg.png"
class="graf-image" data-image-id="1*hxnddSJ5Ta3FQBo2ewXPjg.png"
data-width="975" data-height="470" />
</figure>

1.  **Set Up pfSense in a Virtual Environment (e.g., VMware)**:

-   Create a new virtual machine with these configurations:
-   **CPU**: 2 vCPUs
-   **RAM**: 4GB
-   **Storage**: 16GB
-   Two **network adapters**:
-   **WAN**: Connect to your internet source.
-   **LAN**: Connect to the internal network.

<figure id="2adc" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*cw2TTVZHku3suKD6c3rhEA.png"
class="graf-image" data-image-id="1*cw2TTVZHku3suKD6c3rhEA.png"
data-width="975" data-height="546" />
</figure>

Next to:

<figure id="4e68" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Nkg9wcsDoDcAM1nw2dsxZg.png"
class="graf-image" data-image-id="1*Nkg9wcsDoDcAM1nw2dsxZg.png"
data-width="975" data-height="524" />
</figure>

1.  **Boot and Install**:

-   Boot the virtual machine with the pfSense ISO.Follow the
    installation wizard to set up the system.
-   Assign network interfaces:
-   WAN: Default to your external network.
-   LAN: Internal-facing network (default: 192.168.88.1).

(n/b make sure you create the two adapter one for WAN and the other for
LAN)

<figure id="c449" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*gdau4blXk066HXCPYer8Mw.png"
class="graf-image" data-image-id="1*gdau4blXk066HXCPYer8Mw.png"
data-width="975" data-height="524" />
</figure>

**Our pfsense is now ready:**

<figure id="1939" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*BA1tLqgtws77jxfsXnzd7g.png"
class="graf-image" data-image-id="1*BA1tLqgtws77jxfsXnzd7g.png"
data-width="975" data-height="548" />
</figure>

**Our linux is also ready:**

<figure id="61b4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*IrzWR7yNOEq-p-kwQeruPA.png"
class="graf-image" data-image-id="1*IrzWR7yNOEq-p-kwQeruPA.png"
data-width="975" data-height="546" />
</figure>

**They both need to communicate first ,so**

**I did aping command from linux to pfsense and there was a
communication.**

<figure id="ed61" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*JOcXT-VZFJv46XwBJVZAJw.png"
class="graf-image" data-image-id="1*JOcXT-VZFJv46XwBJVZAJw.png"
data-width="975" data-height="475" />
</figure>

**I did another ping scan from pfsense to linux:**

<figure id="f14d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*XQyEyBBPrwf-Df_XOqNd5A.png"
class="graf-image" data-image-id="1*XQyEyBBPrwf-Df_XOqNd5A.png"
data-width="975" data-height="546" />
</figure>

They both communicated very well so the next step was to access the
pfsense web interface from linux firefox:

**4.Access the Web Interface**:

-   Open a browser on a machine connected to the LAN.
-   Navigate to
    http://192.168.88.1.](http://192.168.88.1.){.markup--anchor
    .markup--li-anchor data-href="http://192.168.88.1." rel="noopener"
    target="_blank"}
-   Log in with the default credentials:
-   **Username**: admin
-   **Password**: pfsense

<figure id="1f5d" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*QqB0zZxJ9A3E2871BRhSqA.png"
class="graf-image" data-image-id="1*QqB0zZxJ9A3E2871BRhSqA.png"
data-width="975" data-height="548" />
</figure>

Then I logged using the above details to access the pfsense
configuration setting.

**2. Create VLANs for Segmentation**

1.  **Navigate to VLAN Settings**:

-   Go to **Interfaces \> Assignments** and click on the **VLANs**
    tab.

<figure id="670c" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*oVOUyr6-8zFowJA5GsWlnQ.png"
class="graf-image" data-image-id="1*oVOUyr6-8zFowJA5GsWlnQ.png"
data-width="975" data-height="488" />
</figure>

1.  **Create Two VLANs**:

**VLAN 10** (virtual 10 local area network):

-   VLAN ID: 10
-   Parent Interface: LAN

**VLAN 20** (virtual 20 local area network):

-   VLAN ID: 20
-   Parent Interface: LAN

<figure id="ddb3" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*VkksAGilBVgwV546vDNN2Q.png"
class="graf-image" data-image-id="1*VkksAGilBVgwV546vDNN2Q.png"
data-width="975" data-height="1111" />
</figure>

1.  **Assign VLANs to Interfaces**:

-   Under **Interfaces \> Assignments**, assign the VLANs created to
    new interfaces.

o Go back to **Interfaces \> Assignments**.

o Assign each VLAN to a new interface:

-   **VLAN 10**: Add as OPT1 and rename it to VLAN 10.
-   **VLAN 20**: Add as OPT2 and rename it to VLAN 20.

<figure id="385e" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*kxuM8TXkzpX1mKLoRPM29g.png"
class="graf-image" data-image-id="1*kxuM8TXkzpX1mKLoRPM29g.png"
data-width="975" data-height="565" />
</figure>

**4.Configure IP Addresses for VLAN Interfaces**

**(n/b) for your case you are free to apply your own ip addresses:**

1.  Go to **Interfaces \> VLAN 10**:

-   Enable the interface.
-   Set the static IPv4 address to: 192.168.88.1/25.

1.  Go to **Interfaces \> VLAN 20**:

-   Enable the interface.
-   Set the static IPv4 address to: 192.168.88.129/25.

Using the above configuration ,I though they were the best reason for me
being that they were under my subnets mask only to receive this error.

<figure id="bb32" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*WR7Iwxz_7qom1oFaqBf8nQ.png"
class="graf-image" data-image-id="1*WR7Iwxz_7qom1oFaqBf8nQ.png"
data-width="975" data-height="895" />
</figure>

The above error occurs because my WAN and LAN interfaces are already
using overlapping IP address ranges (192.168.88.0/24), and my VLANs also
fall within the same range. To fix this issue, i need to adjust the IP
addressing to avoid overlap.so I used a separate subnet mask

**Use a Separate Subnet for VLANs**

You must use a new IP range for your VLANs that does not overlap with
your existing **WAN** or **LAN** subnets. For example:

-   **WAN**: Keep 192.168.88.131/24 (existing).
-   **LAN**: Keep 192.168.88.0/24 (existing, if necessary).
-   **VLAN 10 (General Users)**: Use 192.168.10.0/24.
-   **VLAN 20 (Sensitive Systems)**: Use 192.168.20.0/24.

For vlan 10 below it now successful.

<figure id="737f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*4FLGpqoN4m2GXWXGgqe54Q.png"
class="graf-image" data-image-id="1*4FLGpqoN4m2GXWXGgqe54Q.png"
data-width="975" data-height="904" />
</figure>

For Vlan 20 above is now successful.

<figure id="f6ae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*XDp-OB6vBGQRolMJ_qVMMw.png"
class="graf-image" data-image-id="1*XDp-OB6vBGQRolMJ_qVMMw.png"
data-width="975" data-height="1007" />
</figure>

#### 4. Set DHCP Servers for VLANs 

1.  Navigate to **Services \> DHCP Server**.
2.  Enable DHCP for each VLAN:

-   **VLAN 10**:
-   Range: 192.168.10.10 to 192.168.10.100.

<figure id="b919" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*31CMGEt8Rfah0jooc_JuCg.png"
class="graf-image" data-image-id="1*31CMGEt8Rfah0jooc_JuCg.png"
data-width="975" data-height="880" />
</figure>

-   **VLAN 20**:
-   Range: 192.168.20.10 to 192.168.20.100.

<figure id="cfe6" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*fBq4bujze1MCsfBC-RqLCg.png"
class="graf-image" data-image-id="1*fBq4bujze1MCsfBC-RqLCg.png"
data-width="975" data-height="910" />
</figure>

#### **3. Configure Firewall Rules** 

1.  Navigate to **Firewall \> Rules**.

<figure id="52dd" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*IXTaaJpzx-dDmwkdNyyEBw.png"
class="graf-image" data-image-id="1*IXTaaJpzx-dDmwkdNyyEBw.png"
data-width="975" data-height="924" />
</figure>

2.Set up rules for each VLAN:

**VLAN 10**:

-Allow **internet access**.

-Block traffic to **VLAN 20**.

**VLAN 20**:

-   Restrict access to only necessary services ( database
    servers).

Save and apply the changes.

**Below image is for vlan 10 opt1 rules configured:**

<figure id="7d01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*1JSm0kuybaBJb7dnV9wNBQ.png"
class="graf-image" data-image-id="1*1JSm0kuybaBJb7dnV9wNBQ.png" />
</figure>

What I did:

**Create Rules for VLAN 10 (Internet Access):**

-   **Add a new rule:** Click the **Add** button under the "Floating"
    tab. This will create a new rule at the top of the list.
-   **Set interface:** Select **OPT1** connected to vlan 10.
-   **Action:** Choose **Pass** to allow traffic.
-   **Protocol:** Leave as **Any** to allow all protocols.
-   **Source:** Set to **any** to allow traffic from any
    source.
-   **Destination:** Set to **any** to allow traffic to any
    destination.
-   **Port:** Leave as **Any**.
-   **Gateway:** Leave as **Default**.
-   **Schedule:** Leave as **Always**.
-   **Description:** Enter a descriptive name, such as "Allow Internet
    for VLAN 10".
-   **Save** the rule.

**Below image is for vlan 20 opt2 rules configured:**

<figure id="304a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*8HPob21n0dQjfiHYiGAWNA.png"
class="graf-image" data-image-id="1*8HPob21n0dQjfiHYiGAWNA.png"
data-width="975" data-height="869" />
</figure>

What I did**:**

· Add **a new rule** for the OPT2 interface (as shown in the
screenshot).

· Action**:** Choose **Block** to deny traffic.

· Protocol**:** Leave as **Any**.

· **Source:** Set to **any** to block traffic from any source.

· **Destination:** Set to **any** to block traffic to any destination.

· **Port:** Leave as **Any**.

· **Gateway:** Leave as **Default**.

· **Schedule:** Leave as **Always**.

· **Description:** Enter a descriptive name, such as "Block all traffic
for VLAN 20".

· **Save** the rule.

#### **4.** Test Network Segmentation

Below image shows my pfsense with both configured vlans

<figure id="46a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*_ApYcu-CIrBZtG5jw8zgaA.png"
class="graf-image" data-image-id="1*_ApYcu-CIrBZtG5jw8zgaA.png"
data-width="975" data-height="543" />
</figure>

1.  **Connect Devices**:

-   Assign one device (Linux machine) to VLAN 10.
-   Assign another device (server) to VLAN 20.

1.  **Run Ping Tests**:

-   **From VLAN 10, run:**
-   **ping 192.168.20.1**

This should **fail**, indicating restricted access.

<figure id="a678" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*OTT4Z3YkzzQWxbYlJCsG-w.png"
class="graf-image" data-image-id="1*OTT4Z3YkzzQWxbYlJCsG-w.png"
data-width="975" data-height="462" />
</figure>

-   **Ping the pfSense gateway for VLAN 10:**
-   **ping 192.168.10.2**

This should **succeed**, verifying connectivity to the router.

<figure id="35dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*OTT4Z3YkzzQWxbYlJCsG-w.png"
class="graf-image" data-image-id="1*OTT4Z3YkzzQWxbYlJCsG-w.png"
data-width="975" data-height="462" />
</figure>

.

### **Step 2: Implement MFA Using google authenticator with OpenVPN** 

### **Prerequisites:** 

**1.pfSense Setup**: Ensure your pfSense is installed and running.

**2.OpenVPN Package**: Installed and configured on pfSense.

Install OpenVPN from **System \> Package Manager** \> Available
Packages.

**3.Google Authenticator App**: Downloaded and installed on your mobile
device.

**4.FreeRADIUS**: Installed and configured as the authentication server.

<figure id="9f5d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*G4kcLSl13lFsN-NvVBOOqg.png"
class="graf-image" data-image-id="1*G4kcLSl13lFsN-NvVBOOqg.png"
data-width="975" data-height="886" />
</figure>

**Step-by-Step Guide**

**1. Set Up FreeRADIUS for MFA**

-   Install FreeRADIUS from the pfSense package manager:
-   Navigate to **System \> Package Manager \> Available
    Packages**.
-   Search for "FreeRADIUS" and click **Install**.
-   Configure FreeRADIUS:

1.  Navigate to **Services \> FreeRADIUS**.
2.  Go to the **Users** tab and add a user:

-   Username: kelvinkiplagat]{#b831}
-   Password: \*\*\*\*\*\*\*\*\*\*\*\*\*\*

<figure id="7634" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*C3M5AzZPuODgAyWVniGCKw.png"
class="graf-image" data-image-id="1*C3M5AzZPuODgAyWVniGCKw.png"
data-width="975" data-height="947" />
</figure>

1.  Enable **Time-Based One-Time Passwords (TOTP)**:

-   In the FreeRADIUS configuration, enable TOTP for the user you
    created.
    
1.  Start the FreeRADIUS service:

-   Navigate to **Status \> Services**, locate FreeRADIUS, and click
    **Start**.

**2. Enable OpenVPN on pfSense**

-   Navigate to **VPN \> OpenVPN** and set up a new server:
-   Choose the **Wizard** to simplify the configuration.
-   Use the RADIUS server (FreeRADIUS) as the authentication
    backend.

I went to the diagnostic and I did an authentication test1 and below
image show that it was successful

<figure id="6746" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*HqwA8HS32OrSrWS7XzMRoA.png"
class="graf-image" data-image-id="1*HqwA8HS32OrSrWS7XzMRoA.png"
data-width="975" data-height="547" />
</figure>

I went to the diagnostic and I did an authentication test2 and below
image show that it was successful

<figure id="0f93" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ve4lsmAlOw4gHDR9mlPRxw.png"
class="graf-image" data-image-id="1*ve4lsmAlOw4gHDR9mlPRxw.png"
data-width="975" data-height="546" />
</figure>

**3. Configure goohle Authenticator app for TOTP**

-  Open the app on your mobile device.but in our case we shall be
    using google authentication

<figure id="6b21" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*RJb5aDEwSo-qYFzOX9ZL9g.png"
class="graf-image" data-image-id="1*RJb5aDEwSo-qYFzOX9ZL9g.png"
data-width="889" data-height="632" />
</figure>

-   dd a new account and manually set it up with the TOTP secret
    generated by FreeRADIUS.

<figure id="a8fb" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*6KsPuUzsnJvhckXmgjDYCw.png"
class="graf-image" data-image-id="1*6KsPuUzsnJvhckXmgjDYCw.png"
data-width="975" data-height="507" />
</figure>

-   A TOTP (6-digit code) will now be generated every 30
    seconds.

<figure id="c305" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*m_in54oQsmL0xNMxqSzXpg.png"
class="graf-image" data-image-id="1*m_in54oQsmL0xNMxqSzXpg.png"
data-width="323" data-height="657" />
</figure>

This is the google authenticator looks likes in my phone and it keeps
changing every 5 seconds

#### **4. Test the MFA Integration** 

1.  Connect to the OpenVPN server using a VPN client (OpenVPN
    Connect).
2.  When prompted for credentials, enter:I have hidden my
    credetilas

-   Username:kelvin kiplagat
-   Password:\*\*\*\*\*\*\*\*
-   ollowed by the 6-digit TOTP from Authy.
-   For example, if your TOTP is 123456, the password will be:
    word123456.

<figure id="3f13" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*cGegSmPtR2StPIEGqH5HOQ.png"
class="graf-image" data-image-id="1*cGegSmPtR2StPIEGqH5HOQ.png"
data-width="273" data-height="598" />
</figure>

3\. Test the connection:

-   Connection should fail if the TOTP is incorrect or missing. Via the
    mobile phone

<figure id="c536" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*xhXeaDoP5PcDgrLgo_I9pg.png"
class="graf-image" data-image-id="1*xhXeaDoP5PcDgrLgo_I9pg.png"
data-width="232" data-height="516" />
</figure>

-   Connection should succeed if both the static password and TOTP are
    correct.

<figure id="e854" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*Ov3bIzLmHEgo8SopoE61_g.png"
class="graf-image" data-image-id="1*Ov3bIzLmHEgo8SopoE61_g.png"
data-width="307" data-height="379" />
</figure>

**Step 3: Set Up Continuous Monitoring Using Splunk on Kali Linux**

**1. Install Splunk**

1.  **Download Splunk Free**:

-   Visit [Splunk Enterprise Download
    Page](https://www.splunk.com/en_us/download/splunk-enterprise.html){.markup--anchor
    .markup--li-anchor
    data-href="https://www.splunk.com/en_us/download/splunk-enterprise.html"
    rel="noopener" target="_blank"}.]{#09bb}
-   Choose the .tgz installer for Linux.
-   Register or log in if prompted.
-   Download the .tgz file to your Kali Linux system.

<figure id="c9cf" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*22MNoc1V72_-7aggnQIjdg.png"
class="graf-image" data-image-id="1*22MNoc1V72_-7aggnQIjdg.png"
data-width="975" data-height="542" />
</figure>

1.  **Install Splunk**:

-   Open a terminal and navigate to the folder where the .tgz file is
    saved.
-   Extract the file:

***Sudo tar -xvzf splunk-9.0.4.1--419ad9369127-linux-x86_64.tgz -C
/opt***

***cd /opt/splunk/bin***

<figure id="2185" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*zPULHUIh2KcQu4sxqBfTCQ.png"
class="graf-image" data-image-id="1*zPULHUIh2KcQu4sxqBfTCQ.png"
data-width="975" data-height="454" />
</figure>

Run the following command to accept the license, and then follow the
prompts to enter your ***username*** and ***password***

***sudo ./splunk start --- accept-license***

<figure id="6e2d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*XCICEOgEUY2OwcQjqbHOrQ.png"
class="graf-image" data-image-id="1*XCICEOgEUY2OwcQjqbHOrQ.png"
data-width="920" data-height="535" />
</figure>

1.  **Access Splunk**:

-   Open your browser and navigate to
    http://localhost:8000.](http://localhost:8000.){.markup--anchor
    .markup--li-anchor data-href="http://localhost:8000." rel="noopener"
    target="_blank"}
-   Log in using the credentials you created.

Go to the Splunk address in your browser, and enter credentials.

<figure id="9ee4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*fq-RLuMblTx0-OLB-9p7lg.png"
class="graf-image" data-image-id="1*fq-RLuMblTx0-OLB-9p7lg.png"
data-width="975" data-height="434" />
</figure>

-   Log in using the credentials you created.

<figure id="9d86" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*z2q-DAA2IwFjnQ3eITao3w.png"
class="graf-image" data-image-id="1*z2q-DAA2IwFjnQ3eITao3w.png"
data-width="975" data-height="451" />
</figure>

<figure id="c1cd" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*QSMyLxpYWpw6M6u6pJIlCg.png"
class="graf-image" data-image-id="1*QSMyLxpYWpw6M6u6pJIlCg.png"
data-width="975" data-height="465" />
</figure>

**2. Set Up Syslog Inputs**

1.  **Configure pfSense Firewall to Forward Logs**:

-   Log in to the pfSense web interface.
-   Navigate to Status \> System Logs \> Settings.

<figure id="dc5d" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*Gb6A9RY1SeYtWPJOrPuulA.png"
class="graf-image" data-image-id="1*Gb6A9RY1SeYtWPJOrPuulA.png"
data-width="770" data-height="446" />
</figure>

-   Enable **Remote Logging Options** and specify the
    following:
-   Remote log server: **IP address of your Splunk server (Kali
    Linux)**
-   Port: **514**
-   Protocol: **UDP**
-   Save changes

<figure id="799d" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*ymWdpMCQ1JPSjTbjveOR5A.png"
class="graf-image" data-image-id="1*ymWdpMCQ1JPSjTbjveOR5A.png"
data-width="975" data-height="543" />
</figure>

**One need to enable 'Default Allow Logging**'.

-   To enable logging of allowed packets from the default allow rule,
    go to to **Status \> System Logs \> Settings** tab, then check Log
    packets allowed by the default rule.
-   Click **Save** to apply the changes.

<figure id="61b9" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*rnOA4zQ9KlwQcUGy4y8ZmQ.png"
class="graf-image" data-image-id="1*rnOA4zQ9KlwQcUGy4y8ZmQ.png"
data-width="1683" data-height="205" />
</figure>

1.  **Set Up Splunk to Receive Syslog Data**:

-   In the Splunk web interface, navigate to Settings \> Data
    Inputs.

<figure id="fe90" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*Qm8dhla_OqQpp7RMQkFHvg.png"
class="graf-image" data-image-id="1*Qm8dhla_OqQpp7RMQkFHvg.png"
data-width="975" data-height="398" />
</figure>

-   Under **Local Inputs**, click **Add New** for Syslog.

<figure id="819f" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*KQzmprvYUIuN1PZUc2za_w.png"
class="graf-image" data-image-id="1*KQzmprvYUIuN1PZUc2za_w.png"
data-width="975" data-height="390" />
</figure>

-   Configure the following:
-   **Port**: Enter 514 (to match the pfSense configuration).
-   **Source**: Provide a meaningful name, e.g., pfSense_logs.

<figure id="23a9" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*znR5obvfjaXOs8T3-pZeww.png"
class="graf-image" data-image-id="1*znR5obvfjaXOs8T3-pZeww.png"
data-width="975" data-height="377" />
</figure>

-   **Host**: Choose "Custom" and enter pfSense.

**Submit**

<figure id="fad0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*jLslRcm-AalZNUKTvkLk9A.png"
class="graf-image" data-image-id="1*jLslRcm-AalZNUKTvkLk9A.png"
data-width="975" data-height="390" />
</figure>

-   Save the configuration.

1.  **Verify Syslog Data**:

-   Use the search bar in Splunk to check for incoming syslog
    events:

#### ***index=\_test*** {#0d45 .graf .graf--h4 .graf-after--li name="0d45"}

<figure id="2be7" class="graf graf--figure graf-after--h4">
<img
src="https://cdn-images-1.medium.com/max/800/1*lmZQdio2XQpfTbuvq455fA.png"
class="graf-image" data-image-id="1*lmZQdio2XQpfTbuvq455fA.png"
data-width="975" data-height="429" />
</figure>

#### Or *index =test sourcetype"pfsense_syslog"* 

<figure id="5ee5" class="graf graf--figure graf-after--h4">
<img
src="https://cdn-images-1.medium.com/max/800/1*mEs5KDHiM5xek1SSWLBRrw.png"
class="graf-image" data-image-id="1*mEs5KDHiM5xek1SSWLBRrw.png"
data-width="975" data-height="405" />
</figure>

I managed to capture more of syslog pfsense capture

<figure id="191c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*Gdr5lGdYvdnRNczo0jQKDQ.png"
class="graf-image" data-image-id="1*Gdr5lGdYvdnRNczo0jQKDQ.png"
data-width="975" data-height="422" />
</figure>

**Summary of Implementation:**

***Network Segmentation with pfSense:***

Using pfSense, I created two VLANs: VLAN 10 for general users and VLAN
20 for sensitive systems. Firewall rules were configured to restrict
inter-VLAN traffic, ensuring that general users could not access
sensitive systems. This segmentation reduces the attack surface and
limits lateral movement within the network. Testing confirmed that
traffic between the VLANs was effectively blocked, as evidenced by
screenshots of the rules and blocked attempts.

***Multi-Factor Authentication with google authentocator:***

I enabled MFA on a selected application using google authenticator to
generate time-based one-time passwords (TOTP). This added an extra layer
of authentication beyond just a password. Testing validated that login
attempts without the TOTP were rejected, while successful logins
required both the password and the Authy-generated code. Screenshots
captured the successful MFA setup and usage.

***Continuous Monitoring with Splunk:***

Splunk was configured to collect syslog data from the pfSense firewall
and the MFA-enabled application. A custom Splunk dashboard was created
to monitor key metrics, such as user login attempts, blocked access, and
network activity between VLANs. Alerts were set up to notify of
suspicious activities like repeated failed logins or unauthorized VLAN
access attempts. Screenshots illustrated the Splunk configuration and
visualized data on the dashboard.

***Conclusion:***

Implementing these Zero Trust principles --- network segmentation, MFA,
and continuous monitoring --- significantly strengthens CyberTech
Solutions' security by adopting a "never trust, always verify" approach.
Network segmentation ensures that sensitive systems are isolated from
general users, reducing exposure to potential threats. MFA mitigates
risks associated with credential theft, adding a robust second layer of
defense. Continuous monitoring enables real-time visibility and rapid
response to anomalous or malicious activities. Together, these measures
create a cohesive security framework that minimizes vulnerabilities and
proactively safeguards the network.


By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [January 24, 2025](https://medium.com/p/adb9c211d237).

[Canonical
link](https://medium.com/@kiplagatkelvin034/a-practical-guide-to-zero-trust-security-implementing-network-segmentation-with-pfsense-mfa-with-adb9c211d237){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
