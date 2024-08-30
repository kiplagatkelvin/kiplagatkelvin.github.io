---
title: "Digital Forensics and Incidence Response"
date: 2024-01-10
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Credit to TryHackMe" # Here you can write a small summary of the post if needed
tags: [DFIR]
categories: [Blue Team, TryHackMe]
---
# Introduction
[TryHackMe](https://tryhackme.com/signup?referrer=6325877cfcc474005111479e) has provide a well summarised and understood content that can be applied into real world scenarios. Furthermore, to acquire the practical skills, one can try the hands on labs in the platform.

# Digital Forensics and Incident Response


## What is DFIR?

As already mentioned, DFIR stands for Digital Forensics and Incident 
Response. This field covers the collection of forensic artifacts from 
digital devices such as computers, media devices, and smartphones to 
investigate an incident. This field helps Security Professionals 
identify footprints left by an attacker when a security incident occurs,
 use them to determine the extent of compromise in an environment, and 
restore the environment to the state it was before the incident 
occurred.

## The need for DFIR

DFIR helps security professionals in various ways, some of which are summarized below:

- Finding evidence of attacker activity in the network and sifting false alarms from actual incidents.
- Robustly removing the attacker, so their foothold from the network no longer remains.
- Identifying the extent and timeframe of a breach. This helps in communicating with relevant stakeholders.
- Finding the loopholes that led to the breach. What needs to be changed to avoid the breach in the future?
- Understanding attacker behavior to pre-emptively block further intrusion attempts by the attacker.
- Sharing information about the attacker with the community.

## Who performs DFIR?

As the name suggests, DFIR requires expertise in both Digital 
Forensics and Incident Response. Dividing these two fields this way, the
 following skillset is needed to become a DFIR professional:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6e2d93818b9a293a246d9db91fad6aea.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6e2d93818b9a293a246d9db91fad6aea.png)

- **Digital Forensics:** These professionals are experts in identifying forensic artifacts or evidence of human activity in digital devices.
- **Incident Response:** Incident responders are experts in cybersecurity and leverage forensic
information to identify the activity of interest from a security
perspective.****

DFIR professionals know about Digital 
Forensics and cybersecurity and combine these domains to achieve their 
goals. Digital Forensics and Incident Response domains are often 
combined because they are highly interdependent. Incident Response 
leverages knowledge gained from Digital Forensics. Similarly, Digital 
Forensics takes its goals and scop

## Artifacts:

Artifacts are pieces of evidence that point to an activity performed 
on a system. When performing DFIR, artifacts are collected to support a 
hypothesis or claim about attacker activity. For example, if we are to 
claim that the attacker used Windows registry keys to maintain 
persistence on a system, we can use the said registry key to support our
 claim. In this case, the mentioned registry key will be considered an 
artifact. Artifact collection is, therefore, an essential part of the 
DFIR process. Artifacts can be collected from the Endpoint or Server's file system, memory, or network activity.

Most
 of the time, enterprise environments mainly consist of Windows and 
Linux Operating Systems. To learn more about the forensic artifacts in 
these Operating Systems, you can head to the [Windows Forensics 1](https://tryhackme.com/room/windowsforensics1), [Windows Forensics 2](https://tryhackme.com/room/windowsforensics2), or the [Linux Forensics](https://tryhackme.com/room/linuxforensics)
 room. Windows systems are primarily used for endpoints and server 
use-cases, like Active Directory Domain Controllers or MS Exchange email
 servers. Enterprises primarily use Linux systems in the capacity of 
servers hosting some service, for example, web servers or database 
servers.

## Evidence Preservation:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3b232e0148db97109a77afc200c5d177.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3b232e0148db97109a77afc200c5d177.png)

When performing DFIR, we must maintain the integrity of the evidence 
we are collecting. For this reason, certain best practices are 
established in the industry. We must note that any forensic analysis 
contaminates the evidence. Therefore, the evidence is first collected 
and write-protected. Then, a copy of the write-protected evidence is 
used for analysis. This process ensures that our original evidence is 
not contaminated and remains safe while analyzing. If our copy under 
investigation gets corrupted, we can always return and make a new copy 
from the evidence we had preserved.

## Chain of custody:

Another critical aspect of maintaining the integrity of evidence is 
the chain of custody. When the evidence is collected, it must be made 
sure that it is kept in secure custody. Any person not related to the 
investigation must not possess the evidence, or it will contaminate the 
chain of custody of the evidence. A contaminated chain of custody raises
 questions about the integrity of the data and weakens the case being 
built by adding unknown variables that can't be solved. For example, 
suppose a hard drive image, while being transferred from the person who 
took the image to the person who will perform the analysis, gets into 
the hands of a person who is not qualified to handle such evidence. In 
that case, we can't be sure if he dealt with the evidence correctly and 
hence didn't contaminate the evidence with his activity.

## Order of volatility:

Digital evidence is often volatile, i.e., it can be lost forever if 
not captured in time. For example, data in a computer system's memory 
(RAM) will be lost when the computer is shut down since the RAM keeps 
data only as long as it remains powered on. Some sources are more 
volatile as compared to others. For example, a hard drive is persistent 
storage and maintains the data even if power is lost. Therefore, a hard 
drive is less volatile than RAM. While performing DFIR, it is vital to 
understand the order of volatility of the different evidence sources to 
capture and preserve accordingly. In the example above, we will need to 
preserve the RAM before preserving the hard drive since we might lose 
data in the RAM if we don't prioritize it.

## Timeline creation:

Once we have collected the artifacts and maintained their integrity, 
we need to present them understandably to fully use the information 
contained in them. A timeline of events needs to be created for 
efficient and accurate analysis. This timeline of events puts all the 
activities in chronological order. This activity is called timeline 
creation. Timeline creation provides perspective to the investigation 
and helps collate information from various sources to create a story of 
how things happened.

**DFIR TOOLS**

## Eric Zimmerman's tools:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1a89eb9ecd42f493fcdf7d105b41dba7.jpg](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1a89eb9ecd42f493fcdf7d105b41dba7.jpg)

Eric
 Zimmerman is a security researcher who has written a few tools to help 
perform forensic analysis on the Windows platform. These tools help the 
registry, file system, timeline, and many other analyses. To learn more 
about these tools, you can check out the [Windows Forensics 1](https://tryhackme.com/room/windowsforensics1) and [Windows Forensics 2](https://tryhackme.com/room/windowsforensics2) rooms, where these tools are discussed concerning the different artifacts found in the Windows Operating System.

## KAPE:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/0c82470617c7ebdbfcf956ee9d9547cf.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/0c82470617c7ebdbfcf956ee9d9547cf.png)

Kroll
 Artifact Parser and Extractor (KAPE) is another beneficial tool by Eric
 Zimmerman. This tool automates the collection and parsing of forensic 
artifacts and can help create a timeline of events. You can check out 
the [KAPE room](https://tryhackme.com/room/kape) to learn more about KAPE.

## Autopsy:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/ea383ef541cfaf0cbbc40a64af0f47ba.jpg](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/ea383ef541cfaf0cbbc40a64af0f47ba.jpg)

Autopsy is an open-source forensics platform that helps analyze data 
from digital media like mobile devices, hard drives, and removable 
drives. Various plugins for autopsy speed up the forensic process and 
extract and present valuable information from the raw data sources. 
TryHackMe's [Autopsy room](https://tryhackme.com/room/btautopsye0) can help if you want to learn more about it.

## Volatility:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c25405634d4fda8271d8df63a252d16a.jpg](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c25405634d4fda8271d8df63a252d16a.jpg)

Volatility is a tool that helps perform memory analysis for memory 
captures from both Windows and Linux Operating Systems. It is a powerful
 tool that can help extract valuable information from the memory of a 
machine under investigation. You can learn more about Volatility in the [Volatility room](https://tryhackme.com/room/volatility).

## Redline:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/622d38cddd96ddcc98b8002da9920eec.jpg](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/622d38cddd96ddcc98b8002da9920eec.jpg)

Redline is an incident response tool developed and freely distributed
 by FireEye. This tool can gather forensic data from a system and help 
with collected forensic information. You can learn more about Redline in
 the [Redline room](https://tryhackme.com/room/btredlinejoxr3d).

## Velociraptor:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fca62b1d63bfcd0e11557606e451c412.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fca62b1d63bfcd0e11557606e451c412.png)

Velociraptor is an advanced endpoint-monitoring, forensics, and 
response platform. It is open-source but very powerful. TryHackMe has 
created a [Velociraptor room](https://tryhackme.com/room/velociraptorhp) for you to learn more about it.

**The Incident Response process**

In Security Operations,
 the prominent use of Digital Forensics is to perform Incident Response.
 We will learn the Incident Response process and observe how Digital 
Forensics helps in the IR process in this task.

Different organizations have published standardized methods to perform Incident Response. NIST has defined a process in their [SP-800-61 Incident Handling guide](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf), which has the following steps:

1. Preparation
2. Detection and Analysis
3. Containment, Eradication, and Recovery
4. Post-incident Activity

Similarly, SANS has published an [Incident Handler's handbook](https://www.sans.org/white-papers/33901/). The handbook defines the steps as follows:

1. Preparation
2. Identification
3. Containment
4. Eradication
5. Recovery
6. Lessons Learned

The
 steps defined by SANS are often summarized as the acronym PICERL, 
making them easy to remember. We can see that the steps specified by 
SANS and NIST are identical. While NIST combines Containment, 
Eradication, and Recovery, SANS separates them into different steps. **Post-incident activity** and **Lessons learned** can be comparable, while **Identification** and **Detection and Analysis** have the same implications.

Now
 that we understand that the two processes are similar let's learn 
briefly what the different steps mean. We explain the PICERL steps as 
they are easier to remember by the acronym, but as described above, they
 are identical to the steps defined by NIST.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f714eea27bb41e82ce3d3e56ea41a9ab.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f714eea27bb41e82ce3d3e56ea41a9ab.png)

1. **Preparation**: Before an incident happens, preparation needs to be done so that everyone is
ready in case of an incident. Preparation includes having the required
people, processes, and technology to prevent and respond to incidents.
2. **Identification**: An incident is identified through some indicators in the identification
phase. These indicators are then analyzed for False Positives,
documented, and communicated to the relevant stakeholders.
3. **Containment**: In this phase, the incident is contained, and efforts are made to limit
its effects. There can be short-term and long-term fixes for containing
the threat based on forensic analysis of the incident that will be a
part of this phase.
4. **Eradication**: Next, the threat
is eradicated from the network. It has to be ensured that a proper
forensic analysis is performed and the threat is effectively contained
before eradication. For example, if the entry point of the threat actor
into the network is not plugged, the threat will not be effectively
eradicated, and the actor can gain a foothold again.
5. **Recovery**: Once the threat is removed from the network, the services that had been
disrupted are brought back as they were before the incident happened.
6. **Lessons Learned**: Finally, a review of the incident is performed, the incident is documented, and
steps are taken based on the findings from the incident to make sure
that the team is better prepared for the next time an incident occurs.

## **WINDOWS FORENSICS**

**Introduction to Computer Forensics for Windows:**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/35c1c080687b084a9ebbaca0a4e9cfc9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/35c1c080687b084a9ebbaca0a4e9cfc9.png)

Computer forensics is an essential field of cyber security that involves gathering evidence of activities performed on computers.
 It is a part of the wider Digital Forensics field, which deals with 
forensic analysis of all types of digital devices, including recovering,
 examining, and analyzing data found in digital devices. The 
applications of digital and computer forensics are wide-ranging, from 
the legal sphere, where it is used to support or refute a hypothesis in a
 civil or criminal case, to the private sphere, where it helps in 
internal corporate investigations and incident and intrusion analysis.

A perfect example of Digital Forensics solving a criminal case is the [BTK serial killer](https://en.wikipedia.org/wiki/Dennis_Rader)
 case. This case had gone cold for more than a decade when the killer 
started taunting the police by sending letters. The case took a major 
turn when he sent a floppy disk to a local news station that was later 
taken to into evidence by the police. The police were able to recover a 
deleted word document on the drive, and using the metadata and some 
other evidence, they pinpointed and arrested him.

Microsoft Windows is by large the most used Desktop Operating System right now. Private users and Enterprises prefer it,
 and it currently holds roughly 80% of the Desktop market share. This 
means that it is important to know how to perform forensic analysis on 
Microsoft Windows for someone interested in Digital Forensics. In this 
module, we will learn about the different ways we can gather forensic 
data from the Windows Registry and make conclusions about the activity 
performed on a Windows system based on this data.

# **Forensic Artifacts:**

When
 performing forensic analysis, you will often hear the word 'artifact'. 
Forensic artifacts are essential pieces of information that provide 
evidence of human activity. For example, during the investigation of a 
crime scene, fingerprints, a broken button of a shirt or coat, the tools
 used to perform the crime are all considered forensic artifacts. All of
 these artifacts are combined to recreate the story of how the crime was
 committed.

In computer forensics, forensic artifacts can be 
small footprints of activity left on the computer system. On a Windows 
system, a person's actions can be traced back quite accurately using 
computer forensics because of the various artifacts a Windows system 
creates for a given activity. These artifacts often reside in locations 
'normal' users won't typically venture to. For our purposes, these 
artifacts can be analyzed to provide the trial of activity for an 
investigation.

**So is my computer spying on me?**

What do you think?

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/720842074f8b1f89e0eeae132a55424a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/720842074f8b1f89e0eeae132a55424a.png)

A
 Windows system keeps track of a lot of activity performed by a user. 
But is all that tracking for malicious purposes, or is there another 
reason for that? As we'll see in this room, the filesystem components 
that forensic experts deem artifacts primarily originated from 
Microsoft's efforts to improve the user's experience.

Assuming the
 same build of Windows is installed on a system, excluding the actions 
taken during installation, the out-of-the-box experience is similar for 
all users. However, with time, each user personalizes their computer 
according to their preferences. These preferences include the Desktop 
layout and icons, the bookmarks in the internet browser, the name of the
 user, installing of different applications, and logging in to different
 accounts for each of these applications and other accounts using the 
internet browser.

Windows saves these preferences to make your 
computer more personalized. However, forensic investigators use these 
preferences as artifacts to identify the activity performed on a system.
 So while your computer might be spying on you, it is not for the 
explicit reason of spying, instead to make it more pleasant to use the 
computer according to your taste. But that same information is used by 
forensic investigators to perform forensic analysis. As we move through 
this room, we'll see that Windows stores these artifacts in different 
locations throughout the file system such as in the registry, a user's 
profile directory, in application-specific files, etc.

**Windows Registry and Forensics**

**Windows Registry:**

The Windows Registry is a collection of databases that contains the 
system's configuration data. This configuration data can be about the 
hardware, the software, or the user's information. It also includes data
 about the recently used files, programs used, or devices connected to 
the system. As you can understand, this data is beneficial from a 
forensics standpoint. Throughout this room, we will learn ways to read 
this data to identify the required information about the system. You can
 view the registry using regedit.exe, a built-in Windows utility to view
 and edit the registry. We'll explore other tools to learn about the 
registry in the upcoming tasks.

The Windows registry consists of Keys and Values. When you open the 
regedit.exe utility to view the registry, the folders you see are 
Registry Keys. Registry Values are the data stored in these Registry 
Keys. A [Registry Hive](https://docs.microsoft.com/en-us/windows/win32/sysinfo/registry-hives#:~:text=Registry%20Hives.%20A%20hive%20is%20a%20logical%20group,with%20a%20separate%20file%20for%20the%20user%20profile.) is a group of Keys, subkeys, and values stored in a single file on the disk.

**Structure of the Registry:**

The registry on any Windows system contains the following five root keys:

1. HKEY_CURRENT_USER
2. HKEY_USERS
3. HKEY_LOCAL_MACHINE
4. HKEY_CLASSES_ROOT
5. HKEY_CURRENT_CONFIG

You can view these keys when you open the `regedit.exe` utility. To open the registry editor, press the Windows key and the R key simultaneously. It will open a `run` prompt that looks like this:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9d33389f2fd0445a63e75dce3f6d7a88.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9d33389f2fd0445a63e75dce3f6d7a88.png)

In this prompt, type `regedit.exe`, and you will be greeted with the registry editor window. It will look something like this:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e14ef3193fce1f4b35c37a96862d71da.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e14ef3193fce1f4b35c37a96862d71da.png)

Here you can see the root keys in the left pane in a tree view that 
shows the included registry keys, and the values in the selected key are
 shown in the right pane. You can right-click on the value shown in the 
right pane and select properties to view the properties of this value.

Here is how Microsoft defines each of these root keys. For more 
detail and information about the following Windows registry keys, please
 visit [Microsoft's documentation](https://docs.microsoft.com/en-US/troubleshoot/windows-server/performance/windows-registry-advanced-users).

| Folder/predefined key | Description |
| --- | --- |
| **HKEY_CURRENT_USER** | Contains the root of the configuration information for the user who is
                currently logged on. The user's folders, screen colors, and Control Panel settings are stored here.
                This information is associated with the user's profile. This key is sometimes abbreviated as
                HKCU. |
| **HKEY_USERS** | Contains all the actively loaded user profiles on the computer.
                HKEY_CURRENT_USER is a subkey of HKEY_USERS. HKEY_USERS is sometimes abbreviated as HKU. |
| **HKEY_LOCAL_MACHINE** | Contains configuration information particular to the computer (for any
                user). This key is sometimes abbreviated as HKLM. |
| **HKEY_CLASSES_ROOT** | Is a subkey of `HKEY_LOCAL_MACHINE\Software`. The information
                that is stored here makes sure that the correct program opens when you open a file by using Windows
                Explorer. This key is sometimes abbreviated as HKCR.
 Starting with Windows 2000, this information is
                stored under both the HKEY_LOCAL_MACHINE and HKEY_CURRENT_USER keys. The
                `HKEY_LOCAL_MACHINE\Software\Classes` key contains default settings that can apply to all
                users on the local computer. The `HKEY_CURRENT_USER\Software\Classes` key has settings
                that override the default settings and apply only to the interactive user.
The HKEY_CLASSES_ROOT key
                provides a view of the registry that merges the information from these two sources.
                HKEY_CLASSES_ROOT also provides this merged view for programs that are designed for earlier versions
                of Windows. To change the settings for the interactive user, changes must be made under
                `HKEY_CURRENT_USER\Software\Classes` instead of under HKEY_CLASSES_ROOT.
To change the
                default settings, changes must be made under `HKEY_LOCAL_MACHINE\Software\Classes` .If you
                write keys to a key under HKEY_CLASSES_ROOT, the system stores the information under
                `HKEY_LOCAL_MACHINE\Software\Classes`.
If you write values to a key under
                HKEY_CLASSES_ROOT, and the key already exists under `HKEY_CURRENT_USER\Software\Classes`,
                the system will store the information there instead of under
                `HKEY_LOCAL_MACHINE\Software\Classes`. |
| **HKEY_CURRENT_CONFIG** | Contains information about the hardware profile that is used by the local
                computer at system startup. |

**Accessing registry hives offline**

If you are accessing a live system, you will be able to access the 
registry using regedit.exe, and you will be greeted with all of the 
standard root keys we learned about in the previous task. However, if 
you only have access to a disk image, you must know where the registry 
hives are located on the disk. The majority of these hives are located 
in the `C:\Windows\System32\Config` directory and are:

1. **DEFAULT** (mounted on `HKEY_USERS\DEFAULT`)
2. **SAM** (mounted on `HKEY_LOCAL_MACHINE\SAM`)
3. **SECURITY** (mounted on `HKEY_LOCAL_MACHINE\Security`)
4. **SOFTWARE** (mounted on `HKEY_LOCAL_MACHINE\Software`)
5. **SYSTEM** (mounted on `HKEY_LOCAL_MACHINE\System`)

**Hives containing user information:**

Apart from these hives, two other hives containing user information 
can be found in the User profile directory. For Windows 7 and above, a 
user’s profile directory is located in `C:\Users\<username>\` where the hives are:

1. **NTUSER.DAT** (mounted on HKEY_CURRENT_USER when a user logs in)
2. **USRCLASS.DAT** (mounted on HKEY_CURRENT_USER\Software\CLASSES)

The USRCLASS.DAT hive is located in the directory `C:\Users\<username>\AppData\Local\Microsoft\Windows`.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3ffadf20ebe241040d659958db115c2f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3ffadf20ebe241040d659958db115c2f.png)

The NTUSER.DAT hive is located in the directory `C:\Users\<username>\`.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f3091f38f680b418f89cf79128d1933c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f3091f38f680b418f89cf79128d1933c.png)

Remember that NTUSER.DAT and USRCLASS.DAT are hidden files.

**The Amcache Hive:**

Apart from these files, there is another very important hive called the AmCache hive. This hive is located in `C:\Windows\AppCompat\Programs\Amcache.hve`. Windows creates this hive to save information on programs that were recently run on the system.

**Transaction Logs and Backups:**

Some other very vital sources of forensic data are the registry 
transaction logs and backups. The transaction logs can be considered as 
the journal of the changelog of the registry hive. Windows often uses 
transaction logs when writing data to registry hives. This means that 
the transaction logs can often have the latest changes in the registry 
that haven't made their way to the registry hives themselves. The 
transaction log for each hive is stored as a .LOG file in the same 
directory as the hive itself. It has the same name as the registry hive,
 but the extension is .LOG. For example, the transaction log for the SAM
 hive will be located in `C:\Windows\System32\Config` in the 
filename SAM.LOG. Sometimes there can be multiple transaction logs as 
well. In that case, they will have .LOG1, .LOG2 etc., as their 
extension. It is prudent to look at the transaction logs as well when 
performing registry forensics.

Registry backups are the opposite of Transaction logs. These are the backups of the registry hives located in the `C:\Windows\System32\Config` directory. These hives are copied to the `C:\Windows\System32\Config\RegBack`
 directory every ten days. It might be an excellent place to look if you
 suspect that some registry keys might have been deleted/modified 
recently.

**Data Acquisition**

When performing 
forensics, we will either encounter a live system or an image taken of 
the system. For the sake of accuracy, it is recommended practice to 
image the system or make a copy of the required data and perform 
forensics on it. This process is called data acquisition. Below we 
discuss different ways to acquire registry data from a live system or a 
disk image:

Though we can view the registry through the 
registry editor, the forensically correct method is to acquire a copy of
 this data and perform analysis on that. However, when we go to copy the
 registry hives from `%WINDIR%\System32\Config`, we cannot because it is a restricted file. So, what to do now?

For acquiring these files, we can use one of the following tools:

**KAPE:**

[KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape)
 is a live data acquisition and analysis tool which can be used to 
acquire registry data. It is primarily a command-line tool but also 
comes with a GUI.
 The below screenshot shows what the KAPE GUI looks like. We have 
already selected all the settings to extract the registry data using 
KAPE in this screenshot. We will learn more about collecting forensic 
artifacts using KAPE in a dedicated KAPE room.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9ec88ef00c70bf2c854b4c66afbf5470.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9ec88ef00c70bf2c854b4c66afbf5470.png)

**Autopsy:**

[Autopsy](https://www.autopsy.com/) gives
 you the option to acquire data from both live systems or from a disk 
image. After adding your data source, navigate to the location of the 
files you want to extract, then right-click and select the Extract 
File(s) option. It will look similar to what you see in the screenshot 
below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/5faf350078f7e7e1d1400f46e11e74a9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/5faf350078f7e7e1d1400f46e11e74a9.png)

**FTK Imager:**

[FTK Imager](https://www.exterro.com/ftk-imager) is
 similar to Autopsy and allows you to extract files from a disk image or
 a live system by mounting the said disk image or drive in FTK Imager. 
Below you can see the option to Export files as highlighted in the 
screenshot.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bb82d24f00e15c3d16b352cdec57f256.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bb82d24f00e15c3d16b352cdec57f256.png)

Another
 way you can extract Registry files from FTK Imager is through the 
Obtain Protected Files option. This option is only available for live systems and is highlighted
 in the screenshot below. This option allows you to extract all the 
registry hives to a location of your choosing. However, it will not copy
 the `Amcache.hve` file, which is often necessary to investigate evidence of programs that were last executed.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8292e36577413227ec24446ae1c72a35.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8292e36577413227ec24446ae1c72a35.png)

**Exploring Windows Registry**

Once
 we have extracted the registry hives, we need a tool to view these 
files as we would in the registry editor. Since the registry editor only
 works with live systems and can't load exported hives, we can use the 
following tools:

**Registry Viewer:**

As we can see in the screenshot below, [AccessData's Registry Viewer](https://accessdata.com/product-download/registry-viewer-2-0-0) has
 a similar user interface to the Windows Registry Editor. There are a 
couple of limitations, though. It only loads one hive at a time, and it 
can't take the transaction logs into account.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/888afb265fa265d771dc02ae8f610dc0.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/888afb265fa265d771dc02ae8f610dc0.png)

**Zimmerman's Registry Explorer:**

Eric Zimmerman has developed a handful of [tools](https://ericzimmerman.github.io/#!index.md)
 that are very useful for performing Digital Forensics and Incident 
Response. One of them is the Registry Explorer. It looks like the below 
screenshot. It can load multiple hives simultaneously and add data from 
transaction logs into the hive to make a more 'cleaner' hive with more 
up-to-date data. It also has a handy 'Bookmarks' option containing 
forensically important registry keys often sought by forensics 
investigators. Investigators can go straight to the interesting registry
 keys and values with the bookmarks menu item. We will explore these in 
more detail in the upcoming tasks.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/414dee2639b9456334c9580aacdc2be1.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/414dee2639b9456334c9580aacdc2be1.png)

**RegRipper:**

[RegRipper](https://github.com/keydet89/RegRipper3.0)
 is a utility that takes a registry hive as input and outputs a report 
that extracts data from some of the forensically important keys and 
values in that hive. The output report is in a text file and shows all 
the results in sequential order.

RegRipper is available in both a CLI and GUI form which is shown in the screenshot below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/70e6fef3920cb9b0443bc1fa9d9fac5d.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/70e6fef3920cb9b0443bc1fa9d9fac5d.png)

One
 shortcoming of RegRipper is that it does not take the transaction logs 
into account. We must use Registry Explorer to merge transaction logs 
with the respective registry hives before sending the output to 
RegRipper for a more accurate result.

**System Information and System Accounts**

Now that we have learned how to read registry data, let's find out 
where to look in the registry to perform our forensic analysis.

When
 we start performing forensic analysis, the first step is to find out 
about the system information. This task will cover gathering information
 related to a machine's System and Account information.

**OS**

If we only have triage data to perform forensics, we can determine the OS version from which this data was pulled through the registry. To find the OS version, we can use the following registry key:

`SOFTWARE\Microsoft\Windows NT\CurrentVersion`

This is how Registry Explorer shows this registry key. Take a look and answer Question # 1.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1362c5a15d1879a1a5a5a5237a426108.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1362c5a15d1879a1a5a5a5237a426108.png)

**Current control set:**

The
 hives containing the machine’s configuration data used for controlling 
system startup are called Control Sets. Commonly, we will see two 
Control Sets, ControlSet001 and ControlSet002, in the SYSTEM hive on a 
machine. In most cases, ControlSet001 will point to the Control Set that
 the machine booted with, and ControlSet002 will be the `last known good` configuration. Their locations will be:

`SYSTEM\ControlSet001`

`SYSTEM\ControlSet002`

Windows creates a volatile Control Set when the machine is live, called the CurrentControlSet (`HKLM\SYSTEM\CurrentControlSet`).
 For getting the most accurate system information, this is the hive that
 we will refer to. We can find out which Control Set is being used as 
the CurrentControlSet by looking at the following registry value:

`SYSTEM\Select\Current`

Similarly, the `last known good` configuration can be found using the following registry value:

`SYSTEM\Select\LastKnownGood`

This is how it looks like in Registry Explorer. Take a look and answer Question # 2.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f3b34b5e44e98e76034b76fc608a7670.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f3b34b5e44e98e76034b76fc608a7670.png)

It
 is vital to establish this information before moving forward with the 
analysis. As we will see, many forensic artifacts we collect will be 
collected from the Control Sets.

**Computer Name:**

It
 is crucial to establish the Computer Name while performing forensic 
analysis to ensure that we are working on the machine we are supposed to
 work on. We can find the Computer Name from the following location:

`SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`

Registry Explorer shows it like this. Take a look and answer Question # 3:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bb73d7942a6e30cb96e78926ad36fddb.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bb73d7942a6e30cb96e78926ad36fddb.png)

**Time Zone Information:**

For
 accuracy, it is important to establish what time zone the computer is 
located in. This will help us understand the chronology of the events as
 they happened. For finding the Time Zone Information, we can look at 
the following location:

`SYSTEM\CurrentControlSet\Control\TimeZoneInformation`

Here's how it looks in Registry Explorer. Take a look and answer Question # 4.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/08d5e86bb3a5be6057928a8062cf7de3.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/08d5e86bb3a5be6057928a8062cf7de3.png)

Time
 Zone Information is important because some data in the computer will 
have their timestamps in UTC/GMT and others in the local time zone. 
Knowledge of the local time zone helps in establishing a timeline when 
merging data from all the sources.

**Network Interfaces and Past Networks:**

The following registry key will give a list of network interfaces on the machine we are investigating:

`SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`

Take a look at this registry key as shown in Registry Explorer and answer Question # 5.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/7f0ed33ad442f22ec9475488d6af4421.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/7f0ed33ad442f22ec9475488d6af4421.png)

Each
 Interface is represented with a unique identifier (GUID) subkey, which 
contains values relating to the interface’s TCP/IP configuration. This 
key will provide us with information like IP addresses, DHCP
 IP address and Subnet Mask, DNS Servers, and more. This information is 
significant because it helps you make sure that you are performing 
forensics on the machine that you are supposed to perform it on.

The past networks a given machine was connected to can be found in the following locations:

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged`

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fae511770c0ac57458073992ef221251.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fae511770c0ac57458073992ef221251.png)

These
 registry keys contain past networks as well as the last time they were 
connected. The last write time of the registry key points to the last 
time these networks were connected.

**Autostart Programs (Autoruns):**

The following registry keys include information about programs or commands that run when a user logs on.

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`

`SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`

`SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`

`SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6745df01d5c2f896795d5d6f481461b7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6745df01d5c2f896795d5d6f481461b7.png)

The following registry key contains information about services:

`SYSTEM\CurrentControlSet\Services`

Notice the Value of the Start key in the screenshot below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/5605bfda34393bfcb8c4aee6a5ad771f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/5605bfda34393bfcb8c4aee6a5ad771f.png)

In this registry key, if the `start` **key is set to 0x02, this means that this service will start at boot.

**SAM hive and user information:**

The
 SAM hive contains user account information, login information, and 
group information. This information is mainly located in the following 
location:

`SAM\Domains\Account\Users`

Take a look at the below screenshot and answer Question # 6.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d24056c00af7ef9e77ea25b883cdf06c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d24056c00af7ef9e77ea25b883cdf06c.png)

The
 information contained here includes the relative identifier (RID) of 
the user, number of times the user logged in, last login time, last 
failed login, last password change, password expiry, password policy and
 password hint, and any groups that the user is a part of.

**Usage or knowledge of files/folders**

## **Recent Files:**

Windows maintains a list of recently 
opened files for each user. As we might have seen when using Windows 
Explorer, it shows us a list of recently used files. This information is stored in the NTUSER hive and can be found on the following location:

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aff5ea8e993f2989f5f8caf94798a3c7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aff5ea8e993f2989f5f8caf94798a3c7.png)

Registry Explorer allows us to sort data contained in registry keys 
quickly. For example, the Recent documents tab arranges the Most 
Recently Used (MRU) file at the top of the list. Registry Explorer also 
arranges them so that the Most Recently Used (MRU) file is shown at the 
top of the list and the older ones later.

Another interesting piece of information in this registry key is that there are different keys with file extensions, such as `.pdf`, `.jpg`, `.docx` etc.
 These keys provide us with information about the last used files of a 
specific file extension. So if we are looking specifically for the last 
used PDF files, we can look at the following registry key:

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.pdf`

Registry Explorer also lists the Last Opened time of the files. Answer Question # 1 by looking at the above screenshot.

## **Office Recent Files:**

Similar to the Recent Docs maintained by Windows Explorer, Microsoft 
Office also maintains a list of recently opened documents. This list is 
also located in the NTUSER hive. It can be found in the following 
location:

`NTUSER.DAT\Software\Microsoft\Office\VERSION`

The version number for each Microsoft Office release is different. An example registry key will look like this:

`NTUSER.DAT\Software\Microsoft\Office\15.0\Word`

Here, the 15.0 refers to Office 2013. A list of different Office releases and their version numbers can be found on [this link](https://docs.microsoft.com/en-us/deployoffice/install-different-office-visio-and-project-versions-on-the-same-computer#office-releases-and-their-version-number).

Starting from Office 365, Microsoft now ties the location to the user's [live ID](https://www.microsoft.com/security/blog/2008/05/07/what-is-a-windows-live-id/). In such a scenario, the recent files can be found at the following location.

`NTUSER.DAT\Software\Microsoft\Office\VERSION\UserMRU\LiveID_####\FileMRU`

In such a scenario, the recent files can be found at the following 
location. This location also saves the complete path of the most 
recently used files.

## **ShellBags:**

When any user opens a folder, it opens in a specific layout. Users 
can change this layout according to their preferences. These layouts can
 be different for different folders. This information about the Windows *'shell'* is
 stored and can identify the Most Recently Used files and folders. Since
 this setting is different for each user, it is located in the user 
hives. We can find this information on the following locations:

`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`

`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`

`NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`

`NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags`

Registry Explorer doesn't give us much information about ShellBags. 
However, another tool from Eric Zimmerman's tools called the ShellBag 
Explorer shows us the information in an easy-to-use format. We just have
 to point to the hive file we have extracted, and it parses the data and
 shows us the results. An example is shown below. Take a look and answer
 Question # 2.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/666bd5bd3db41b4b6e3f09311f25666a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/666bd5bd3db41b4b6e3f09311f25666a.png)

## **Open/Save and LastVisited Dialog MRUs:**

When we open or save a file, a dialog box appears asking us where to 
save or open that file from. It might be noticed that once we open/save a
 file at a specific location, Windows remembers that location. This 
implies that we can find out recently used files if we get our hands on 
this information. We can do so by examining the following registry keys

```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU
```

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU`

This is how Registry Explorer shows this registry key. Take a look to answer Question # 3 and 4.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e996b8939895b4b5e55e780baa4335e9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e996b8939895b4b5e55e780baa4335e9.png)

## **Windows Explorer Address/Search Bars:**

Another way to identify a user's recent activity is by looking at the
 paths typed in the Windows Explorer address bar or searches performed 
using the following registry keys, respectively.

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`

Here is how the TypedPaths key looks like in Registry Explorer:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/782204163443e8f21ddd14297ba756dd.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/782204163443e8f21ddd14297ba756dd.png)

