---
title: "Crocodile"
description: this is a writeup on Crocodile starting point Tier 1 level machine on HackTheBox
date: 2024-09-18
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Croco, why did the FTP server break up with the client? Because it just couldn't handle all the passive aggression! 😄" # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier1, Starting point]
---
# Crocodile


![Untitled.jpg](Untitled.jpg)

## Task 1

What Nmap scanning switch employs the use of default scripts during a scan? 

![image.png](image.png)

-sC

## Task 2

What service version is found to be running on port 21?

![image.png](image%201.png)

vsftpd 3.0.3 

## Task 3

What FTP code is returned to us for the "Anonymous FTP login allowed" message? 

![image.png](image%202.png)

230

## Task 4

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously? 

![image.png](image%203.png)

anonymous

## Task 5

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server? 

![image.png](image%204.png)

Get command but to download all files once, one can use the command mget as seen above.

## Task 6

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?

![image.png](image%205.png)

admin

## Task 7

What version of Apache HTTP Server is running on the target host?

![image.png](image%206.png)

Apache httpd 2.4.41 

## Task 8

What switch can we use with Gobuster to specify we are looking for specific filetypes? 

![image.png](image%207.png)

-x

## Task 9

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?

![image.png](image%208.png)

login.php

After checking, the two files we downloaded, we were adble to get the admin and the password for the as seen as seen below.

![image.png](image%209.png)

we used the above credentials to log in to the platform and we got our flag.

![image.png](image%2010.png)