---
title: "Responder"
description: This is a writeup on the Responder machine from HackTheBox Starting point Tier1 level.
date: 2024-09-19
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Why did the hacker bring a map to the server? Because they were trying to locate the LFI and remotely call the RFI! 😄" # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier1, Starting point]
---
# Responder

![Untitled.jpg](Untitled.jpg)

## Task 1

When visiting the web service using the IP address, what is the domain that we are being redirected to?

First we had to scan the IP for open ports only to find port was open as shown below.

![image.png](image.png)

on visiting the web page, we are directed to the following domain.

![image.png](image%201.png)

unika.htb

In order to be able to access the webpage on our machine, we are required to add it to the 

```jsx
etc/hosts directory
```

![image.png](image%202.png)

and now we are able to see the page.

![image.png](image%203.png)

## Task 2

Which scripting language is being used on the server to generate webpages?

![image.png](image%204.png)

PHP

## Task 3

What is the name of the URL parameter which is used to load different language versions of the webpage?

![image.png](image%205.png)

page

## Task 4

Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "[//10.10.14.6/somefile](https://10.10.14.6/somefile)", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

![image.png](image%206.png)

../../../../../../../../windows/system32/drivers/etc/hosts

## Task 5

Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "[//10.10.14.6/somefile](https://10.10.14.6/somefile)", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

![image.png](image%207.png)

[//10.10.14.6/somefile](https://10.10.14.6/somefile)

## Task 6

What does NTLM stand for?

![image.png](image%208.png)

New Technology LAN Manager

## Task 7

Which flag do we use in the Responder utility to specify the network interface?

![image.png](image%209.png)

-I

## Task 8

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?.

![image.png](image%2010.png)

John The Ripper

## Task 9

What is the password for the administrator user?

For this section, we had to serve a file and set responder ready to catch a credential when the web-server tries to access the file from our machine by exploiting remote file inclusion vulnerability as shown below

![image.png](image%2011.png)

the file we were serving is called somefile that contains nothing at all

![image.png](image%2012.png)

After a while  when the web server was trying to access the file from our machine, responder caught some credentials of which seems to be of an admin.

![image.png](image%2013.png)

![image.png](image%2014.png)

Now next we shall try to crack the admin hash to get the password for the admin using john the ripper.

![image.png](image%2015.png)

After cracking it, we got the password, as seen below.

![image.png](image%2016.png)

badminton

## Task 10

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?

Here we are required to do further enumeration to get the other port that is open 

![image.png](image%2017.png)

5985

From the port above, it is clear that we can log in to the machine using evil-winrm to get our root flag.

![image.png](image%2018.png)

our flag was under the user mike’s Desktop as shown below

![image.png](image%2019.png)