**Evidence of Execution**

**UserAssist
:**

Windows
 keeps track of applications launched by the user using Windows Explorer
 for statistical purposes in the User Assist registry keys. These keys 
contain information about the programs launched, the time of their 
launch, and the number of times they were executed. However, programs 
that were run using the command line can't be found in the User Assist 
keys. The User Assist key is present in the NTUSER hive, mapped to each 
user's GUID. We can find it at the following location:

`NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count`

Take a look at the below screenshot from Registry Explorer and answer Question #1.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9bd8461865865ac3ff774c8a88d1afd5.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9bd8461865865ac3ff774c8a88d1afd5.png)

# **ShimCache:**

ShimCache is a mechanism used to keep track of application compatibility with the OS and tracks all applications launched
 on the machine. Its main purpose in Windows is to ensure backward 
compatibility of applications. It is also called Application 
Compatibility Cache (AppCompatCache). It is located in the following 
location in the SYSTEM hive:

`SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`

ShimCache stores file name, file size, and last modified time of the executables.

Our
 goto tool, the Registry Explorer, doesn't parse ShimCache data in a 
human-readable format, so we go to another tool called AppCompatCache 
Parser, also a part of Eric Zimmerman's tools. It takes the SYSTEM hive 
as input, parses the data, and outputs a CSV file that looks like this:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aad7dc918dbf3b1ab207dd71d03e8c0c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aad7dc918dbf3b1ab207dd71d03e8c0c.png)

We can use the following command to run the AppCompatCache Parser Utility:

`AppCompatCacheParser.exe
 --csv <path to save output> -f <path to SYSTEM hive for data 
parsing> -c <control set to parse>`

The output can be viewed using EZviewer, another one of Eric Zimmerman's tools.

**AmCache:**

The
 AmCache hive is an artifact related to ShimCache. This performs a 
similar function to ShimCache, and stores additional data related to 
program executions. This data includes execution path, installation, 
execution and deletion times, and SHA1 hashes of the executed programs. 
This hive is located in the file system at:

`C:\Windows\appcompat\Programs\Amcache.hve`

Information about the last executed programs can be found at the following location in the hive:

`Amcache.hve\Root\File\{Volume GUID}\`

This is how Registry Explorer parses the AmCache hive:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a569dfdf155c1a26fe3a693c388a44c7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a569dfdf155c1a26fe3a693c388a44c7.png)

**BAM/DAM:**

Background 
Activity Monitor or BAM keeps a tab on the activity of background 
applications. Similar Desktop Activity Moderator or DAM is a part of 
Microsoft Windows that optimizes the power consumption of the device. 
Both of these are a part of the Modern Standby system in Microsoft 
Windows.

In the Windows registry, the following locations contain 
information related to BAM and DAM. This location contains information 
about last run programs, their full paths, and last execution time.

`SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`

`SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`

Below you can see how Registry Explorer parses data from BAM:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8a672c6580ab63d757ee5c08c09c924a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8a672c6580ab63d757ee5c08c09c924a.png)

**External Devices/USB device forensics**

When performing 
forensics on a machine, often the need arises to identify if any USB or 
removable drives were attached to the machine. If so, any information 
related to those devices is important for a forensic investigator. In 
this task, we will go through the different ways to find information on 
connected devices and the drives on a system using the registry.

# Device identification:

The
 following locations keep track of USB keys plugged into a system. These
 locations store the vendor id, product id, and version of the USB 
device plugged in and can be used to identify unique devices. These 
locations also store the time the devices were plugged into the system.

`SYSTEM\CurrentControlSet\Enum\USBSTOR`

`SYSTEM\CurrentControlSet\Enum\USB`

Registry
 Explorer shows this information in a nice and easy-to-understand way. 
Take a look at this and answer Questions # 1 and 2.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/03c87eaaf8458db97ffbddd30a6463e8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/03c87eaaf8458db97ffbddd30a6463e8.png)

# First/Last Times:

Similarly,
 the following registry key tracks the first time the device was 
connected, the last time it was connected and the last time the device 
was removed from the system.

`SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`

In this key, the #### sign can be replaced by the following digits to get the required information:

| **Value** | **Information** |
| --- | --- |
| 0064 | First Connection time |
| 0066 | Last Connection time |
| 0067 | Last removal time |

Although
 we can check this value manually, as we have seen above, Registry 
Explorer already parses this data and shows us if we select the USBSTOR 
key.

**USB device Volume Name:**

The device name of the connected drive can be found at the following location:

`SOFTWARE\Microsoft\Windows Portable Devices\Devices`

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6c9f71cdf4c71afdc19fc8c254a6a3cc.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6c9f71cdf4c71afdc19fc8c254a6a3cc.png)

We
 can compare the GUID we see here in this registry key and compare it 
with the Disk ID we see on keys mentioned in device identification to 
correlate the names with unique devices. Take a look at these two 
screenshots and answer Question # 3.

**The FAT file systems**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/776f8e49bad9fe979ef112c2ace58b33.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/776f8e49bad9fe979ef112c2ace58b33.png)

A
 storage device in a computer system, for example, a hard disk drive or a
 USB device, is just a collection of bits. To convert these bits into 
meaningful information, they need to be organized. For this purpose, 
computer scientists and engineers have created different file systems 
that organize the bits in a hard drive as per a standard, so that 
information stored in these bits can be interpreted easily.

## The File Allocation Table (FAT):

The
 File Allocation Table (FAT) is one of these file systems. It has been 
the default file system for Microsoft Operating Systems since at least 
the late 1970s and is still in use, though not the default anymore. As 
the name suggests, the File Allocation Table creates a table that 
indexes the location of bits that are allocated to different files. If 
you are interested in the history of the FAT file system, you can head 
to the [Wikipedia page](https://en.wikipedia.org/wiki/File_Allocation_Table) for it.

## **Data structures of the FAT file system:**

The FAT file system supports the following Data structures:

### Clusters:

A cluster is a basic storage unit of the FAT file system. Each file 
stored on a storage device can be considered a group of clusters 
containing bits of information.

### Directory:

A directory contains information about file identification, like file name, starting cluster, and filename length.

### File Allocation Table:

The File Allocation Table is a linked list of all the clusters. It 
contains the status of the cluster and the pointer to the next cluster 
in the chain.

In summary, the bits that make up a file are stored in clusters. All 
the filenames on a file system, their starting clusters, and their 
lengths are stored in directories. And the location of each cluster on 
the disk is stored in the File Allocation Table. We can see that we 
started with a raw disk composed of bits and organized it to define what
 group of bits refers to what file stored on the disk.

## **FAT12, FAT16, and FAT32:**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/182f455a34bfcbd86d4a5f1ecca0286b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/182f455a34bfcbd86d4a5f1ecca0286b.png)

The FAT file format divides the available disk space into clusters 
for more straightforward addressing. The number of these clusters 
depends on the number of bits used to address the cluster. Hence the 
different variations of the FAT file system. FAT was initially developed
 with 8-bit cluster addressing, and it was called the FAT Structure. 
Later, as the storage needed to be increased, FAT12, FAT16, and FAT32 
were introduced. The last one of them was introduced in 1996.

Theoretically, FAT12 used 12-bit cluster addressing for a maximum of 
4096 clusters(2^12). FAT16 used 16-bit cluster addressing for a maximum 
of 65,536 clusters (2^16). In the case of FAT32, the actual bits used to
 address clusters are 28, so the maximum number of clusters is actually 
268,435,456 or 2^28. However, not all of these clusters are used for 
file storage. Some are used for administrative purposes, e.g., to store 
the end of a chain of clusters, the unusable parts of the disk, or other
 such purposes.

The following table summarizes the information as mentioned earlier and how it impacts the maximum volume and file sizes:

| **Attribute** | **FAT12** | **FAT16** | **FAT32** |
| --- | --- | --- | --- |
| **Addressable bits** | 12 | 16 | 28 |
| **Max number of clusters** | 4,096 | 65,536 | 268,435,456 |
| **Supported size of clusters** | 512B - 8KB | 2KB - 32KB | 4KB - 32KB |
| **Maximum Volume size** | 32MB | 2GB | 2TB |

Even though the maximum volume size for FAT32 is 2TB, Windows limits 
formatting to only 32GB. However, volume sizes formatted on other OS 
with larger volume sizes are supported by Windows.

The chances of 
coming across a FAT12 filesystem are very rare nowadays. FAT16 and FAT32
 are still used in some places, like USB drives, SD cards, or Digital 
cameras. However, the maximum volume size and the maximum file size (4GB
 - 1 file size for both FAT16 and FAT32) are limiting factors that have 
reduced their usage.

## **The exFAT file system:**

As the file sizes have grown, especially with higher resolution 
images and videos being supported by the newer digital cameras, the 
maximum file size limit of FAT32 became a substantial limiting factor 
for camera manufacturers. Though Microsoft had moved on to the NTFS file
 system, it was not suitable for digital media devices as they did not 
need the added security features and the overhead that came with it. 
Therefore, these manufacturers lobbied Microsoft to create the exFAT 
file system.

The exFAT file system is now the default for SD cards
 larger than 32GB. It has also been adopted widely by most manufacturers
 of digital devices. The exFAT file system supports a cluster size of 
4KB to 32MB. It has a maximum file size and a maximum volume size of 
128PB (Petabytes). It also reduces some of the overheads of the FAT file
 system to make it lighter and more efficient. It can have a maximum of 
2,796,202 files per directory.

**The NTFS File System**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bef41dd6a6e84e675c8106a6d5fe4b3b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/bef41dd6a6e84e675c8106a6d5fe4b3b.png)

## **The NTFS file system**

As observed in the previous task, the FAT file system is a very basic
 file system. It does the job when it comes to organizing our data, but 
it offers little more in terms of security, reliability, and recovery 
capabilities. It also has certain limitations when it comes to file and 
volume sizes. Hence, Microsoft developed a newer file system called the 
New Technology File System (NTFS) to add these features. This file 
system was introduced in 1993 with the Windows NT 3.1. However, it 
became mainstream since Windows XP. The NTFS file system resolves many 
issues present in the FAT file system and introduces a lot of new 
features. We will discuss some of the features below.

### Journaling

The NTFS file system keeps a log of changes to the metadata in the 
volume. This feature helps the system recover from a crash or data 
movement due to defragmentation. This log is stored in $LOGFILE in the 
volume's root directory. Hence the NTFS file system is called a 
journaling file system.

### Access Controls

The FAT file system did not have access controls based on the user. 
The NTFS file system has access controls that define the owner of a 
file/directory and permissions for each user.

### Volume Shadow Copy

The NTFS file system keeps track of changes made to a file using a 
feature called Volume Shadow Copies. Using this feature, a user can 
restore previous file versions for recovery or system restore. In recent
 ransomware attacks, ransomware actors have been noted to delete the 
shadow copies on a victim's file systems to prevent them from recovering
 their data.

### Alternate Data Streams

A file is a stream of data organized in a file system. Alternate data
 streams (ADS) is a feature in NTFS that allows files to have multiple 
streams of data stored in a single file. Internet Explorer and other 
browsers use Alternate Data Streams to identify files downloaded from 
the internet (using the ADS Zone Identifier). Malware has also been 
observed to hide their code in ADS.

## **Master File Table**

Like the File Allocation Table, there is a Master File Table in NTFS.
 However, the Master File Table, or MFT, is much more extensive than the
 File Allocation Table. It is a structured database that tracks the 
objects stored in a volume. Therefore, we can say that the NTFS file 
system data is organized in the Master File Table. From a forensics 
point of view, the following are some of the critical files in the MFT:

### $MFT

The $MFT is the first record in the volume. The Volume Boot Record 
(VBR) points to the cluster where it is located. $MFT stores information
 about the clusters where all other objects present on the volume are 
located. This file contains a directory of all the files present on the 
volume.

### $LOGFILE

The $LOGFILE stores the transactional logging of the file system. It 
helps maintain the integrity of the file system in the event of a crash.

### $UsnJrnl

It stands for the Update Sequence Number (USN) Journal. It is present
 in the $Extend record. It contains information about all the files that
 were changed in the file system and the reason for the change. It is 
also called the change journal.

### MFT Explorer

MFT Explorer is one of Eric Zimmerman's tools used to explore MFT 
files. It is available in both command line and GUI versions. We will be
 using the CLI version for this task.

Start the machine attached 
with the task. It will open in the split view. If preferred, login to 
the machine through RDP using the following credentials:

Username: thm-4n6

Password: 123

Open an elevated command prompt (right-click command prompt, and click `Run as Administrator`). Navigate to the directory `C:\Users\THM-4n6\Desktop\Eztools` and run the command `MFTECmd.exe`. You will see the following options:

Administrator: Command Prompt

```
user@machine$ MFTECmd.exeMFTECmd version 0.5.0.1

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/MFTECmd

        f               File to process ($MFT | $J | $LogFile | $Boot | $SDS). Required        m               $MFT file to use when -f points to a $J file (Use this to resolve parent path in $J CSV output).        json            Directory to save JSON formatted results to. This or --csv required unless --de or --body is specified
        jsonf           File name to save JSON formatted results to. When present, overrides default name
        csv             Directory to save CSV formatted results to. This or --json required unless --de or --body is specified
        csvf            File name to save CSV formatted results to. When present, overrides default name

        body            Directory to save bodyfile formatted results to. --bdl is also required when using this option
        bodyf           File name to save body formatted results to. When present, overrides default name
        bdl             Drive letter (C, D, etc.) to use with bodyfile. Only the drive letter itself should be provided
        blf             When true, use LF vs CRLF for newlines. Default is FALSE

        dd              Directory to save exported FILE record. --do is also required when using this option
        do              Offset of the FILE record to dump as decimal or hex. Ex: 5120 or 0x1400 Use --de or --vl 1 to see offsets

        de              Dump full details for entry/sequence #. Format is 'Entry' or 'Entry-Seq' as decimal or hex. Example: 5, 624-5 or 0x270-0x5.        fls             When true, displays contents of directory specified by --de. Ignored when --de points to a file.
        ds              Dump full details for Security Id as decimal or hex. Example: 624 or 0x270

        dt              The custom date/time format to use when displaying time stamps. Default is: yyyy-MM-dd HH:mm:ss.fffffff
        sn              Include DOS file name types. Default is FALSE
        fl              Generate condensed file listing. Requires --csv. Default is FALSE
        at              When true, include all timestamps from 0x30 attribute vs only when they differ from 0x10. Default is FALSE

        vss             Process all Volume Shadow Copies that exist on drive specified by -f . Default is FALSE
        dedupe          Deduplicate -f & VSCs based on SHA-1. First file found wins. Default is FALSE

        debug           Show debug information during processing
        trace           Show trace information during processing

Examples: MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out" --csvf MyOutputFile.csv
          MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out"
          MFTECmd.exe -f "C:\Temp\SomeMFT" --json "c:\temp\jsonout"
          MFTECmd.exe -f "C:\Temp\SomeMFT" --body "c:\temp\bout" --bdl c
          MFTECmd.exe -f "C:\Temp\SomeMFT" --de 5-5

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes
```

MFTECmd parses data from the different files created by the NTFS file
 system like $MFT, $Boot, etc. The above screenshot shows the available 
options for parsing MFT files. For parsing the $MFT file, we can use the
 following command:

`MFTECmd.exe -f <path-to-$MFT-file> --csv <path-to-save-results-in-csv>`

You can then use the EZviewer tool inside the EZtools folder to view 
the output of MFTECmd, or to view CSV files in the next tasks as well. 
You will see that it lists information about all the files present on 
the volume. You can similarly parse the $Boot file, which will provide 
information about the boot sector of the volume. MFTECmd doesn't support
 $LOGFILE as of now.

Let's parse the MFT files present on the location `C:\users\THM-4n6\Desktop\triage\C\` in the attached VM and answer the questions below. Currently, MFTECmd.exe doesn't support $Logfile.

**Recovering deleted files**

## **Deleted files and Data recovery:**

Understanding the file systems makes it easier to know how files are 
deleted, recovered, and wiped. As we learned in the previous two tasks, a
 file system stores the location of a file on the disk in a table or a 
database. When we delete a file from the file system, the file system 
deletes the entries that store the file's location on the disk. For the 
file system, the location where the file existed is now available for 
writing or unallocated. However, the file contents on disk are still 
there, as long as they are not overwritten by the file system while 
copying another file or by the disk firmware while performing 
maintenance on the disk.

Similarly, there is data on the disk in 
different unallocated clusters, which can possibly be recovered. To 
recover this data, we have to understand the file structure of different
 file types to identify the specific file through the data we see in a 
hex editor. However, we will not cover that in this room. What we will 
do, is to use a tool that does this work for us and identifies deleted 
files in a disk image file. But what is a disk image file?

### Disk Image:

A disk image file is a file that contains a bit-by-bit copy of a disk
 drive. A bit-by-bit copy saves all the data in a disk image file, 
including the metadata, in a single file. Thus, while performing 
forensics, one can make several copies of the physical evidence, i.e., 
the disk, and use them for investigation. This helps in two ways. 1) The
 original evidence is not contaminated while performing forensics, and 
2) The disk image file can be copied to another disk and analyzed 
without using specialized hardware.

### Recovering files using Autopsy

With that out of the way, let's see how we can recover deleted files 
from a disk. We will use Autopsy for recovering deleted files. For a 
room dedicated to Autopsy, you can go [here](https://tryhackme.com/room/btautopsye0).

On
 the attached VM, you will find an icon for Autopsy on the Desktop. 
Double-click it to run Autopsy. You will be greeted with the following 
screen:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1efa320c87b2f2d564e60bf4c6ec6dc5.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1efa320c87b2f2d564e60bf4c6ec6dc5.png)

Click on the 'New Case' Option. You will find a window similar to the following:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1411fbe2ad57d4cd474be027c72b3968.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/1411fbe2ad57d4cd474be027c72b3968.png)

Enter a name to save your case by, and click Next.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a60c87484f00a38ce9e5250cb3b85055.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a60c87484f00a38ce9e5250cb3b85055.png)

You
 can add the required details here. For now, we can click Finish to move
 forward. Autopsy will perform some processing and then show the 
following screen. Click Next to move forward.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/77d222f83d80c4682301a809fb98999f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/77d222f83d80c4682301a809fb98999f.png)

You
 will see this screen. Since we will be performing analysis on a disk 
image, select the topmost option, Disk Image or VM File.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83d738a83fc1dd47e49106508087fab7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83d738a83fc1dd47e49106508087fab7.png)

It will ask you for the location of the data source.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/deb3837cf6fd3766b084cc4ecb006650.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/deb3837cf6fd3766b084cc4ecb006650.png)

Provide
 the location of the data source. You will find a disk image named 
'usb.001' on the Desktop. Provide the path to that file in the above 
window and click next. You will see the following window:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/99a0874ffec490f0468910cc2990ec2f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/99a0874ffec490f0468910cc2990ec2f.png)

Here,
 click Deselect All. These are different modules that Autopsy runs on 
the data for processing. For this task, we don't need any of these. If 
enabled, they take a lot of time to run. Click Next after clicking 
Deselect All. Autopsy will load the disk image. You will see the 
following in the left panel.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6aa98fadbab058ee3d760e520198d2f1.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/6aa98fadbab058ee3d760e520198d2f1.png)

The
 Data Sources show the data sources that we have added to Autopsy. We 
can add more sources as well. The File Views and Tags menus show what 
Autopsy has found after processing the data. Expand the Data Sources, 
and click on the usb.001 device. Autopsy will show the contents of the 
disk image in the following way:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/905832f92232c0e982fb84588d5fea1f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/905832f92232c0e982fb84588d5fea1f.png)

The
 contents of the disk are shown on the right side. All the files and 
folders present in the disk are listed in the upper tab. In the lower 
tab, details about the selected files are shown. There are different 
options to see the details here. You can check them out to find 
interesting information.

Notice the X mark on the last file in the
 screenshot above, named New Microsoft Excel 
Worksheet.xlsx~RFcd07702.TMP. This indicates that this is a deleted 
file. Deleted files will have this X mark on them. To recover a deleted 
file, right-click on it, and select the Extract File(s) option.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/14acd357e9c89b8ce8297b076ed43c02.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/14acd357e9c89b8ce8297b076ed43c02.png)

**Evidence of Execution**

Now that we have 
learned about the File system, let's learn where to find artifacts 
present in the file system to perform forensic analysis. In this task, 
we will look into the artifacts that provide us evidence of execution:

## Windows Prefetch files

When a program is run in Windows, it stores its information for 
future use. This stored information is used to load the program quickly 
in case of frequent use. This information is stored in prefetch files 
which are located in the `C:\Windows\Prefetch` directory.

Prefetch files have an extension of `.pf`. Prefetch files 
contain the last run times of the application, the number of times the 
application was run, and any files and device handles used by the file. 
Thus it forms an excellent source of information about the last executed
 programs and files.

We can use Prefetch Parser (PECmd.exe) from 
Eric Zimmerman's tools for parsing Prefetch files and extracting data. 
When we run PECmd.exe in an elevated command prompt, we get this output:

Administrator: Command Prompt

```
user@machine$ PECmd.exePECmd version 1.4.0.0

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/PECmd

        d               Directory to recursively process. Either this or -f is required
        f               File to process. Either this or -d is required
        k               Comma separated list of keywords to highlight in output. By default, 'temp' and 'tmp' are highlighted. Any additional keywords will be added to these.
        o               When specified, save prefetch file bytes to the given path. Useful to look at decompressed Win10 files
        q               Do not dump full details about each file processed. Speeds up processing when using --json or --csv. Default is FALSE

        json            Directory to save json representation to.
        jsonf           File name to save JSON formatted results to. When present, overrides default name
        csv             Directory to save CSV results to. Be sure to include the full path in double quotes
        csvf            File name to save CSV formatted results to. When present, overrides default name
        html            Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
        dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss
        mp              When true, display higher precision for timestamps. Default is FALSE

        vss             Process all Volume Shadow Copies that exist on drive specified by -f or -d . Default is FALSE
        dedupe          Deduplicate -f or -d & VSCs based on SHA-1. First file found wins. Default is TRUE

        debug           Show debug information during processing
        trace           Show trace information during processing

