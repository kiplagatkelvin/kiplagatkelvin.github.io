---
title: "Sequel"
description: This is a writeup on the Sequel starting point machine Tier1 level
date: 2024-09-17
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Why did the database administrator break up with the SQL query? Because it had too many joins! 😄" # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier1, Starting point]
---
# Sequel


![Untitled.jpg](Untitled.jpg)

## Task 1

During our scan, which port do we find serving MySQL? 

![image.png](image.png)

3306

## Task 2

 What community-developed MySQL version is the target running? 

![image.png](image%201.png)

MariaDB

## Task 3

When using the MySQL command line client, what switch do we need to use in order to specify a login username? 

![image.png](image%202.png)

-u from [Mysql](https://dev.mysql.com/doc/refman/8.4/en/connecting.html)

## Task 4

Which username allows us to log into this MariaDB instance without providing a password? 

![image.png](image%203.png)

root

## Task 5

In SQL, what symbol can we use to specify within the query that we want to display everything inside a table? 

![image.png](image%204.png)

*

## Task 6

In SQL, what symbol do we need to end each query with? 

![image.png](image%205.png)

;

## Task 7

There are three databases in this MySQL instance that are common across all MySQL instances. What is the name of the fourth that's unique to this host? 

![image.png](image%206.png)

htb

To get the root flag, we had to enumerate the htb box as shown below and we found our flag.

We have two tables, users and config.

![image.png](image%207.png)

Selecting the data in users, we found nothing of interest, aside form the users

![image.png](image%208.png)

But for the config table, we found our flag

![image.png](image%209.png)