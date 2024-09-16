---
title: "Appointment"
date: 2024-09-16
description: This is a writeup on Appoint machine from HackTheBox starting point Tier1.
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Waiting on the line." # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier1, Starting point]
---
# Appointment


![Untitled.png](Untitled.png)

## Task 1

What does the acronym SQL stand for? 

![image.png](image.png)

Structured Query Language

## Task 2

What is one of the most common type of SQL vulnerabilities? 

![image.png](image%201.png)

**SQL injection**

## Task 3

What is the 2021 OWASP Top 10 classification for this vulnerability? 

![image.png](image%202.png)

**A03:2021-Injection**

## Task 4

What does Nmap report as the service and version that are running on port 80 of the target? 

![image.png](image%203.png)

Apache httpd 2.4.38 

## **Task 5**

What is the standard port used for the HTTPS protocol? 

![image.png](image%204.png)

443

## Task 6

 What is a folder called in web-application terminology? 

![image.png](image%205.png)

Directories

## Task 7

What is the HTTP response code is given for 'Not Found' errors? 

![image.png](image%206.png)

404

## Task 8

Gobuster is one tool used to brute force directories on a webserver. What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains? 

![image.png](image%207.png)

dir

## Task 9

 What single character can be used to comment out the rest of a line in MySQL? 

![image.png](image%208.png)

#

## Task 10

If user input is not handled carefully, it could be interpreted as a comment. Use a comment to login as admin without knowing the password. What is the first word on the webpage returned? 

![image.png](image%209.png)

Congratulations

After I visited the site, I went ahead and used the payload admin’ # on the username field and then put some gibberish data on the password field  and was able to log in. I got my payload from [PayloadAllThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/MySQL%20Injection.md#mysql-error-based).

And just like that, we were able to pawn the machine .