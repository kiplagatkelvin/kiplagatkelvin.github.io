---
title: "Reedemer"
dscription: This is a writeup on Reedemer machine on HackTheBox starting point Tier0 level, have some fun while solving the box.
date: 2024-09-14
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Reedeming yourself" # Here you can write a small summary of the post if needed
tags: [HTB, Very Easy ]
categories: [Tier0, Starting point]
---
# Reedemer


![Untitled.png](Untitled.png)

## Task 1

**Which TCP port is open on the machine**

![image.png](image.png)

6379

## Task 2

Which service is running on the port that is open on the machine? 

![image.png](image%201.png)

Redis

## Task 3

What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database 

![image.png](image%202.png)

in-memory

[What is Redis Explained? | IBM](https://www.ibm.com/topics/redis)

## Task 4

Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments. 

![image.png](image%203.png)

https://redis.io/docs/latest/operate/rs/references/cli-utilities/redis-cli/

## Task 5

Which flag is used with the Redis command-line utility to specify the hostname? 

![image.png](image%204.png)

**-h**

the tool I used is a simplified version of man, a tool used to give more details about a cli tool,

below is the explanation of the tool

![image.png](image%205.png)

## Task 6

Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server? 

![image.png](image%206.png)

info

## Task 7

What is the version of the Redis server being used on the target machine? 

![image.png](image%207.png)

**5.0.7**

## Task 8

Which command is used to select the desired database in Redis? 

![image.png](image%208.png)

https://redis.io/docs/latest/commands/

## Task 9

How many keys are present inside the database with index 0? 

![image.png](image%209.png)

**4**

## Task 10

Which command is used to obtain all the keys in a database? 

![image.png](image%2010.png)

https://redis.io/docs/latest/commands/keys/

## Task 11

Submit root flag 

![image.png](image%2011.png)