Examples: PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf"
          PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf" --json "D:\jsonOutput" --jsonpretty
          PECmd.exe -d "C:\Temp" -k "system32, fonts"
          PECmd.exe -d "C:\Temp" --csv "c:\temp" --csvf foo.csv --json c:\temp\json
          PECmd.exe -d "C:\Windows\Prefetch"

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Either -f or -d is required. Exiting
```

To run Prefetch Parser on a file and save the results in a CSV, we can use the following command:

`PECmd.exe -f <path-to-Prefetch-files> --csv <path-to-save-csv>`

Similarly, for parsing a whole directory, we can use the following command:

`PECmd.exe -d <path-to-Prefetch-directory> --csv <path-to-save-csv>`

We can use this information to answer the questions at the end.

## Windows 10 Timeline

Windows 10 stores recently used applications and files in an SQLite 
database called the Windows 10 Timeline. This data can be a source of 
information about the last executed programs. It contains the 
application that was executed and the focus time of the application. The
 Windows 10 timeline can be found at the following location:

`C:\Users\<username>\AppData\Local\ConnectedDevicesPlatform\{randomfolder}\ActivitiesCache.db`

We can use Eric Zimmerman's WxTCmd.exe for parsing Windows 10 Timeline. We get the following options when we run it:

Administrator: Command Prompt

```
user@machine$ WxTCmd.exeWxTCmd version 0.6.0.0

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/WxTCmd

        f               File to process. Required
        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss

Examples: WxTCmd.exe -f "C:\Users\eric\AppData\Local\ConnectedDevicesPlatform\L.eric\ActivitiesCache.db" --csv c:\temp

          Database files are typically found at 'C:\Users\\AppData\Local\ConnectedDevicesPlatform\L.\ActivitiesCache.db'

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

-f is required. Exiting

```

We can use the following command to run WxTCmd:

`WxTCmd.exe -f <path-to-timeline-file> --csv <path-to-save-csv>`

## Windows Jump Lists

Windows introduced jump lists to help users go directly to their 
recently used files from the taskbar. We can view jumplists by 
right-clicking an application's icon in the taskbar, and it will show us
 the recently opened files in that application. This data is stored in 
the following directory:

`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations`

Jumplists include information about the applications executed, first 
time of execution, and last time of execution of the application against
 an AppID.

We can use Eric Zimmerman's JLECmd.exe to parse Jump Lists. We get the following options when we run it:

Administrator: Command Prompt

```
user@machine$ JLECmd.exeJLECmd version 1.4.0.0

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/JLECmd

        d               Directory to recursively process. Either this or -f is required
        f               File to process. Either this or -d is required
        q               Only show the filename being processed vs all output. Useful to speed up exporting to json and/or csv. Default is FALSE

        all             Process all files in directory vs. only files matching *.automaticDestinations-ms or *.customDestinations-ms. Default is FALSE

        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        csvf            File name to save CSV formatted results to. When present, overrides default name

        html            Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
        json            Directory to save json representation to. Use --pretty for a more human readable layout
        pretty          When exporting to json, use a more human readable layout. Default is FALSE

        ld              Include more information about lnk files. Default is FALSE
        fd              Include full information about lnk files (Alternatively, dump lnk files using --dumpTo and process with LECmd). Default is FALSE

        appIds          Path to file containing AppIDs and descriptions (appid|description format). New appIds are added to the built-in list, existing appIds will have their descriptions updated
        dumpTo          Directory to save exported lnk files
        withDir         When true, show contents of Directory not accounted for in DestList entries
        Debug           Debug mode

        dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss
        mp              Display higher precision for timestamps. Default is FALSE

Examples: JLECmd.exe -f "C:\Temp\f01b4d95cf55d32a.customDestinations-ms" --mp
          JLECmd.exe -f "C:\Temp\f01b4d95cf55d32a.automaticDestinations-ms" --json "D:\jsonOutput" --jsonpretty
          JLECmd.exe -d "C:\CustomDestinations" --csv "c:\temp" --html "c:\temp" -q
          JLECmd.exe -d "C:\Users\e\AppData\Roaming\Microsoft\Windows\Recent" --dt "ddd yyyy MM dd HH:mm:ss.fff"

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Either -f or -d is required. Exiting
```

We can use the following command to parse Jumplists using JLECmd.exe:

`JLECmd.exe -f <path-to-Jumplist-file> --csv <path-to-save-csv>`

**File/folder knowledge**

## Shortcut Files

Windows creates a shortcut file for each file opened either locally 
or remotely. The shortcut files contain information about the first and 
last opened times of the file and the path of the opened file, along 
with some other data. Shortcut files can be found in the following 
locations:

`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\`

`C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent\`

We
 can use Eric Zimmerman's LECmd.exe (Lnk Explorer) to parse Shortcut 
files. When we run the LECmd.exe, we see the following options:

Administrator: Command Prompt

```
user@machine$ LECmd.exeLECmd version 1.4.0.0

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/LECmd

        d               Directory to recursively process. Either this or -f is required
        f               File to process. Either this or -d is required
        q               Only show the filename being processed vs all output. Useful to speed up exporting to json and/or csv. Default is FALSE

        r               Only process lnk files pointing to removable drives. Default is FALSE
        all             Process all files in directory vs. only files matching *.lnk. Default is FALSE

        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        csvf            File name to save CSV formatted results to. When present, overrides default name

        xml             Directory to save XML formatted results to. Be sure to include the full path in double quotes
        html            Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
        json            Directory to save json representation to. Use --pretty for a more human readable layout
        pretty          When exporting to json, use a more human readable layout. Default is FALSE

        nid             Suppress Target ID list details from being displayed. Default is FALSE
        neb             Suppress Extra blocks information from being displayed. Default is FALSE

        dt              The custom date/time format to use when displaying time stamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss
        mp              Display higher precision for time stamps. Default is FALSE

Examples: LECmd.exe -f "C:\Temp\foobar.lnk"
          LECmd.exe -f "C:\Temp\somelink.lnk" --json "D:\jsonOutput" --jsonpretty
          LECmd.exe -d "C:\Temp" --csv "c:\temp" --html c:\temp --xml c:\temp\xml -q
          LECmd.exe -f "C:\Temp\some other link.lnk" --nid --neb
          LECmd.exe -d "C:\Temp" --all

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Either -f or -d is required. Exiting

```

We can use the following command to parse shortcut files using LECmd.exe:

`LECmd.exe -f <path-to-shortcut-files> --csv <path-to-save-csv>`

The creation date of the shortcut file points to the date/time when 
the file was first opened. The date/time of modification of the shortcut
 file points to the last time the file was accessed.

## IE/Edge history

An interesting thing about the IE/Edge browsing history is that it 
includes files opened in the system as well, whether those files were 
opened using the browser or not. Hence, a valuable source of information
 on opened files in a system is the IE/Edge history. We can access the 
history in the following location:

`C:\Users\<username>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat`

The files/folders accessed appear with a `file:///*` prefix
 in the IE/Edge history. Though several tools can be used to analyze Web
 cache data, you can use Autopsy to do so in the attached VM. For doing 
that, select Logical Files as a data source.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8da15f822b9a82b094d1cd4b80aed83c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8da15f822b9a82b094d1cd4b80aed83c.png)

It will then ask you to select the path from which you want files to be analyzed. You can provide the path to the triage folder.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c5d0b8ea02333e7609edf0a727e037dd.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c5d0b8ea02333e7609edf0a727e037dd.png)

In
 the Window where Autopsy asks about ingest modules to process data, 
check the box in front of 'Recent Activity' and uncheck everything else.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/413c734d28f51bfdba616f9c6c8a9ed8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/413c734d28f51bfdba616f9c6c8a9ed8.png)

You will be able to view local files accessed in the Web history option in the left panel.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/2ff14f1bd6b4e92c5e700054e7f68e5c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/2ff14f1bd6b4e92c5e700054e7f68e5c.png)

This is what it will look like in the right panel.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/4169c85581f1f227a44c12a5da776617.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/4169c85581f1f227a44c12a5da776617.png)

As shown above, the 'Data Artifacts' tab displays information about the file accessed.

## Jump Lists

As we already learned in the last task, Jump Lists create a list of 
the last opened files. This information can be used to identify both the
 last executed programs and the last opened files in a system. 
Remembering from the last task, Jump Lists are present at the following 
location:

`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations`

We
 have already learned about parsing Jump lists in the previous task so 
we won't go over that again. Let's analyze the triage data available on 
the following location in the attached VM to answer the questions:

`C:\Users\THM-4n6\Desktop\triage\C\`

**External Devices/USB device forensics**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8fff2de1491706bdf56f9abec132b02b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8fff2de1491706bdf56f9abec132b02b.png)

Setupapi dev logs for USB devices

When any new device is attached to a system, information related to the setup of that device is stored in the `setupapi.dev.log`. This log is present at the following location:

`C:\Windows\inf\setupapi.dev.log`

This log contains the device serial number and the first/last times when the device was connected.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/da93720ac86a73115f4eeabd6581a5a7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/da93720ac86a73115f4eeabd6581a5a7.png)

Here is what it looks like when opened in Notepad.exe. Notice the first line where we can see the device ID and Serial Number.

## Shortcut files

As we learned in the previous task, shortcut files are created 
automatically by Windows for files opened locally or remotely. These 
shortcut files can sometimes provide us with information about connected
 USB devices. It can provide us with information about the volume name, 
type, and serial number. Recalling from the previous task, this 
information can be found at:

`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\`

`C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent\`

### **LINNUX FORENSIC**

**os and Account Information**

## OS release information

To find the OS release information, we can use the `cat` utility to read the file located at `/etc/os-release`.To know more about the `cat` utility, you can read its man page.

`man cat`

The below terminal shows the OS release information.

OS release

```
user@machine$ cat /etc/os-release NAME="Ubuntu"
VERSION="20.04.1 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.1 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

## User accounts

The `/etc/passwd` file contains information about the user accounts that exist on a Linux system. We can use the `cat`
 utility to read this file. The output contains 7 colon-separated 
fields, describing username, password information, user id (uid), group 
id (gid), description, home directory information, and the default shell
 that executes when the user logs in. It can be noticed that just like 
Windows, the user-created user accounts have uids 1000 or above. You can
 use the following command to make it more readable:

`cat /etc/passwd| column -t -s :`

User accounts

```
user@machine$cat /etc/passwd| column -t -s :root                  x  0      0      root                                /root                    /bin/bash
daemon                x  1      1      daemon                              /usr/sbin                /usr/sbin/nologin
bin                   x  2      2      bin                                 /bin                     /usr/sbin/nologin
sys                   x  3      3      sys                                 /dev                     /usr/sbin/nologin
sync                  x  4      65534  sync                                /bin                     /bin/sync
games                 x  5      60     games                               /usr/games               /usr/sbin/nologin
.
.
.
.
.
ubuntu                x  1000   1000   Ubuntu                              /home/ubuntu             /bin/bash
pulse                 x  123    130    PulseAudio daemon,,,                /var/run/pulse           /usr/sbin/nologin
tryhackme             x  1001   1001   tryhackme,,,                        /home/tryhackme          /bin/bash

```

In the above command, we can see the information for the user ubuntu.
 The username is ubuntu, its password information field shows `x`, which signifies that the password information is stored in the `/etc/shadow`
 file. The uid of the user is 1000. The gid is also 1000. The 
description, which often contains the full name or contact information, 
mentions the name Ubuntu. The home directory is set to `/home/ubuntu`, and the default shell is set to `/bin/bash`. We can see similar information about other users from the file as well.

## Group Information

The `/etc/group` file contains information about the different user groups present on the host. It can be read using the cat utility.

Group information

```
user@machine$ cat /etc/grouproot:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,ubuntu
tty:x:5:syslog

```

We can see that the user `ubuntu` belongs to the `adm` group, which has a password stored in the `/etc/shadow` file, signified by the `x` character. The gid is 4, and the group contains 2 users, Syslog, and ubuntu.

## Sudoers List

A Linux host allows only those users to elevate privileges to `sudo`, which are present in the Sudoers list. This list is stored in the file `/etc/sudoers` and can be read using the `cat` utility. You will need to elevate privileges to access this file.

Sudoers list

```
user@machine$ sudo cat /etc/sudoers#
# This file MUST be edited with the 'visudo' command as root.#
# Please consider adding local content in /etc/sudoers.d/ instead of# directly modifying this file.#
# See the man page for details on how to write a sudoers file.#
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# Host alias specification# User alias specification# Cmnd alias specification# User privilege specificationroot	ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges%admin ALL=(ALL) ALL# Allow members of group sudo to execute any command%sudo	ALL=(ALL:ALL) ALL# See sudoers(5) for more information on "#include" directives:#includedir /etc/sudoers.d
```

## Login information

In the /var/log directory, we can find log files of all kinds including `wtmp` and `btmp`. The `btmp` file saves information about failed logins, while the `wtmp` keeps historical data of logins. These files are not regular text files that can be read using `cat`, `less` or `vim`; instead, they are binary files, which have to be read using the `last` utility. You can learn more about the `last` utility by reading its man page.

```
man last
```

The following terminal shows the contents of `wtmp` being read using the `last` utility.

Login information

```
user@machine$ sudo last -f /var/log/wtmpreboot   system boot  5.4.0-1029-aws   Tue Mar 29 17:28   still running
reboot   system boot  5.4.0-1029-aws   Tue Mar 29 04:46 - 15:52  (11:05)
reboot   system boot  5.4.0-1029-aws   Mon Mar 28 01:35 - 01:51 (1+00:16)

wtmp begins Mon Mar 28 01:35:10 2022

```

## Authentication logs

Every user that authenticates on a Linux host is logged in the auth log. The auth log is a file placed in the location `/var/log/auth.log`. It can be read using the `cat` utility, however, given the size of the file, we can use `tail`, `head`, `more` or `less` utilities to make it easier to read.

Auth logs

```
user@machine$ cat /var/log/auth.log |tailMar 29 17:28:48 tryhackme gnome-keyring-daemon[989]: The PKCS#11 component was already initialized
Mar 29 17:28:48 tryhackme gnome-keyring-daemon[989]: The SSH agent was already initialized
Mar 29 17:28:49 tryhackme polkitd(authority=local): Registered Authentication Agent for unix-session:2 (system bus name :1.73 [/usr/lib/x86_64-linux-gnu/polkit-mate/polkit-mate-authentication-agent-1], object path /org/mate/PolicyKit1/AuthenticationAgent, locale en_US.UTF-8)
Mar 29 17:28:58 tryhackme pkexec[1618]: ubuntu: Error executing command as another user: Not authorized [USER=root] [TTY=unknown] [CWD=/home/ubuntu] [COMMAND=/usr/lib/update-notifier/package-system-locked]
Mar 29 17:29:09 tryhackme dbus-daemon[548]: [system] Failed to activate service 'org.bluez': timed out (service_start_timeout=25000ms)
Mar 29 17:30:01 tryhackme CRON[1679]: pam_unix(cron:session): session opened for user root by (uid=0)
Mar 29 17:30:01 tryhackme CRON[1679]: pam_unix(cron:session): session closed for user root
Mar 29 17:49:52 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/cat /etc/sudoers
Mar 29 17:49:52 tryhackme sudo: pam_unix(sudo:session): session opened for user root by (uid=0)
Mar 29 17:49:52 tryhackme sudo: pam_unix(sudo:session): session closed for user root

```

In the above log file, we can see that the user ubuntu elevated privileges on `Mar 29 17:49:52` using `sudo` to run the command `cat /etc/sudoers`.
 We can see the subsequent session opened and closed events for the root
 user, which were a result of the above-mentioned privilege escalation.

**System Configuration**

Once we have identified the OS and account information, we can start looking into the system configuration of the host.

## Hostname

The hostname is stored in the `/etc/hostname` file on a Linux Host. It can be accessed using the `cat` utility.

Hostname

```
user@machine$ cat /etc/hostname tryhackme
```

## Timezone

Timezone information is a significant piece of information that gives
 an indicator of the general location of the device or the time window 
it might be used in. Timezone information can be found at the location `/etc/timezone` and it can be read using the `cat` utility.

Timezone

```
user@machine$ cat /etc/timezoneEtc/UTC
```

## Network Configuration

To find information about the network interfaces, we can `cat` the `/etc/network/interfaces` file. The output on your machine might be different from the one shown here, depending on your configuration.

Network interfaces

```
user@machine$ cat /etc/network/interfaces# This file describes the network interfaces available on your system# and how to activate them. For more information, see interfaces(5).source /etc/network/interfaces.d/*

# The loopback network interfaceauto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

```

Similarly, to find information about the MAC and IP addresses of the different interfaces, we can use the `ip` utility. To learn more about the `ip` utility, we can see its `man` page.

`man ip`

The below terminal shows the usage of the `ip` utility. Note that this will only be helpful on a live system.

IP information

```
user@machine$ ip address show 1: lo:  mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0:  mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 02:20:61:f1:3c:e9 brd ff:ff:ff:ff:ff:ff
    inet 10.10.95.252/16 brd 10.10.255.255 scope global dynamic eth0
       valid_lft 2522sec preferred_lft 2522sec
    inet6 fe80::20:61ff:fef1:3ce9/64 scope link
       valid_lft forever preferred_lft forever

```

## Active network connections

On a live system, knowing the active network connections provides additional context to the investigation. We can use the `netstat` utility to find active network connections on a Linux host. We can learn more about the `netstat` utility by reading its `man` page.

`man netstat`

The below terminal shows the usage of the `netstat` utility.

Active network connections

```
user@machine$ netstat -natp(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:5901          0.0.0.0:*               LISTEN      829/Xtigervnc
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:60602         127.0.0.1:5901          ESTABLISHED -
tcp        0      0 10.10.95.252:57432      18.66.171.77:443        ESTABLISHED -
tcp        0      0 10.10.95.252:80         10.100.1.33:51934       ESTABLISHED -
tcp        0      0 127.0.0.1:5901          127.0.0.1:60602         ESTABLISHED 829/Xtigervnc
tcp6       0      0 ::1:5901                :::*                    LISTEN      829/Xtigervnc
tcp6       0      0 :::22                   :::*                    LISTEN      -
tcp6       0      0 ::1:631                 :::*                    LISTEN      -
```

## Running processes

If performing forensics on a live system, it is helpful to check the running processes. The `ps` utility shows details about the running processes. To find out about the `ps` utility, we can use the `man` page.

`man ps`

The below terminal shows the usage of the `ps` utility.

Running processes

```
user@machine$ ps auxUSER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMANDroot         729  0.0  0.0   7352  2212 ttyS0    Ss+  17:28   0:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600 ttyS0 vt220
root         738  0.0  0.0   5828  1844 tty1     Ss+  17:28   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
root         755  0.0  1.5 272084 63736 tty7     Ssl+ 17:28   0:00 /usr/lib/xorg/Xorg -core :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch
ubuntu      1672  0.0  0.1   5264  4588 pts/0    Ss   17:29   0:00 bash
ubuntu      1985  0.0  0.0   5892  2872 pts/0    R+   17:40   0:00 ps au

```

## DNS information

The file `/etc/hosts` contains the configuration for the DNS name assignment. We can use the `cat` utility to read the hosts file. To learn more about the hosts file, we can use the `man` page.

`man hosts`

The below terminal shows a sample output of the hosts file.

hosts file

```
user@machine$ cat /etc/hosts127.0.0.1 localhost

# The following lines are desirable for IPv6 capable hosts::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```

The information about DNS servers that a Linux host talks to for DNS 
resolution is stored in the resolv.conf file. Its location is `/etc/resolv.conf`. We can use the `cat` utility to read this file.

Resolv.conf

```
user@machine$ cat /etc/resolv.conf # This file is managed by man:systemd-resolved(8). Do not edit.#
# This is a dynamic resolv.conf file for connecting local clients to the# internal DNS stub resolver of systemd-resolved. This file lists all# configured search domains.#
# Run "resolvectl status" to see details about the uplink DNS servers# currently in use.#
# Third party programs must not access this file directly, but only through the# symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a different way,# replace this symlink by a static file or a different symlink.#
# See man:systemd-resolved.service(8) for details about the supported modes of# operation for /etc/resolv.conf.nameserver 127.0.0.53
options edns0 trust-ad
search eu-west-1.compute.internal
```

**Persistence mechanisms**

Knowing the environment
 we are investigating, we can then move on to finding out what 
persistence mechanisms exist on the Linux host under investigation. 
Persistence mechanisms are ways a program can survive after a system 
reboot. This helps malware authors retain their access to a system even 
if the system is rebooted. Let's see how we can identify persistence 
mechanisms in a Linux host.

## Cron jobs

Cron jobs are commands that run periodically after a set amount of 
time. A Linux host maintains a list of Cron jobs in a file located at `/etc/crontab`. We can read the file using the `cat` utility.

Cron jobs

```
user@machine$ cat /etc/crontab # /etc/crontab: system-wide crontab# Unlike any other crontab you don't have to run the `crontab'# command to install the new version when you edit this file# and files in /etc/cron.d. These files also have username fields,# that none of the other crontabs do.SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# Example of job definition:# .---------------- minute (0 - 59)# |  .------------- hour (0 - 23)# |  |  .---------- day of month (1 - 31)# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat# |  |  |  |  |# *  *  *  *  * user-name command to be executed17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#

```

The above terminal output shows the contents of a sample `/etc/crontab`
 file. As can be seen, the file contains information about the time 
interval after which the command has to run, the username that runs the 
command, and the command itself. It can also contain scripts to run, 
where the script that needs to be run will be placed on the disk, and 
the command to run it will be added to this file.

## Service startup

Like Windows, services can be set up in Linux that will start and run
 in the background after every system boot. A list of services can be 
found in the `/etc/init.d` directory. We can check the contents of the directory by using the `ls` utility.

Service startup

```
user@machine$ ls /etc/init.d/acpid       avahi-daemon      cups          hibagent           kmod             networking     pppd-dns                     screen-cleanup     unattended-upgrades
alsa-utils  bluetooth         cups-browsed  hwclock.sh         lightdm          open-iscsi     procps                       speech-dispatcher  uuidd
anacron     console-setup.sh  dbus          irqbalance         lvm2             open-vm-tools  pulseaudio-enable-autospawn  spice-vdagent      whoopsie
apparmor    cron              gdm3          iscsid             lvm2-lvmpolld    openvpn        rsync                        ssh                x11-common
apport      cryptdisks        grub-common   kerneloops         multipath-tools  plymouth       rsyslog                      udev
atd         cryptdisks-early  hddtemp       keyboard-setup.sh  network-manager  plymouth-log   saned                        ufw

```

## .Bashrc

When a bash shell is spawned, it runs the commands stored in the `.bashrc`
 file. This file can be considered as a startup list of actions to be 
performed. Hence it can prove to be a good place to look for 
persistence.

The following terminal shows an example .bashrc file.

Bashrc

```
user@machine$ cat ~/.bashrc# ~/.bashrc: executed by bash(1) for non-login shells.# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)# for examples# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

