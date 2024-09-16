---
title: "Dancing"
description: This is a writeup on Dancing machine on HackTheBox starting point Tier0.
date: 2024-09-13
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Only the flexible to dance." # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier0, Starting point]
---
# Dancing


![image.png](image.png)

## Introduction

For this machine we shall be comprising SMB service in order to get our root flag and pawn the machine. Furthermore, there is a share that allows access without password.

## Enumeration

We shall first start by confirming that we can access the IP by pinging it.

![image.png](image%201.png)

As we can see the host is reachable from our attacking machine, we shall therefore go ahead and enumerate the machine using nmap to see services that are running as shown below.

![image.png](image%202.png)

As seen above we have SMB service open on port 445. Without going further, we can try to list the shares available on the host as seen below.

![image.png](image%203.png)

The syntax used to list the shares as seen above is **smbclient -L ///<IP>. The -L flag is used to specify that we want to list all shares on the host. Moreover, as seen above the WorkShares share can be accessed without a password**

## Accessing the WorkShares

We will be downloading the contents of the share using the get command but first, we shall starting enumerating the directories in the share.

![image.png](image%204.png)

As seen above, we have two directories, Amy.J and James.P, I accessed the Amy.J directory and found a worknotes.txt file and went ahead to download it. We shall then go to the James.P directory and see what content is in the directory.

![image.png](image%205.png)

As seen above the James.P directory has the flag, and opening the worknotes.txt file we are given some instructions to what seems like how to secure the ftp server, start an apache server on our machine and setup winrm to be able to connect to the machine.

### Root

![image.png](image%206.png)

As seen below we have been able to get the root flag and compromised the SMB server.

# Conclusion

In this lab we were able to exploit a share that has no password set to it, moreover, we were able to root the machine by accessing the root flag from the share.

![image.png](image%207.png)