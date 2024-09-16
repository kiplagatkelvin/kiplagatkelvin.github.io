---
title: "Fawn"
description: This a writeup on the Fawn machine from HackTheBox starting point Tier0 level, heave some fun reading it.
date: 2024-09-12
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "FTP" # Here you can write a small summary of the post if needed
tags: [HTB, FTP, Very Easy]
categories: [Tier0, Starting point]
---
# Fawn


![images.jpg](images.jpg)

# Introduction

For this machine we shall be exploiting the ftp service to get the root flag of the machine. However, we will first need to do the following.

1. Enumeration of the machine
2. Service discovery
3. FTP anonymous log in

# Enumeration

Before enumerating, we shall start by checking if the IP is reachable from our attacking machine by pinging it as shown below.

![image.png](image.png)

After enumeration, we were able to find out that  ftp service is up and running as shown below.

![image.png](image%201.png)

As seen above the host is reachable from our attacking machine. We shall now enumerate the host using nmap using the following syntax as shown below

**Nmap -sCV <IP>**

Furthermore, anonymous log in is allowed hence, we can easily now get our flag and pawn the machine.

# FTP Log in

After that we can now easily login and get our flag from the server easily as shown below.

![image.png](image%202.png)

Below as we can see, we have transferred the flag to our machine

![image.png](image%203.png)

Now we can get the flag and pawn the machine.

![image.png](image%204.png)

With that we have successfully pawned the machine.

![image.png](image%205.png)

We have now successfully pawned the machine

# Conclusion

In this lab we were able to learn that ftp is an insecure service for storing and transmitting of files over the internet, the secure service of it is **SFTP.**