```

System-wide settings are stored in `/etc/bash.bashrc` and `/etc/profile` files, so it is often a good idea to take a look at these files as well.

**Evidence of Execution**

Knowing what programs 
have been executed on a host is one of the main purposes of performing 
forensic analysis. On a Linux host, we can find the evidence of 
execution from the following sources.

## Sudo execution history

All the commands that are run on a Linux host using `sudo` are stored in the auth log. We already learned about the auth log in Task 3. We can use the `grep` utility to filter out only the required information from the auth log.

Auth logs

```
user@machine$ cat /var/log/auth.log* |grep -i COMMAND|tailMar 29 17:28:58 tryhackme pkexec[1618]: ubuntu: Error executing command as another user: Not authorized [USER=root] [TTY=unknown] [CWD=/home/ubuntu] [COMMAND=/usr/lib/update-notifier/package-system-locked]
Mar 29 17:49:52 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/cat /etc/sudoers
Mar 29 17:55:22 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/cat /var/log/btmp
Mar 29 17:55:39 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/cat /var/log/wtmp
Mar 29 18:00:54 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/tail -f /var/log/btmp
Mar 29 18:01:24 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/last -f /var/log/btmp
Mar 29 18:03:58 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/last -f /var/log/wtmp
Mar 29 18:05:41 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/last -f /var/log/btmp
Mar 29 18:07:51 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/last -f /var/log/utmp
Mar 29 18:08:13 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home/ubuntu ; USER=root ; COMMAND=/usr/bin/last -f /var/run/utmp

```

The above terminal shows commands run by the user ubuntu using `sudo`.

## Bash history

Any commands other than the ones run using `sudo` are 
stored in the bash history. Every user's bash history is stored 
separately in that user's home folder. Therefore, when examining bash 
history, we need to get the bash_history file from each user's home 
directory. It is important to examine the bash history from the root 
user as well, to make note of all the commands run using the root user 
as well.

Bash history

```
user@machine$ cat ~/.bash_history cd Downloads/
ls
unzip PracticalMalwareAnalysis-Labs-master.zip
cd PracticalMalwareAnalysis-Labs-master/
ls
cd ..
ls
rm -rf sality/
ls
mkdir wannacry
mv Ransomware.WannaCry.zip wannacry/
cd wannacry/
unzip Ransomware.WannaCry.zip
cd ..
rm -rf wannacry/
ls
mkdir exmatter
mv 325ecd90ce19dd8d184ffe7dfb01b0dd02a77e9eabcb587f3738bcfbd3f832a1.7z exmatter/
cd exmatter/
strings -d 325ecd90ce19dd8d184ffe7dfb01b0dd02a77e9eabcb587f3738bcfbd3f832a1|sort|uniq>str-sorted
cd ..
ls

```

## Files accessed using vim

The `Vim` text editor stores logs for opened files in `Vim` in the file named `.viminfo`
 in the home directory. This file contains command line history, search 
string history, etc. for the opened files. We can use the `cat` utility to open `.viminfo`.

Viminfo

```
user@machine$ cat ~/.viminfo# This viminfo file was generated by Vim 8.1.# You may edit it if you're careful!

# Viminfo version
|1,4

# Value of 'encoding' when this file was written
*encoding=utf-8

# hlsearch on (H) or off (h):
~h
# Command Line History (newest to oldest):
:q
|2,0,1636562413,,"q"

# Search String History (newest to oldest):

# Expression History (newest to oldest):

# Input Line History (newest to oldest):

# Debug Line History (newest to oldest):

# Registers:

# File marks:
'0  1139  0  ~/Downloads/str|4,48,1139,0,1636562413,"~/Downloads/str"

# Jumplist (newest first):-'  1139  0  ~/Downloads/str
|4,39,1139,0,1636562413,"~/Downloads/str"
-'  1  0  ~/Downloads/str
|4,39,1,0,1636562322,"~/Downloads/str"

# History of marks within files (newest to oldest):> ~/Downloads/str
	*	1636562410	0
	"	1139	0

```

**Log files**

One of the most 
important sources of information on the activity on a Linux host is the 
log files. These log files maintain a history of activity performed on 
the host and the amount of logging depends on the logging level defined 
on the system. Let's take a look at some of the important log sources. 
Logs are generally found in the `/var/log` directory.

## Syslog

The Syslog contains messages that are recorded by the host about 
system activity. The detail which is recorded in these messages is 
configurable through the logging level. We can use the `cat` utility to view the Syslog, which can be found in the file `/var/log/syslog`. Since the Syslog is a huge file, it is easier to use `tail`, `head`, `more` or `less` utilities to help make it more readable.

Syslog

```
user@machine$ cat /var/log/syslog* | headMar 29 00:00:37 tryhackme systemd-resolved[519]: Server returned error NXDOMAIN, mitigating potential DNS violation DVE-2018-0001, retrying transaction with reduced feature level UDP.
Mar 29 00:00:37 tryhackme rsyslogd: [origin software="rsyslogd" swVersion="8.2001.0" x-pid="635" x-info="https://www.rsyslog.com"] rsyslogd was HUPed
Mar 29 00:00:37 tryhackme systemd[1]: man-db.service: Succeeded.
Mar 29 00:00:37 tryhackme systemd[1]: Finished Daily man-db regeneration.
Mar 29 00:09:01 tryhackme CRON[7713]: (root) CMD (   test -x /etc/cron.daily/popularity-contest && /etc/cron.daily/popularity-contest --crond)
Mar 29 00:17:01 tryhackme CRON[7726]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
Mar 29 00:30:45 tryhackme snapd[2930]: storehelpers.go:721: cannot refresh: snap has no updates available: "amazon-ssm-agent", "core", "core18", "core20", "lxd"
Mar 29 00:30:45 tryhackme snapd[2930]: autorefresh.go:536: auto-refresh: all snaps are up-to-date
Mar 29 01:17:01 tryhackme CRON[7817]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
Mar 29 01:50:37 tryhackme systemd[1]: Starting Cleanup of Temporary Directories...

```

The above terminal shows the system time, system name, the process 
that sent the log [the process id], and the details of the log. We can 
see a couple of cron jobs being run here in the logs above, apart from 
some other activity. We can see an asterisk(*) after the syslog. This is
 to include rotated logs as well. With the passage of time, the Linux 
machine rotates older logs into files such as syslog.1, syslog.2 etc, so
 that the syslog file doesn't become too big. In order to search through
 all of the syslogs, we use the asterisk(*) wildcard.

## Auth logs

We have already discussed the auth logs in the previous tasks. The 
auth logs contain information about users and authentication-related 
logs. The below terminal shows a sample of the auth logs.

Auth logs

```
user@machine$ cat /var/log/auth.log* |headFeb 27 13:52:33 ip-10-10-238-44 useradd[392]: new group: name=ubuntu, GID=1000
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: new user: name=ubuntu, UID=1000, GID=1000, home=/home/ubuntu, shell=/bin/bash, from=none
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'adm'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'dialout'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'cdrom'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'floppy'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'sudo'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'audio'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'dip'
Feb 27 13:52:33 ip-10-10-238-44 useradd[392]: add 'ubuntu' to group 'video'

```

We can see above that the log stored information about the creation 
of a new group, a new user, and the addition of the user into different 
groups.

### Third-party logs

Similar to the syslog and authentication logs, the `/var/log/`
 directory contains logs for third-party applications such as webserver,
 database, or file share server logs. We can investigate these by 
looking at the `/var/log/` directory.

Third-party logs

```
user@machine$ ls /var/logXorg.0.log          apt                    cloud-init.log  dmesg.2.gz      gdm3                    kern.log.1         prime-supported.log  syslog.2.gz
Xorg.0.log.old      auth.log               cups            dmesg.3.gz      gpu-manager-switch.log  landscape          private              syslog.3.gz
alternatives.log    auth.log.1             dist-upgrade    dmesg.4.gz      gpu-manager.log         lastlog            samba                syslog.4.gz
alternatives.log.1  btmp                   dmesg           dpkg.log        hp                      lightdm            speech-dispatcher    syslog.5.gz
amazon              btmp.1                 dmesg.0         dpkg.log.1      journal                 openvpn            syslog               unattended-upgrades
apache2             cloud-init-output.log  dmesg.1.gz      fontconfig.log  kern.log                prime-offload.log  syslog.1             wtmp

```

As is obvious, we can find the apache logs in the apache2 directory and samba logs in the samba directory.

Apache logs

```
user@machine$  ls /var/log/apache2/access.log  error.log  other_vhosts_access.log

