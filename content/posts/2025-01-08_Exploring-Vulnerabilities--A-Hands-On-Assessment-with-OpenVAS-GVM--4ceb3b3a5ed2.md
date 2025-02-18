<div>

# Exploring Vulnerabilities: A Hands-On Assessment with OpenVAS(GVM) {#exploring-vulnerabilities-a-hands-on-assessment-with-openvasgvm .p-name}

</div>

::: {.section .p-summary field="subtitle"}
Introduction
:::

::: {.section .e-content field="body"}
::: {#32af .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Exploring Vulnerabilities: A Hands-On Assessment with OpenVAS(GVM) {#9d1b .graf .graf--h3 .graf--leading .graf--title name="9d1b"}

<figure id="5188" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*RoMzwk3AeZzbximpNs2XBg.png"
class="graf-image" data-image-id="1*RoMzwk3AeZzbximpNs2XBg.png"
data-width="665" data-height="439" data-is-featured="true" />
</figure>

**Introduction**

In today's ever-evolving cybersecurity landscape, identifying and
mitigating vulnerabilities is a vital practice. In this case study, I
explore the vulnerability assessment of CyberTech Solutions' network
using OpenVAS on Kali Linux. By conducting a comprehensive scan,
analyzing results, and recommending remediations, this exercise
demonstrates the importance of proactive measures in securing IT
infrastructure.

**Setup and Installation**

To carry out this assessment, I installed and configured OpenVAS on a
Kali Linux system. OpenVAS, a powerful open-source vulnerability
scanner, allows for detailed analysis of network security.

<figure id="150c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*PZL4LerH_8JvhyaTXwUySw.png"
class="graf-image" data-image-id="1*PZL4LerH_8JvhyaTXwUySw.png"
data-width="975" data-height="483" />
</figure>

**Steps to Install OpenVAS:**

1.  [**Install OpenVAS:**]{#a211}

sudo apt update && sudo apt install -y openvas

1.  [**Set up OpenVAS:**]{#0f99}

sudo gvm-setup

1.  [**Start the service:**]{#eb49}

sudo gvm-start

<figure id="eb8b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*L7dFCA0A6XxAkvXvRT899Q.png"
class="graf-image" data-image-id="1*L7dFCA0A6XxAkvXvRT899Q.png"
data-width="1918" data-height="921" />
</figure>

1.  [**Access the Web Interface:** Navigate to https://\<your-ip\>:9392
    and log in using the credentials set during the setup.]{#a8ab}

<figure id="762c" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*ADnVCbUyVzo_yURKqAJP6g.png"
class="graf-image" data-image-id="1*ADnVCbUyVzo_yURKqAJP6g.png"
data-width="975" data-height="509" />
</figure>

These steps ensure a ready-to-use environment for scanning. For an
enhanced experience, screenshots of the installation process are
included.

**Scanning Process**

Once OpenVAS was configured, I created a scanning task to assess
CyberTech Solutions' network, targeting the IP address 10.6.6.12. The
steps included:

1.  [**Configuring the Target:**]{#a032}

-   [Added 10.6.6.12 as a new target under **Configuration \>
    Targets**.]{#c5bf}
-   [Selected "Full and Fast" as the scan configuration for efficiency
    and coverage.]{#7b79}

<figure id="42d1" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/1*Iyhe6rNeBLzM4hTu0tuFww.png"
class="graf-image" data-image-id="1*Iyhe6rNeBLzM4hTu0tuFww.png"
data-width="975" data-height="387" />
</figure>

2\. **Running the Scan:**

Created a new task under **Scans \> Tasks**, linked it to the target,
and started the scan.

<figure id="c258" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*_8eteu9pP3bXG3Z5MFiAMA.png"
class="graf-image" data-image-id="1*_8eteu9pP3bXG3Z5MFiAMA.png"
data-width="1915" data-height="874" />
</figure>

Monitored the progress and reviewed results upon completion.

<figure id="a099" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ZfHFa18vIb7wKgpaZarl9Q.png"
class="graf-image" data-image-id="1*ZfHFa18vIb7wKgpaZarl9Q.png"
data-width="975" data-height="505" />
</figure>

**Findings**

The scan yielded two low-severity vulnerabilities. Here are the details:

<figure id="9fe6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*AZK16IPA33CMgiDZ0cRjlg.png"
class="graf-image" data-image-id="1*AZK16IPA33CMgiDZ0cRjlg.png"
data-width="1029" data-height="250" />
</figure>

**Detailed Analysis**

<figure id="0ba5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*nOfNlRa_y3anl0TbvEgFMQ.png"
class="graf-image" data-image-id="1*nOfNlRa_y3anl0TbvEgFMQ.png"
data-width="975" data-height="546" />
</figure>

-   [**TCP Timestamps Information Disclosure**]{#d1b8}
-   [**Impact:** The remote host implements TCP timestamps, which can
    disclose uptime information.]{#e0ba}
-   [**Mitigation:** Add the following to /etc/sysctl.conf and apply
    it:net.ipv4.tcp_timestamps = 0sudo sysctl -p]{#a43e}
-   [**ICMP Timestamp Reply Information Disclosure**]{#2e7f}
-   [**Impact:** ICMP timestamp replies could be exploited in timing
    attacks.]{#2f05}
-   [**Mitigation:** Configure the firewall to block ICMP packets from
    untrusted networks.]{#00b0}

**Analysis and Prioritization**

Although both vulnerabilities were rated low, they could be leveraged in
larger attacks. Prioritizing these issues ensures a stronger security
posture:

1.  [**Disable TCP timestamps** to reduce information leakage.]{#5ce9}
2.  [**Restrict ICMP packets** using firewalls for an additional layer
    of defense.]{#06dd}

**Conclusion**

This vulnerability assessment highlights the value of tools like OpenVAS
in identifying and mitigating risks. Regular scans and proactive
remediation are essential to maintaining a secure network. By addressing
even low-severity issues, organizations can reduce their attack surface
and improve resilience against potential threats.
:::
:::
:::
:::

By [Kiplagatkelvin](https://medium.com/@kiplagatkelvin034){.p-author
.h-card} on [January 8, 2025](https://medium.com/p/4ceb3b3a5ed2).

[Canonical
link](https://medium.com/@kiplagatkelvin034/exploring-vulnerabilities-a-hands-on-assessment-with-openvas-gvm-4ceb3b3a5ed2){.p-canonical}

Exported from [Medium](https://medium.com) on February 13, 2025.
