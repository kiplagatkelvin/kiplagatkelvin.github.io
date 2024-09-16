---
title: "Elements of Security Operation"
description: This is a blog on what is required as the elements of  security operation, the elements here are mostly done by SOC annalyst in their day to day work.
date: 2023-05-12
draft: false
summary: "Operations here and there.."
tags: ["Security Operation"]
---

## ELEMENTS OF SECURITY OPERATION



## **Data Sources**

Some of the data sources that SOC use to monitor network for signs of intrusion and detect malicious behavior are;

1. **Server logs -** logs contain information about various activities, such as successful and failed login attempts,etc.there are many types of servers such as mail, web and domain controller in ms windows networks.
2. **DNS Activity - DNS** domain name system,protocol responsible for converting a domain name to an ip address
3. **Firewall logs -** firewall is a device that controls network traffic entering and leaving the network mainly by letting them through or blocking them.
4. **DHCP Logs - DHCP** stands for dynamic host configuration protocol, it is responsible for assigning ip addresses to devices that try to connect to a network.

## **SOC services**

SOC services include both reactive and proactive services.

The reactive services imply to the tasks initiated after detecting an intrusion or a malicious event, some of the services include;

1. **Monitor security posture -** is the basic role of  a SOC, furthermore, it includes monitoring the network and computers for security alerts and notifications and responding to them as them as the need dictatess.
2. **vulnerability management -** it involves finding vulnerabilities and patching them,however, the SOC can assist with this task but cannot execute it.
3. **Malware analysis -** here the SOC can monitor the behavior of the recovered malicious program in a controlled environment but more advanced analysis requires sending the program to a dedicated team.
4. **Intrusion detection -** IDS(an Intrusion Detection System) is used to detect and log intrusions and suspicious packets.A SOC’s job is to maintain its alerts and go through its logs as the need dictates.
5. **Reporting -** It is essential to report incidents and alarms. Reporting is necessary to ensure a smooth workflow and to support compliance requirements.

The proactive services refer to the tasks handled by the SOC without any indicator of an intrusion, they include;

1. **Network Security Monitoring(NSM) -** focuses on monitoring the network data and analyzing the traffic to detect signs of intrusions.
2. **Threat hunting -** threat intelligence focuses on learning about  potential adversaries and techniques to improve the company’s defense. The purpose would to establish a threat-informed defense.