```

Similarly, if any database server like MySQL is installed on the system, we can find the logs in this directory.

### **AUTOPSY**

[**The official description**](https://www.autopsy.com/): "*Autopsy is the premier open source forensics platform which is fast, 
easy-to-use, and capable of analysing all types of mobile devices and 
digital media. Its plug-in architecture enables extensibility from 
community-developed or custom-built modules. Autopsy evolves to meet the
 needs of hundreds of thousands of professionals in law enforcement, 
national security, litigation support, and corporate investigation.*"

**Workflow Overview and Case Analysis**

**Workflow Overview**

Before
 diving into Autopsy and analysing data, there are a few steps to 
perform; such as identifying the data source and what Autopsy actions to
 perform with the data source.

Basic workflow:

1. Create/open the case for the data source you will investigate
2. Select the data source you wish to analyse
3. Configure the ingest modules to extract specific artefacts from the data source
4. Review the artefacts extracted by the ingest modules
5. Create the report

# **Case Analysis | Create a New Case**

To prepare a new case investigation, you need to create a case file from the data source. When you start Autopsy, there will be three options. You can create a new case file using the **"New Case"** option. Once you click on the "New Case" option, the **Case Information** menu opens**,** where information about the case is populated.

- **Case Name**: The name you wish to give to the case
- **Base Directory**: The root directory that will store all the files specific to the case (the full path will be displayed)
- **Case Type**: Specify whether this case will be local (**Single-user**) or hosted on a server where multiple analysts can review (**Multi-user**)

**Note**: In this room, the focus is on **Single-User**. Also, the room doesn't simulate a new case creation, and the given VM has a sample case file to practice covered Autopsy features.

The following screen is titled "**Optional Information"** and
 can be left blank for our purposes. In an actual forensic environment, 
you should fill out this information. Once you click on "Finish", 
Autopsy will create a new case file from the given data source.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/e488c3548327c1bd78aff63060e2d2a9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/e488c3548327c1bd78aff63060e2d2a9.png)

# **Case Analysis | Open an Existing Case**

The
 Autopsy can also open prebuilt case files. Note that supported data 
sources are discussed in the next task. This part aims to show how to 
create/open case files with Autopsy.

**Note:** Autopsy case files have a ".aut" file extension.

**In this room, you will import a case.** To
 open a case, select the "Open Case" option. Navigate to the case folder
 (located on the desktop) and select the .aut file you wish to open. 
Next, Autopsy will process the case files and open the case. You can 
identify the name of the case at the top left corner of the Autopsy 
window. In the image below, the name of this case is **"Sample Case"**.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/e54b49da6843e66582b797a8a3553723.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/e54b49da6843e66582b797a8a3553723.png)

![https://assets.tryhackme.com/additional/autopsy/autopsy-casename2.png](https://assets.tryhackme.com/additional/autopsy/autopsy-casename2.png)

**Note**: A warning box will appear if Autopsy cannot locate the disk image. At this point, you can point to the location of the disk image it's attempting to find, or you can click **NO**; you can still analyse the data from the Autopsy case.

![https://assets.tryhackme.com/additional/autopsy/autopsy-missing-image3.png](https://assets.tryhackme.com/additional/autopsy/autopsy-missing-image3.png)

Once the case you wish to analyse is open, you are ready to start exploring the data.

**Data Sources**

Autopsy
 can analyse multiple disk image formats. Before diving into the data 
analysis step, let's briefly cover the different data sources Autopsy 
can analyse. You can add data sources by using the **"Add Data Source"** button. Available options are shown in the picture below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c75224413dfb9884adbdc8c5a778383d.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c75224413dfb9884adbdc8c5a778383d.png)

**We will focus primarily on the Disk Image or VM File option in this room.**

Supported Disk Image Formats:

- **Raw Single** (For example: *.img, *.dd, *.raw, *.bin)
- **Raw Split** (For example: *.001, *.002, *.aa, *.ab, etc)
- **EnCase** (For example: *.e01, *.e02, etc)
- **Virtual Machines** (For example: *.vmdk, *.vhd)

If
 there are multiple image files (e.i. E01, E02, E03, etc.) Autopsy only 
needs you to point to the first image file, and Autopsy will handle the 
rest.

**Note**: Refer to the Autopsy [documentation](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ds_page.html) to understand the other data sources that can be added to a case.

**Ingest Modules**

Essentially **Ingest Modules**
 are Autopsy plug-ins. Each Ingest Module is designed to analyse and 
retrieve specific data from the drive. You can configure Autopsy to run 
specific modules during the source-adding stage or later by choosing the
 target data source available on the dashboard. By default, the Ingest Modules are configured to run on All Files, Directories, and Unallocated Space.
 You can change this setting during the module selecting step. You can 
track the process with the bar appearing in the lower right corner.

The
 below screenshots simulate mentioned two different approaches to using 
ingest modules. Note that using ingest modules requires time to 
implement. Therefore we will not cover ingest modules in this room.

Note: Autopsy adds metadata about files to the local database, not the actual file contents.

**Configuring ingest modules while adding data sources:**

![https://assets.tryhackme.com/additional/autopsy/autopsy-configure-modules.png](https://assets.tryhackme.com/additional/autopsy/autopsy-configure-modules.png)

**Using ingest modules after adding data sources:**

1. Open the "Run Ingest Modules" menu by right-clicking on the data source.
2. Choose the modules to implement and click on the finish button.
3. Track the progress of implementation.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/04138be7675286ea5f9066a893c0b199.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/04138be7675286ea5f9066a893c0b199.png)

The
 results of any Ingest Module you select to run against a data source 
will populate the Results node in the Tree view, which is the left pane 
of the Autopsy user interface. Below is an example of using the **"Interesting Files Identifier"** ingest
 module. Note that the results depend on the dataset. If you choose a 
module to retrieve specific data that is unavailable in the drive, there
 will be no results.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/9ee9f606ea3444fd04c45b15c2c7f819.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/9ee9f606ea3444fd04c45b15c2c7f819.png)

Drawing the attention back to the Configure Ingest Modules window, notice that some Ingest Modules have per-run settings and some do not. For example, the Keyword Search Ingest Module does not have per-run settings. In contrast, the Interesting Files Finder Ingest Module does. The yellow triangle represents the "per-run settings option".

As Ingest Modules run, alerts may appear in the **Ingest Inbox**. Below is an example of the Ingest Inbox after a few Ingest Modules have completed running.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/212c83e75693ce2d8f485633a11dd697.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/212c83e75693ce2d8f485633a11dd697.png)

To learn more about Ingest Modules, read Autopsy documentation [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ingest_page.html).

# **The User Interface I**

Let's look at the Autopsy user interface, which is comprised of 5 primary areas:

**Tree Viewer**

![https://assets.tryhackme.com/additional/autopsy/autopsy-tree-view.png](https://assets.tryhackme.com/additional/autopsy/autopsy-tree-view.png)

The **Tree Viewer** has **five top-level nodes**:

- **Data Sources** all the data will be organised as you would typically see it in a normal Windows File Explorer.
- **Views** - files will be organised based on file types, MIME types, file size, etc.
- **Results** - as mentioned earlier, this is where the results from Ingest Modules will appear.
- **Tags** - will display files and/or results that have been tagged (read more about tagging [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/tagging_page.html)).
- **Reports** - will display reports either generated by modules or the analyst (read more about reporting [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/reporting_page.html)).

Refer to the Autopsy documentation on the **Tree Viewer** for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/tree_viewer_page.html).

# **Result Viewer**

**Note**: Don't confuse the Results node (from the Tree Viewer) with the Result Viewer.

When ****a
 volume, file, folder, etc., is selected from the Tree Viewer, 
additional information about the selected item is displayed in the 
Result Viewer. For example, the Sample case's data source is selected, and now additional information is visible in the Results Viewer.

![https://assets.tryhackme.com/additional/autopsy/autopsy-table-view.png](https://assets.tryhackme.com/additional/autopsy/autopsy-table-view.png)

If
 a volume is selected, the Result Viewer's information will change to 
reflect the information in the local database for the selected volume.

![https://assets.tryhackme.com/additional/autopsy/autopsy-table-view2.png](https://assets.tryhackme.com/additional/autopsy/autopsy-table-view2.png)

Notice that the Result Viewer pane has three tabs: **Table**, **Thumbnail**, and **Summary**. The above screenshots reflect the information displayed in the Table tab. The Thumbnail tab works best with image or video files. If the view of the above data is changed from Table to Thumbnail, not much information will be displayed. See below.

![https://assets.tryhackme.com/additional/autopsy/autopsy-thumbnail-view.png](https://assets.tryhackme.com/additional/autopsy/autopsy-thumbnail-view.png)

Volume nodes can be expanded, and an analyst can navigate the volume's contents like a typical Windows system.

![https://assets.tryhackme.com/additional/autopsy/autopsy-volume.png](https://assets.tryhackme.com/additional/autopsy/autopsy-volume.png)

In the **Views** tree node, files are categorised by File Types - **By Extension, By** **MIME Type**, **Deleted Files**, and **By** **File Size**.

![https://assets.tryhackme.com/additional/autopsy/autopsy-views.png](https://assets.tryhackme.com/additional/autopsy/autopsy-views.png)

**Tip**: When it comes to **File Types**,
 pay attention to this section. An adversary can rename a file with a 
misleading file extension. So the file will be 'miscategorised' **By** **Extension** but will be categorised appropriately by **MIME Type**. Expand **By Extension** and more children nodes appear, categorising files even further (see below).

![https://assets.tryhackme.com/additional/autopsy/autopsy-byextension.png](https://assets.tryhackme.com/additional/autopsy/autopsy-byextension.png)

Refer to the Autopsy documentation on the **Result Viewer** for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/result_viewer_page.html).

# **Contents Viewer**

From
 the Table tab in the Result Viewer, if you click any folder/file, 
additional information is displayed in the Contents Viewer pane.

![https://assets.tryhackme.com/additional/autopsy/autopsy-contents-view.png](https://assets.tryhackme.com/additional/autopsy/autopsy-contents-view.png)

In the given image, three columns might not be quickly understood what they represent.

- **S** = **Score**

The **Score**
 will show a red exclamation point for a folder/file marked/tagged as 
notable and a yellow triangle pointing downward for a folder/file 
marked/tagged as suspicious. These items can be marked/tagged by an 
Ingest Module or the analyst.

- **C** = **Comment**

If a yellow page is visible in the Comment column, it will indicate that there is a comment for the folder/file.

- **O** = **Occurrence**

In a nutshell, this column will indicate how many times this file/folder has been seen in past cases (this will require the [Central Repository](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/central_repo_page.html))

Refer to the Autopsy documentation on the Contents Viewer for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/content_viewer_page.html).

**Keyword Search**

At the top right, you will find **Keyword Lists** and **Keyword Search**. With **Keyword Search,** an analyst can perform an AD-HOC keyword search.

![https://assets.tryhackme.com/additional/autopsy/autopsy-keyword-search.png](https://assets.tryhackme.com/additional/autopsy/autopsy-keyword-search.png)

In the image above, the analyst searches for the word 'secret.' Below are the search results.

![https://assets.tryhackme.com/additional/autopsy/autopsy-keyword-search2.png](https://assets.tryhackme.com/additional/autopsy/autopsy-keyword-search2.png)

Refer to the Autopsy [documentation](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ad_hoc_keyword_search_page.html) for more information on performing keyword searches with either option.

**Status Area**

Lastly, the **Status Area** is
 at the bottom right. When Ingest Modules run, a progress bar (along 
with the percentage completed) will be displayed in this area. More 
detailed information regarding the Ingest Modules is provided if you 
click on the bar.

![https://assets.tryhackme.com/additional/autopsy/autopsy-statusbar2.png](https://assets.tryhackme.com/additional/autopsy/autopsy-statusbar2.png)

If the `X` (directly next to the progress bar) is clicked, a prompt will appear confirming if you wish to end/cancel the Ingest Modules.

# **The User Interface II**

Let's
 look at where we can find summarised info with ease. Summarised info 
can help analysts decide where to focus by evaluating available 
artefacts. It is suggested to view the summary of the data sources 
before starting an investigation. Therefore you can have a general idea 
about the system and artefacts.

**Data Sources Summary**

The **Data Sources Summary** provides
 summarised info in nine different categories. Note that this is an 
overview of the total findings. If you want to dive deep into the 
findings and look for a specific artefact, you need to analyse each 
module separately using the **"Result Viewer"** shown in the previous task.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a8ab6999fabaf538c2e9eb3742b0ff29.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a8ab6999fabaf538c2e9eb3742b0ff29.png)

# Generate Report

You
 can create a report of your findings in multiple formats, enabling you 
to create data sheets for your investigation case. The report provides 
all information listed under the "Result Viewer" pane. Reports can help 
you to re-investigate findings after finishing the live investigation. **However, reports don't have additional search options, so you must manually find artefacts for the event of interest.**

**Tip:** The
 Autopsy tool can be heavy for systems with low resources. Therefore 
completing an investigation with Autopsy on low resources can be slow 
and painful. Especially browsing long results might end up with a system
 freeze. You can avoid that situation by using reports. You can use the 
tool for parsing the data and generating the report, then continue to 
analyse through the generated report without a need for Autopsy. Note 
that it is always easier to conduct and manage an investigation with the
 GUI.

You can use the **"Generate Report"** option to create reports. The steps are shown below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/581fe3b1caa19ed94ad2564e3ecd8003.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/581fe3b1caa19ed94ad2564e3ecd8003.png)

Once
 you choose your report format and scope, Autopsy will generate the 
report. You can click on the "HTML Report" section (shown above) to view
 the report on your browser. Reports contain all of the "Result Viewer" 
pane results on the left side.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/68fc3dcf815f47183dd62c35438dc98c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/68fc3dcf815f47183dd62c35438dc98c.png)

**
Visualisation Tools**

You may have noticed that other parts of the user interface weren't discussed as of yet.

![https://assets.tryhackme.com/additional/autopsy/autopsy-top-bar.png](https://assets.tryhackme.com/additional/autopsy/autopsy-top-bar.png)

Please refer to the Autopsy documentation for the following visualisation tool:

- **Images/Videos:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/image_gallery_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/image_gallery_page.html)
- **Communications:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/communications_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/communications_page.html)
- **Timeline:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/timeline_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/timeline_page.html)

**Note**: Within the attached VM, you will **NOT** be able to practice with some of the visualisation tools, except for **Timeline**. Below is a screenshot of the **Timeline**.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline.png)

**The Timeline tool is composed of three areas:**

1. **Filters:** Narrow the events displayed based on the filter criteria
2. **Events:** The events are displayed here based on the **View Mode**
3. **Files/Contents:** Additional information on the event(s) is displayed in this area

**There are three view modes:**

1. **Counts:** The number of events is displayed in a bar chart view
2. **Details:** Information on events is displayed, but they are clustered and collapsed, so the UI is not overloaded
3. **List:** The events are displayed in a table view

In the above screenshot, the View Mode is **Counts**. Below is a screenshot of the **Details** View Mode.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-details.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-details.png)

The numbers (seen above) indicate the number of clustered/collapsed events for a specific time frame. For example, for /Windows, there are 130,257 events between 2009-06-10 and 2010-03-18. See the below image.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-clustered.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-clustered.png)

To expand a cluster, click on the `green icon with the plus sign`. See the below example.

![https://assets.tryhackme.com/additional/autopsy/autopsy-cluster-expand.png](https://assets.tryhackme.com/additional/autopsy/autopsy-cluster-expand.png)

To collapse the events, click on the `red icon with a minus sign`. Click `the map marker icon with a plus sign` if you wish to pin a group of events. This will move (pin) the events to an isolated section of the Events view.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-clustered2.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-clustered2.png)

To unpin the events, click on the `map marker with the minus sign`. The last group of icons to cover are the `eye` icons. If you wish to hide a group of events from the Events view, click on the `eye with a minus sign`.  In the below screenshot, the clustered events for /Boot were hidden and placed in `Hidden Descriptions` (in the Filters area).

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-hidden.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-hidden.png)

If you wish to reverse that action and unhide the events, right-click and select `Unhide and remove from list`. See the below example.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-unhide.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-unhide.png)

Last but not least, a screenshot of the **List** View Mode is below.

![https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-list.png](https://assets.tryhackme.com/additional/autopsy/autopsy-timeline-list.png)

This should be enough information to get you started interacting with the Timeline with some level of confidence.

### **REDLINE**

Data Collection

Now that you have the overview for Redline, let's move to the Data Collection stage.

There are three ways or options to collect data using Redline:

![https://assets.tryhackme.com/additional/redline101/capture2.png](https://assets.tryhackme.com/additional/redline101/capture2.png)

1. Standard Collector - this method configures the script to gather a minimum amount of data
for the analysis. This is going to be our preferred method to collect
data in this room. It is also usually the fastest method to collect the
data you need. It takes only a few minutes to complete.
2. Comprehensive Collector - this method configures the script to gather the most data from your
host for further analysis. This method takes up to an hour or more. You
will choose this method if you prefer the full analysis of the system.
3. IOC Search Collector (Windows only) - this method collects data that matches with the [Indicators of Compromise (IOCs)](https://www.crowdstrike.com/cybersecurity-101/indicators-of-compromise/) that you created with the help of [IOC Editor](https://fireeye.market/apps/S7cWpi9W). You will choose this method if you want to run the data collection
against known IOCs that you have gathered either through threat
intelligence (data feed or narrative report), incident response, or
malware analysis. You imported them into [IOC Editor](https://fireeye.market/apps/S7cWpi9W). We'll look at the IOC Editor a bit further in the next task.

Before proceeding, launch Redline. The icon is conveniently on the taskbar.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/021b2784b3b39c0e5817c79815885a15.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/021b2784b3b39c0e5817c79815885a15.png)

In this task, we will be using the Standard Collector method.

- From Redline, click on "Create a Standard Collector".
- You will have an option to choose the target platform. In our case, we will select **Windows**.

![https://assets.tryhackme.com/additional/redline101/targetos.png](https://assets.tryhackme.com/additional/redline101/targetos.png)

- Under the *Review Script Configuration,* click on “Edit your script”, this is one of the crucial steps since you will be presented with the set of data to choose to collect from the host. There will be five tabs, which include **Memory, Disk, System, Network**, and **Other.**

Let's dive into some details:

Memory:

![https://assets.tryhackme.com/additional/redline101/memoryyy.png](https://assets.tryhackme.com/additional/redline101/memoryyy.png)

You
 can configure the script to collect memory data such as process 
listings, drivers enumeration (Windows hosts only), and hook detection (versions before Windows 10).

**Note**: For this exercise, uncheck **Hook Detection** and make sure **Aquire Memory Image** is also unchecked.

Be sure to make changes to the settings in each tab as necessary to mirror the settings illustrated in the task content.

Disk:

This is where you can collect the data on Disks partitions and Volumes along with File Enumeration.

![https://assets.tryhackme.com/additional/redline101/diskkk.png](https://assets.tryhackme.com/additional/redline101/diskkk.png)

System:

The system will provide you with machine information:

- Machine and operating system (OS) information
- Analyze system restore points (Windows versions before 10 only)
- Enumerate the registry hives (Windows only)
- Obtain user accounts (Windows and OS X only)
- Obtain groups (OS X only)
- Obtain the prefetch cache (Windows only)

![https://assets.tryhackme.com/additional/redline101/systemm.png](https://assets.tryhackme.com/additional/redline101/systemm.png)

Network:

Network Options supports Windows, OS
 X, and Linux platforms. You can configure the script to collect network
 information and browser history, which is essential when investigating 
the browser activities, including malicious file downloads and 
inbound/outbound connections.

![https://assets.tryhackme.com/additional/redline101/networkkk.png](https://assets.tryhackme.com/additional/redline101/networkkk.png)

Other:

![https://assets.tryhackme.com/additional/redline101/other.png](https://assets.tryhackme.com/additional/redline101/other.png)

With this option, you can collect the data on different services and tasks running on the system, including the hashes.

- Now we are ready to proceed to the next important step. After choosing your data options - click OK. And then click on*"Browse"* under *"Save Your Collector To"*. Why is this an important step? Because you will need to create a folder where your analysis file will be saved and the script for collecting
the data you need. In our case, we are saving it to the *Analysis* folder.

![https://assets.tryhackme.com/additional/redline101/32.png](https://assets.tryhackme.com/additional/redline101/32.png)

**Note**: You can choose any folder you wish but make sure that the folder is EMPTY. Complete this dialog by clicking the OK button.

- After you choose to save the collector to the folder, you will see the Collector Instructions.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/f8ddaa960778e373c108ea2fa3ebe67f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/f8ddaa960778e373c108ea2fa3ebe67f.png)

- If you go into the folder, you will notice the bat file under the name "RunRedlineAudit". This is the executable script to collect data from the host. The script needs to be *run as Administrator* to be able to collect the data we need.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/ef6666436c67665ba44f03f149a89320.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/ef6666436c67665ba44f03f149a89320.png)

- Running the script will open a command prompt window; this indicates that the
script is running successfully. It will close automatically when the
data collection process finishes.

![https://assets.tryhackme.com/additional/redline101/1213.png](https://assets.tryhackme.com/additional/redline101/1213.png)

**Note**: This process may take between 15-20 minutes to complete.

- After the script is finished, you will notice a new file created - AnalysisSession1 (in the **Sessions** folder) with the *.mans* extension. This file is what we need to be able to import into Redline for
investigation. Just double-click on the file to import the audit data.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/93f84b334ff930f8fdbb3bb316d010c3.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/93f84b334ff930f8fdbb3bb316d010c3.png)

**The Redline Interface**

Let's look at the Redline Interface.

You should have your first analysis file. Double-click on the *AnalysisSession1.mans* file and the data will be imported automatically into Redline. Please give it up to 10 minutes to get the data imported.

![https://i.ibb.co/CH6zS38/red1.png](https://i.ibb.co/CH6zS38/red1.png)

When the data is imported, you will be presented with this view:

![https://i.ibb.co/8YhfzHb/redlineee.png](https://i.ibb.co/8YhfzHb/redlineee.png)

On the left panel, you will see different types of *Analysis Data;* this is where you will perform information gathering and investigation process.

- System Information: this is where you will see the information about the machine, BIOS (Windows only), operating system, and user information.
- Processes: processes will contain different attributes such as Process Name, PID, Path,
Arguments, Parent process, Username, etc. When you expand the Processes
tab, there will be four sections: Handles, Memory Sections, Strings, and Ports.

A handle is a
 connection from a process to an object or resource in a Windows 
operating system. Operating systems use handles for referencing internal
 objects like files, registry keys, resources, etc.

Memory Sections will
 let you investigate unsigned memory sections used by some processes. 
Many processes usually use legitimate dynamic link libraries (DLLs), 
which will be signed. This is particularly interesting because if you 
see any unsigned DLLs then it will be worth taking a closer look.

Strings - you will see the information on the captured strings.

Ports -
 this is one of the critical sections to pay attention to. Most malware 
often initiates the outbound or inbound connections to communicate to 
their command and control server (C2) to do some malicious activities 
like exfiltrating the data or grabbing a payload to the machine. This 
situation is where you can review the suspicious connections from ports 
and IP addresses. Pay attention to the system processes as well. The 
threat actors like to avoid detection by hiding under the system 
processes. For example, explorer.exe or notepad.exe shouldn't be on the 
list of processes with outbound connections.

Some of the other important sections you need to pay attention to are:

- File System (**not included in this analysis session**)
- Registry
- Windows Services
- Tasks (Threat actors like to create scheduled tasks for persistence)
- Event Logs (this another great place to look for the suspicious Windows
PowerShell events as well as the Logon/Logoff, user creation events, and others)
- ARP and Route Entries (**not included in this analysis session**)
- Browser URL History (**not included in this analysis session**)
- File Download History

The **Timeline**
 will help you to better understand when the compromise happened and 
what steps the malicious actor took to escalate the attack. The **Timeline** will also record every action on the file if it got create, changed, modified, accessed.

![https://i.ibb.co/mN1GyRf/files.png](https://i.ibb.co/mN1GyRf/files.png)

If you know when the host compromise or suspicious activity occurred, you can use TimeWrinkles™ to filter out the timeline to only the events that took place around that time.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/0d3564554dec83b1e948cf2e78a41b26.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/0d3564554dec83b1e948cf2e78a41b26.png)

![https://i.ibb.co/k4gB91m/wrinklee.png](https://i.ibb.co/k4gB91m/wrinklee.png)

TimeCrunches™ helps
 to reduce the excessive amount of data that is not relevant in the 
table view. A TimeCrunch will hide the same types of events that 
occurred within the same minute you specified.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e38cdd16a6b56e484a6d9a4549c7348b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e38cdd16a6b56e484a6d9a4549c7348b.png)

![https://i.ibb.co/RTc3t0z/timeline2.png](https://i.ibb.co/RTc3t0z/timeline2.png)

You can find out more about each type of data analysis using the Redline User Guide: [https://fireeye.market/assets/apps/211364/documents/877936_en.pdf](https://fireeye.market/assets/apps/211364/documents/877936_en.pdf).

**IOC Search Collector**

We briefly discussed the usage of the **IOC Search Collector** in the **Data Collection** task.

Let's take a closer look at the capabilities of this collector type. But first, let's recap what an IOC is.

IOC stands for **Indicators of Compromise**;
 they are artifacts of the potential compromise and host intrusion on 
the system or network that you need to look for when conducting threat 
hunting or performing incident response. IOCs can be MD5, SHA1, SHA256 hashes, IP address, C2 domain, file size, filename, file path, a registry key, etc.

One of the great tools you can use is [IOC Editor,](https://fireeye.market/apps/S7cWpi9W) created by FireEye, to create IOC files. You can refer to this link to learn how to use the IOC Editor: [https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf](https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf).

**Note**: According to the [IOC Editor](https://fireeye.market/apps/S7cWpi9W) download page Windows 7 is the latest operating system officially supported. It is the same version installed in the attached VM. There is another tool called [OpenIOC Editor](https://fireeye.market/apps/211404) by FireEye, which supports Windows 10 that is worth taking a look at.

**Tip**: Before proceeding you can close Redline to free up some system resources while using IOC Editor.

You can create a text file containing IOCs, modify them, and share it with other people in the InfoSec industry.

In this example, we will look at an IOC of a keylogger created with IOC Editor.

**Note**: Below, you may follow along with the screenshots and don't have to create the IOC file in this task. You will create an IOC file using IOC Editor and perform an IOC Search in the next task.

Open IOC Editor which was conveniently placed for you in the taskbar next to Redline.

**Note:** It may take ~60 seconds for the application to launch.

Before proceeding,  create the directory which will store the IOC file (IOC Directory).

Next, create the IOC file.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/b26d9e80ac55821643531c3a0436f633.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/b26d9e80ac55821643531c3a0436f633.png)

**Keylogger indicators in IOC Editor**:

![https://i.ibb.co/02VS0M6/keylogger2.png](https://i.ibb.co/02VS0M6/keylogger2.png)

A brief explanation of the above image:

- The **Name** of the IOC file is Keylogger, Keylogger.ioc. (this field you can edit)
- The **Author** is RussianPanda. (this field you can edit)
- **GUID**, **Created**, and **Modified** are fields you can **NOT** edit, and IOC Editor populates the information.
- Under **Description**, you can add a summary explaining the purpose of the IOC file.

The actual IOCs will be added under, you guessed it, **Add**.

Here are the values from the image above:

- **File Strings** - `psylog.exe`
- **File Strings** - `RIDEV_INPUTSINK`
- **File MD5** - `791ca706b285b9ae3192a33128e4ecbb`
- **File Size** - `35400`

Refer to the gif below to get an idea of adding specific IOCs to the IOC file.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/01db4361981d214c2692aa10d59961d1.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/01db4361981d214c2692aa10d59961d1.gif)

Once you select an item you can enter the value for the item directly.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/81e9ffdb97a2ce98e8b9cec57a2be261.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/81e9ffdb97a2ce98e8b9cec57a2be261.png)

You can also add it within the **Properties**.

All the fields are read-only except for **Content** and **Comment**. To add a value to the item enter it under **Content**.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5a0e549950f7ca673699d51a2ff14bc9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5a0e549950f7ca673699d51a2ff14bc9.png)

Once you enter the value click Save to save it.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9d95abf1f3d62f3fe7d2eb6352b86235.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9d95abf1f3d62f3fe7d2eb6352b86235.png)

**Note**: You can right-click on an item for additional options. See below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/f5173beaf331e84b7672daf6be726092.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/f5173beaf331e84b7672daf6be726092.png)

We'll leave that for you to explore on your own.

Now that we've created and saved the IOC file, let's move on and go back to the **IOC Search Collector** in the **Redline** tool.

**Note**: If you closed Redline now is the time to relaunch the application. You can close IOC Editor, again, to free up system resources.

**IOC Search Collector**

will ignore the data that doesn't match an

IOC

you have gathered. Although, you can always choose to collect 
additional data. As the Redline User Guide states, the quality of the 
IOC analysis will depend on the data you have available in the analysis 
session.

![https://i.ibb.co/SwvyRyq/ioc.png](https://i.ibb.co/SwvyRyq/ioc.png)

To create an IOC
 Search Collector, click "Browse..." and choose the location of the .ioc
 file. Redline will automatically detect the .ioc file and place it in 
the Indicators section, as shown below.

**IOC Search Collector**:

![https://i.ibb.co/2S2t1sB/keylogger.png](https://i.ibb.co/2S2t1sB/keylogger.png)

**Unsupported Search Terms:** These terms will not show any successful hits in Redline, which means Redline doesn't recognize specific search terms.

**Supported Search Terms:** The terms that Redline will recognize and search for.

After
 you are finished reviewing the configured IOCs, click "Next". Now click
 on "Edit your script" to configure what data will be collected for the 
analysis. For this example, Keylogger file IOC Search, the following parameters were selected.

![https://i.ibb.co/g7JkhPr/keylogger3.png](https://i.ibb.co/g7JkhPr/keylogger3.png)

**Note**: When you configure your own IOC Search, you will choose different settings for your script compared to the settings above.

When done editing the script, click "OK".

In
 the "Save Your Collector To" section, click "Browse" and choose an 
empty folder where your analysis file will be saved along with the **RunRedlineAudit.bat** file.

After executing the .bat file in the same manner as before, let's now wait for the analysis to finish.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/014d546f9f31bb0e7458c835ebf17386.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/014d546f9f31bb0e7458c835ebf17386.png)

After
 the analysis is finished, you will see the .mans file (AnalysisSession1
 in our example). Double-click the file to open it in Redline.

![https://i.ibb.co/xhJwX1f/analysis.png](https://i.ibb.co/xhJwX1f/analysis.png)

If Redline fails to generate the IOC Report automatically, you can manually generate it by clicking "Create a New IOC Report" and importing your .ioc file.

When the report generation completes, you should see the "Hits". You can expand the list by clicking on the entries in each row.

![https://i.ibb.co/bvVVdj5/keyllogger4.png](https://i.ibb.co/bvVVdj5/keyllogger4.png)

From the screenshot, you can see that there was one hit on "chrome.dll", this is a false positive. Let's review the details below.

![https://i.ibb.co/d0RCvdH/hits2.png](https://i.ibb.co/d0RCvdH/hits2.png)

As you can see, the DLL
 file matched with the string "RIDEV_INPUTSINK" that we had in our .ioc 
file. It's important to gather granulated and accurate artifacts to add 
to your IOC file to avoid false positives.

The screenshot below is of a file with the most amount of "Hits", which means it is most likely the file we are looking for.

![https://i.ibb.co/tzvyS6w/hits3.png](https://i.ibb.co/tzvyS6w/hits3.png)

- Redline User Guide: [https://fireeye.market/assets/apps/211364/documents/877936_en.pdf](https://fireeye.market/assets/apps/211364/documents/877936_en.pdf)
- IOC Editor User Guide: [https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf](https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf)

### **KAPE**

Kroll Artifact Parser and Extractor (KAPE) parses and extracts 
Windows forensics artifacts. It is a tool that can significantly reduce 
the time needed to respond to an incident by providing forensic 
artifacts from a live system or a storage device much earlier than the 
imaging process completes.

KAPE serves two primary purposes, 1) collect files and 2) process the
 collected files as per the provided options. For achieving these 
purposes, KAPE uses the concept of targets and modules. Targets can be 
defined as the forensic artifacts that need to be collected. Modules are
 programs that process the collected artifacts and extract information 
from them. We will learn about them in the upcoming tasks.

## **How it works**

KAPE is extensible and highly configurable. In essence, the KAPE 
binary ﻿ collects files and processes them as per the provided 
configuration.

The collection of files (targets) KAPE adds the files to a queue and 
copies them in two passes. In the first pass, it copies the files that 
it can. This works for files that the OS has not locked. The rest of the
 files are passed to a secondary queue. The secondary queue is processed
 using a different technique that uses raw disk reads to bypass the OS 
locks and copy the files. The copied files are saved with original 
timestamps and metadata and stored in a similar directory structure.

Once the data is collected, KAPE can process it using modules. The 
modules can be independent binaries that run on the collected data and 
process them to extract information. For example, KAPE will collect and 
copy the Prefetch file to our target destination during the target 
collection. Running a Prefetch Parser (PECmd) module on this target will
 extract the prefetch file and save it in a CSV file.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d1489a8062d714fa227dd3382dfd15d1.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d1489a8062d714fa227dd3382dfd15d1.png)

As the above image shows, KAPE can extract targets from a Live system, a mounted image, or the [F-response](https://www.f-response.com/) utility. KAPE does not need to be installed. It is portable and can be used from network locations or USB drives.

**Target Options**

In KAPE's lexicon, `Targets`
 are the artifacts that need to be collected from a system or image and 
copied to our provided destination. For example, as we learned in the 
last room, Windows Prefetch is a forensic artifact for evidence of 
execution so that we can create a `Target` for it. Similarly, we can also create `Targets` for the registry hives. In short, `Targets` copy files from one place to another.

When we open the `Targets` directory of KAPE, this is what we will see:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3902f2f2088969b01e9672553f48c9e4.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/3902f2f2088969b01e9672553f48c9e4.png)

The last four files at the bottom are guides and templates to create `Targets` and `Compound Targets` of our own. We will discuss `Compound Targets` later in this task. As you can see, the targets are grouped into different directories. Let's check out the `Windows` directory to see what we have:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/20d9d19240bcaeb95b55ad2efb105c1c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/20d9d19240bcaeb95b55ad2efb105c1c.png)

We can see different .tkape extension files. This is how a `Target`
 is defined for KAPE. A TKAPE file contains information about the 
artifact that we want to collect, such as the path, category, and file 
masks to collect. As an example, below is how the Prefetch `Target` is defined.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/92dce7807d9ea37f6f5e1e62f271275b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/92dce7807d9ea37f6f5e1e62f271275b.png)

This TKAPE file tells KAPE to collect files with the file mask `*.pf` from the path `C:\Windows\prefetch` and `C:\Windows.old\prefetch`.

Notice that we have the `C:\Windows.old` path listed here 
as well. This path contains files retained after Windows has updated to a
 new version. For forensic analysis, we can also find interesting 
historical artifacts from this directory.

## **Compound Targets:**

KAPE also supports `Compound Targets`. These are `Targets`
 that are compounds of multiple other targets. As mentioned in the 
previous tasks, KAPE is often used for quick triage collection and 
analysis. The purpose of KAPE will not be fulfilled if we have to 
collect each artifact individually. Therefore, `Compound Targets` help us collect multiple targets by giving a single command. Examples of `Compound Targets` include `!BasicCollection`, `!SANS_triage` and `KAPEtriage`. We can view the `Compound Targets` on the path `KAPE\Targets\Compound`. The following image shows what a `Compound Target` for evidence of execution looks like:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/76260284a8d68c7d38126a7237e9c16a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/76260284a8d68c7d38126a7237e9c16a.png)

The above `Compound Target` will collect evidence of execution from Prefetch, RecentFileCache, AmCache, and Syscache `Targets`.

## **!Disabled**

This directory contains `Targets` that you want to keep in the KAPE instance, but you don't want them to appear in the active Targets list.

## **!Local**

If you have created some `Targets` that you don't want to sync with the KAPE Github repository, you can place them in this directory. These can be `Targets` that are specific to your environment. Similarly, anything not present in th

**Module Options**

`Modules`, 
in KAPE's lexicon, run specific tools against the provided set of files.
 Their goal is not to copy files from one place to another but rather 
run some command and store the output. Generally, the output is in the 
form of CSV or TXT files.

This is what the `Modules` directory looks like in KAPE:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e4dbd842fa5b548ac8fade7b94ab0c8a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/e4dbd842fa5b548ac8fade7b94ab0c8a.png)

Similar to the previous task, we see guides and templates for creating `Modules` and `Compound Modules`. We also see the `!Disabled`, `!Local` and `Compound`
 directories, which are similar to what we saw in the previous task. We 
will not discuss these again, as we discussed them in the last task. We 
see that most of the `Modules` are grouped together in different directories. One thing we find different is the `bin` directory. We will discuss that in a bit. For now, let's open the Windows directory and see what we have there:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9a9760a2f1004e74b23294681f7bfdef.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9a9760a2f1004e74b23294681f7bfdef.png)

Here we see files with the `.mkape` extension. These are understood as `Modules` by KAPE. Let's open an MKAPE file and see how it is structured. The following image shows the Windows_IPConfig MKAPE file.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/15bfb563be1d5bf1e988ab3e7486b58e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/15bfb563be1d5bf1e988ab3e7486b58e.png)

Notice
 that the MKAPE file tells KAPE about the executable that has to be run,
 the command line parameters of the executable file, the output export 
format, and the filename to export to. But what if the executable that 
we want to run is not present on the system? This brings us to the `bin` directory.

## **The bin directory:**

The `bin` directory contains executables that we want to 
run on the system but are not natively present on most systems. KAPE 
will run executables either from the `bin` directory or the complete path. An example of files to be kept in the `bin`
 directory are Eric Zimmerman's tools, which are generally not present 
on a Windows system. We used them extensively in the Windows Forensics 
rooms.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a3547f25552d5d440d4f85022b53bc01.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a3547f25552d5d440d4f85022b53bc01.png)

Notice that most of the binaries present here are from Eric Zimmerman's Tools.

**KAPE GUI**

Now that we have learned about the different components of KAPE let's take it for a test drive. In the attached VM, double-click to open the gkape.exe file. You will see the following Window:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/2c483331a6c0218db3bad9d79289447c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/2c483331a6c0218db3bad9d79289447c.png)

**Tip:** If the Window is not correctly visible in the split-screen, you can open it in a full browser tab by clicking this button:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/af1a133b7384aac273451343dadc032d.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/af1a133b7384aac273451343dadc032d.png)

Here you can see that there are different options, but most are disabled. To collect `Targets` We will go ahead by enabling the `Use Target Options` checkbox. This will enable the options present in the left half of the Window:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/ef839c3076a311b29ac9fedd933d58d8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/ef839c3076a311b29ac9fedd933d58d8.png)

If we want to perform forensics on the same machine on which KAPE is running, we will provide `C:\`
 for the Target source. We can select the target destination of our 
choice. All the triage files will be copied to the Target destination 
that we provide.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f4a865927aef7b0fa4668f13ef8f9cfa.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/f4a865927aef7b0fa4668f13ef8f9cfa.png)

Here, the `Flush`
 checkbox will delete all the contents of the Target destination, so we 
have to be careful when using that. We have disabled the `Flush` checkbox so that it does not delete data already present in the directories. `Add %d` will append date info to the directory name where the collected data is saved. Similarly, `Add %m`
 will append machine info to the Target destination directory. We can 
select our desired Target from the list shown above. The Search bar 
helps us search for the names of the desired Targets quickly.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a513c60028421e8fd103a161e1492e0a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a513c60028421e8fd103a161e1492e0a.png)

We can select if we want to process Volume Shadow Copies by enabling `Process VSCs`. We can select the `transfer` checkbox if we want to transfer the collected artifacts through an SFTP server or an S3 bucket.
 For transfer, the files must be enclosed in a container, which can be 
Zip, VHD, or VHDX. Similarly, we can provide exclusions based on SHA-1, 
and KAPE will not copy the excluded files. When enclosing in a container, we will need to give a `Base name`
 that will be used for all the created files. It is not required if we 
are not transferring files or enclosing them in a container.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/22a7063c7c3bb75bc2ddaede7fcf9f57.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/22a7063c7c3bb75bc2ddaede7fcf9f57.png)

In the `Current command line` tab,
 we can see the command line options being added or removed while 
configuring the UI. This Window will show more options in the command 
line as we add options. Please note that the destination path in your 
case will be different from the one shown in the image. Notice the `--tflush` flag here. It means that when this command line was created, the `Flush` checkbox was still checked.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fd514feceacfd972097ef26b5ac433ed.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/fd514feceacfd972097ef26b5ac433ed.png)

By checking the Use Module Options checkbox, the right side of the KAPE Window will also be enabled.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/811ceeea4083ab70546d89f5ecfc2f6f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/811ceeea4083ab70546d89f5ecfc2f6f.png)

When
 using both Target and Module Options, providing Module Source is not 
required. The selected Modules will use the Target destination as the 
source.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8807a5d8eaf027af5f6e0a174e8079d3.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8807a5d8eaf027af5f6e0a174e8079d3.png)

The rest of the options for Modules are similar to the ones for Targets, so we won't go into details for them.

Below you will see what the configuration looks like when we have KAPE all set up for collecting Targets and processing them using Modules.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d4e260cbc96fd497859c9133cdb345a8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d4e260cbc96fd497859c9133cdb345a8.png)

We have selected the `KapeTriage` compound Target and `!EZParser` Compound Module. The command line below shows the CLI command that will be run. The `Execute!` button in the bottom right corner will execute the command. The `Disable flush warnings` checkbox underneath it will not warn us when we are using the `Flush` flags. When we press `Execute!` We will see a command line window open and show us the logs as KAPE
 performs its tasks. It will take a few minutes to execute since it will
 be collecting all the data and then running the module processes on it.
 Once it completes, it will show us the total execution time, and we can
 press any key to terminate the command window.

D:\Kape\kape.exe

```
KAPE version 1.1.0.1 Author: Eric Zimmerman (kape@kroll.com)

KAPE directory: D:\KAPE
Command line: --tsource C: --tdest C:\Users\Umair\Desktop\kape --target KapeTriage --mdest C:\Users\Umair\Desktop\4n6-2 --module !EZParser --gui

System info: Machine name: UMAIR-THINKBOOK, 64-bit: True, User: Umair OS: Windows10 (10.0.22000)

Using Target operations
Found 14 targets. Expanding targets to file list...
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Found 3,059 files in 4.257 seconds. Beginning copy...
        Deferring 'C:\Windows\System32\winevt\logs\Application.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4Operational.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4WHC.evtx' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPDetection-20220126-183133.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPDeviceControl-20211016-164735.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPLog-10172021-040927.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MpWppTracing-20220210-070038-00000003-ffffffff.bin' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\HardwareEvents.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\IntelAudioServiceLog.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\Internet Explorer.evtx' due to IOException...
.
.
.
.
Executing remaining modules...
        Running 'EvtxECmd\EvtxECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\EventLogs
        Running 'JLECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'LECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'PECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\ProgramExecution -q
        Running 'RBCmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileDeletion -q
        Running 'RECmd\RECmd.exe': -d C:\Users\Umair\Desktop\kape --bn BatchExamples\Kroll_Batch.reb --nl false --csv C:\Users\Umair\Desktop\4n6-2\Registry -q
        Running 'SBECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'SQLECmd\SQLECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\SQLDatabases
        Running 'SrumECmd.exe': -d C:\Users\Umair\Desktop\kape -k --csv C:\Users\Umair\Desktop\4n6-2\SystemActivity
        Running 'SumECmd.exe': -d C:\Users\Umair\Desktop\kape\Windows\System32\LogFiles\SUM --csv C:\Users\Umair\Desktop\4n6-2\SUMDatabase
Executed 18 processors in 192.2738 seconds

Total execution time: 258.1812 seconds

Press any key to exit

```

Notice that at the backend, KAPE is running the `kape.exe` in a command line. We can check out the files created by KAPE once it completes processing them. The below snapshot shows our `Module destination`. Notice how KAPE has processed the files according to different categories.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a0fad94b0afd9f8f424f3071f0d4e475.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/a0fad94b0afd9f8f424f3071f0d4e475.png)

**KAPE CLI**

Though we used the GUI
 in the previous task, KAPE is a command-line tool. Therefore, it is 
pertinent to know how to use KAPE through the command line to make full 
use of it.

For a list of all the different switches that can be used with KAPE, open an elevated PowerShell (Run As Administrator), go to the path where the KAPE binary is located, and type `kape.exe`. You will see something like this as an output.

Administrator: Command Prompt

```
D:\KAPE>kape.exe

KAPE version 1.1.0.1 Author: Eric Zimmerman (kape@kroll.com)

        tsource         Target source drive to copy files from (C, D:, or F:\ for example)
        target          Target configuration to use
        tdest           Destination directory to copy files to. If --vhdx, --vhd or --zip is set, files will end up in VHD(X) container or zip file
        tlist           List available Targets. Use . for Targets directory or name of subdirectory under Targets.
        tdetail         Dump Target file details
        tflush          Delete all files in 'tdest' prior to collection
        tvars           Provide a list of key:value pairs to be used for variable replacement in Targets. Ex: --tvars user:eric would allow for using %user% in a Target which is replaced with eric at runtime. Multiple pairs should be separated by ^
        tdd             Deduplicate files from --tsource (and VSCs, if enabled) based on SHA-1. First file found wins. Default is TRUE

        msource         Directory containing files to process. If using Targets and this is left blank, it will be set to --tdest automatically
        module          Module configuration to use
        mdest           Destination directory to save output to
        mlist           List available Modules. Use . for Modules directory or name of subdirectory under Modules.
        mdetail         Dump Module processors details
        mflush          Delete all files in 'mdest' prior to running Modules
        mvars           Provide a list of key:value pairs to be used for variable replacement in Modules. Ex: --mvars foo:bar would allow for using %foo% in a module which is replaced with bar at runtime. Multiple pairs should be separated by ^
        mef             Export format (csv, html, json, etc.). Overrides what is in Module config

        sim             Do not actually copy files to --tdest. Default is FALSE
        vss             Process all Volume Shadow Copies that exist on --tsource. Default is FALSE

        vhdx            The base name of the VHDX file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhd or --zip
        vhd             The base name of the VHD file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhdx or --zip
        zip             The base name of the ZIP file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhdx or --vhd

        scs             SFTP server host/IP for transferring *compressed VHD(X)* container
        scp             SFTP server port. Default is 22
        scu             SFTP server username. Required when using --scs
        scpw            SFTP server password
        scd             SFTP default directory to upload to. Will be created if it does not exist
        scc             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        s3p             S3 provider name. Example: spAmazonS3 or spGoogleStorage. See 'https://bit.ly/34s9nS6' for list of providers. Default is 'spAmazonS3'
        s3r             S3 region name. Example: us-west-1 or ap-southeast-2. See 'https://bit.ly/3aNxXhc' for list of regions by provider
        s3b             S3 bucket name
        s3k             S3 Access key
        s3s             S3 Access secret
        s3st            S3 Session token
        s3kp            S3 Key prefix. When set, this value is used as the beginning of the key. Example: 'US1012/KapeData'
        s3o             When using 'spOracle' provider, , set this to the 'Object Storage Namespace' to use
        s3c             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        s3url           S3 Presigned URL. Must be a PUT request vs. a GET request

        asu             Azure Storage SAS Uri
        asc             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        zv              If true, the VHD(X) container will be zipped after creation. Default is TRUE
        zm              If true, directories in --mdest will be zipped. Default is FALSE
        zpw             If set, use this password when creating zip files (--zv | --zm | --zip)

        hex             Path to file containing SHA-1 hashes to exclude. Only files with hashes not found will be copied

        debug           Show debug information during processing
        trace           Show trace information during processing

        gui             If true, KAPE will not close the window it executes in when run from gkape. Default is FALSE

        ul              When using _kape.cli, when true, KAPE will execute entries in _kape.cli one at a time vs. in parallel. Default is FALSE

        cu              When using _kape.cli, if true, KAPE will delete _kape.cli and both Target/Module directories upon exiting. Default is FALSE

        sftpc           Path to config file defining SFTP server parameters, including port, users, etc. See documentation for examples
        sftpu           When true, show passwords in KAPE switches for connection when using --sftpc. Default is TRUE

        rlc             If true, local copy of transferred files will NOT be deleted after upload. Default is FALSE
        guids           KAPE will generate 10 GUIDs and exit. Useful when creating new Targets/Modules. Default is FALSE
        sync            If true, KAPE will download the latest Targets and Modules from specified URL prior to running. Default is https://github.com/EricZimmerman/KapeFiles/archive/master.zip

        ifw             If false, KAPE will warn if a process related to FTK is found, then exit. Set to true to ignore this warning and attempt to proceed. Default is FALSE

        Variables: %d = Timestamp (yyyyMMddTHHmmss)
                   %s = System drive letter                   %m = Machine nameExamples: kape.exe --tsource L: --target RegistryHives --tdest "c:\temp\RegistryOnly"
          kape.exe --tsource H --target EvidenceOfExecution --tdest "c:\temp\default" --debug
          kape.exe --tsource \\server\directory\subdir --target Windows --tdest "c:\temp\default_%d" --vhdx LocalHost
          kape.exe --msource "c:\temp\default" --module LECmd --mdest "c:\temp\modulesOut" --trace --debug

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

          Full documentation: https://ericzimmerman.github.io/KapeDocs/

D:\KAPE>
```

We can see from the above screenshot that while collecting Targets, the switches `tsource`, `target` and `tdest` are required. Similarly, when processing files using Modules, `module` and `mdest` are required switches. The other switches are optional as per the requirements of the collection.

With
 this information, let's build a command to perform the same task we 
performed in the previous task. i.e., collect triage data using the `KapeTriage` Compound Target and process it using the `!EZParser` Compound Module. Since we are not using the GUI version, we will start with typing:

`kape.exe`

To add a Target source, let's append `--tsource` and that Target path:

`kape.exe --tsource C:`

The `--target` flag will be used for selecting the Target the `--tdest`
 flag for the Target destination. For the sake of simplicity, we will 
set the Target destination to a directory named target on the Desktop. KAPE will create a new directory if it doesn't already exist. Our command line now looks like this:

`kape.exe --tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\target`

Running
 the above command will collect triage data defined in the KapeTriage 
Target and save it to the provided destination. However, it will not 
process it or perform any other activity on the data.

If we want to flush the Target destination, we can add `--tflush` to do that. For now, let's move on to adding the Module options. If we were using a Module source, we would have used a >`--msource` flag in a similar manner to the `--tsource`
 flag. But in this case, let's use the Target destination as the Module 
source. By doing this, we will not need to add it explicitly, and we can
 move on to adding the Module destination using the `--mdest` flag:

`kape.exe --tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module`

We have just used a directory named module for the Module destination.

To Process the Target destination using a Module, we need to provide the Module name using the `--module` flag. To process it using the `!EZParser` Module, we will append `--module !EZParser`, making our command look like this:

`kape.exe --tsource C: --target KapeTriage --tdest 
C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module 
--module !EZParser`

Please note that we will need to run this command in an elevated shell (with Administrator privileges) for KAPE to collect the data.

We can modify the command as per our needs and the switches provided by KAPE.
 When we run this command, we will see a similar window as in the 
previous task. You can check out the files collected by KAPE Targets and
 Modules once it completes.

## **Batch Mode:**

KAPE can also be run in batch mode. What this means is that we can provide a list of commands for KAPE to run in a file named `_kape.cli`. Then we keep this file in the directory containing the KAPE binary. When `kape.exe` is executed as an administrator, it checks if there is `_kape.cli`
 file present in the directory. If so, it executes the commands 
mentioned in the cli file. This mode can be used if you need someone to 
run KAPE
 for you, you will keep all the commands in a single line, and all you 
need is for the person to right-click and run kape.exe as administrator.
 For example, if we have to perform the same task as we did earlier in 
this task using batch mode, we will have to create a _kape.cli file with
 the following content:

- `-tsource C: --target KapeTriage --tdest
C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module
--module !EZParser`

When we run `kape.exe`, it will perform the same tasks as when we ran it through CLI above.

### **VOLATILITY**

**Identifying Image Info and Profiles**

By default, Volatility comes with all existing Windows profiles from Windows XP to Windows 10.

Image profiles can be hard to determine if you don't know exactly 
what version and build the machine you extracted a memory dump from was.
 In some cases, you may be given a memory file with no other context, 
and it is up to you to figure out where to go from there. In that case, 
Volatility has your back and comes with the `imageinfo` plugin. This plugin will take the provided memory dump and assign it a list of the best possible OS
 profiles. OS profiles have since been deprecated with Volatility3, so 
we will only need to worry about identifying the profile if using 
Volatility2; this makes life much easier for analyzing memory dumps.

Note: `imageinfo` is not always correct and can have 
varied results depending on the provided dump; use with caution and test
 multiple profiles from the provided list.

If we are still looking to get information about what the host is 
running from the memory dump, we can use the following three plugins `windows.info` `linux.info` `mac.info`.  This plugin will provide information about the host from the memory dump.

Syntax: `python3 vol.py -f <file> windows.info`

`DTB     0x2fe000                                                                                                                                                Symbols file:///opt/volatility3/volatility3/symbols/windows/ntkrnlpa.pdb/30B5FB31AE7E4ACAABA750AA241FF331-1.json.xz                                             Is64Bit False                                                                                                                                                   IsPAE   True                                                                                                                                                    primary 0 WindowsIntelPAE                                                                                                                                       memory_layer    1 FileLayer                                                                                                                                     KdDebuggerDataBlock     0x80545ae0                                                                                                                              NTBuildLab      2600.xpsp.080413-2111                                                                                                                           CSDVersion      3                                                                                                                                               KdVersionBlock  0x80545ab8                                                                                                                                      Major/Minor     15.2600                                                                                                                                         MachineType     332                                                                                                                                             KeNumberProcessors      1                                                                                                                                       SystemTime      2012-07-22 02:45:08                                                                                                                             NtSystemRoot    C:\WINDOWS                                                                                                                                      NtProductType   NtProductWinNt                                                                                                                                  NtMajorVersion  5                                                                                                                                               NtMinorVersion  1                                                                                                                                               PE MajorOperatingSystemVersion  5                                                                                                                               PE MinorOperatingSystemVersion  1                                                                                                                               PE Machine      332                                                                                                                                             PE TimeDateStamp        Sun Apr 13 18:31:06 2008                                                                                                                thmanalyst@ubuntu:/opt/volatility3$ exit`

Listing Processes and Connections

Five different plugins 
within Volatility allow you to dump processes and network connections, 
each with varying techniques used. In this task, we will be discussing 
each and its pros and cons when it comes to evasion techniques used by 
adversaries.

The most basic way of listing processes is using `pslist`;
 this plugin will get the list of processes from the doubly-linked list 
that keeps track of processes in memory, equivalent to the process list 
in task manager. The output from this plugin will include all current 
processes and terminated processes with their exit times.

Syntax: `python3 vol.py -f <file> windows.pslist`

```

```

00:00

Some
 malware, typically rootkits, will, in an attempt to hide their 
processes, unlink itself from the list. By unlinking themselves from the
 list you will no longer see their processes when using `pslist`.  To combat this evasion technique, we can use `psscan`;this technique of listing processes will locate processes by finding data structures that match `_EPROCESS`. While this technique can help with evasion countermeasures, it can also cause false positives.

Syntax: `python3 vol.py -f <file> windows.psscan`

```

```

00:00

The third process plugin, `pstree`,
 does not offer any other kind of special techniques to help identify 
evasion like the last two plugins; however, this plugin will list all 
processes based on their parent process ID, using the same methods as `pslist`.
 This can be useful for an analyst to get a full story of the processes 
and what may have been occurring at the time of extraction.

Syntax: `python3 vol.py -f <file> windows.pstree`

```

```

00:00

Now
 that we know how to identify processes, we also need to have a way to 
identify the network connections present at the time of extraction on 
the host machine. `netstat` will attempt to identify all memory structures with a network connection.

Syntax: `python3 vol.py -f <file> windows.netstat`

This
 command in the current state of volatility3 can be very unstable, 
particularly around old Windows builds. To combat this, you can utilize 
other tools like bulk_extractor to extract a PCAP
 file from the memory file. In some cases, this is preferred in network 
connections that you cannot identify from Volatility alone. [https://tools.kali.org/forensics/bulk-extractor](https://tools.kali.org/forensics/bulk-extractor)

The last plugin we will cover is `dlllist`. This plugin will list all DLLs
 associated with processes at the time of extraction. This can be 
especially useful once you have done further analysis and can filter 
output to a specific DLL that might be an indicator for a specific type 
of malware you believe to be present on the system.

Syntax: `python3 vol.py -f <file> windows.dlllist`

**Volatility Hunting and Detection Capabilities**

Volatility offers a 
plethora of plugins that can be used to aid in your hunting and 
detection capabilities when hunting for malware or other anomalies 
within a system's memory.

It is recommended that you have a basic understanding of how evasion 
techniques and various malware techniques are employed by adversaries, 
as well as how to hunt and detect them before going through this 
section.

The first plugin we will be talking about that is one of the most useful when hunting for code injection is `malfind`.
 This plugin will attempt to identify injected processes and their PIDs 
along with the offset address and a Hex, Ascii, and Disassembly view of 
the infected area. The plugin works by scanning the heap and identifying
 processes that have the executable bit set `RWE or RX` and/or no memory-mapped file on disk (file-less malware).

Based on what `malfind` identifies, the injected area will
 change. An MZ header is an indicator of a Windows executable file. The 
injected area could also be directed towards shellcode which requires 
further analysis.

Syntax: `python3 vol.py -f <file> windows.malfind`

```
01 00 00 00 00 00 00 00 ........        00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 2a 00 2a 00 01 00 00 00 00 00 00 00                                                                                         1484    explorer.exe    0x1460000       0x1480fff       VadS    PAGE_EXECUTE_READWRITE  33      1       Disabled                                                4d 5a 90 00 03 00 00 00 MZ......                                                                                                                                04 00 00 00 ff ff 00 00 ........                                                                                                                                b8 00 00 00 00 00 00 00 ........                                                                                                                                40 00 00 00 00 00 00 00 @.......                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 e0 00 00 00 ........        4d 5a 90 00 03 00 00 00 04 00 00 00 ff ff 00 00 b8 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 e0 00 00 00                                                                                         1640    reader_sl.exe   0x3d0000        0x3f0fff        VadS    PAGE_EXECUTE_READWRITE  33      1       Disabled                                                4d 5a 90 00 03 00 00 00 MZ......                                                                                                                                04 00 00 00 ff ff 00 00 ........                                                                                                                                b8 00 00 00 00 00 00 00 ........                                                                                                                                40 00 00 00 00 00 00 00 @.......                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 00 00 00 00 ........                                                                                                                                00 00 00 00 e0 00 00 00 ........        4d 5a 90 00 03 00 00 00 04 00 00 00 ff ff 00 00 b8 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 e0 00 00 00                                                                                         thmanalyst@ubuntu:/opt/volatility3$ exit
```

00:12

Volatility also offers the capability to compare the memory file against YARA rules. `yarascan`
 will search for strings, patterns, and compound rules against a rule 
set. You can either use a YARA file as an argument or list rules within 
the command line.

Syntax: `python3 vol.py -f <file> windows.yarascan`

There
 are other plugins that can be considered part of Volatility's hunting 
and detection capabilities; however, we will be covering them in the 
next task.

**Advanced Memory Forensics**

Advanced Memory 
Forensics can become confusing when you begin talking about system 
objects and how malware interacts directly with the system, especially 
if you do not have prior experience hunting some of the techniques used 
such as hooking and driver manipulation. When dealing with an advanced 
adversary, you may encounter malware, most of the time rootkits that 
will employ very nasty evasion measures that will require you as an 
analyst to dive into the drivers, mutexes, and hooked functions. A 
number of modules can help us in this journey to further uncover malware
 hiding within memory.

The first evasion technique we will be hunting is hooking; there are 
five methods of hooking employed by adversaries, outlined below:

- SSDT Hooks
- IRP Hooks
- IAT Hooks
- EAT Hooks
- Inline Hooks

We will only be focusing on hunting SSDT hooking as this one of the 
most common techniques when dealing with malware evasion and the easiest
 plugin to use with the base volatility plugins.

The `ssdt` plugin will search for hooking and output its 
results. Hooking can be used by legitimate applications, so it is up to 
you as the analyst to identify what is evil. As a brief overview of what
 SSDT hooking is: `SSDT` stands for *System Service Descriptor Table;* the
 Windows kernel uses this table to look up system functions. An 
adversary can hook into this table and modify pointers to point to a 
location the rootkit controls.

There can be hundreds of table entries that `ssdt` will 
dump; you will then have to analyze the output further or compare 
against a baseline. A suggestion is to use this plugin after 
investigating the initial compromise and working off it as part of your 
lead investigation.

Syntax: `python3 vol.py -f <file> windows.ssdt`

```
262     0x8057971c      ntoskrnl        NtUnloadDriver                                                                                                          263     0x80618b36      ntoskrnl        NtUnloadKey                                                                                                             264     0x80618d50      ntoskrnl        NtUnloadKeyEx                                                                                                           265     0x8056e856      ntoskrnl        NtUnlockFile                                                                                                            266     0x805ac4ce      ntoskrnl        NtUnlockVirtualMemory                                                                                                   267     0x805a8296      ntoskrnl        NtUnmapViewOfSection                                                                                                    268     0x805f1502      ntoskrnl        NtVdmControl                                                                                                            269     0x80639288      ntoskrnl        NtWaitForDebugEvent                                                                                                     270     0x805b6176      ntoskrnl        NtWaitForMultipleObjects                                                                                                271     0x805b608c      ntoskrnl        NtWaitForSingleObject                                                                                                   272     0x8060d5ba      ntoskrnl        NtWaitHighEventPair                                                                                                     273     0x8060d556      ntoskrnl        NtWaitLowEventPair                                                                                                      274     0x80572248      ntoskrnl        NtWriteFile                                                                                                             275     0x80572858      ntoskrnl        NtWriteFileGather                                                                                                       276     0x8059b1ac      ntoskrnl        NtWriteRequestData                                                                                                      277     0x805a981c      ntoskrnl        NtWriteVirtualMemory                                                                                                    278     0x8050222c      ntoskrnl        NtYieldExecution                                                                                                        279     0x8060e632      ntoskrnl        NtCreateKeyedEvent                                                                                                      280     0x8060e71c      ntoskrnl        NtOpenKeyedEvent                                                                                                        281     0x8060e7ce      ntoskrnl        NtReleaseKeyedEvent                                                                                                     282     0x8060ea5a      ntoskrnl        NtWaitForKeyedEvent                                                                                                     283     0x805c1798      ntoskrnl        NtQueryPortInformationProcess                                                                                           thmanalyst@ubuntu:/opt/volatility3$ exit
```

00:09

Adversaries will also use malicious driver files as part of their evasion. Volatility offers two plugins to list drivers.

The `modules`
 plugin will dump a list of loaded kernel modules; this can be useful in
 identifying active malware. However, if a malicious file is idly 
waiting or hidden, this plugin may miss it.

This plugin is best 
used once you have further investigated and found potential indicators 
to use as input for searching and filtering.

Syntax: `python3 vol.py -f <file> windows.modules`

```
0x8205f2f8      0xf888a000      0x9000  wanarp.sys      \SystemRoot\system32\DRIVERS\wanarp.sys Disabled                                                        0x822095b8      0xf889a000      0x10000 Cdfs.SYS        \SystemRoot\System32\Drivers\Cdfs.SYS   Disabled                                                        0x82291110      0xf89aa000      0x8000  usbccgp.sys     \SystemRoot\system32\DRIVERS\usbccgp.sys        Disabled                                                0x82250cc8      0xf82d4000      0x3000  hidusb.sys      \SystemRoot\system32\DRIVERS\hidusb.sys Disabled                                                        0x81e86090      0xf88aa000      0x9000  HIDCLASS.SYS    \SystemRoot\system32\DRIVERS\HIDCLASS.SYS       Disabled                                                0x81e350c8      0xf89b2000      0x7000  HIDPARSE.SYS    \SystemRoot\system32\DRIVERS\HIDPARSE.SYS       Disabled                                                0x82303488      0xf82d0000      0x3000  mouhid.sys      \SystemRoot\system32\DRIVERS\mouhid.sys Disabled                                                        0x8224e700      0xf7f77000      0x18000 dump_atapi.sys  \SystemRoot\System32\Drivers\dump_atapi.sys     Disabled                                                0x821488a8      0xf8bae000      0x2000  dump_WMILIB.SYS \SystemRoot\System32\Drivers\dump_WMILIB.SYS    Disabled                                                0x8224d280      0xbf800000      0x1c3000        win32k.sys      \SystemRoot\System32\win32k.sys Disabled                                                        0x820c21f8      0xf82c0000      0x3000  Dxapi.sys       \SystemRoot\System32\drivers\Dxapi.sys  Disabled                                                        0x82219e78      0xf89ba000      0x5000  watchdog.sys    \SystemRoot\System32\watchdog.sys       Disabled                                                        0x822f31d8      0xbf9c3000      0x12000 dxg.sys \SystemRoot\System32\drivers\dxg.sys    Disabled                                                                0x82066e80      0xf8d43000      0x1000  dxgthk.sys      \SystemRoot\System32\drivers\dxgthk.sys Disabled                                                        0x81e85008      0xbff50000      0x3000  framebuf.dll    \SystemRoot\System32\framebuf.dll       Disabled                                                        0x81e296b8      0xf7c6f000      0x4000  ndisuio.sys     \SystemRoot\system32\DRIVERS\ndisuio.sys        Disabled                                                0x8227aa38      0xf792a000      0x15000 wdmaud.sys      \SystemRoot\system32\drivers\wdmaud.sys Disabled                                                        0x822d64a8      0xf7bdf000      0xf000  sysaudio.sys    \SystemRoot\system32\drivers\sysaudio.sys       Disabled                                                0x822937c0      0xf7887000      0x2d000 mrxdav.sys      \SystemRoot\system32\DRIVERS\mrxdav.sys Disabled                                                        0x82198138      0xf8be0000      0x2000  ParVdm.SYS      \SystemRoot\System32\Drivers\ParVdm.SYS Disabled                                                        0x82259430      0xf780d000      0x52000 srv.sys \SystemRoot\system32\DRIVERS\srv.sys    Disabled                                                                0x821c5120      0xf75c4000      0x41000 HTTP.sys        \SystemRoot\System32\Drivers\HTTP.sys   Disabled                                                        thmanalyst@ubuntu:/opt/volatility3$ exit
```

00:09

The `driverscan` plugin will scan for drivers present on 
the system at the time of extraction. This plugin can help to identify 
driver files in the kernel that the `modules` plugin might have missed or were hidden.

As
 with the last plugin, it is again recommended to have a prior 
investigation before moving on to this plugin. It is also recommended to
 look through the `modules` plugin before `driverscan`.

Syntax: `python3 vol.py -f <file> windows.driverscan`

In most cases, `driverscan` will come up with no output; however, if you do not find anything with the `modules` plugin, it can be useful to attempt using this plugin.

There are also other plugins listed below that can be helpful when attempting to hunt for advanced malware in memory.

- `modscan`
- `driverirp`
- `callbacks`
- `idt`
- `apihooks`
- `moddump`
- `handles`

Note: Some of these are only present on Volatility2 or are part 
of third-party plugins. To get the most out of Volatility, you may need 
to move to some third-party or custom plugins.

### **VELOCIRAPTOR**

Per the official Velociraptor [documentation](https://docs.velociraptor.app/docs/overview/), "*Velociraptor is a unique, advanced open-source endpoint monitoring, digital forensic and cyber response platform. It was developed by Digital Forensic and Incident Response (DFIR)
 professionals who needed a powerful and efficient way to hunt for 
specific artifacts and monitor activities across fleets of endpoints. 
Velociraptor provides you with the ability to more effectively respond 
to a wide range of digital forensic and cyber incident response 
investigations and data breaches*".

This tool was created by Mike Cohen, a former Google employee who worked on tools such as [GRR](https://github.com/google/grr) (GRR Rapid Response) and [Rekall](https://github.com/google/rekall) (Rekall
 Memory Forensic Framework). Mike joined Rapid7's Detection and Response
 Team and continues to work on improving Velociraptor. At the date of 
this entry, the latest release for Velociraptor is [0.6.3](https://www.rapid7.com/blog/post/2022/02/03/velociraptor-version-0-6-3-dig-deeper-with-more-speed-and-scalability/).

**Interacting with client machines**

**Inspecting Clients**

If you didn't notice, some links are grayed out when you first log into Velociraptor. See below.

![https://assets.tryhackme.com/additional/velociraptor/dashboard-grayed-out-links.png](https://assets.tryhackme.com/additional/velociraptor/dashboard-grayed-out-links.png)

These
 links are specific to client endpoints and will become active once the 
analyst interacts with these endpoints within the Velociraptor UI.

Let's add a client to Velociraptor. Remember, since the attached VM is running Windows Subsystem for Linux (WSL), the Velociraptor server is running in Ubuntu, but the client will be Windows.

Run the commands for 'Add Windows as a client (CMD)' from the commands.txt on the desktop.

Add Windows as a client (CMD)

```
C:\Program Files\Velociraptor> velociraptor-v0.5.8-windows-amd64.exe --config velociraptor.config.yaml client -v
[INFO] 2022-03-31T05:47:36-07:00  _    __     __           _                  __
[INFO] 2022-03-31T05:47:36-07:00 | |  / /__  / /___  _____(_)________ _____  / /_____  _____
[INFO] 2022-03-31T05:47:36-07:00 | | / / _ \/ / __ \/ ___/ / ___/ __ `/ __ \/ __/ __ \/ ___/
[INFO] 2022-03-31T05:47:36-07:00 | |/ /  __/ / /_/ / /__/ / /  / /_/ / /_/ / /_/ /_/ / /
[INFO] 2022-03-31T05:47:36-07:00 |___/\___/_/\____/\___/_/_/   \__,_/ .___/\__/\____/_/
[INFO] 2022-03-31T05:47:36-07:00                                   /_/
[INFO] 2022-03-31T05:47:36-07:00 Digging deeper!                  https://www.velocidex.com
[INFO] 2022-03-31T05:47:36-07:00 This is Velociraptor 0.5.8 built on 2021-04-11T22:11:10Z (e468f54c)
[INFO] 2022-03-31T05:47:36-07:00 Loading config from file velociraptor.config.yaml
Generating new private key....
[INFO] 2022-03-31T05:47:36-07:00 Setting temp directory to C:\Program Files\Velociraptor\Tools
[...]
```

To see the client and interact with it, click on the `magnifying glass` with an empty search query (no text in the search bar) or click `Show All`.

![https://assets.tryhackme.com/additional/velociraptor/search-clients.png](https://assets.tryhackme.com/additional/velociraptor/search-clients.png)

The output will display a list of client machines running the Velociraptor agent in a table form.

![https://assets.tryhackme.com/additional/velociraptor/client-list.png](https://assets.tryhackme.com/additional/velociraptor/client-list.png)

Below is a brief explanation of each column.

| **Online State** | A
 green dot indicates the endpoint is online and communicating with the 
Velociraptor server. A yellow dot means the server hasn't received any 
communication from the endpoint within a 24-hour time frame. A red dot 
means it's been more than 24 hours since the server last heard from the 
endpoint. |
| --- | --- |
| **Client ID** | This is a unique ID
 assigned to the client by the Velociraptor server, and the server will 
use this client ID to identify the endpoint. A client ID always starts 
with the letter **C**. |
| **Hostname** | This 
is the hostname the client identifies itself to the Velociraptor server.
 Remember that hostnames can change, hence why Velociraptor uses the 
Client ID instead of identifying a client machine. |
| **Operating System Version** | The Velociraptor client can run on Windows, Linux, or MacOS. The details regarding the client operating system are displayed in this column. |
| **Labels** | Client machines may have multiple labels attached to them. This is useful to identify multiple clients as a group. |

Click on the agent to bring you to a semi-detailed view. By default, the view shown is the **overview** for the client. 
****

# **Overview**

In this view, the analyst (you) will see additional information about the client. The additional details are listed below:

- **Client ID**
- **Agent Version**
- **Agent Name**
- **Last Seen At**
- **Last Seen IP**
- **Operating System**
- **Hostname**
- **Release**
- **Architecture**
- **Client Metadata**

**VQL Drilldown**In this view, there is additional information about the client, such as Memory and CPU
 usage over 24 hours timespan, the Active Directory domain if the client
 is a domain-joined machine and the active local accounts for the 
client.

The data is represented in two colors in the Memory and CPU footprint over the past 24 hours.

- **Orange** - Memory usage
- **Blue** - CPU usage

# **Shell**

With the shell, commands can be executed remotely on the client machine. Commands can be run in  **PowerShell**, **CMD**, **Bash**, or **VQL**.
 Depending on the target operating system will determine which the 
analyst will pick. For example, CMD will not be a viable option if the 
client machine is running Linux.

It's straightforward, choose one of the options to run the command in and click `Launch`.

In the example below, the command `whoami` was executed with PowerShell. The command results are not immediately visible, and the **eyeball** icon needs to be toggled to see the command results.

![https://assets.tryhackme.com/additional/velociraptor/powershell-whoami.png](https://assets.tryhackme.com/additional/velociraptor/powershell-whoami.png)

# **Collected**

Here
 the analyst will see the results from the commands executed previously 
from Shell. Other actions, such as interacting with the **VFS** (**Virtual File System**), will appear here in Collected. VFS will be discussed later in upcoming tasks.

Across the top pane are brief details of the' collected' artifact. See below.

![https://assets.tryhackme.com/additional/velociraptor/collected1.png](https://assets.tryhackme.com/additional/velociraptor/collected1.png)

Clicking
 on any FlowId will populate the bottom pan with additional details 
regarding the information collected for that artifact or collection.

In the below screenshot, the output is from **Artifact Collection**.

![https://assets.tryhackme.com/additional/velociraptor/collected2b.png](https://assets.tryhackme.com/additional/velociraptor/collected2b.png)

This
 section is very busy, and I'll leave you to acquaint yourself with the 
information displayed here for each collected artifact.

The 
questions in this task will help nudge you to navigate throughout the 
output returned for each shell execution (e.i. whoami).

In the next task, we'll explore how to create a new collection and review the results in Collected.

# **Interrogate**

Per the [documentation](https://docs.velociraptor.app/docs/gui/clients/),
 "Interrogate operation. Interrogation normally occurs when the client 
first enrolls, but you can interrogate any client by clicking the 
Interrogate button".

To confirm this, click `Interrogate`. Now navigate back to Collected. You will notice that the **Artifact Collection** is **Generic. Client.Info**, which is an additional collection on the list. The first artifact collection in the list is indeed **Generic.Client.Info**. This is the same information displayed under **VQL Drilldown**.

Refer to the official Velociraptor documentation titled [Inspecting Clients](https://docs.velociraptor.app/docs/gui/clients/) for additional information.

**﻿
Creating a new collection**

In this task let's create a new collection.

![https://assets.tryhackme.com/additional/velociraptor/new-collection.png](https://assets.tryhackme.com/additional/velociraptor/new-collection.png)

We will take advantage of the WSL set-up in the attached VM and choose an artifact specific to Ubuntu.

There will be 5 stages in this process.

- **Select Artifacts**
- **Configure Parameters**
- **Specify Resources**
- **Review**
- **Launch**

# **Select Artifacts**

In the search bar, type `Windows.KapeFiles.Targets`. If you're not familiar with **KAPE**, please visit the KAPE [room](https://tryhackme.com/room/kape).

In short, **KapeFiles** are community-created targets and modules for use with KAPE. But as you can see, other tools use these Kapefiles as well.

When
 you select the artifact, a brief description of the collector will be 
displayed on the right, along with a rundown of the parameters.

![https://assets.tryhackme.com/additional/velociraptor/select-artifacts2.png](https://assets.tryhackme.com/additional/velociraptor/select-artifacts2.png)

# Configure Parameters

![https://assets.tryhackme.com/additional/velociraptor/configure-parameters.png](https://assets.tryhackme.com/additional/velociraptor/configure-parameters.png)

Scroll down and check **Ubuntu**.

![https://assets.tryhackme.com/additional/velociraptor/check-ubuntu.png](https://assets.tryhackme.com/additional/velociraptor/check-ubuntu.png)

Next, click on **Specify Resources**.

# **Specify Resources**

You can leave this untouched. See the below screenshot.

![https://assets.tryhackme.com/additional/velociraptor/specify-resources.png](https://assets.tryhackme.com/additional/velociraptor/specify-resources.png)

Next, click on **Review**.

# **Review**

The output will display in JSON format and it's pretty straightforward. Only one setting was enabled to collect, which was Ubuntu.

![https://assets.tryhackme.com/additional/velociraptor/review-request.png](https://assets.tryhackme.com/additional/velociraptor/review-request.png)

# **Launch**

Everything should be in order. Now it's time to launch the collection to gather the artifacts.

When you click **Launch**, you will be redirected to the Collected view. Notice that there should be a new entry with the newly created collection.

In
 particular, notice the State. It should show an hourglass which 
indicates the artifacts are actively being gathered for that 
collection.

![https://assets.tryhackme.com/additional/velociraptor/collection-running.png](https://assets.tryhackme.com/additional/velociraptor/collection-running.png)

Once the artifacts have been gathered, the state will change from an hourglass to a checkmark like the others.

![https://assets.tryhackme.com/additional/velociraptor/collection-done-2.png](https://assets.tryhackme.com/additional/velociraptor/collection-done-2.png)

As
 the list of collections grows, you can search for specific collections 
using the textfield at the top of the column. See the above screenshot.

Sweet! Now that we got that covered, let's look at VFS.

Refer to the Velociraptor documentation to learn more about [Artifacts](https://docs.velociraptor.app/docs/gui/artifacts/).

# **The Virtual File System**

Per the [documentation](https://docs.velociraptor.app/docs/gui/vfs/), "*The VFS is simply a server side cache of the files on the endpoint. It is merely a familiar GUI to allow inspection of the client’s filesystem*".

This can prove useful in an incident response scenario where you, the analyst, need to inspect artifacts in a client.

Refer
 to the official documentation for a complete overview of the VFS. In 
this task, we're going to focus on getting hands-on with VFS.

Below is what you should see when you first access the VFS for a client.

![https://assets.tryhackme.com/additional/velociraptor/default-vfs.png](https://assets.tryhackme.com/additional/velociraptor/default-vfs.png)

In the left pane, along with the middle pane, there are 4 folders (or accessors, filesystem access drivers):

- **file - uses operating system APIs to access files**
- **ntfs - uses raw NTFS parsing to access low level files**
- **registry - uses operating system APIs to access the Windows registry**
- **artifacts - previously run collections.**

Three buttons are highlighted in the above image. Below is a brief explanation for each.

![https://assets.tryhackme.com/additional/velociraptor/vfs-buttons-2.png](https://assets.tryhackme.com/additional/velociraptor/vfs-buttons-2.png)

1. Refresh the current directory (sync its listing from the client)
2. Recursively refresh this directory (sync its listing from the client)
3. Recursively download this directory from the client

Let's continue interacting with VFS.

When
 any folder is clicked  in the left pane, additional details are 
displayed in the middle pane. For example, if the file folder is 
clicked, a subfolder will appear, which is **C:**. Now the details in the middle pane change to reflect C:.

# **Velociraptor Query Language**

Per the official [documentation](https://docs.velociraptor.app/docs/overview/#vql---the-velociraptor-difference), "*Velociraptor’s
 power and flexibility comes from the Velociraptor Query Language (VQL).
 VQL is a framework for creating highly customized artifacts, which 
allow you to collect, query, and monitor almost any aspect of an 
endpoint, groups of endpoints, or an entire network. It can also be used
 to create continuous monitoring rules on the endpoint, as well as 
automate tasks on the server*".

With many tools that you will encounter in your SOC career, some tools may have their own query language. For example, in Splunk its SPL ([Search Processing Language](https://docs.splunk.com/Splexicon:SPL#:~:text=abbreviation,functions%2C%20arguments%2C%20and%20clauses.)), Elastic has KQL ([Kibana Query Language](https://www.elastic.co/guide/en/kibana/current/kuery-query.html)), Microsoft Sentinel has KQL [too] ([Kusto Query Language](https://docs.microsoft.com/en-us/azure/sentinel/kusto-overview)), etc.

VQL
 is the meat and potatoes of Velociraptor. Throughout each task thus 
far, unbeknownst to you, you have been interacting with VQL.

To jog your memory, navigate back to **Collected** and inspect **Generic.Client.Info**. Click the Requests tab in the bottom pane. See below image.

![https://assets.tryhackme.com/additional/velociraptor/vql-example.png](https://assets.tryhackme.com/additional/velociraptor/vql-example.png)

If you are familiar with SQL (Structured Query Language) then you should notice the similarities, for example: **SELECT**, **FROM**, and **WHERE**.

To execute a simple VQL on your own, first create a [**Notebook**](https://docs.velociraptor.app/docs/vql/notebooks).

Navigate to the Notebooks tab. In Velociraptor, Notebooks are *containers* that we can use to execute our queries and commands, as demonstrated below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/a107fe7d78711c90b9c31f5584e4c281.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/a107fe7d78711c90b9c31f5584e4c281.gif)

Notebooks **consist of two languages - [**Markdown**](https://www.markdownguide.org/getting-started/) and (of course) **VQL**. If you are familiar with [Jupyter Notebooks](https://jupyter.org/) they function in a very similar fashion!

Let's create our first notebook and enter some simple markdown. We'll circle back to VQL shortly.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/d2879fb5600bbe69f4b2d3e67e8de2ef.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/d2879fb5600bbe69f4b2d3e67e8de2ef.gif)

Sweet! Now let's set our notebook to use VQL instead & query basic information from the current agent, we can use `SELECT * FROM info()`

**Note**: Click into the lower box to display the options for this, then select the pencil to edit.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/f01b684ac748c4484a4949adfae0ba89.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/f01b684ac748c4484a4949adfae0ba89.png)

Let's save this notebook and run it against the agent as demonstrated below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/f12b007342f3041b129d70edd408c2bf.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/f12b007342f3041b129d70edd408c2bf.gif)

VQL can also be run via the command line. See the example below.

For this example, VQL is run from the command line querying an agent for details such as its hostname.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/646326ad4c3925702619529657e3ee36.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/646326ad4c3925702619529657e3ee36.gif)

# Artifacts

Before wrapping up this task, let's touch on **Artifacts** (or VQL Modules).

Per the [documentation](https://docs.velociraptor.app/docs/vql/artifacts/), "*Velociraptor allows packaging VQL queries inside mini-programs called Artifacts. An artifact is simply a structured YAML
 file containing a query, with a name attached to it. This allows 
Velociraptor users to search for the query by name or description and 
simply run the query on the endpoint without necessarily needing to 
understand or type the query into the UI*".

This was a **BRIEF** intro to VQL. It is recommended to review the official [documentation](https://docs.velociraptor.app/docs/vql/) thoroughly to fully understand it and how you can wield its power to execute advanced queries. Also, reference the [VQL Reference](https://docs.velociraptor.app/vql_reference/) and [Extending VQL](https://docs.velociraptor.app/docs/extending_vql/) for further information on VQL.

**Forensic Analysis VQL Plugins**

# **Forensic Analysis**

Per the [documentation](https://docs.velociraptor.app/docs/forensic/), "*VQL is not useful without a good set of plugins that make DFIR
 work possible. Velociraptor’s strength lies in the wide array of VQL 
plugins and functions that are geared towards making DFIR investigations
 and detections effective*".

There is a lot of 
information to cover here regarding VQL plugins. This task aims to give 
you enough information regarding these plugins so you can construct your
 VQL query to hunt for artifacts of a popular exploit known as 
Printnightmare.

At the date of the entry of this content, below are the categories surrounding forensic analysis:

- **Searching Filenames**
- **Searching Content**
- **NTFS Analysis**
- **Binary Parsing**
- **Evidence of Execution**
- **Event Logs**
- **Volatile Machine State**

Have a skim through **Searching Filenames** and **NTFS Analysis** to provide a solid brain dump to prep you for the questions below and for the next task.

### **THE HIVE PROJECT**

Introduction

TheHive Project is a 
scalable, open-source and freely available Security Incident Response 
Platform, designed to assist security analysts and practitioners working
 in SOCs, CSIRTs and CERTs to track, investigate and act upon identified
 security incidents in a swift and collaborative manner.

Security 
Analysts can collaborate on investigations simultaneously, ensuring 
real-time information pertaining to new or existing cases, tasks, 
observables and IOCs are available to all team members.

More information about the project can be found on [https://thehive-project.org/](https://thehive-project.org/) & their [GitHub Repo](https://github.com/TheHive-Project/TheHive).

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/b249487ffe52d672accdfceb365462fa.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/b249487ffe52d672accdfceb365462fa.png)

Image: Cases dashboard on TheHive by order of reported severity

TheHive Project operates under the guide of three core functions:

- **Collaborate:** Multiple analysts from one organisation can work together on the same case
simultaneously. Through its live stream capabilities, everyone can keep
an eye on the cases in real time.
- **Elaborate:**
Investigations correspond to cases. The details of each case can be
broken down into associated tasks, which can be created from scratch or
through a template engine. Additionally, analysts can record their
progress, attach artifacts of evidence and assign tasks effortlessly.
- **Act:** A quick triaging process can be supported by allowing analysts to add
observables to their cases, leveraging tags, flagging IOCs and
identifying previously seen observables to feed their threat
intelligence.

**TheHive Features & Integrations**

TheHive allows analysts
 from one organisation to work together on the same case simultaneously.
 This is due to the platform's rich feature set and integrations that 
support analyst workflows. The features include:

- **Case/Task Management:** Every investigation is meant to correspond to a case that has been created.
Each case can be broken down into one or more tasks for added
granularity and even be turned into templates for easier management.
Additionally, analysts can record their progress, attach pieces of
evidence or noteworthy files, add tags and other archives to cases.
- **Alert Triage:** Cases can be imported from SIEM alerts, email reports and other security
event sources. This feature allows an analyst to go through the imported alerts and decide whether or not they are to be escalated into
investigations or incident response.
- **Observable Enrichment with Cortex:** One of the main feature integrations TheHive supports is Cortex, an
observable analysis and active response engine. Cortex allows analysts
to collect more information from threat indicators by performing
correlation analysis and developing patterns from the cases. More
information on [Cortex](https://github.com/TheHive-Project/Cortex/).
- **Active Response:** TheHive allows analysts to use Responders and run active actions to
communicate, share information about incidents and prevent or contain a
threat.
- **Custom Dashboards:** Statistics on cases,
tasks, observables, metrics and more can be compiled and distributed on
dashboards that can be used to generate useful KPIs within an
organisation.
- **Built-in MISP Integration:** Another useful integration is with [MISP](https://www.misp-project.org/index.html), a threat intelligence platform for sharing, storing and correlating
Indicators of Compromise of targeted attacks and other threats. This
integration allows analysts to create cases from MISP events, import
IOCs or export their own identified indicators to their MISP
communities.

Other notable integrations that TheHive supports are [DigitalShadows2TH](https://github.com/TheHive-Project/DigitalShadows2TH) & [ZeroFox2TH](https://github.com/TheHive-Project/Zerofox2TH), free and open-source extensions of alert feeders from [DigitalShadows](https://www.digitalshadows.com/) and [ZeroFox](https://www.zerofox.com/) respectively.
 These integrations ensure that alerts can be added into TheHive and 
transformed into new cases using pre-defined incident response templates
 or by adding to existing cases

**User Profiles & Permissions**

TheHive
 offers an administrator the ability to create an organisation group to 
identify the analysts and assign different roles based on a list of 
pre-configured user profiles.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/853ee5298bfa5e60bf2fcf8d832268ff.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/853ee5298bfa5e60bf2fcf8d832268ff.png)

Admin Console -  Create Organisation

The pre-configured user profiles are:

- **admin:** full administrative permissions on the platform; can't manage any Cases or other data related to investigations;
- **org-admin:** manage users and all organisation-level
configuration, can create and edit Cases, Tasks, Observables and run
Analysers and Responders;
- **analyst:** can create and edit Cases, Tasks, Observables and run Analysers & Responders;
- **read-only:** Can only read, Cases, Tasks and Observables details;

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/b38aa62d7e9b6ddb08a200987a2bb3df.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/b38aa62d7e9b6ddb08a200987a2bb3df.png)

Admin Console -  Add User

Each
 user profile has a pre-defined list of permissions that would allow the
 user to perform different tasks based on their role. When a profile has
 been selected, its permissions will be listed.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/a0413ab7ab43bdb220919d7a48e4ddfe.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/a0413ab7ab43bdb220919d7a48e4ddfe.png)

The full list of permissions includes:

| **Permission** | **Functions** |
| --- | --- |
| **manageOrganisation (1)** | Create & Update an organisation |
| **manageConfig (1)** | Update Configuration |
| **manageProfile (1)** | Create, update & delete Profiles |
| **manageTag (1)** | Create, update & Delete Tags |
| **manageCustomField (1)** | Create, update & delete Custom Fields |
| **manageCase** | Create, update & delete Cases |
| **manageObservable** | Create, update & delete Observables |
| **manageALert** | Create, update & import Alerts |
| **manageUser** | Create, update & delete Users |
| **manageCaseTemplate** | Create, update & delete Case templates |
| **manageTask** | Create, update & delete Tasks |
| **manageShare** | Share case, task & observable with other organisations |
| **manageAnalyse (2)** | Execute Analyse |
| **manageAction (2)** | Execute Actions |
| **manageAnalyserTemplate (2)** | Create, update & delete Analyser Templates |

*Note
 that (1) Organisations, configuration, profiles and tags are global 
objects. The related permissions are effective only on the “admin” 
organisation. (2) Actions, analysis and template are available only if 
the Cortex connector is enabled.*

In addition to adding new user profiles, the admin can also 
perform other operations such as creating case custom fields, custom 
observable types, custom analyser templates and importing TTPs from the 
MITRE ATT&CK framework, as displayed in the image below.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/23c56b240bbeabf412e2bb69651e9a52.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/23c56b240bbeabf412e2bb69651e9a52.png)

Imported list of ATT&CK Patterns

**Analyst Interface Navigation**

**SCENARIO**

You
 have captured network traffic on your network after suspicion of data 
exfiltration being done on the network. This traffic corresponds to FTP 
connections that were established. Your task is to analyse the traffic 
and create a case on TheHive to facilitate the progress of an 
investigation. If you are unfamiliar with using Wireshark, please check 
out [this room](https://tryhackme.com/room/wireshark) first and come back to complete this task.

*Source of PCAP file: IntroSecCon CTF 2020*

Once
 an analyst has logged in to the dashboard, they will be greeted with 
the screen below. At the top, various menu options are listed that allow
 the user to create new cases and see their tasks and alerts. A list of 
active cases will be populated on the centre console when analysts 
create them.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/9b044f28a831732ff79c94109e84baf0.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/9b044f28a831732ff79c94109e84baf0.png)

Image: TheHive Main Landing Page

On clicking the `New Case`
 tab, a pop-up window opens, providing the analyst with fields to input 
their case details and tasks. The following options must be indicated on
 the case to set different categories and filter options:

- ***Severity*:** This showcases the level of impact the incident being investigated has on the environment from low to critical levels.
- ***TLP*:** The Traffic Light Protocol is a set of designations to ensure that
sensitive information is shared with the appropriate audience. The range of colours represents a scale between full disclosure of information (*White*) and No disclosure/ Restricted (*Red*). You can find more information about the definitions on the [CISA](https://www.cisa.gov/tlp) website.
- ***PAP*:** The Permissible Actions Protocol is used to indicate what an analyst
can do with the information, whether an attacker can detect the current
analysis state or defensive actions in place. It uses a colour scheme
similar to TLP and is part of the [MISP taxonomies](https://www.misp-project.org/taxonomies.html#_pap).

With
 this in mind, we open a new case and fill in the details of our 
investigation, as seen below. Additionally, we add a few tasks to the 
case that would guide the investigation of the event.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/15ff110d1a816ca7ff517ee63288783b.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/15ff110d1a816ca7ff517ee63288783b.gif)

New Case Window

In the visual below, we add the corresponding tactic and technique associated with the case. The TTPs are imported from [MITRE ATT&CK](https://attack.mitre.org/tactics/enterprise/). This provides additional
 information that can be helpful to map out the threat. As this is an 
exfiltration investigation, that is the specific tactic chosen and 
followed by the specific T1048.003 technique for Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/f390eb83345ba7e4d5582ae8038ef2c1.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/f390eb83345ba7e4d5582ae8038ef2c1.gif)

TTPs Selection Window

Case observables will be added from the Observables tab and you would have to indicate the following details:

| **Field** | **Description** | **Examples** |
| --- | --- | --- |
| *Type *:* | The observable dataType | IP address, Hash, Domain |
| *Value *:* | Your observable value | 8.8.8.8, 127.0.0.1 |
| *One observable per line:* | Create one observable per line inserted in the value field. |  |
| *One single multiline observable:* | Create one observable, no matter the number of lines | Long URLs |
| *TLP *:* | Define here the way the information should be shared. |  |
| *Is IOC:* | Check if this observable is considered an Indicator of Compromise | Emotet IP |
| *Has been sighted:* | Has this observable been sighted on your information system? |  |
| *Ignore for similarity:* | Do not correlate this observable with other similar observables. |  |
| *Tags **:* | Insightful information Tags. | Malware IP; MITRE Tactics |
| *Description **:* | Description of the observable |  |

In
 our scenario, we are adding the IP address 192... as our observable as 
this IP is the source of the FTP requests. Depending on the situation of
 your analysis, this observable can be marked as an IOC or if it has 
been sighted before in a different investigation.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/d3e3e6f85aa9169aa78104beebc79b8e.gif](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/d3e3e6f85aa9169aa78104beebc79b8e.gif)

New Observables Window

### **MALWARE ANALYSIS**

## Malware

The word malware is derived from the term MALicious softWARE. 
Therefore, any software that has a malicious purpose can be considered 
malware. Malware is further classified into different categories based 
on its behavior. However, we will not go into the details of those in 
this room. Here we will ponder the steps we will take if we suspect that
 we found malware in a machine. So, let's get started.

## The purpose behind Malware Analysis

Malware Analysis is an important skill to have. As a quick overview, 
Malware Analysis is performed by the following people in the Security 
Industry:

- **Security Operations** teams analyze malware to write detections for malicious activity in their networks.
- **Incident Response** teams analyze malware to determine what damage has been done to an environment to remediate and revert that damage.
- **Threat Hunt** teams analyze malware to identify IOCs, which they use to hunt for malware in a network.
- **Malware Researchers** in security product vendor teams analyze malware to add detections for them in their security products.
- **Threat Research** teams in OS Vendors like Microsoft and Google analyze malware to
discover the vulnerabilities exploited and add more security features to the OS/applications.

Overall, it seems like many different people do malware Analysis for many compelling reasons. So let's see how to start!

## Before we begin!

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/07dbfda63ff296b6732c4533145d4eb8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/07dbfda63ff296b6732c4533145d4eb8.png)

Please note that malware is like a weapon because it can produce 
great harm if not handled with care. For this reason, always take the 
following precautions while analyzing malware:

- Never analyze malware or suspected malware on a machine that does not have the sole purpose of analyzing malware.
- When not analyzing or moving malware samples around to different locations,
always keep them in password-protected zip/rar or other archives so that we can avoid accidental detonation.
- Only extract the malware from this password-protected archive inside the isolated environment, and only when analyzing it.
- Create an isolated VM specifically for malware analysis, which has the
capability of being reverted to a clean slate once you are done.
- Ensure that all internet connections are closed or at least monitored.
- Once you are done with malware analysis, revert the VM to its clean slate
for the next malware analysis session to avoid residue from a previous
malware execution corrupting the next one.

**Techniques of malware analysis**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/34dab1a51b037a8d4306b7485e575c2b.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/34dab1a51b037a8d4306b7485e575c2b.png)

Malware
 Analysis is like solving a puzzle. Different tools and techniques are 
used to find the pieces of this puzzle, and joining those pieces gives 
us the complete picture of what the malware is trying o do. Most of the 
time, you will have an executable file (also called a binary or a PE 
file. PE stands for Portable Executable), a malicious document file, or a
 Network Packet Capture (Pcap). The Portable Executable is the most 
prevalent type of file analyzed while performing Malware Analysis.

To find the different puzzle pieces, you will often use various tools, 
tricks, and shortcuts. These techniques can be grouped into the 
following two categories:

- Static Analysis
- Dynamic Analysis

## Static Analysis

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/be58bfb0a97f8987f8dc36f5d40a8ba7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/be58bfb0a97f8987f8dc36f5d40a8ba7.png)

When malware is analyzed without being executed, it is called Static 
Analysis. In this case, the different properties of the PE file are 
analyzed without running it. Similarly, in the case of a malicious 
document, exploring the document's properties without analyzing it will 
be considered Static Analysis. Examples of static analysis include 
checking for strings in malware, checking the PE header for information 
related to different sections, or looking at the code using a 
disassemble. We will look at some of these techniques later in the room.

Malware often uses techniques to avoid static analysis. Some of these
 techniques use obfuscation, packing, or other means of hiding its 
properties. To circumvent these techniques, we often use dynamic 
analysis.

## Dynamic Analysis

Malware faces a dilemma. It has to execute to fulfill its purpose, 
and no matter how much obfuscation is added to the code, it becomes an 
easy target for detection once it runs.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83824aaebb362a7b528f7587af2f5295.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83824aaebb362a7b528f7587af2f5295.png)

Static
 analysis might provide us with crucial information regarding malware, 
but sometimes that is not enough. We might need to run the malware in a 
controlled environment to observe what it does in these cases. Malware 
can often hide its properties to thwart Static Analysis. However, in 
most of those cases, Dynamic Analysis can prove fruitful. Dynamic 
analysis techniques include running the malware in a VM, either in a 
manual fashion with tools installed to monitor the malware's activity or
 in the form of sandboxes that perform this task automatically. We will 
learn about some of these techniques later in this room. Once we run the
 malware in a controlled environment, we can use our knowledge from the 
Windows Forensics rooms to identify what it did in our environment. The 
advantage here is that since we control the environment, we can 
configure it to avoid noise, like activity from a legitimate user or 
Windows Services. Thus, everything we observe in such an environment 
points to malware activity, making it easier to identify what the 
malware did in this scenario.

Malware, however, often uses techniques to prevent an analyst from 
performing dynamic analysis. Since most dynamic analysis is performed in
 a controlled environment, most methods to bypass dynamic analysis 
include detecting the environment in which it is being run. Therefore, 
in these cases, the malware uses a different, benign code path if it 
identifies that it is being run in a controlled environment.

## Advanced Malware Analysis

Advanced malware analysis techniques are used to analyze malware that
 evades basic static and dynamic analysis. For performing advanced 
malware analysis, disassemblers and debuggers are used. Disassemblers 
convert the malware's code from binary to assembly so that an analyst 
can look at the instructions of the malware statically. Debuggers attach
 to a program and allow the analyst to monitor the instructions in 
malware while it is running. A debugger allows the analyst to stop and 
run the malware at different points to identify interesting pieces of 
information while also providing an overview of the memory and CPU of 
the system. We will not cover advanced malware a

**Basic Static Analysis**

When analyzing a new 
piece of malware, the first step is usually performing basic static 
analysis. Basic static analysis can be considered sizing up the malware,
 trying to find its properties before diving deep into analysis. It 
provides us with an overview of what we are dealing with. Sometimes it 
might give us some critical information, for example, what API
 calls the malware is making or whether it's packed or not. However, 
other times, it might only give us information to help us size the 
malware up and give us an idea of the effort required to analyze it.

So without further ado, let's see some of the techniques we can use to perform basic static analysis.

## Caution!

Although static analysis is performed without running the malware, it
 is highly recommended that you perform malware analysis in an isolated 
Virtual Machine. You can create a clean snapshot of your Virtual Machine
 before performing any malware analysis and revert it to start from a 
clean state again after every analysis. Don't perform malware analysis 
on a live machine not purpose-built for malware analysis. For this room,
 we will be using the attached [Remnux VM](https://docs.remnux.org/). Remnux (**R**everse **E**ngineering **M**alware Li**nux**) is a Linux distribution purpose-built for malware analysis. It has many tools required for malware analysis already installed on it.

## Examining the file type

Though often the file type of malware is visible in the file 
extension and is obvious, sometimes malware authors try to trick users 
by using misleading file extensions. In such scenarios, it is helpful to
 know how to find the actual file type of a file without depending on 
file extensions. In Linux, we can find the file type of a file using the `file` command. To understand what the file command does, we can read its `man page` or use the `--help` option:

`man file` or `file --help`

We will find out that it is a simple command to use. We can use the following command to find the file type of a file:

`file <filename>`

Remnux

```markup
user@machine$ file wannacry
wannacry: PE32 executable (GUI) Intel 80386, for MS Windows
user@machine$
```

There is a folder named `Samples` on the Desktop in the attached VM. We will be using the samples present in that folder for our analysis. The above terminal shows the `file`
 command being run on the 'wannacry' sample. The output shows a PE32 
executable file with a Graphical User Interface, which was compiled for a
 system that runs Microsoft Windows with an Intel 80386-based processor.
 The Intel 80386 processor was one of the first 32-bit processors ever, 
and the instruction set designed for the 80386 is still used for 32-bit 
Intel processors, which is why you see "x86" processors and code. This 
means that the "80386" in the output above tells us that this 
application was designed for 32-bit Intel processors.

## Examining Strings

Another really important command that provides us with useful information about a file is the `strings` command. This command lists down the strings present in a file. To understand what the string command does, we can read its `man page` or use the `--help` option:

`man strings` or `strings --help`

We will find that it is also a simple command to use. We can use the following command to find the strings in a file:

`strings <filename>`

Looking at strings in a file can often give clues related to 
the behavior of malware. For example, if we see URLDownloadToFile in the
 output of the strings command, we will know that this malware is doing 
something with the URLDownloadToFile Windows API.
 Most likely, it is downloading a file from the internet and saving it 
on the disk. Similarly, strings might also provide contextual 
information that helps us later during malware analysis.

Remnux

```markup
user@machine$ strings wannacry
!This program cannot be run in DOS mode.
Rich
.text
`.rdata
@.data
.rsrc
49t$
TVWj
PVVh
tE9u
.
.
.
.
 inflate 1.1.3 Copyright 1995-1998 Mark Adler
 n;^
Qkkbal
i]Wb
9a&g
MGiI
wn>Jj
#.zf
+o*7
- unzip 0.15 Copyright 1998 Gilles Vollant
CloseHandle
GetExitCodeProcess
TerminateProcess
WaitForSingleObject
CreateProcessA
GlobalFree
GetProcAddress
LoadLibraryA
GlobalAlloc
SetCurrentDirectoryA
GetCurrentDirectoryA
GetComputerNameW
SetFileTime
SetFilePointer
MultiByteToWideChar
GetFileAttributesW
GetFileSizeEx
.
.
.
.
user@machine$
```

Here we can see the `strings` command being run against the 'wannacry' sample. We will see that the output starts with the `DOS Stub`, which is the text that says `!This program cannot be run in DOS mode`.
 Some values don't make much sense and look like garbage, but you will 
also see useful output. For example, we can see above that some strings 
look like Windows APIs. For example, `CloseHandle`, `GetExitCodeProcess`, `TerminateProcess`, and so on. Similarly, we can see text that says `inflate 1.1.3 Copyright 1995-1998 Mark Adler`. A quick search shows that it is a part of the [zlib data compression](http://zlib.net/) library, this tells us that the sample might be using this library.

**Tip:** Sometimes, the output of the strings command is too big 
to be shown on the terminal completely. We can redirect it, write it to a
 file, and read it using vim or any other tool. The below terminal shows
 the output being redirected to a file named str:

Remnux

```markup
user@machine$ strings wannacry>str
user@machine$
```

Alternatively, you can use the `more` or `less` command to parse the output in a more visible manner:

Remnux

```markup
user@machine$ strings wannacry |more
!This program cannot be run in DOS mode.
Rich
.text
`.rdata
@.data
.rsrc
49t$
TVWj
PVVh
tE9u
PVVW
SVWjcf
X_^[
X_^[
^t19
QPPh
tXVP
X_^]
^t)9
X_^[]
WWWWWPj
SjJ3
X[_^
Yu#j
uSh8
Yu8S
SSh
hn!@
SVWj@
--more--
```

We can use the space key to scroll down the list of strings here. If you are interested, [this room](https://tryhackme.com/room/malstrings) contains more information about strings.

## Calculating Hashes

File Hashing provides us with a fixed-size unique number that 
identifies a file. A File Hash can therefore be considered a unique 
identifier for a file, similar to Social Security Numbers or National 
Identification Numbers used for the citizens of a country. Hashing is an
 important concept in malware analysis. It can be used as an identifier 
for specific malware. As we will see later in this task, this identifier
 can then be shared with other analysts or searched online for 
information sharing purposes. Please note that a single bit of 
difference in two files will result in different hashes, so changing the
 hash of a file is as simple as changing one bit in it.

Commonly, `md5sum`, `sha1sum` and `sha256sum` hashes are used for file hashing. We can calculate file hashes by using a simple command in Linux, as shown below for the md5sum hash:

`md5sum <filename>`

Remnux

```
user@machine$ md5sum wannacry
84c82835a5d21bbcf75a61706d8ab549  wannacry
user@machine$
```

Above, we can see the md5sum hash is calculated for the file named 'wannacry.'

Similarly, `sha1sum` and `sha256sum` commands can be used for calculating `sha1sum` or `sha256sum` of a file (Hashes are often referred to without the `sum` at the end, e.g. `md5` instead of `md5sum` and so on.)

If you are interested in learning more about hashes, you can check out [this room](https://tryhackme.com/room/malresearching).

## AV scans and VirusTotal

Scanning a file using AVs or searching for a hash on [VirusTotal](https://www.virustotal.com/gui/home/upload)
 can also provide useful information about the classification of malware
 performed by security researchers. However, when using an online 
scanner, it is recommended to search for the malware's hash instead of 
uploading online to avoid leaking sensitive information online. Only 
upload a sample if you are sure of what you are doing.

Let's see 
what it says about the sample we calculated the hash for above. We can 
search for the md5sum we calculated for the wannacry sample on the 
VirusTotal homepage:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/4fa91c3c465940314f55bce4427a6a4a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/4fa91c3c465940314f55bce4427a6a4a.png)

VirusTotal has a mix of handy features. It provides scan results from 60+ AV vendors and each AV vendor's classification to the sample.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/60903062574c8a2c9083100f096465b6.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/60903062574c8a2c9083100f096465b6.png)

The details tab lists the history of the sample, the first submission, the last submission, and the metadata of the sample.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/88d7d3ed42be6f54b17a863fd8c9d308.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/88d7d3ed42be6f54b17a863fd8c9d308.png)

Sometimes
 it also provides information about the behavior of a sample and its 
relations as seen in different environments online.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83c4544bf2865f4561b74645b1856793.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/83c4544bf2865f4561b74645b1856793.png)

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/99f474d91d736cf063978fbeb82dfd9c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/99f474d91d736cf063978fbeb82dfd9c.png)

We
 can also find comments about the sample by the community on VirusTotal,
 which can sometimes provide additional context about the sample.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d35a057fa8b2394174a1e4c6d12a6992.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/d35a057fa8b2394174a1e4c6d12a6992.png)

Perhaps it is very clear from the above screenshots that we are looking at a sample of wannacry ransomware.

**The PE file Header**

## PE Header

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/180bb73415dd511f9399ce6cfff9db9a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/180bb73415dd511f9399ce6cfff9db9a.png)

The PE
 File Header contains the metadata about a Portable Executable file. 
This data can help us find a lot of helpful information to help us in 
our analysis. We will go into detail about the PE header and the 
information it contains in the upcoming Malware Analysis module for the 
advanced path. However, some of the vital information found in the PE 
header is explained below:

### Imports/Exports

A PE
 file seldom contains all the code that it needs to run on a system on 
its own. Most of the time, it re-uses code provided by the Operating 
System. This is done to use less space and leverage the framework the 
Operating System has laid to perform tasks instead of re-inventing the 
wheel. Imports are such functions that the PE file imports from outside 
to perform different tasks.

For example, if a developer wants to Query a Windows Registry value, they will import the [RegQueryValue](https://docs.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regqueryvaluew)
 function provided by Microsoft instead of writing the code themselves. 
It is understood that this function will be present on any Windows 
machine on which the developer's code is going to run, so it does not 
need to be included in the PE
 file itself. Similarly, any PE file export functions are exposed to 
other binaries that can use that function instead of implementing it 
themselves. Exports are generally associated with Dynamically-Linked 
libraries (DLL files), and it is not typical for a non-DLL PE file to 
have a lot of exports.

Since most PE
 files use the Windows API to perform the bulk of their jobs, a PE 
file's imports provide us with crucial information on what that PE file 
will do. It becomes evident that a PE file that is importing the 
InternetOpen function will communicate with the internet, a 
URLDownloadToFile function shows that a PE file will download something 
from the internet, and so on. Names of Windows APIs are generally 
intuitive and self-explanatory. However, we can always consult [Microsoft Documentation](https://docs.microsoft.com/en-us/windows/win32/api/_winprog/) to verify the purpose of a particular Windows function.

### Sections:

Another useful piece of information available in the PE
 file header is the information about sections in the PE file. A PE file
 is divided into different sections which have different purposes. 
Although the sections in a PE file depend on the compiler or packer used
 to compile or pack the binary, the following are the most commonly seen
 sections in a PE file.

- .**text:** This Section generally contains the CPU instructions executed when the PE file is run. This section is marked as executable.
- **.data:** This Section contains the global variables and other global data used by the PE file.
- **.rsrc:** This Section contains resources that are used by the PE file, for example, images, icons, etc.

## Analyzing PE header using pecheck utility

We can use the pecheck utility present in the Remnux VM attached with the room to check the PE header.

Remnux

```
user@machine$ pecheck wannacryPE check for 'wannacry':
Entropy: 7.995471 (Min=0.0, Max=8.0)
MD5     hash: 84c82835a5d21bbcf75a61706d8ab549
SHA-1   hash: 5ff465afaabcbf0150d1a3ab2c2e74f3a4426467
SHA-256 hash: ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa
SHA-512 hash: 90723a50c20ba3643d625595fd6be8dcf88d70ff7f4b4719a88f055d5b3149a4231018ea30d375171507a147e59f73478c0c27948590794554d031e7d54b7244
.text entropy: 6.404235 (Min=0.0, Max=8.0)
.rdata entropy: 6.663571 (Min=0.0, Max=8.0)
.data entropy: 4.455750 (Min=0.0, Max=8.0)
.rsrc entropy: 7.999868 (Min=0.0, Max=8.0)
Dump Info:
----------DOS_HEADER----------

[IMAGE_DOS_HEADER]
0x0        0x0   e_magic:                       0x5A4D
0x2        0x2   e_cblp:                        0x90
0x4        0x4   e_cp:                          0x3
.
.
.
.
.
[IMAGE_IMPORT_DESCRIPTOR]
0xD5D0     0x0   OriginalFirstThunk:            0xD60C
0xD5D0     0x0   Characteristics:               0xD60C
0xD5D4     0x4   TimeDateStamp:                 0x0        [Thu Jan  1 00:00:00 1970 UTC]
0xD5D8     0x8   ForwarderChain:                0x0
0xD5DC     0xC   Name:                          0xDC84
0xD5E0     0x10  FirstThunk:                    0x8000

ADVAPI32.dll.CreateServiceA Hint[100]
ADVAPI32.dll.OpenServiceA Hint[431]
ADVAPI32.dll.StartServiceA Hint[585]
ADVAPI32.dll.CloseServiceHandle Hint[62]
ADVAPI32.dll.CryptReleaseContext Hint[160]
ADVAPI32.dll.RegCreateKeyW Hint[467]
ADVAPI32.dll.RegSetValueExA Hint[516]
ADVAPI32.dll.RegQueryValueExA Hint[503]
ADVAPI32.dll.RegCloseKey Hint[459]
ADVAPI32.dll.OpenSCManagerA Hint[429]
.
.
.
.
.
.
```

Here we can see information pecheck has extracted from the PE
 header of the wannacry sample. We see that the sample has 4 sections, 
.text, .rdata, .data and .rsrc and their respective entropy. Similarly, 
it has also shown us the different hashes of the sample. Pecheck also 
shows us the functions that a PE file imports. In the above terminal 
window, we can see the IMAGE_IMPORT_DESCRIPTOR, which shows the 
functions it imports from the ADVAPI32.dll Linked library. We will see 
similar descriptors for all the other linked libraries whose functions 
are imported by the sample.

We can see that pecheck shows 
us a lot more information than what we discussed in this task; however, 
discussing all that information is out of the scope of this room. We 
will dive into further details in the upcoming malware analysis module. 
We will take what we are looking for from the information we see, 
namely, the section information and the imports of our samples.

**Basic Dynamic Analysis**

While basic static 
analysis provides us with useful information about a sample, most times,
 we need to perform additional analysis to move further in our analysis 
procedure. One quick and dirty way to find more clues about a malware's 
behavior is by performing basic dynamic analysis. Many of the properties
 of a malware sample can be hidden when it's not running. However, when 
we perform dynamic analysis, we can lay these properties bare and learn 
more about the behavior of a malware sample.

## Caution!

Dynamic
 analysis requires running live malware samples that can be destructive.
 It is highly recommended that you perform malware analysis in an 
isolated Virtual Machine. You can create a clean snapshot of your 
Virtual Machine before performing any malware analysis and revert it to 
start from a clean state again after every analysis. Don't perform 
malware analysis on a live machine not purpose-built for malware 
analysis.

## Introduction to Sandboxes

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/7c03de48312f00f8a4fa904f9666668e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/7c03de48312f00f8a4fa904f9666668e.png)

Sandbox is a term borrowed from the military. A sandbox is a box of 
sand, as the name suggests, modeling the terrain where an operation has 
to take place, in which a military team dry runs their scenarios to 
identify possible outcomes. In malware analysis, a sandbox is an 
isolated environment mimicking the actual target environment of a 
malware, where an analyst runs a sample to learn more about it. Malware 
analysis sandboxes heavily rely on Virtual Machines, their ability to 
take snapshots and revert to a clean state when required.

## Construction of a sandbox

For malware analysis using sandboxes, the following considerations make the malware analysis effective:

- Virtual Machine mimicking the actual target environment of the malware sample
- Ability to take snapshots and revert to clean state
- OS monitoring software, for example, Procmon, ProcExplorer or Regshot, etc.
- Network monitoring software, for example, Wireshark, tcpdump, etc.
- Control over the network through a dummy DNS server and webserver.
- A mechanism to move analysis logs and malware samples in and out of the
Virtual Machine without compromising the host (Be careful with this one. If you have a shared directory with your malware analysis VM that remains accessible when running malware, you might risk malware affecting all files in your shared directory)

## Open Source Sandboxes

Though it is good to understand what a good sandbox is made of, 
building a sandbox from scratch is not always necessary. One can always 
set up Open Source Sandboxes. These sandboxes provide the framework for 
performing basic dynamic analysis and are also customizable to a 
significant extent to help those with a more adventurous mindset.

### Cuckoo's Sandbox

[Cuckoo's sandbox](https://cuckoosandbox.org/)
 is the most widely known sandbox in the malware analysis community. It 
was developed as part of a Google Summer of Code project in 2010. It is 
an open-source project that you will often see deployed in SOC
 environments and with enthusiasts' home labs. Advantages of Cuckoo's 
sandbox include huge community support, easy-to-understand 
documentation, and lots of customizations. You can deploy it on your 
network and let the community signatures guide you into identifying 
which files are malicious and which are benign because of the vast 
corpus of community signatures that come with it.

Cuckoo's 
sandbox has been archived, and an update is pending. It also doesn't 
support Python 3, making it obsolete right now. However, all is not lost
 because we have alternatives.

### CAPE Sandbox

[CAPE Sandbox](https://github.com/kevoreilly/CAPEv2)
 is a little more advanced version of Cuckoo's sandbox. It supports 
debugging and memory dumping to support the unpacking of packed malware 
(We will learn more about packing and unpacking in the advanced malware 
analysis module). Though beginners can use this sandbox, advanced 
knowledge is required for making full use of it. A community version of 
this sandbox is available online, which can be used to test run it 
before installing. CAPE Sandbox is so far actively developed and 
supports Python 3.

## Online Sandboxes:

Setting up and maintaining a sandbox can be
 a time-consuming task. Keeping that in view, online sandboxes can be of
 great help. Some of the most commonly used online sandboxes are as 
follows:

- [Online Cuckoo Sandbox](https://cuckoo.cert.ee/)
- [Online CAPE Sandbox](https://www.capesandbox.com/)
- [Any.run](https://any.run/)
- [Intezer](https://analyze.intezer.com/)
- [Hybrid Analysis](https://hybrid-analysis.com/)

Though
 online sandboxes provide a useful utility, it is best not to submit a 
sample online unless you are sure of what you are doing. A better 
approach is to search for the sample's hash on the service you are using
 to see if someone has already submitted it. Let's look at Hybrid 
Analysis to see what interesting analysis it provides for our sample.

### Analyzing samples using Hybrid Analysis

On its homepage, we are greeted with the following screen:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/947a74dd9d2ff42810c1a0c91079a1e8.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/947a74dd9d2ff42810c1a0c91079a1e8.png)

As
 we mentioned, we will not be submitting a sample. Instead, we will 
search for the hash of our sample. Therefore, we will search for the 
md5sum of the wannacry sample from the attached VM. We will see that it is already submitted multiple times, and we can choose from the submitted results.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9d8e2a97315e6b458f583d211b4819ba.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9d8e2a97315e6b458f583d211b4819ba.png)

Let's open the one submitted on Windows 7 64 bit from among these.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/cb173e0611090adc2327e7f5770d89c1.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/cb173e0611090adc2327e7f5770d89c1.png)

We
 will see the above interface when we click on the sample. We can see a 
navigation pane on the right that highlights different parts of the 
report. We can also see that the verdict is malicious, with a threat 
score of 100/100 and AV
 detection of 95%. Below that, we see the overview of the sample's 
behavior. Below that, we will see the mapping to MITRE ATT&CK 
techniques. We will see the following mapping when we click `view all details`:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9e1a1a01fcf353c9a75c33ab0358a877.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/9e1a1a01fcf353c9a75c33ab0358a877.png)

Below
 that, we will see some indicators and context information and some 
static analysis information for the sample. The dynamic analysis part 
comes below that:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c817a7e0dcaa383e9d9f84bd19f527c1.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/c817a7e0dcaa383e9d9f84bd19f527c1.png)

This
 part provides us with a lot of information about the behavior of the 
sample when it was run in a sandbox. We can click each process to find 
more detail about it. In the above screenshot, of particular interest 
can be the executions of cmd.exe. We can see that the sample is running 
script files and deleting backups and volume shadow copies, something 
often done by ransomware operators to stop the victim from restoring 
their files from these sources.

Below this section, we will see network analysis of the sample:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/77053f26e9374259ca622908bcb0fab0.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/77053f26e9374259ca622908bcb0fab0.png)

Extracted
 strings and extracted files are also available in the report. These can
 provide information about the batch scripts we saw in the processes 
above.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/afe475fcc71679a4c07297bdcf60cd48.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/afe475fcc71679a4c07297bdcf60cd48.png)

And
 there are comments from the community at the very end. As we might have
 seen, we can find many pieces of the puzzle that a malware sample is, 
using the discussed techniques. However, in some cases, these techniques
 can prove insufficient to make a decision. Let's move to the next task 
to determine what scenarios can make it challenging to analyze malware.

**Anti-analysis techniques**

While the security 
researchers are devising techniques and tools to analyze malware, the 
malware authors are working on rendering these tools and techniques 
ineffective. We found a great deal of information in the previous tasks 
about the malware we analyzed. However, there are ways malware authors 
can make our life difficult. Below are some of the techniques used by 
malware authors to do the same.

## Packing and Obfuscation:

Malware authors often use packing and obfuscation to make an 
analyst's life difficult. A packer obfuscates, compresses, or encrypts 
the contents of malware. These techniques make it difficult to analyze 
malware statically. Specifically, a packed malware will not show 
important information when running a string search against it. For 
example, let's run a string search against the file named `zmsuz3pinwl` in the Samples folder in the attached VM.

Remnux

```
user@machine$ strings zmsuz3pinwl!This program cannot be run inDOS mode.
RichH
.rsrc
.data
.adata
dApB
Qtq5
wn;3b:TC,n
*tVlr
D6j[
^sZ"4V
JIoL
j~AI
tYFu
7^V1
vYB09
"PeHy
M4AF#
3134
%}W\+3A;a5
dLq<
.
.
.
.
.
.

```

We will notice that this sample contains mainly garbage strings that 
don't provide much value to us. Let's run pecheck on the sample to see 
what else we get.

Remnux

```
user@machine$ pecheck zmsuz3pinwlPE check for 'zmsuz3pinwl':
Entropy: 7.978052 (Min=0.0, Max=8.0)
MD5     hash: 1ebb1e268a462d56a389e8e1d06b4945
SHA-1   hash: 1ecc0b9f380896373e81ed166c34a89bded873b5
SHA-256 hash: 98c6cf0b129438ec62a628e8431e790b114ba0d82b76e625885ceedef286d6f5
SHA-512 hash: 6921532b4b5ed9514660eb408dfa5d28998f52aa206013546f9eb66e26861565f852ec7f04c85ae9be89e7721c4f1a5c31d2fae49b0e7fdfd20451191146614a
 entropy: 7.999788 (Min=0.0, Max=8.0)
 entropy: 7.961048 (Min=0.0, Max=8.0)
 entropy: 7.554513 (Min=0.0, Max=8.0)
.rsrc entropy: 6.938747 (Min=0.0, Max=8.0)
 entropy: 0.000000 (Min=0.0, Max=8.0)
.data entropy: 7.866646 (Min=0.0, Max=8.0)
.adata entropy: 0.000000 (Min=0.0, Max=8.0)
Dump Info:
----------Parsing Warnings----------

Suspicious flags set for section 0. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 1. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 2. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 3. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 4. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 5. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Suspicious flags set for section 6. Both IMAGE_SCN_MEM_WRITE and IMAGE_SCN_MEM_EXECUTE are set. This might indicate a packed executable.

Imported symbols contain entries typical of packed executables.
.
.
.
.
.
.
.

```

As suspected, we see that the executable has characteristics typical 
of a packed executable, as per pecheck. We will notice that there is no 
.text section in the sample, and other sections have execute 
permissions, which shows that these sections contain executable 
instructions or will be populated with executable instructions during 
execution. We will also see that this sample does not have many imports 
that might show us its functionality, as we saw with the previous 
sample.

For analysis of packed executables, the first step is 
generally to unpack the sample. This is an advanced topic that will be 
covered in the upcoming rooms.

## Sandbox evasion:

As we have seen previously, we can always run a sample in a sandbox 
to analyze it. In many cases, that might help us analyze samples that 
evade our basic static analysis techniques. However, malware authors 
have some tricks up their sleeves that hamper that effort. Some of these
 techniques are as follows:

- **Long sleep calls:** Malware
authors know that sandboxes run for a limited time. Therefore, they
program the malware not to perform any activity for a long time after
execution. This is often accomplished through long sleep calls. The
purpose of this technique is to time out the sandbox.
- **User activity detection:** Some malware samples will wait for user activity before performing malicious activity. The premise of this technique is that there will be no user
in a sandbox. Therefore there will be no mouse movement or typing on the keyboard. Advanced malware also detects patterns in mouse movements
that are often used in automated sandboxes. This technique is designed
to bypass automated sandbox detection.
- **Footprinting user activity:** Some malware checks for user files or activity, like if there are any files
in the MS Office history or internet browsing history. If no or little
activity is found, the malware will consider the machine as a sandbox
and quit.
- **Detecting VMs:** Sandboxes run on virtual
machines. Virtual machines leave artifacts that can be identified by
malware. For example, some drivers installed in VMs being run on VMWare or Virtualbox give away the fact that the machine
is a VM. Malware authors often associate VMs with sandboxes and would
terminate the malware if a VM is detected.

The above 
list is not exhaustive but gives us an idea of what to expect when 
analyzing malware. In a future module dedicated to malware analysis, we 
will discuss these techniques and ways to detect malware that employs 
them.
