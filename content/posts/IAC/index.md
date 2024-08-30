---
title: "Infrastructure as code"
date: 2024-03-02
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Credit to TryHackMe" # Here you can write a small summary of the post if needed
tags: [Infrastructure as code]
categories: [Infras, TryHackMe]
---
# Introductoin

[TryHackMe](https://tryhackme.com/signup?referrer=6325877cfcc474005111479e) provides one of the best contents when it comes to cybersecurity, below is a snippet of the content one will acquire when subcribed to the premium learning path of TryHackMe Infrastructure as code.
They have summarised the content very well and clealry understood, for practical experience, subscribe to their platform to gain the skills.

# INFRASTRUCTURE AS CODE


## INTRO

**Infrastructure Before IaC**

Before defining IaC, it’s important to understand why we need it. In other words, what problems is it solving?

Let us consider what was required when infrastructure was configured and 
managed in the days before IaC. Here are some tasks which would have 
been the responsibility of various teams (depending on companies 
structure), such as DevOps/DevSecOps, Platform, Infrastructure, Network 
and Systems Administration:

- Manually provisioning servers (physically installing servers or manually deploying virtual machines)
- Network configuration (setting up a network for the infrastructure, including
setting up IP addresses, subnets, routing tables and any network
components tat the infra needs like routers, switches or firewalls)
- Installing an OS
- Installation, configuration and updating of software (database, web server etc.)
- Disaster recovery (DR) (this involves having a backup infrastructure on standby, making a detailed “failover” plan, and having clear procedures in place should the primary data centre go down).

# Infrastructure as Code Explained

Instead of provisioning and managing infrastructure manually, as discussed 
above, infrastructure as code allows the automation of these tasks 
through code. This code can be used to define a "desired state" for the 
infrastructure, acting as a blueprint for IaC tools to provision the 
infrastructure. For example, you may define some resources in your code,
such as network components, virtual machines, and a database. An IaC 
tool will build this blueprint and ensure the infrastructure is always 
in line with it. Should you want to make an infrastructure change, like 
increasing the number of VMs,
 only a simple change needs to be made to the code, which will be 
reflected in your infrastructure once applied. Compare this to what was 
previously required to add a VM, which would involve making a manual 
request through a portal and waiting for that request to be actioned by a
 systems administrator, and it becomes easy to see the utility of IaC.

# The Many Benefits of IaC

Having infrastructure deployed from code also means it can be a collaborative 
process and a shared responsibility. This means knowledge of 
infrastructure and its configuration isn't siloed to a single team 
member, avoiding knowledge dependencies whilst supporting continuous 
integration (CI). Continuous deployment (CD) is also supported through the ability to 
deploy consistent infrastructure across multiple environments. As well 
as reducing the manual efforts and risk of error, an IaC approach can 
make it possible to have a reliable infrastructure that 
is scalable, versionable, and repeatable.

**Scalable**

This technology begins to make even more sense when you consider the 
widespread adoption of cloud computing and its elastic nature, with 
virtual machines and resources being scaled up and down based on demand 
due to resources being billed per second/minute/hour. With IaC, you can 
do this scaling with a single command or even automate the process, 
whereas in the past, this would have involved weeks of work (e.g., 
logging tickets and manually provisioning and de-provisioning).

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b6e2ee40f4e71121225f291804036b58.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b6e2ee40f4e71121225f291804036b58.png)

**Versionable**

Infrastructure as code should be treated as any other code and versioned using a 
version control system. Versioning an infrastructure means it's 
self-documenting, allowing infrastructure changes to be tracked and 
recorded. This benefits the many teams that work with infrastructure 
with all sorts of tasks, from audits to troubleshooting infrastructure 
issues. Speaking of infrastructure issues, versioning also means that 
should your latest infrastructure start having problems, you can 
redeploy your infrastructure to the last known working version, an 
example of how IaC allows for reliable infrastructure. Versioning 
infrastructure can also improve testing capabilities; for example, an 
application can be tested using a historical infrastructure build.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/af0e4d32762b91bc2df2ade961373378.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/af0e4d32762b91bc2df2ade961373378.svg)

**Repeatable**

In the dev world, it is common to work between multiple environments. 
Developers first build their code in a dev environment before testing it in a staging environment (which mirrors production) and finally 
deploying the fully functional and tested code into the production 
environment. In the past, these three environments would require the 
manual provisioning and configuration of 3 respective infrastructures. 
With IaC, you can use the same code/configuration to set up identical 
infrastructures across multiple environments with the push of a button. 
While saving massive amounts of time, this also ensures 
consistency/reliability across environments, which is critical when 
testing software and was very hard to achieve in the days of manual 
provisioning.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/d82ac6ab32e5e5b1b3c5b49b61b35a5f.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/d82ac6ab32e5e5b1b3c5b49b61b35a5f.svg)

# IaC in Practice

IaC
 is a powerful technology that can streamline and improve 
business-critical processes if used correctly. To demonstrate this 
utility, let us take one of the example responsibilities mentioned at 
the beginning of the task, disaster recovery, and examine how IaC can 
aid this process. As touched on above, disaster recovery is the process 
of restoring infrastructure after a catastrophic/disruptive event; for 
example, if you are working for a company that has a physical 
on-premises infrastructure located in a data centre, a disaster can 
range from a simple power outage to extreme examples such as natural 
disasters like wildfires or hurricanes bringing this "primary" data 
centre down. Failing over from this primary data centre to a secondary 
backup data centre, when done manually, is a very time-consuming, 
high-pressure situation which can lead to many issues. Here are a few 
ways in which IaC can help with disaster recovery:

**Infrastructure Automation:** Since
 IaC allows the automation of the provisioning and configuration of an 
infrastructure, reprovisioning and re-configuring an infrastructure in a
 backup data centre is streamlined and less time-consuming.

**Data Backup and Recovery:** Data
 loss or corruption is one of the most significant risks associated with
 disaster recovery and can be very costly to the affected company. 
Infrastructure as code can be used to automate the backup and recovery 
of data. Backup procedures can be defined in code, which will be 
triggered in the event of a disaster to ensure data is restored.

**Failover Automation:** During
 a disaster, critical services can become unavailable as they will point
 to the broken infrastructure. IaC can be used to automate the failover 
process so critical services use the backup infrastructure, which 
reduces downtime.

**Configuration Consistency:** IaC
 keeps infrastructure consistent and well-documented; this consistency 
is vital during the disaster recovery process and helps avoid 
misconfigurations (often caused by simple human error or lack of 
documentation on the current configuration)  during the transition to a 
backup environment.

**Scaling Resources:** The
 recovery process can be resource intensive, and IaC can be used to 
scale resources to handle the increased workloads (and scale back down 
afterwards).

These
 are just some examples of how IaC can aid and streamline processes, 
with a wide range of teams benefitting from infrastructure as code's 
versionable, scalable, and repeatable nature - saving them time and 
headaches.

# Summary

In conclusion, infrastructure as code is a fundamental concept in DevSecOps,
 with the technology supporting key concepts like continuous integration
 (allowing for infrastructure development to be a collaborative process 
with versioning in place) and continuous deployment (allowing for the 
automation of infrastructure deployment across multiple environments 
consistently). IaC also improves efficiency by facilitating 
infrastructure changes in code, allowing for changes to be made quickly 
to adapt to developing infrastructure requirements and reduce manual 
tasks in the process.

IaC - The Tools Part 1

**Get to Know Your Toolkit**

Now that we’ve established *what* IaC
 is, we can start thinking about some of the tools used for 
infrastructure as code. Many tools fall under the IaC umbrella, 
including Terraform, AWS
 CloudFormation, Google Cloud Deployment Manager, Ansible, Puppet, Chef,
 SaltStack and Pulumi. It’s important to understand that some of these 
tools have different use cases, each with its own benefits. Due to the 
varied use cases of these IaC tools, having infrastructure provisioned, 
configured and deployed end-to-end will require using a combination of 
IaC tools rather than a single solution. To better understand these 
tools, this task will cover some of the key characteristics which 
distinguish these tools from each other so you know *what* tool to use and *when*.
 Bear in mind that the behaviour of these tools can often depend on 
exactly how they are used, often leading to debate over some of their 
characteristics; with this in mind, we will define those characteristics
 in question and how each tool is *generally* used.

**Declarative vs. Imperative**

First
 off, let’s establish the difference between declarative and imperative 
(also known as functional and procedural) IaC tools:

**Declarative**

This
 involves declaring an explicit desired state for your infrastructure, 
min/max resources, x components, etc.; the IaC tool will perform actions
 based on what is defined. A state file is kept to ensure your 
infrastructure’s current state matches the desired state. In other 
words, it focuses on the **what** rather than the **how**. A
 declarative IaC tool is usually idempotent, meaning the same result 
will be achieved when run repeatedly. This is because that check is done
 against the state file, and if the infrastructure is already 
provisioned, it will make no changes if rerun. Examples of declarative 
IaC tools are Terraform, AWS CloudFormation, Pulumi and Puppet (Ansible also supports declarative).

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1fe8ba3fc1a6c19ff9a54e81d3d84580.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1fe8ba3fc1a6c19ff9a54e81d3d84580.svg)

**Imperative**

This
 approach involves defining specific commands to be run to achieve the 
desired state; these commands need to be executed in a particular order.
 Imperative IaC is usually not idempotent in that if you run these tools
 multiple times, the same result won’t be replicated, or the tool may 
run into some configuration issues. This is because these commands will 
be run regardless of the state of your infrastructure, so running these 
commands on an already provisioned infrastructure may cause additional 
unwanted infrastructure to be added or may break the configuration of 
some existing components (depending on the set-up of the infrastructure 
and the commands being run). Examples of imperative IaC tools: Chef is 
the best example of an imperative tool; however, SaltStack and Ansible 
both support imperative programming as well.

Imagine
 it like directions to an X on a map, where imperative will give you a 
list of directions which will bring you to X if you are at the known 
start point (e.g., an unconfigured server). However, if you are not at 
this known start point (e.g., a partially configured server), you will 
not arrive at X but somewhere slightly different. Declarative takes into
 account where you are on the map and works out which directions need to
 be taken to get to X from that point. Deciding which to use can depend 
on what your infrastructure needs are. Declarative is considered a more 
straightforward approach that is easier to manage, especially for 
long-term infrastructure. In contrast, imperative IaC is more flexible, 
giving the user more control and allowing them to specify exactly how 
the infrastructure is provisioned/managed rather than the tool itself 
taking care of it.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/2bd68304fbc939b4212c471a0868b202.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/2bd68304fbc939b4212c471a0868b202.png)

# Agent-based vs. Agentless

Agent-based
 vs Agentless is a term that extends beyond infrastructure as code and 
is also used in the context of monitoring and security tools. In the 
context of IaC:

**Agent-based**

An
 “agent” will need to be installed on the server that is to be managed. 
It runs in the background and acts as a communication channel between 
the IaC tool and the resources that need managing. This agent is 
responsible for executing and reporting on the state of the 
infrastructure/managed resources. Note that this agent must be installed
 on every target system/node that needs to be managed. An agent-based 
IaC tool can perform tasks even when the system has limited connectivity
 or is offline, making it a robust choice for automation; however, you 
need to take care with maintenance when using these tools, monitoring 
the agent software closely so it can be restarted in the event of a 
crash.

Another
 thing to consider with agent-based IaC tools is that some of these 
tools will require opening ports on the server for inbound and outbound 
traffic so that the agent can push/pull configuration information; from a
 security perspective, more open ports are negative. Despite this, they 
offer a level of granular control over managed resources and can collect
 more detailed monitoring data. Because of this, they might be ideal if 
control is an important factor in your setup. Some agent-based IaC 
tools: Puppet, Chef, and Saltstack.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/20605c0c3f9cb08bddf3d3d1b1fb5d81.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/20605c0c3f9cb08bddf3d3d1b1fb5d81.png)

**Agentless**

Agentless
 IaC tools, as you may have guessed, do not require agents to be 
installed on target systems. Instead, these tools leverage existing 
communication protocols like SSH,
 WinRM or Cloud APIs to interact with and provision resources on the 
target system. Agentless IaC tools benefit from being easier to use; 
their simplicity during set-up can mean faster deployment time, and 
their agentless nature can also mean the tool can be deployed across 
multiple environments without custom agent changes needing to be made 
based on each environment’s needs, making it a flexible choice. Also, 
compared to agent-based IaC tools, there is less maintenance and no 
risks surrounding the securing of an agent. However, agentless IaC tools
 generally have less control over target systems than agent-based tools.
 Agentless tools are useful in environments which have to adapt to 
fluctuating workloads, with resources being created/destroyed to meet 
these workloads. These newly created resources can be managed without 
having to rely on pre-installed agents. Agentless IaC tools: Terraform, 
AWS CloudFormation, Pulumi and Ansible.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/10e228ac974caf680f0fa21a854924c5.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/10e228ac974caf680f0fa21a854924c5.png)

Once
 again, both options have their advantages and disadvantages. 
Infrastructure provisioning and configuration can present developers 
with a very particular set of problems, and choosing the correct tool 
for the job, depending on what needs to be done, involves taking these 
into account.

IaC - The Tools Part 2

**Immutable vs. Mutable**

Immutable
 vs mutable infrastructure refers to whether or not changes can be made 
to an infrastructure. To define both, let’s imagine we have a simple 
infrastructure, a virtual machine with a web server and application. If 
you want to change this infrastructure, for example, deploy some 
application code to your web application, this code will mean your web 
application will go from version 1 to version 2. How might that look for
 each?

Mutable

Mutable
 infrastructure means you can make changes to that infrastructure in 
place. So, in our current example, we can upgrade the application on the
 server it’s currently running on. The advantage here is that no 
additional resources need to be provisioned for this update, with the 
resources already being used just needing to be changed. Where mutable 
infrastructure starts presenting issues is, imagine your web application
 update contains three changes, and whilst these updates are being made,
 one of the changes fails to apply. This is a common occurrence in 
development and can occur for several reasons, such as application 
misconfiguration or a network dropout. Now running on your server will 
be a web application version with two of the three changes required to 
be version 2. In other words, it’s no longer version 1 anymore but not 
quite version 2 either. When an application is updated in a production 
environment, it will have been tested first in development and staging 
environments. What won’t have been tested is this halfway version, 
leading to all kinds of potential issues. Imagine now that this update 
was not just rolled out on a single server, but many, maybe some updates
 succeeded, and some failed with errors in different changes. You can 
see how this can become an issue very quickly with different versions of
 the web application existing across many servers.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/48c0d1e0a1fdfa62bcdb829892462093.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/48c0d1e0a1fdfa62bcdb829892462093.png)

Immutable

Immutable
 infrastructure means you cannot make changes to it. Once an 
infrastructure has been provisioned, that’s how it will be until it’s 
destroyed. Now, let’s apply that to our example. When this new version 2
 of the web application is deployed, an entirely new infrastructure will
 be deployed with this new version. Now, you have two infrastructures 
stood up: one with version 1 of the web application and one with version
 2. However, if all of the changes are implemented successfully (and 
only if they ALL are; otherwise, if it fails, the infrastructure will be
 torn down, and the process will be retried), the version 1 
infrastructure can be torn down. This approach has some drawbacks, as 
having multiple infrastructures stood up side by side or retrying on 
failed attempts is more resource-intensive than simply updating in 
place, but it allows for consistency across servers. You know with 
certainty that x server is running version 2 of the web application.

Immutable IaC tools: Terraform, AWS
 CloudFormation, Google Cloud Deployment Manager, Pulumi (some of these 
tools can be configured to be used with a mutable infrastructure but 
work better with an immutable approach)

In
 the example given, it makes more sense to use an immutable 
infrastructure. However, to demonstrate further that each can have its 
own use case, imagine the server instead is a critical database system 
that requires regular maintenance updates and patching. If you were to 
use an immutable infrastructure for this, the critical database would 
have to be rebuilt from scratch every time, which can be a risky process
 when dealing with business-critical data. So, in this instance, it 
might make sense to use a mutable infrastructure.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/97dcbf50ca109f1e26f2751c3d3fbf16.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/97dcbf50ca109f1e26f2751c3d3fbf16.png)

# Provisioning vs. Configuration Management

All
 the characteristics discussed in this task so far are behavioural; in 
other words, how does this tool work? This way or that way. Considering what a tool's purpose is and when it is used in the development of infrastructure will tell us whether it is a *provisioning* tool or a *configuration* *management* tool. You
 might see these primary functions defined differently elsewhere, for 
example, infrastructure as code vs. configuration as code, but to 
determine which tool falls into which category, you simply need to ask, 
"What can it do?". If we think about four key tasks: Infrastructure 
provisioning (the set-up of the infrastructure), infrastructure 
management (changes made to infrastructure), software installation 
(initial installation and configuration of software/applications), and 
software management (updates made to software or config changes).

There
 is no single tool that can perform all 4 of these tasks. Instead, 
combining two tools, a provisioning tool and a configuration management 
tool, is common practice to cover all these. There will be a practical 
example of exactly what tools can cover which tasks in the static site 
coming up. Some examples of each type of tool:

Provisioning tools: Terraform, AWS CloudFormation, Google Cloud Deployment Manager, Pulumi

Configuration management tools: Ansible, Chef, Puppet, Saltstack

Let’s
 consider a real-life industry example of how these two types of tools 
might be used. Say you work for a company which needs to set up a new 
infrastructure for a web application. A similar one has been deployed 
before and fell prey to some malicious activity, so this time, you will 
install an agent to monitor for this activity. The infrastructure would 
be defined and provisioned using a provisioning tool like Terraform, and
 then a configuration management tool like Ansible would be used to 
install an agent within the provisioned infrastructure to monitor for 
malicious behaviour.

# Put That All Together

Now,
 you’ve been introduced to the world of infrastructure as code tools and
 their various uses. Each has its characteristics which best suit 
different use cases and scenarios. In that way, they are no different to
 physical tools; you have to assess the problem and choose the best tool
 to address it. Here's a little summary of what we've discussed, as well
 as a little bit more information about some of the tools mentioned:

**Terraform**:
 is a declarative, agentless infrastructure provisioning tool that works
 with immutable infrastructure. Terraform is one of the most popular 
infrastructure provisioning tools out there, allowing for the management
 of infrastructure across multiple cloud providers like AWS, GCP and Azure.

**Ansible:**
 is a hybrid, typically agentless configuration management tool that 
works with mutable infrastructure. Another example of a massively 
popular tool in the DevSecOps
 space. It's slightly harder to categorise than some of the other tools,
 because of how this tool functions and what it does can depend on how 
you employ it. For example, there is much discussion over whether 
Ansible is an imperative or declarative tool. In reality, Ansible is 
sort of a hybrid in a sense.

**Pulumi:**
 is a declarative, agentless infrastructure provisioning tool that works
 with immutable infrastructure. Pulumi is similar in nature to Terraform
 but has become increasingly popular in recent years due to its ability 
to let users define their desired infrastructure using familiar 
general-purpose languages like Python, JavaScript, Go, Java and markup 
languages like YAML.

**Aws CloudFormation:** is a declarative, agentless infrastructure provisioning tool which can be used to implement an immutable infrastructure on AWS. This is an AWS-managed service and provisions AWS cloud resources using JSON / YAML templates.

**Chef:**
 is an imperative, agent-based configuration management tool that works 
with mutable infrastructure. Chef gets an infrastructure to a desired 
state by running a series of instructions contained in a file referred 
to as a 'Recipe'; a collection of these files is referred to as a 
'Cookbook'.

**Puppet:** is
 a declarative, agent-based configuration management tool that works 
with mutable infrastructure. In Puppet, you define the desired 
configuration state using their own domain-specific language (DSL), 
"Puppet Code"; Puppet then automates this configuration through a Puppet
 primary server and agent.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/63d2d4fc39187ca84cc6f9dc15197b01.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/63d2d4fc39187ca84cc6f9dc15197b01.png)

Infrastructure as Code Lifecycle

# The Lifecycle

Now
 that it has been established what IaC is and the tools we use to 
implement it, it’s time to define the lifecycle. There is talk about an 
IaC lifecycle across forms, blog posts, and academic papers. Still, 
there is yet to be an agreed-upon and widely adopted lifecycle (as there
 is for DevOps/DevSecOps). Because we think you, the reader, would 
benefit from having an IaC lifecycle to use as an educational tool, we 
have defined one, the infrastructure as code lifecycle (IaCLC). The 
actions/tasks performed by developers and IaC tools can be broken down 
into phases, which together make a lifecycle; this lifecycle helps us 
understand that infrastructure as code has continual and repeatable 
processes, which don't simply follow a linear sequence of provision and 
management tasks. This task will outline the stages of the IaC 
lifecycle, its phases and how they are connected.

The IaCLC is designed to give DevOps
 Engineers (or anyone else assigned with the task) guidance on the tasks
 associated with provisioning infrastructure and the continued support 
of that infrastructure. Key DevOps practices such as continuous 
integration and continuous deployment are also parts of best practices 
throughout the lifecycle.

Due to IaC being a development process, some parallels can be drawn between the IaC lifecycle and the SDLC,
 which also covers a solution's planning/designing, implementation, 
testing, deployment and monitoring. While these parallels exist due to 
these lifecycles being created on the same foundations (providing 
developer guidance and improving output quality), they don't directly 
fit into each other. Both lifecycles break down tasks into phases. 
However, due to the frequently changing infrastructure needs, the IaCLC distinguishes between two different types of phases.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/248f6eebfa09c336733237216b1b4b8b.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/248f6eebfa09c336733237216b1b4b8b.svg)

**Breaking it Down**

As mentioned above, these phases are separated into two types. Let's break that down:

**Continual (Best Practice) Phases:**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/5773fd17068a833784ff86ecaef4b97e.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/5773fd17068a833784ff86ecaef4b97e.svg)

These
 phases are continually done to ensure best practices throughout the 
various stages of infrastructure development and management. Continual 
phases can trigger repeatable phases

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/821fd689bebc77ac57c22f309ee3caa9.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/821fd689bebc77ac57c22f309ee3caa9.svg)

**Repeatable(Infra Creation + Config) Phases:**

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/f41d65ba204de1ab577d9e2cc981dfa8.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/f41d65ba204de1ab577d9e2cc981dfa8.svg)

These phases are done during the creation/configuration of an infrastructure and are
 done one or many times at different points and with differing 
variations depending on what needs to be done. Some examples are below:

Activity: Entirely new infra

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b01d5b3df9751d5b35a6d23b724ecfc3.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b01d5b3df9751d5b35a6d23b724ecfc3.svg)

Activity: Config change

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/feb147861ab6640feb45ea3494d08678.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/feb147861ab6640feb45ea3494d08678.svg)

**The Continual (Best Practice) Phases**

| Version Control | This
 phase involves versioning code while defining your infrastructure and 
making changes. This way, when it comes to the later rollback phase, 
there are clearly defined versions to fall back on should a new change 
break something. |
| --- | --- |
| Collaboration | When
 working as part of a team on infrastructure, it is crucial to 
communicate and collaborate so everyone is on the same page. Otherwise, 
this can lead to a disconnect between modular infrastructure components 
or general confusion over infrastructure. |
| Monitoring/Maintenance | Once
 an infrastructure has been provisioned/configured, it must be monitored
 for poor performance, security events, failure events, warnings, etc. 
Automated maintenance tasks (e.g. disk clean-up) can help avoid some of 
these events. In certain events, this phase can trigger the rollback 
phase. |
| Rollback | In
 the event of a failure event post-deployment, the infrastructure will 
need to be rolled back to the last known working version. |
| Review + Change | Just
 because an infrastructure works doesn’t mean it’s as efficient as it 
could be. Perhaps a new security vulnerability has been discovered, or 
maybe there’s a new business requirement that would benefit from an 
infrastructure change. Infrastructure should routinely be reviewed to 
determine if this is the case, and changed if so. |

**The Repeatable (Infra Creation + Config) Phases**

| Design | The
 infrastructure needs to be designed based on needs, taking security 
into account throughout the whole process (for example, poor scaling 
policy design can lead to availability issues, which is a huge security 
concern). |
| --- | --- |
| Define | Use the design to define the infrastructure that needs to be provisioned in code. |
| Test | Using
 a linter, validate the code for syntax errors or logical issues. Before
 provisioning is done in production, test the infrastructure in a 
replica environment (staging). |
| Provision | Provision the infrastructure that has been defined in the production environment using a provisioning tool, e.g. Terraform. |
| Configure | Configure the provisioned environment using a configuration management tool, e.g. Ansible. |

On-Prem IaC vs. Cloud-Based IaC

Infrastructure as code has two use cases. On-premises IaC and cloud-based IaC.
 Going forward, this module will go in-depth and give practical examples
 of both of these. Let’s first establish the key differences between the
 two. Here, we outline key differences between on-prem IaC and cloud-based IaC across five categories: Location, Tech, Resources, Scalability and Cost.

# Comparison

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/ec6e26a0a171e8f0177a0626903bb581.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/ec6e26a0a171e8f0177a0626903bb581.png)

**On-prem:**
 As the name implies, if your infrastructure is on-prem, then the code 
written will configure servers, network devices, storage and software 
located on your premises. This can mean physical infrastructure in a 
premises owned by an organisation or rented in a data centre.

**Cloud-based:** This
 means provisioning and configuring infrastructure resources in a cloud 
environment using cloud resources. This is done using a cloud service 
provider (CSP) such as AWS, Microsoft Azure, GCP, etc.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/299069e9a2214ef21b905a52b39b0e60.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/299069e9a2214ef21b905a52b39b0e60.png)

**On-prem:**
 Typically, when working with an on-premises infrastructure, IaC tools 
like Ansible, Chef and Puppet would be used (although others can be 
configured to do so) to manage and provision infrastructure on physical 
servers or virtual machines in an on-prem data centre.

**Cloud-based:**
 There are many tools available to provision and manage cloud 
infrastructure designed to leverage the elastic nature of cloud 
computing, with some cloud service providers having their own IaC 
tool/service. Some examples of tools that can be used for cloud-based 
IaC are Terraform, AWS CloudFormation, Azure Resource Manager (ARM) templates and Google Cloud Deployment Manager.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/470fd2be85001e01882c12235ac8d787.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/470fd2be85001e01882c12235ac8d787.png)

**On-prem:**
 When using on-prem IaC, you’ll likely be dealing with physical 
hardware, which comes with the caveats of hardware compatibility, 
physical upkeep and limited physical resources. This will mean setting 
up and configuring those physical resources (physical servers, storage 
devices, network equipment, etc.). On-prem IaC may be used by companies 
who rely on their on-premises infrastructure due to legacy systems and 
require assistance in the efficient management of this infrastructure.

**Cloud-based:** In the cloud, you interact with virtual resources provided by the cloud service provider (AWS,
 GCP, Azure, etc.). These resources can be provisioned/managed by 
cloud-based IaC tools. The underlying infrastructure is handled by the 
CSP and not the user. Cloud-based IaC would be perfect for companies 
that offer video streaming services. Due to the nature of this service, 
it can lead to a fluctuating demand on computing resources, which can 
peak. Cloud-based IaC makes it easy to gain access to additional 
cloud-based virtual machines or storage depending on resource 
consumption to ensure consistent performance during these peaks.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/9b34ecfc02cb1c877a80306d889f6ab2.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/9b34ecfc02cb1c877a80306d889f6ab2.png)

**On-prem:**
 Scaling resources using on-prem IaC can be a slow and cumbersome 
process. This can involve manual/physical changes and procurement. 
Because scalability is such a slow process, consideration is required, 
and hardware limitations must be enough to handle peak load. This can 
prove challenging in situations where an on-premises infrastructure 
starts receiving increased traffic (think enrolment or exam season at a 
university/college).

**Cloud-based:**
 Due to the cloud’s elastic nature, scaling resources is far more 
flexible than on-premises. Cloud-based IaC tools can define scaling 
policies so resources can be scaled up or down based on demand and 
resource consumption, leveraging auto-scaling features. This ensures 
that only the resources needed are paid for. Cloud-based IaC can 
streamline the process of scaling infrastructure to meet demands during 
peak seasons. Imagine an infrastructure that supports an online game. 
This infrastructure would see increased traffic when the game releases a
 new update, or an event is underway.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/59742076f49a1fa228dfd972a330ec7f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/59742076f49a1fa228dfd972a330ec7f.png)

**On-prem:**
 On-premises infrastructure expenses mean having to pay for physical 
hardware (or leasing a server from a third-party data centre - depending
 on the use case); this also comes with the costs of physical upkeep 
(fault repairs/part replacements, etc.), operational costs and expenses 
involved in upgrading the infrastructure. An on-premises infrastructure 
and the use of on-prem IaC doesn't boast any cost benefits per se. If 
choosing on-prem, it would likely be due to a combination of other 
factors rather than cost.

**Cloud-based:**
 When using cloud-based IaC, you’ll deal with infrastructure that cloud 
service providers bill for on a pay-as-you-go basis. This means you only
 need to pay for what you use (which can be made more cost-effective by 
the efficient use of auto-scaling). Cloud-based IaC tools are an ideal 
and cost-effective solution for scenarios where infrastructure needs to 
be automatically scaled up and down on demand. For example, if an online
 retailer is expecting an increase in traffic over Black Friday weekend 
or over the holiday period, they may want to scale up their resources 
but not have to pay for those resources when traffic returns to an 
average rate.

When
 comparing cloud-based infrastructure as code with on-premises 
infrastructure as code, it primarily comes down to the location of the 
infrastructure and what tools are used in their management and 
provisioning. Cloud-based IaC uses virtual elastic resources, which are 
charged on a pay-as-you-go basis and provided by a CSP, whereas on-prem IaC deals with physical hardware.

**Benefits**

Let’s
 examine how the above-mentioned differences translate into benefits 
depending on specific use cases. Here are some of the benefits of each 
to give you an idea of when you might use on-prem IaC and Cloud based 
IaC:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b85b36e8d1cc6a9e0a38c0e8ad908124.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b85b36e8d1cc6a9e0a38c0e8ad908124.png)

**On-prem IaC:** The
 main advantage of on-premises infrastructure as code is that it allows 
complete control. This complete control is sometimes required due to 
regulations/security and compliance requirements. This is common in 
bigger banking corporations or businesses that deal with 
customer-sensitive or government data. These regulations can call for 
data sovereignty (meaning the data has to be stored and processed within
 the country). Whilst cloud providers offer specialised government cloud
 environments for some of these cases (e.g. us gov cloud in AWS),
 these offerings are only available in certain regions; for regions like
 Africa, there is no dedicated government cloud, meaning on-premises 
infrastructure as code would need to be used to adhere to strict 
security/compliance requirements.

**Cloud-based IaC:** It
 has many advantages for fast-paced and growing businesses. The 
scalability allows infrastructure to be rapidly scaled up or down to 
meet fluctuating demand without the constraints of physical on-premises 
infrastructure. Cloud-based infrastructure also allows infrastructure to
 be deployed globally across different regions, reducing user latency, 
which can be essential for businesses that need to provide a service to 
customers worldwide with little to no latency, like online gaming. With 
cloud providers billing on a pay-as-you-go basis, this can mean that 
companies can pay only for the infrastructure that they need/use, 
meaning investment doesn’t need to be made into physical hardware and 
the maintenance of that hardware.

## KURBENETES

Kubernetes 101

# A New Dawn

To
 better understand Kubernetes, let us first consider the context of its 
emergence. In other words, why was it needed in the first place? Back in
 the day, it was more common for companies to have a monolithic 
architecture. That is, an application is built as a single unit, a 
single code base, and usually, a single executable deployed as a single 
component. This worked and still works for a lot of companies; however, 
some companies started to switch to a microservices architecture, so 
instead of having one monolithic application, it would be broken down 
into different components, each of these components usually having 
different business functions, meaning high demand business functions can
 be scaled without having to scale the entire application. One 
high-profile example of this happened in 2009 (before microservices even
 had a name) when Netflix had issues meeting their increased demands 
with their monolithic architecture, and so began the adoption of 
microservices architecture.

Microservices 
architecture is now an increasingly popular approach, and the reason why
 this is so important for today's lesson is that container technologies 
offer the perfect host for these microservices. With microservices 
architecture often comprising hundreds or even thousands of these 
containers, there was a need for a technology to help manage and 
organise them - no prizes for guessing what technology came to the 
rescue.

# Enter Kubernetes

Let's
 start with the big question, shall we? What is Kubernetes? In the 
previous rooms in this module, we discussed containers and Docker, so 
let's use that as our jumping-off point. Imagine you have a Docker 
container that is running an app that can be accessed externally. 
Suddenly, this application starts receiving a lot of traffic, so a new 
container with this application needs to be spun up so the traffic can 
be distributed between the two. This is where Kubernetes comes in as a 
container orchestration system. The term "orchestration" conjures up 
images of a literal orchestra. This metaphor does have some traction, 
with the containers being like instruments and Kubernetes being the 
conductor in control of the flow. It would just be a very strange 
orchestra where the conductor tells the players to leave when they're no
 longer needed for the song and brings new ones on when they are.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3afbfcf74be2eb28be74009467758d5f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3afbfcf74be2eb28be74009467758d5f.png)

# The Many Benefits of Kubernetes

Now
 that we've established what Kubernetes is and why it’s needed, let's 
look at how this technology can benefit the DevSecOps space.

- Kubernetes makes an application **highly available and scalable**. It does this by, for example, duplicating an application (and its db
component) and load balancing external requests to this application to
an available resource, therefore removing a single point of failure from the architecture and removing bottlenecks, which can slow down
application response times. As mentioned earlier, scalability is a big
concern for many companies; Kubernetes allows workloads to be scaled up
or down to match demand.
- Kubernetes is also **highly portable** in that it can be run anywhere with nearly any type of infrastructure and
can be used with a single or multi-cloud set, making it a very flexible
tool.
- Another benefit of Kubernetes is its popularity; because of this, many
technologies are compatible with it and can be used to make each tool
more powerful.

These are just a few ways Kubernetes benefits the DevSecOps space, and it explains why that word is thrown around so much!

Kubernetes Architecture

# Cluster Architecture

Okay,
 so we've learned what Kubernetes is, why it's needed and how it can 
benefit us in DevSecOps. Now, it's time to deepen our understanding by 
looking under the hood and analysing how it can do what it does. That's 
right! It's architecture time! We will go through each key component 
that makes up Kubernetes architecture, one by one, before putting it all
 together at the end and showing how all these components connect. Let's
 get into it!

**Kubernetes Pod**

Pods
 are the smallest deployable unit of computing you can create and manage
 in Kubernetes. When you work in DevSecOps with Kubernetes, you'll hear a
 lot of this word. You can think of a pod as a group of one or more 
containers. These containers share storage and network resources. 
Because of this, containers on the same pod can communicate easily as if
 they were on the same machine whilst maintaining a degree of isolation.
 Pods are treated as a unit of replication in Kubernetes; if a workload 
needs to be scaled up, you will increase the number of pods running.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/98b54b6b8427fae556be0cdd516b9e36.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/98b54b6b8427fae556be0cdd516b9e36.svg)

Kubernetes Nodes

Kubernetes
 workloads (applications) are run inside containers, which are placed in
 a pod. These pods run on nodes. When talking about node architecture, 
there are two types to consider. The **control plane** (also known as "master node") and **worker nodes**.
 Both of these have their own architecture/components, so let's take a 
look at them. Nodes can either be a virtual or physical machine. Think 
of it this way: if applications run in containers which are placed in a 
pod, nodes contain all the services necessary to run pods.

**Kubernetes Cluster**

At the highest level, we have our Kubernetes Cluster; put simply, a Cluster is just a set of nodes.

# The Kubernetes Control Plane

The
 control plane manages the worker nodes and pods in the cluster. It does
 this with the use of various components. Take a look at each of the 
components and what they are responsible for. Then see them all put 
together in a control plane architecture diagram.

**Kube-apiserver**

The
 API server is the front end of the control plane and is responsible for
 exposing the Kubernetes API. The kube-apiserver component is scalable, 
meaning multiple instances can be created so traffic can be 
load-balanced.

**Etcd**

Etcd
 is a key/value store containing cluster data / the current state of the
 cluster. It is highly available and consistent. If a change is made in 
the cluster, for example, another pod is spun up, this will be reflected
 in the key/value store, etcd. The other control plane components rely 
on etcd as an information store and query it for information such as 
available resources.

**Kube-scheduler**

The
 kube-scheduler component actively monitors the cluster. Its job is to 
catch any newly created pods that have yet to be assigned to a node and 
make sure it gets assigned to one. It makes this decision based on 
specific criteria, such as the resources used by the running application
 or available resources on all worker nodes.

**Kube-controller-manager**

This
 component is responsible for running the controller processes. There 
are many different types of controller processes, but one example of a 
controller process is the **node controller** process, which is 
responsible for noticing when nodes go down. The controller manager 
would then talk to the scheduler component to schedule a new node to 
come up.

Cloud-controller-manager

This
 component enables communication between a Kubernetes cluster and a 
cloud provider API. The purpose of this component is to allow the 
separation of components that communicate internally within the cluster 
and those that communicate externally by interacting with a cloud 
provider. This also allows cloud providers to release features at their 
own pace.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/84f898f84e80373f4a4a34e1f658d914.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/84f898f84e80373f4a4a34e1f658d914.svg)

# Kubernetes Worker Node

Worker
 nodes are responsible for maintaining running pods. Let's take a look 
at the components, which are present on every worker node, and what they
 are responsible for:

**Kubelet**

Kubelet
 is an agent that runs on every node in the cluster and is responsible 
for ensuring containers are running in a pod. Kubelet is provided with 
pod specifications and ensures the containers detailed in this pod 
specification are running and healthy! It executes actions given to it 
by the controller manager, for example, starting the pod with a 
container inside.

**Kube-proxy**

Kube-proxy
 is responsible for network communication within the cluster. It makes 
networking rules so traffic can flow and be directed to a pod (from 
inside or outside of the cluster). Traffic won't hit a pod directly but 
instead hit something called a Service (which would be associated with a
 group of pods), and then gets directed to one of the associated pods. 
More on services in the next task!

**Container runtime**

Pods
 have containers running inside of them. A container runtime must be 
installed on each node for this to happen. So far, we have covered one 
example of this in this module, which is probably the most popular 
choice, Docker. However, some alternatives can be used, such as rkt or 
runC.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1bf22d1f65ab408e71d15d5049d11129.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1bf22d1f65ab408e71d15d5049d11129.svg)

# Communication Between Components

Okay,
 so we've covered a lot there. Let's take a step and look at how all 
those individual components we've just covered work together to make up 
Kubernetes architecture. A Kubernetes cluster contains nodes and 
Kubernetes runs a workload by placing containers into pods that run on 
these nodes. Take a look at the graphic below to see how all these 
components come together.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1eba5a686238be009bc802dd419a09c8.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1eba5a686238be009bc802dd419a09c8.svg)

Kubernetes Landscape

# The Lay of the Land

So
 we've just looked at Kubernetes architecture and how things work and 
are set up behind the scenes! Now it's time to show you the lay of the 
land. In other words, what, as a DevSecOps engineer, would you be 
interacting with daily? We will go through some of the most common 
concepts in Kubernetes and break down what they are.

**Namespaces**

In
 Kubernetes, namespaces are used to isolate groups of resources in a 
single cluster. For example, say you want to group resources associated 
with a particular component, or if you are using a cluster to host 
multiple tenants, to group resources by tenant. Resources must be 
uniquely named within a namespace, but the same resource name can be 
used across various namespaces.

**ReplicaSet**

As
 the name suggests, a ReplicaSet in Kubernetes maintains a set of 
replica pods and can guarantee the availability of x number of identical
 pods (identical pods are helpful when a workload needs to be 
distributed between multiple pods). ReplicaSets usually aren't defined 
directly (neither are pods, for that matter) but are instead managed by a
 deployment, which brings us to our next concept.

**Deployments**

Deployments
 in Kubernetes are used to define a desired state. Once this desired 
state is defined, the deployment controller (one of the controller 
processes) changes the actual state to the desired state. Deployments 
provide declarative updates for pods and replica sets. In other words, 
as a user, you can define a deployment, let's say, for example, 
"test-nginx-deployment". In the definition, you can note that you want 
this deployment to have a ReplicaSet comprising three nginx pods. Once 
this deployment is defined, the ReplicaSet will create the pods in the 
background.

**StatefulSets**

To
 understand what Kubernetes Statefulsets are, you must first understand 
the difference between stateful and stateless apps. Stateful apps store 
and record user data, allowing them to return to a particular state. For
 example, suppose you have an open session using an email application 
and read 3 emails, but your session is interrupted. In that case, you 
can reload this application, and the state will have saved, ensuring 
these 3 emails are still read. Stateless applications, however, have no 
knowledge of any previous user interactions as it does not store user 
session data. For example, think of using a search engine to ask a 
question. If that session were to be interrupted, you would start the 
process again by searching the question, not relying on any previous 
session data.

For these stateless applications 
(search engine example), deployments can be used to define and manage 
pod replicas. Because of the application's stateless nature, replicas 
can be created with random pod names, and when removed, a pod can be 
deleted at random.

However, this is not the 
case for stateful applications (email example), because stateful 
applications need to access and update the current state of the user 
session. Imagine this current state is being stored in a database 
running across 3 pods (meaning the database is replicated 3 times). Now,
 what happens when one of the databases is updated? This would leave 2 
of the databases out of sync. This is where StatefulSets come in and is 
why you would use that instead of a deployment to manage stateful 
applications in Kubernetes.

Statefulsets 
enable stateful applications to run on Kubernetes, but unlike pods in a 
deployment, they cannot be created in any order and will have a unique 
ID (which is persistent, meaning if a pod fails, it will be brought back
 up and keep this ID) associated with each pod. In other words, these 
pods are created from the same specification but are not 
interchangeable. StatefulSets will have one pod that can read/write to 
the database (because there would be absolute carnage and all sorts of 
data inconsistency if the other pods could), referred to as the master 
pod. The other pods, referred to as slave pods, can only read and have 
their own replication of the storage, which is continuously synchronised
 to ensure any changes made by the master node are reflected.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3c0a1d5471d84bd4b86ae3e5a9fefa1f.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3c0a1d5471d84bd4b86ae3e5a9fefa1f.svg)

**Services**

To
 best understand services in Kubernetes, it's important to understand 
the problem they are solving. Kubernetes pods are ephemeral, meaning 
they have a short lifespan and are spun up and destroyed regularly. 
Imagine now a connection needs to be made to these pods. This could be 
from within the cluster; maybe a back-end application is running in 
these pods, and a front-end application needs to access them, or perhaps
 the request is coming from a browser, and these pods are running a web 
application. For this connection to happen, an IP address is required. 
If IP addresses were tied to pods, then these IP addresses would change 
frequently, causing all kinds of issues; services are used so that a 
single static IP address can be associated with a pod and its replicas. 
In other words, a service is placed in front of these pods and exposes 
them, acting as an access point. Having this single access point allows 
for requests to be load-balanced between the pod replicas. There are 
different types of services you can define: ClusterIP, LoadBalancer, 
NodePort and ExternalName. To learn more about these types and services 
in general, check out [here](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/263deb8228845aed0db78319097bd63b.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/263deb8228845aed0db78319097bd63b.svg)

**Ingress**

In
 the above section on Kubernetes services, we mentioned an example of an
 application which can be made accessible by using a service to expose 
the pods running this application (let's call this service A). Imagine 
now that this web application has a new feature. This new feature 
requires its own application and so has its own set of pods, which are 
being exposed by a separate service (let's call this service B). Now, 
let's say a user requests to access this new feature of the web 
application; there will need to be some kind of traffic routing in place
 to ensure this request gets directed to service B. That is where 
ingress comes in. Ingress acts as a single access point to the cluster 
and means that all routing rules are in a single resource.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1b0ab1f0b6ee779c1ee6f2a3f4d4924c.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1b0ab1f0b6ee779c1ee6f2a3f4d4924c.svg)

# DevOps vs. DevSecOps in K8s

This
 task has shown you some of the Kubernetes resources that work together 
to make a cluster. Next up, we're going to discuss how we interact with 
this cluster to create these components, but before we do that, this 
would be a good moment to discuss the division of labour in the world of
 K8s. It's important to understand, especially when learning for a 
certain career path, the difference between DevOps and DevSecOps 
responsibilities. At a very high level, you can think of DevOps tasks as
 those associated with building a cluster and DevSecOps tasks as those 
associated with securing a cluster. There will, of course, be some 
overlap depending on company architecture or corporate set-up, but 
generally, these tasks can be defined as one or the other. As this room 
serves as an introduction, it begins by showing you the building blocks 
of a Kubernetes cluster and how to interact with these resources (DevOps
 tasks). As this knowledge is foundational, understanding these concepts
 will help you in the later tasks when we discuss securing the cluster 
(DevSecOps tasks). That being said, as mentioned, the distinction is 
important, especially for those pursuing a specific career path, so keep
 this in mind going forward!

Kubernetes Configuration

# Time to Configure

Now
 that we've covered some of the key components used in Kubernetes, let's
 combine some of them and walk you through how this would be configured!
 The example we will use is a deployment which controls a ReplicaSet, 
which manages pods exposed by a service.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/a0872c63c555b82e63ce1ea3dbed6c42.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/a0872c63c555b82e63ce1ea3dbed6c42.svg)

To
 configure this setup, we would require two configuration files, one for
 the deployment and one for the service. Before giving you an example of
 how each of these files works, let's go over some of the basics of 
configuration in Kubernetes that will be consistent across these two 
files (and all configuration files, for that matter).

First,
 let's discuss the file format. Kubernetes config files are typically 
written in YAML. They can also be made interchangeably using the JSON 
format, but as per the Kubernetes documentation, it is generally 
considered best practice to use YAML given its easy, human-readable 
nature (just gotta keep an eye on that indentation!).

**Required Fields**

Next,
 let's discuss the four fields which must be present in each of the YAML
 files, breaking down what will need to be included in each one:

**apiVersion:**
 The version of the Kubernetes API you are going to use to create this 
object. The API version you use will depend on the object being defined.
 A cheatsheet for what API version to use for which object can be found [here](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html).

**kind:** What kind of object you are going to create (e.g. Deployment, Service, StatefulSet).

**metadata:** This will contain data that can be used to uniquely identify the object (including name and an optional namespace).

**spec:** The desired state of the object (for deployment, this might be 3 nginx pods).

**Configuring Resources**

Those
 are the very basics of Kubernetes YAML configuration files. Let's 
consider those and look now at the two files mentioned above. We're 
going to take a look at the service config file first, as when defining a
 deployment and service, it is generally best practice to first define 
the service before the back-end deployment/replicaset that it points to 
(this is because when Kubernetes starts a container, it creates an env 
variable for each service that was running when a container started). 
Here is what our example-service.yaml file looks like:

```bash
apiVersion: v1
kind: Service
metadata:
  name: example-nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 80
  type: ClusterIP

```

Let's break that down: **apiVersion** is set to v1 (the version of the Kubernetes API best used for this simple service example), and **kind** is set to service. For the **metadata**, we just called this service "example-nginx-service". The **spec**
 is where it gets more interesting, under 'selector', we have 'app: 
nginx'. This is going to be important going forward when we define our 
deployment configuration, as is the **ports** information, as we are 
essentially saying here: "This service will look for apps with the nginx
 label and will target port 80. An important distinction to make here is
 between the 'port' and 'targetPort' fields. The 'targetPort' is the 
port to which the service will send requests, i.e., the port the pods 
will be listening on. The 'port' is the port the service is exposed on. 
Finally, the 'type' is defined as ClusterIP (earlier, we discussed that 
there were multiple types of services, and this is one of them), which 
is the default service type. Now let's take a look at the Deployment 
YAML and define the back end which this service will point to:

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

```

The first thing you might notice is that inside the 'spec' field, 
there is a nested field called 'template', which itself contains a 
'metadata' and 'spec' field. To understand this, remember the image at 
the start of this task. We are defining a deployment which controls a 
ReplicaSet; here, in the outer 'spec' field, we tell Kubernetes we want 3
 replicas (identical pods) in this ReplicaSet. This template field is 
the template that Kubernetes will use to create those pods and so 
requires its own metadata field (so the pod can be identified) and spec 
field (so Kubernetes knows what image to run and which port to listen 
on). Note that the port defined here is the same as the one in the 
service YAML. This is because the service's target port is 80 and needs 
to match. As well as this, in the outer 'spec' field, you can see we 
have also set the 'selector' field to have a 'matchLabels', which 
matches what we defined in the 'selector' field for the service YAML. 
This is so the service is mapped to the correct pods. With these two 
config YAML files, we have defined a deployment that controls a 
ReplicaSet that manages 3 pods, all of which are exposed to a service. 
It's all coming together!

These config files 
are used to define the desired state of Kubernetes components; 
Kubernetes will constantly be checking this desired state against the 
current state of the cluster. Using the etcd (one of the control plane 
processes mentioned in an earlier task), Kubernetes populates these 
configuration files with the current state and does this comparison. For
 example, if we have told Kubernetes we want 3 nginx pods running, and 
it detects in the status that there are only 2 running pods, it will 
begin the actions to correct this.

Kubectl

# Kubectl to the Rescue

We've
 just covered how to define the desired state of your cluster using YAML
 config files, but currently, those exist only as files. To take these 
from configurations to running processes, we need to interact with the 
cluster. We can do this by interacting with the apiserver component of 
the control plane using different methods: UI if using the Kubernetes 
dashboard, API if using some sort of script or command line using a tool
 called kubectl. This task focuses on the last of these. Simply put, 
kubectl is a command line tool provided by Kubernetes that allows us to 
communicate with a Kubernetes cluster's control plane and is a great 
addition to your DevSecOps arsenal. This task will show you how to take 
the config files outlined in the previous task and apply them, as well 
as give you some boot camp training for this tool, teaching you some of 
the basic commands so you can navigate a Kubernetes cluster like it's 
your back garden!

**Kubectl apply**

Once
 you have defined your deployment and service configurations in the YAML
 file, the next step would be to apply them so Kubernetes can take the 
desired configuration and turn it into a running process(s). This is 
done using the aptly named apply command. For example, if applying the 
service YAML mentioned in the previous task, that would look like this:

```
kubectl apply -f example-deployment.yaml
```

**Kubectl get**

Once 
both configurations have been applied, you'll want to check the status 
of both to ensure things are running as expected. This would be done 
using the Kubectl get command. This is a very versatile command, and you
 will be using it a lot in your time with Kubernetes. The get command 
can be used to check the state of resources. The resource type will 
follow 'get', then `-n` or `--namespace`
 followed by the namespace (unless you are checking a cluster-level 
resource like a node). For example, to check the state of a deployment, 
you would use:

```
kubectl get pods -n example-namespace
```

The output for this command would look something like this:

Terminal

```
user@tryhackme$ kubectl get pods -n example-namespaceNAME          READY   STATUS              RESTARTS   AGE
example-pod   1/1     Running             0          2m18s
```

As mentioned, this command can be used to check on a variety of resources such as deployments, services, pods, and ReplicaSets.

**Kubectl describe**

This
 command can be used to show the details of a resource (or a group of 
resources). These details can help in troubleshooting or analysis 
situations. For example, say one of the pods in your cluster has started
 erroring out, and you want to get more information about the pod to try
 to determine why it has crashed. You would run the following command:

```
kubectl describe pod example-pod -n example-namespace
```

This would give you back some details about the erroring pod. For example:

Terminal

```
user@tryhackme$ kubectl describe pod example-pod -n example-namespaceName:             example-pod
Namespace:        example-namespace
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Mon, 22 Jan 2024 14:01:14 +0000
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.0.21
...
...
```

You can see here that the describe command details 
contain some "events". These events can help shine a light on what the 
issue is. For more details surrounding this event, Kubernetes captures 
logs from each container in a running pod. These logs can be viewed 
using our next command.

**Kubectl logs**

Say
 you want to view the application logs of the erroring pods. Maybe you 
want to view the logs surrounding the event error. For this, we would 
use the kubectl logs command. Here is an example of how this would be 
used:

```
kubectl logs example-pod -n example-namespace
```

These logs can provide valuable insight not just for troubleshooting but for security analysis as well.

**Kubectl exec**

Now,
 let's say the log information was helpful, but there are still some 
unanswered questions, and you want to dig deeper and access the 
container's shell. The kubectl exec command will allow you to get inside
 a container and do this! If a pod has more than one container, you can 
specify a container using the `-c` or `--container` flag. The command for this is (the `-it` flag runs the command in interactive mode, everything after `--` will be run inside the container):

```
kubectl exec -it example-pod -n example-namespace -- sh
```

From here, you can run any command you want from 
within the container itself. Maybe you want to snoop around for your 
security analysis or run a command to test connectivity from the 
container.

**Kubectl port-forward**

Another
 handy command is kubectl port-forward. This command allows you to 
create a secure tunnel between your local machine and a running pod in 
your cluster. An example of when this might be useful is when testing an
 application. Let's imagine we have an nginx web application running 
across 3 pods which are exposed by a web application service. If you 
remember, a service makes a pod externally accessible. We take the port 
that is used to expose these pods and map it to one of our local ports. 
For example, matching the target port (the port the service is exposed 
on, which in our configuration example was 8080) to local port 8090 
would make this web application accessible on our local machine at `http://localhost:8090`. The resources specified are `resource-type/resource-name`. This would be done using the kubectl port-forward command with the following syntax :

```
kubectl port-forward service/example-service 8090:8080
```

There
 are, of course, plenty more kubectl commands that can be used to 
navigate and interact with a Kubernetes cluster, but the ones covered 
give you a solid foundation, and you can perform some day-to-day 
DevSecOps tasks using only these. You will get a chance to demo these 
commands in this room's practical exercise in Task 8.

Now complete these questions: What command would follow 'kubectl' if you wanted to....

Kubernetes & DevSecOps

Okay, by now, you're 
getting pretty familiar with Kubernetes; it's becoming less of an 
acquaintance and more of a friend. You've learned the ins and outs of 
the tool and will soon get a chance to have a hands-on demo of it, but 
before any of that, let's look at exactly how YOU would use this tool as
 a DevSecOps engineer. After all, that's very likely why you're here!

# Kubernetes and Security

Before
 we dive into what a DevSecOps engineer would be responsible for in a 
Kubernetes cluster, let's consider Kubernetes from a security 
perspective to give some context. Kubernetes is, relatively speaking, 
new on the block. That is to say, it is an emerging technology. It's 
emerging but very popular, with many companies adopting Kubernetes, 
especially young tech and start-up companies.

Introducing
 any tool into a system is considered an increased security risk as a 
new tool means a new potential way into that system. These risks are 
amplified when dealing with a tool like Kubernetes, where you have a 
network of pods that can communicate with each other. The default 
setting allows any pod to communicate with another. This implies all 
kinds of security considerations. As a DevSecOps engineer, it is your 
responsibility to ensure these channels are secure.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3d57119b77c26780bd73a7d282bee799.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/3d57119b77c26780bd73a7d282bee799.png)

# Kubernetes Hardening

Container
 hardening is one way in which DevSecOps engineers can secure these 
channels, and we will dive into that later in this module with the [Container Hardening](https://tryhackme.com/room/containerhardening)
 room. It is the process of using container scanning tools to detect 
CVEs present in a cluster and remediate them to ensure minimal security 
breach risk.

Kubernetes hardening is precisely 
that, ensuring these channels are secure by fortifying your cluster 
following best container security practices that you would perform as a 
DevSecOps engineer. Various companies and government agencies have 
defined these best practices; let's go over each area in which we can 
strengthen our container security and how this can be done.

**Secure your Pods!**

Let's begin with a few ways to secure the pods themselves. Some best practices for pod security include:

- Containers that run applications should not have root privileges
- Containers should have an immutable filesystem, meaning they cannot be altered or
added to (depending on the purpose of the container, this may not be
possible)
- Container images should be frequently scanned for vulnerabilities or misconfigurations
- Privileged containers should be prevented
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

**Hardening and Separation of your Network!**

In
 the introduction to this task, one thing especially was flagged as a 
big security risk: communication. That communication happens over a 
network, and it's your job as a DevSecOps engineer to ensure this 
communication is secure. This can be done using the following best 
practices:

- Access to the control plane node should be restricted using a firewall and role-based access control in an isolated network
- Control plane components should communicate using Transport Layer Security (TLS) certificates
- An explicit deny policy should be created
- Credentials and sensitive information should not be stored as plain text in
configuration files. Instead, they should be encrypted and in Kubernetes secrets

**Using Authentication and Authorisation Optimally**

It
 wouldn't be a security lesson if we didn't talk about authentication 
and authorisation, of course! Kubernetes is no different. Here are some 
best practices which can help make sure you are making efficient use of 
Kubernetes authentication and authorisation features:

- Anonymous access should be disabled
- Strong user authentication should be used
- RBAC policies should be created for the various teams using the cluster and the service accounts utilised

**Keeping an Eye Out**

You
 can't rest easy knowing your Kubernetes cluster is secure if you don't 
know what's going on in your Kubernetes cluster. Here are some logging 
best practices to ensure you know exactly what is going on in your 
cluster and can detect threats when they appear:

- Audit logging should be enabled
- A log monitoring and alerting system should be implemented

**Security Never Sleeps**

This
 is in no way an endorsement of a sleepless lifestyle; DevSecOps 
engineers do, in fact, need to sleep! Being secure is one thing, staying
 secure is another. Here are some best practices to ensure your cluster 
stays a safe haven:

- Security patches and updates should be applied quickly
- Vulnerability scans and penetration tests should be done semi-regularly
- Any obsolete components in the cluster should be removed

# Kubernetes Security Best Practices in Action

# 

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6269219b0a19bf47cf26f89bee511374.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6269219b0a19bf47cf26f89bee511374.png)

The above information tells us there are **a lot**
 of ways to harden a Kubernetes infrastructure. There are so many, in 
fact, that breaking down each practice would turn this room into a 
self-published e-book. With the opportunity to get your hands on 
Kubernetes just a task away, let's finish this one by breaking down just
 three of them.

**RBAC**

RBAC
 (Role-Based Access Control) in Kubernetes regulates access to a 
Kubernetes cluster and its resources based on defined roles and 
permissions. These permissions (permission to create/delete x resource, 
etc.) are assigned to users, groups or service accounts. RBAC is a good 
way to ensure the resources in your cluster can only be accessed by 
those who **need** to access it. RBAC can be configured using a YAML 
file (same as defining a resource) where specific rules can be defined 
by declaring the resource type and verbs. Verbs are the actions being 
restricted, such as 'create' and 'get'.

**Secrets Management**

A Kubernetes secret is an object used to store sensitive information (like credentials, OAuth tokens or SSH keys). Secrets are a good
 way to ensure that sensitive data isn't leaked and allow for more 
control over how this information is used. Secrets are stored as a 
base64 encoded string, unencrypted by default. For security, it is best 
to configure encryption at rest. Another way to promote secure secrets 
management in your Kubernetes cluster is to configure the least 
privilege access to secrets using RBAC.

**PSA (Pod Security Admission) and PSS (Pod Security Standards)**

Pod
 Security Standards are used to define security policies at 3 levels 
(privileged, baseline and restricted) at a namespace or cluster-wide 
level. What these levels mean:

- Privileged: This is a near unrestricted policy (allows for known privilege escalations)
- Baseline: This is a minimally restricted policy and will prevent known privilege
escalations (allows deployment of pods with default configuration)
- Restricted: This heavily restricted policy follows the current pod hardening best practices

Pod
 Security Admission (using a Pod Security Admission controller) enforces
 these Pod Security Standards by intercepting API server requests and 
applying these policies.

**Note:**
 Previously, the roles of PSA and PSS were fulfilled using PSPs (Pod 
Security Policies); however, as of Kubernetes v1.25, these have been 
removed. Just to save any confusion if you stumble across PSPs doing 
some extracurricular Kubernetes security study!

As
 you can see, a lot goes into fortifying a Kubernetes cluster and plenty
 to keep a DevSecOps engineer busy. These are some of the best practices
 involved in Kubernetes hardening. DevSecOps engineers, while following 
these practices and utilising techniques such as automated security 
checks, can ensure their Kubernetes environment is safeguarded against 
cyber threats.

Hands-on with Kubernetes

# Getting Started

Press the green **Start** **Machine**
 button located at the top-right of this task. The machine will start in
 split-view. In case it is not showing up, you can press the blue **Show Split View** button at the top-right of the page.

# Phase One: Explore

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/4de91b9b61095d466cc8c7ae3155f9f7.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/4de91b9b61095d466cc8c7ae3155f9f7.png)

Okay,
 let's get going, shall we? The first thing we want to do is start our 
Minikube cluster. You can do this by running the following command in 
the terminal (the cluster will take a couple of minutes to start up):

```
minikube start
```

Once
 the cluster has started up, you're ready to go! This guided walkthrough
 will take you through this cluster, reinforcing knowledge taught in the
 room. That being said, you have a Kubernetes cluster at your disposal, 
so feel free to explore the cluster and experiment with the different 
commands you have learned so far!

Let's see what's running already, shall we? We can do this using the following command (`-A` for all namespaces)

```
kubectl get pods -A
```

After running this, you should see a few pods running. These are the 
default pods present when you first start a Kubernetes cluster (you may 
recognise some of these names as they represent some of the control 
plane and worker node processes). Exciting stuff! But how about we make 
it more exciting by adding a deployment and service into the mix? On the
 VM you will be able to find some config YAML files located here:

```
~/Desktop/configuration
```

There are two config YAMLs here of interest to us:

**nginx-deployment.yaml**

and

**nginx-service.yaml**

. Check these configuration files out using the cat command:

```
cat filename
```

Let's break down what we see in each of these files:

**nginx-deployment.yaml**

This is a relatively simple deployment; we can see the desired state has
 been defined as a single replica pod, inside of which will be a 
container running an nginx image. From the other lines, we can determine
 that this pod will be used to run some kind of web app.

**nginx-service.yaml**

This, again, is a straightforward nginx NodePort service being defined 
here. The eagle-eyed among you may have noticed that the 'selector: 
-> app: ' field matches the app label defined in the deployment, as 
well as the 'targetPort' matching the 'containerPort' outlined in the 
deployment. This service exposes the web application running in the pod,
 which the deployment controls. To apply the configuration outlined in 
these YAML files, we use the kubectl apply command. Remember to apply 
the service file first! Like so:

```
kubectl apply -f nginx-service.yaml
```

```
kubectl apply -f nginx-deployment.yaml
```

Verify the replica pod is running by using the following command (not 
providing any namespace flag will get all the pods in the default 
namespace, which is where our pod should be):

```
kubectl get pods -A
```

You should now see a pod with 'nginx-deployment' in its name! Our deployment has been started!

# Phase Two: Interact

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/df2a998cdc78ae2bfb98eb80650c5241.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/df2a998cdc78ae2bfb98eb80650c5241.png)

Okay,
 now we have a web application running in a pod, which is being exposed 
by a service. If you recall the nginx-service.yaml, the service connects
 to the web application using the target port of port 80 (the port where
 the container is exposed). However, the service's port itself is set to
 8080. We want to access this service. We will do this by using the 
kubectl port-forward command, which allows us to forward a port on our 
localhost to the Kubernetes service port (8080). Here is the full 
command to do so:

```
kubectl port-forward service/nginx-service 8090:8080
```

After running this command, open a web browser (Firefox) and access the web application at the following address:

```
http://localhost:8090/
```

Looks like a simple login terminal, but it needs credentials. Why don't 
we see if there are any Kubernetes secrets on the cluster that can help 
us log in to the terminal? Open another terminal window (so the previous
 window continues to port-forward) and run the following command to see 
if there are any secrets (in the default namespace):

```
kubectl get secrets
```

Ahh, there is! "terminal-creds" sounds like we are onto a winner! Using 
the kubectl describe command, we can get more details on this secret to 
see what is being stored here:

```
kubectl describe secret terminal-creds
```

In the description, we can see that two pieces of "Data" are being stored: a username and a password. While Kubernetes secrets

**are**

stored in plaintext and not encrypted by default, they are base64 
encoded, so we pipe this command and base64 decode the output to get it 
in plain text. To access this data, we can use the following command:

To get the username, run:

```
kubectl get secret terminal-creds -o jsonpath='{.data.username}'| base64 --decode
```

To get the password, run:

```
kubectl get secret terminal-creds -o jsonpath='{.data.password}'| base64 --decode
```

Use these credentials to access the login terminal. That's a bingo! We're in, and you have retrieved the flag!

**Bonus Task:** For
 those curious enough, you can use an alternate method to get this flag.
 It will require some Kubernetes investigation on your part, but the 
first breadcrumb lies in the nginx-deployment.yaml!

# Phase Three: Secure

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/8f63bc5d74b38ac585541f04b59acf9c.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/8f63bc5d74b38ac585541f04b59acf9c.png)

It's
 great that we could access the terminal using the credentials stored in
 the Kubernetes secret, but as a DevSecOps engineer, this is where our 
alarm bells should be going off. Time for us to get to work with some 
Kubernetes secret management. With these credentials being sensitive 
information, we want to restrict access to the Kubernetes secret they 
are stored in. We can do this by configuring RBAC (Role-Based Access 
Control).

First things first, let's decide who it is we want to be
 able to access this secret. Your DevSecOps manager has suggested that 
you restrict access to a service account, which is essentially an 
identity a pod can assume to interact with the Kubernetes API/cluster. 
By doing this, we can maybe even set it up so that in the future, our 
daily terminal tasks can be run by an application in a pod. Let's use 
the kubectl create serviceaccount (can be abbreviated to 'sa') command 
to make two service accounts, the 'terminal-user' for non-admin terminal
 activities (should not have access to secret) and the 'terminal-admin' 
for admin terminal activities (should have access to secret). Run these 
two commands to make those service accounts:

```
kubectl create sa terminal-user
```

```
kubectl create sa terminal-admin
```

With those service accounts created, it's time to restrict access to the
 'terminal-creds' secret so that only the 'terminal-admin' service 
account can access it. We are going to do this by defining and applying 
two configurations. First of all, a Role YAML that defines the role and 
what it can do (get the 'terminal-creds' secret). Then, a Role Binding 
YAML that binds the role we have defined to the 'terminal admin' service
 account. Navigate to the following directory and cat the two YAMLs to 
examine how these are defined:

```
~/Desktop/configuration/rbac
```

**role.yaml**

Here, you can see we define a role named "secret-admin". In the rules 
section, we define what it is this role can do. We define the resource 
(secrets), what verbs are being restricted (we are restricting the 'get'
 verb, but you could restrict others) and finally, the name of our 
secret (terminal-creds).

**role-binding.yaml**

In this YAML, we bind the 'terminal-admin' service account (in the 
'subjects' section) with the 'secret-admin' role defined above (in the 
roleRef section).

Lets now apply these configurations the same way we applied the deployment and service (using kubectl apply):

```
kubectl apply -f role.yaml
```

```
kubectl apply -f role-binding.yaml
```

You have now configured RBAC for this Kubernetes secret! The 
only thing left to do is test whether our RBAC is working. We can do 
this using the kubectl auth command, which tells us if a service account
 has sufficient permission to perform a specific action. Let us first 
verify that the regular 'terminal-user' service account CAN NOT access 
the secret:

```
kubectl auth can-i get secret/terminal-creds --as=system:serviceaccount:default:terminal-user
```

It looks like we expected. This "no" response confirms that this service
 account can no longer access the terminal-creds secret. Now, finally, 
let us verify that our 'terminal-admin' service account CAN access it:

```
kubectl auth can-i get secret/terminal-creds --as=system:serviceaccount:default:terminal-admin
```

With this "yes" output, you have confirmed RBAC is in place and 
fulfilled your duty as a DevSecOps engineer, fortifying the cluster and 
taking a good first step into hardening this cluster. Hope you've 
enjoyed taking a little tour around this Kubernetes cluster and getting 
to know the basics. Until next time!

## ON-PREMISES IAC

Why On-Premises

On-premises IaC refers 
to using infrastructure as code to deploy systems and services on an 
internal network. In essence, all the infrastructure that will host the 
systems and services can be found locally in the organisation's data 
centre.

# Reasons for On-Prem IaC

In the modern world, where we have several cloud providers, using 
on-prem IaC may seem counter-intuitive. However, there are some cases 
where on-prem IaC will suit your needs much better. The biggest benefit 
is that it allows you much better control of your entire IaC pipeline. 
Let's use another popular example, GitHub vs self-hosted GitLab, as a 
case study.

GitHub
 and GitLab are two popular source code management platforms, backed by 
the popular versioning software Git, that are used by organisations. 
However, deciding between the two often becomes a question of control. 
If you self-host the solution using GitLab, you fully control the entire
 stack. You are ultimately not only responsible for the management of 
the GitLab platform, but also the underlying infrastructure. While this 
is a lot more work, it also allows you to lock down access 
significantly. For example, you could only allow access to your GitLab 
instance via VPN, meaning it is not exposed to the internet for 
everyone.

Conversely, using GitHub means you are shifting some of that 
security responsibility. It is important to remember that GitHub is a 
Software-as-a-Service (SaaS)
 solution. That means that if you use GitHub, you have no control over 
the infrastructure hosting your source code. Instead, you are 
transferring the security responsibility of infrastructure management to
 GitHub, which becomes a third party of your organisation. While these 
organisations take security measures seriously, their security is not 
without flaws, which can leave your organisation's source code [exposed](https://thehackernews.com/2023/01/github-breach-hackers-stole-code.html). This is a risk that you have to accept whenever you use a third party.

Extrapolating from this case study, you should see why some 
organisations still prefer on-prem IaC, especially in heavily regulated 
sectors, such as the financial or governmental sectors. While on-prem 
IaC is definitely more effort, it provides an organisation with full 
control and customisation of their IaC pipeline.

# Benefits and Drawbacks

To summarise why one would use on-prem IaC and determine if it is the
 correct solution for your specific problem, let's look at the benefits 
and drawbacks.

**On-prem IaC has the following benefits:**

- Allows full control of the IaC pipeline
- The IaC pipeline can be fully customised for your exact needs
- Data protection and regulation is easier to perform as the IaC pipeline does not host resources on third-party systems
- While the initial investment cost of the infrastructure is high, there are no monthly fees for hosting the IaC pipeline
- It is often easier to do small deployments

**On-prem IaC has the following drawbacks:**

- As you are hosting your own IaC pipeline, you are fully responsible for its security and configuration
- Scalability of deployments is not as flexible as cloud-based IaC,
which can lead to either not having sufficient resources for the
deployment or an over-investment in resources
- The initial investment for on-prem IaC is significantly higher than cloud-based IaC

Now that you understand why on-prem IaC can be used, let's dive into 
some of the tooling that can be used to create your very own on-prem 
IaC. While there are many different tools and software that can be used,
 for this room, we will focus on Vagrant and Ansible as examples.

Vagrant Basics

In our on-prem IaC journey, we will start with [Vagrant](https://developer.hashicorp.com/vagrant).
 Vagrant is a software solution that can be used for building and 
maintaining portable virtual software development environments. In 
essence, Vagrant can be used to create resources from an IaC pipeline. 
You can think of Vagrant as the big brother of Docker. In the context of
 Vagrant, Docker would be seen as a provider, meaning that Vagrant could
 be used to not only deploy Docker instances but also the actual servers
 that would host them.

# Terminology

Before diving into using Vagrant, let's brush up on some terminology first.

| Term | Definition |
| --- | --- |
| Provider | A Vagrant provider is the virtualisation technology that will 
be used to provision the IaC deployment. Vagrant can use different 
providers such as Docker, VirtualBox, VMware, and even AWS for cloud-based deployments. |
| Provision | Provision is the term used to perform an action using Vagrant. This 
can be actions such as adding new files or running a script to configure
 the host created with Vagrant. |
| Configure | Configure is used to perform configuration changes using Vagrant. 
This can be changed by adding a network interface to a host or changing 
its hostname. |
| Variable | A variable stores some value that will be used in the Vagrant deployment script. |
| Box | The Box refers to the image that will be provisioned by Vagrant. |
| Vagrantfile | The Vagrantfile is the provisioning file that will be read and executed by Vagrant. |

# Vagrant Example

Let's take a look at a simple Vagrant provisioning script. In our example here, we have the following folder structure:

```
.
├── provision
│   ├── files.zip
│   └── script.sh
└── Vagrantfile
```

The Vagrantfile script has the following code:

```c
Vagrant.configure("2") do |cfg|
  cfg.vm.define "server" do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "testserver"
    config.vm.provider :virtualbox do |v, override|
       v.gui = false
       v.cpus = 1
       v.memory = 4096
    end

    config.vm.network :private_network,
        :ip => 172.16.2.101
    config.vm.network :private_network,
        :ip => 10.10.10.101
  end

  cfg.vm.define "server2" do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "testserver2"
    config.vm.provider :virtualbox do |v, override|
       v.gui = false
       v.cpus = 2
       v.memory = 4096
    end

    #Upload resources
    config.vm.provision "file", source: "provision/files.zip",    destination: "/tmp/files.zip"

    #Run script
    config.vm.provision "shell", path: "provision/script.sh"
  end
end
```

In
 this example, we are going to provision two servers. Both of these 
servers will start with the base Ubuntu Bionic x64 image. Like Docker, 
these images will be pulled from a public image repo. We could, however,
 tell Vagrant where to find these images, meaning they can be pulled 
from a private repo of images as well. You can see that both servers are
 configured with a hostname and how many CPUs (1) and RAM
 (4GB) each host will have. The first server will also have two network 
interfaces with static IPs attached. The second server will have a file 
called `files.zip` uploaded, and a script called `script.sh` will be executed on the host.

If we want to provision the entire script, we would use the command `vagrant up`.
 This would provision both servers in the order specified in the 
Vagrantfile. We could also decide to only provision one of the servers 
by using the server name. For example, `testserver` could be provisioned using `vagrant up server`.

If you want to play around with VirtualBox provisioning using Vagrant, look at this [repo](https://github.com/MWR-CyberSec/tabletop-lab-creation). Using VirtualBox and Vagrant, this repo will allow you to create your very own Active Directory (AD)
 network with two domain controllers, a server, and a workstation. Give 
the Vagrantfile a read to see what provisioning will be performed on 
each host.

Ansible Basics

The next IaC tool to learn about is [Ansible](https://www.ansible.com/).
 Like Vagrant, Ansible is another suite of software tools that allows 
you to perform IaC. Ansible is also open-source, making it a popular 
choice for IaC pipelines and deployments. One main difference between 
Ansible and Vagrant is that Ansible performs version control on the 
steps executed. This means that Ansible is similar to Docker, in that it
 will only perform updates on steps that require updates, instead of 
requiring a full reprovision.

# Terminology

Before diving into using Ansible, let's brush up on some terminology first.

| Term | Definition |
| --- | --- |
| Playbook | An Ansible playbook is a YAML file with a series of steps that will be executed. |
| Template | Ansible allows for the creation of template files. These act as your
 base files, like a configuration file, with placeholders for Ansible 
variables, which will then be injected into at runtime to create a final
 file that can be deployed to the host. Using Ansible variables means 
that you can change the value of the variable in a single location and 
it will then propagate through to all placeholders in your 
configuration. |
| Role | Ansible allows for the creation of a collection of templates and 
instructions that are then called roles. A host that will be provisioned
 can then be assigned one or more of these roles, executing the entire 
template for the host. This allows you to reuse the role definition with
 a single line of configuration where you specify that the role must be 
provisioned on a host. |
| Variable | A variable stores some value that will be used in the Ansible 
deployment script. Ansible can take this a step further by having 
variable files where each file has different values for the same 
variables, and the decision is then made at runtime for which variable 
file will be used. |

# Ansible Example

Ansible makes use of a specific folder and file structure. The most important part of the structure is the playbook, a YAML
 file that ultimately dictates what commands will be executed for 
provisioning. Let's take a look at the typical folder structure:

```
.
├── playbook.yml
├── roles
│   ├── common
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   ├── apt.yml
│   │   │   ├── main.yml
│   │   │   ├── task1.yml
│   │   │   ├── task2.yml
│   │   │   └── yum.yml
│   │   ├── templates
│   │   │   ├── template1
│   │   │   └── template2
│   │   └── vars
│   │       ├── Debian.yml
│   │       └── RedHat.yml
│   ├── role2
│   ├── role3
│   └── role4
└── variables
    └── var.yml
```

The folder structure was only expanded for the `common` role. However, this same structure would apply for roles 2 to 3.

Let's dive a little bit into what each of these files would do. Let's start with the playbook.yml file:

```c
---
- name: Configure the server
  hosts: all
  become: yes
  roles:
    - common
    - role3
  vars_files:
    - variables/var.yml
```

As we can see, the playbook specifies that the `common` and `role3` roles should be applied for all hosts where this Ansible playbook will be executed. It will also use the `var.yml`
 file to overwrite any default variables within the roles. This allows 
us to only change the default variables where needed, as the defaults 
will then still be applied to all other variables.

To execute the `common` role, Ansible will load variables from the `defaults/main.yml` file and overwrite these variables with any new values found in the `var.yml` file. It will then read and execute the `tasks/main.yml` file. This file would look something like this:

```c
---
- name: includeOS specific variables
  include_vars: "{{ item }}"
  with_first_found:
    - "{{ ansible_distribution }}.yml"
    - "{{ ansible_os_family }}.yml"

- name: set root password
  user:
    name: root
    password: "{{ root_password }}"
  when: root_password is defined

- include: apt.yml
  when: ansible_os_family == "Debian"

- include: yum.yml
  when: ansible_os_family == "RedHat"

- include: task1.yml
- include: task2.yml
```

The first section of the Ansible file will determine the OS
 distribution of the host. It will then use this information to include 
OS-specific provisioning steps. As you can see from our folder 
structure, we have specific provisioning steps based on whether the 
distribution is Debian or RedHat. The second section of the playbook 
will set the root user's password. In the third section, we update the 
host and install some packages. However, we only execute the installing 
step matching the OS distribution. If the host is Debian, we will 
execute the commands specified in the `apt.yml` file. If the host is RedHat, we will execute the commands specified in the `yum.yml` file. This allows our Ansible role to be OS distribution agnostic. Lastly, we will execute the commands contained within the `task1.yml` and `task2.yml` files. These can be any commands, such as adding files to the host or making configuration changes.

This is quite a lot of information to take in, but as you start using
 these tools and follow along with what scripts get executed when, it 
makes a lot more sense.

# Combining Vagrant and Ansible

While you could stick to one IaC tool for your entire pipeline, it 
can often be beneficial to combine toolings. For example, Vagrant could 
be used for the main deployment of hosts, and Ansible can then be used 
for host-specific configuration. This way, you only use Vagrant when you
 want to recreate the entire network from scratch but can still use 
Ansible to make host-specific configuration changes until a full rebuild
 is required. Ansible would then run locally on each host to perform 
these configuration changes, while Vagrant will be executed from the 
hypervisor itself. In order to do this, you could add the following to 
your Vagrantfile to tell Vagrant to provision an Ansible playbook:

```c
config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.become = true
end
```

It
 is also worth noting some of the differences between Vagrant and 
Ansible, if you are looking to only stick to a single IaC solution:

| **Feature/Aspect** | **Vagrant** | **Ansible** |
| --- | --- | --- |
| **Configuration Language** | Ruby (for Vagrantfiles). | YAML (for Playbooks). |
| **Integration with Other Tools** | Often used with provisioning tools like Chef, Puppet, or Ansible. | Can be used standalone or integrated with other CI/CD tools. |
| **Complexity** | Relatively straightforward for setting up development environments. | Higher complexity for larger infrastructures and advanced configurations. |
| **Scalability** | More suited for smaller-scale, individual development environments. | Highly scalable, suitable for managing complex, multi-tier applications. |
| **Execution Model** | Procedural style with sequential execution steps. | Declarative model, describing the desired state of the system. |

Building an On-Prem IaC Workflow

# Creating an IaC Pipeline

Now that we have learned the basics about on-prem IaC, it is time to 
put our knowledge to the test! Start the machine attached to this task 
by pressing the green **Start Machine** button. The machine will start in split-view. In case it's not showing up, you can press the blue **Show Split View** button at the top-right of the page.

Once the machine has started, you can navigate to the `/home/ubuntu/iac/` directory. All of the scripts that we will be using today can be found in this directory.

# Vagrantfile

Let's start by taking a look at the Vagrantfile:

Vagrantfile

```python
Vagrant.configure("2") do |config|
  # DB server will be the backend for our website
  config.vm.define "dbserver"  do |cfg|
    # Configure the local network for the server
    cfg.vm.network :private_network, type: "dhcp", docker_network__internal: true
    cfg.vm.network :private_network, ip: "172.20.128.3", netmask: "24"

    # Boot the Docker container and run Ansible
    cfg.vm.provider "docker" do |d|
      d.image = "mysql"
      d.env = {
        "MYSQL_ROOT_PASSWORD" => "mysecretpasswd"
      }
    end
  end

  # Webserver will be used to host our website
  config.vm.define "webserver"  do |cfg|
    # Configure the local network for the server
    cfg.vm.network :private_network, type: "dhcp", docker_network__internal: true
    cfg.vm.network :private_network, ip: "172.20.128.2", netmask: "24"

    # Link the shared folder with the hypervisor to allow data passthrough.
    cfg.vm.synced_folder "./provision", "/tmp/provision"

    # Boot the Docker container and run Ansible
    cfg.vm.provider "docker" do |d|
      d.image = "ansible2"

      d.has_ssh = true

      # Command will keep the container active
      d.cmd = ["/usr/sbin/sshd", "-D"]
    end

    #We will connect usingSSH so override the defaults here
    cfg.ssh.username = 'root'
    cfg.ssh.private_key_path = "/home/ubuntu/iac/keys/id_rsa"

    #Provision this machine using Ansible
    cfg.vm.provision "shell", inline: "ansible-playbook /tmp/provision/web-playbook.yml"
  end
end
```

In this Vagrantfile, we can see that two machines will be provisioned.

**DB Server**

The first machine that will be provisioned is the `dbserver`. Working through the lines of code, we can see that the machine will be added to a local network and receive the IP of `172.20.128.3`. We can also see that the provision directory will be mounted as a share. Lastly, using Docker as the provider, the `mysql` image will be booted and the mysql password will be configured to be `mysecretpasswd`.

**Web Server**

The second machine that will be provisioned is the `webserver`. Similar to the `dbserver`
 machine, it will be connected to the network and use Docker as its 
provider. However, there are some slight differences.

Firstly, the webserver will expose SSH. Since we are using Docker, we 
have to alter some of the default Vagrant configurations to allow 
Vagrant to connect via SSH. This includes changing the username and the 
private key that will be used for the connection.

Secondly, we can see that an Ansible playbook will be executed on the 
container by looking at the following line:

```c
cfg.vm.provision "shell", inline: "ansible-playbook /vagrant/provision/web-playbook.yml"
```

Let's take a look and see what this Ansible playbook will do.

# Ansible Playbook

Let's start by reviewing the `web-playbook.yml` file:

```c
- hosts: localhost
  connection: all
  roles:
    - webapp
```

This is a simple Ansible script that indicates that the webapp role will be provisioned on the host.

To better understand what the webapp role will entail, we can start by reviewing the `~/iac/provision/roles/webapp/tasks/main.yaml` file:

```c
- include_tasks: "db-setup.yml"
- include_tasks: "app-setup.yml"
```

This shows us that there will be two main portions to the Ansible 
provisioning. At this point, it is worth taking a look as well at the 
default values in the `~/iac/provision/roles/webapp/defaults/main.yml` file:

```c
db_name: BucketList
db_user: root
db_password: mysecretpasswd
db_host: 172.20.128.3

api_key: superapikey
```

We will get back to these variables in a bit, but keep them in mind.

**DB Setup**

Let's take a look at the `db-setup.yml` file:

```c
- name: Create temp folder forSQL scripts
  ansible.builtin.file:
    path: /tmp/sql state: directory

- name: Time delay to allowSQL server to boot
    shell: sleep 10

- name: Copy DB creation script with injected variables
    template:
      src: templates/createdb.sql
      dest: /tmp/sql/createdb.sql

- name: Copy DB SP script with injected variables
    template:
      src: templates/createsp.sql
      dest: /tmp/sql/createsp.sql

- name: Create DB
    shell: mysql -u {{ db_user }} -p{{ db_password }} -h {{ db_host }} < /tmp/sql/createdb.sql

- name: Create Stored Procedures
    shell: mysql -u {{ db_user }} -p{{ db_password }} -h {{ db_host }} < /tmp/sql/createsp.sql

- name: Cleanup Scripts
    shell: rm -r /tmp/sql
```

From
 the script, we can see that 7 tasks will be performed. Reading through 
these tasks, we can see that a temporary folder will be created where SQL scripts will be pushed to and then executed against the database host.

Let's take a look at how Ansible would inject those variables from before. Take a look at the `Create DB` task's shell command:

```
shell: mysql -u {{ db_user }} -p{{ db_password }} -h {{ db_host }} < /tmp/sql/createdb.sql
```

As you can see, the three variables of `db_user`, `db_password`, and `db_host` will be injected using either the values for the default file, or the overwritten values, if they exist.

Ansible allows us to take this a step further. Let's take a look at the actual `createdb.sql` file:

```sql
drop DATABASE IF EXISTS {{ db_name }};

CREATE DATABASE {{ db_name }};
USE {{ db_name }};

drop TABLE IF EXISTS 'tbl_user';

CREATE TABLE {{ db_name }}.tbl_user (
  'user_id' BIGINT AUTO_INCREMENT,
  'user_name' VARCHAR(45) NULL,
  'user_username' VARCHAR(45) NULL,
  'user_password' VARCHAR(162) NULL,
  PRIMARY KEY ('user_id'));
```

As
 we can see, these variables are even injected into the file templates 
that will be used. This allows us to control the variables that will be 
used from a single, centralised location. When we change the user or 
password that will be used to connect to the database, we can change 
this in a single location, and it will propagate throughout all 
provisioning steps for the role.

**Web Setup**

Lastly, let's take a look at the `app-setup.yml` file:

```c
- name: Copy web application files
  shell: cp -r /vagrant/provision/roles/webapp/templates/app /

- name: Copy Flask app script with injected variables
  template:
    src: templates/app.py
    dest: /app/app.py
```

This
 file only has two tasks. The first copies the artefacts required for 
the web application and the second copies the web application file as a 
template. A template copy is performed to ensure that the variables, 
such as the database connection string, are injected into the script as 
well.

We will not do a deep dive into the rest of the files that will be 
used for provisioning, however, it is recommended that you take a look 
at these files to gain a better understanding on what exactly we are 
provisioning.

# Running the IaC Pipeline

Now that we have an understanding of our pipeline, it is time to start it! Let's start our pipeline and the provisioning using `vagrant up` from the `iac` directory. The pipeline will take a while to boot, but pay attention to what is happening.

**Note:
 While you may see some red on the terminal when the Ansible 
provisioning step is running, as long as these lines only indicate 
warnings and not an error, the provisioning will complete as expected.**

Once our pipeline has provisioned the machines, we can verify that they are running using the `docker ps` command:

Terminal

```
ubuntu@tryhackme:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                    NAMES
04fc30613dd6   mysql     "docker-entrypoint.s…"   18 minutes ago   Up 18 minutes   3306/tcp, 33060/tcp      iac_dbserver_1706019401
5529f04a2509   ansible   "/usr/sbin/sshd -D"      18 minutes ago   Up 18 minutes   127.0.0.1:2222->22/tcp   iac_webserver_1706019400
```

If this is running, we can start our web application using the following command:

`vagrant docker-exec -it webserver -- python3 /app/app.py`

Once loaded, you can navigate to the web application using the target machines's browser ([http://172.20.128.2/](http://172.20.128.2/)):

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/39e697edab7cba60952ccdb28ece98c9.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/39e697edab7cba60952ccdb28ece98c9.png)

Congratulations! You have executed your very first IaC pipeline!

Security Concerns in On-Prem IaC

When using IaC, 
regardless of whether the deployment is on-prem or cloud-based, there 
are several things to consider for security. If you are looking for 
security best practices, cheat sheets such as [these from OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Infrastructure_as_Code_Security_Cheat_Sheet.html) are a good place to start. Even frameworks such as [NIST](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-204C.pdf) provide information on how to secure IaC.

However, in this room, we will focus more on the practical security 
of IaC and common mistakes that are seen in the real world. This is not a
 comprehensive list of things to take into consideration, but it is a 
great start either protecting your IaC pipeline against real-world 
attacks or what to look for if you are attacking an IaC pipeline on a 
red team engagement. In total, there are four main elements to consider.

# Dependencies

![https://tryhackme-images.s3.amazonaws.com/room-icons/317702e9ed406144f96699d72b09ef9c.png](https://tryhackme-images.s3.amazonaws.com/room-icons/317702e9ed406144f96699d72b09ef9c.png)

The first element of IaC pipelines where security has to be 
considered is the dependencies. Similar to a software pipeline, our IaC 
pipeline will have dependencies. In IaC pipelines, the biggest 
dependencies are the base images that are pulled and used to build the 
infrastructure. If these dependencies have any security issues, these 
issues will propagate through the pipeline.

A common example would be a vulnerability in the OS
 version of the image. If the image itself is not updated, the deployed 
hosts would have this vulnerability. As such, it is important to ensure 
adequate dependency management for resources used in the IaC pipeline. 
Anytime you are making use of third-party software or systems, it can 
introduce a dependency risk. For more information on dependency 
management and the potential vulnerabilities, have a look at the [Dependency Management](https://tryhackme.com/room/dependencymanagement) room.

# Defaults

A common security flaw in IaC pipelines is not altering defaults. 
When hosts and services are initially provisioned through an IaC 
pipeline, it is extremely common for these systems to be provisioned 
using default credentials or connection strings. Ultimately, this is 
intended as these default credentials are used by the tools in the 
pipeline to provision the hosts. The security misconfiguration is 
therefore not the default credentials, but not removing or altering them
 as the final step in the IaC deployment.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/b2355b480888d1f06134521274217192.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/b2355b480888d1f06134521274217192.png)

An example of default credentials is the credentials used by Vagrant 
to provision Windows hosts. Windows images provisioned by Vagrant often 
have a built-in default account of `vagrant` that has the password of `vagrant`.
 This is to allow the Vagrant script running on the hypervisor to 
connect to the host for file transfer and script execution. If, at the 
end of the deployment, this default user is not removed, a threat actor 
could use this to connect to and take full control of all hosts deployed
 through the IaC pipeline.

Another issue with defaults is in
 the services deployed on the hosts. Let's say, for instance, that our 
IaC pipeline is used to deploy a CI/CD pipeline and would therefore 
install the Jenkins
 role on one of the hosts. It would be common for this role to be 
installed with the default credentials of Jenkins, which would be `jenkins:jenkins`.
 In this case, we cannot really alter these credentials in the last 
stages of the IaC deployment but expect the software engineers that will
 use the CI/CD infrastructure to alter the credentials. In some cases, 
this is not performed, which then leads to insecure infrastructure in 
the deployment. In other cases, even if the software would require the 
user to change their password with the first logon event, as the 
software is never used, the default credential remains, allowing a 
threat actor to compromise the service and potentially its underlying 
infrastructure.

As such, when building an IaC pipeline, it is important to make note 
of cases where defaults are used and where they may be a risk if not 
altered. The alteration of these defaults should then either be embedded
 as the final steps in the IaC pipeline or, where required, be performed
 manually once the deployment is complete.

# Insufficient Hardening

![https://tryhackme-images.s3.amazonaws.com/room-icons/c37f3bd6e21e89c0a8de1607bf56fbab.svg](https://tryhackme-images.s3.amazonaws.com/room-icons/c37f3bd6e21e89c0a8de1607bf56fbab.svg)

The third element that commonly goes wrong in IaC pipelines is 
insufficient hardening. The primary goal of IaC is to rapidly deploy 
infrastructure. This often means that the infrastructure that is being 
deployed has not yet been fully hardened. Hardening is not something 
that just happens automatically; it has to be planned for. As such, it 
is important to ensure that hardening steps are either embedded in the 
IaC pipeline or performed manually post-deployment.

A common example of insufficient hardening is the services used by 
the IaC pipeline for deployment. For example, when Vagrant does 
provisioning of a Windows host, it does this via a WinRM connection. It 
just so happens that WinRM is a service commonly used by threat actors 
for lateral movement. As such, it is important that if the service is no
 longer required for normal operation post-deployment, it should be 
disabled. When planning your IaC pipeline, it is important to include 
not only general hardening steps but also those that would close down 
the services used by the pipeline itself.

# Remote Code Execution as a Feature

The last element to consider is to remember that, ultimately, IaC 
pipelines are nothing more than remote code execution as a feature. In 
essence, the pipeline is effectively executing code that allows for new 
infrastructure to be created and integrated into existing networks. 
While this is incredibly powerful in the right hands, it could also be 
extremely detrimental.

![https://tryhackme-images.s3.amazonaws.com/room-icons/23854ddd89de7b9574e1d71b7609ce43.png](https://tryhackme-images.s3.amazonaws.com/room-icons/23854ddd89de7b9574e1d71b7609ce43.png)

Taking this into consideration, it is important to apply security to 
the IaC pipeline to prevent unauthorised access. This can be done 
through two main security efforts, namely secret management and 
following the principle of least privilege.

With secret management, we can ensure that sensitive information, 
such as final credentials or keys, is securely stored and cannot simply 
be read from the IaC source code to compromise the deployment.

Following
 the principle of least privilege ensures that access to the IaC 
pipeline is only provided to users and services that require it. This 
includes implementing the same security controls that should be in any 
pipeline as taught in the [CI/CD and Build Security](https://tryhackme.com/room/cicdandbuildsecurity)
 room. If a threat actor can compromise the pipeline, they would often 
have the ability to also compromise the deployed infrastructure.

These are some of the key security considerations that are required to secure your IaC pipeline against real-world threats.

## CLOUD-BASED IAC

Terraform 101

# Terraform Overview

Terraform
 is an infrastructure as code tool used for provisioning that allows the
 user to define both cloud and on-prem resources in a human-readable 
configuration file that can be versioned, reused and distributed across 
teams. Terraform uses a consistent workflow to make the management of 
your infrastructure an easy and reliable process. Both this 
configuration and the workflow Terraform follows will be covered by 
subsequent tasks in this room. For now, let's define some terms which 
are key to understanding how Terraform provisions and manages 
infrastructure:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/7cdb769ecb4e5b5a0bb23f30d999454a.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/7cdb769ecb4e5b5a0bb23f30d999454a.svg)

# Terraform's Architecture

Now we know what Terraform does. Let's examine how it is done. We will examine Terraform's architecture:

**Terraform Core**:
 As the name suggests, Terraform Core is responsible for the core 
functionalities that allow users to provision and manage their 
infrastructure using Terraform. As mentioned in the [Intro to IaC](https://tryhackme.com/room/introtoiac) room,
 Terraform is a declarative tool (reminder: this means that a desired 
state is defined, and the tool is responsible for ensuring the 
infrastructure meets that desired state, rather than the user declaring 
each step required to achieve the desired state), to ensure the user 
infrastructure is in the desired state, Terraform Core takes its input 
from two sources:

- **Terraform Config files**: The user defines the desired state of their infrastructure in these
config files, in other words, what resources make up their desired
infrastructure.
- **State**: Terraform has a state file that keeps track of the current state of
provisioned infrastructure. The core component checks this state file
against the desired state defined in the config files, and, if there are resources that are defined but not provisioned (or the other way
around), makes a plan of how to take the infrastructure from its current state to the desired state. By default, this state file is called
terraform.tfstate and is stored in the same directory where Terraform
runs.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b25923ed88b91dc85d24605c3b97f03d.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b25923ed88b91dc85d24605c3b97f03d.svg)

**We
 can see in the graphic above that the Terraform Core takes its input 
from two places: the user-defined configuration files and tfstate. 
Should there be any difference between the desired state (configuration 
files) and the current state (tfstate), the required actions will be 
executed using a provider.**

**Providers**:
 The plan mentioned above is executed using different providers 
depending on the resources defined. Providers are used to interact with 
cloud providers, SaaS
 providers and other APIs. For example, if an AWS resource like an EC2 
instance is defined, the AWS provider would be used; if a Kubernetes 
cluster is defined, the Kubernetes provider would be required.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b6fdcfc9fbc25735baba5ad9376f073e.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/b6fdcfc9fbc25735baba5ad9376f073e.svg)

This tool and its architecture boasts many benefits of this IaC tool for DevSecOps
 engineers. What probably sets Terraform apart the most from other IaC 
tools is the ability to use these providers to provision and manage 
resources across multiple cloud providers. This means if you're working 
with an infrastructure that has infrastructure resources with AWS and 
Azure, Terraform can be used as a single solution for multi-cloud 
environments. This also prevents vendor lock-in and means infrastructure
 can be much more flexible. Another benefit of Terraform is the 
declarative configuration language, which is used to define resources in
 config files; it's easy to understand, and the human-readable format 
makes the definition process simple and streamlined. On top of all this,
 the declarative nature of the tool supports versioning and 
change-tracking practices, allowing team members to collaborate during 
the declaration and development of infrastructure and roll back to 
previous infrastructure iterations. The next task will go into further 
detail on how these resources are defined.

Terraform Configuration

**Configuration & Terraform**

Now
 that we know what Terraform is and how it works, let's take a look at 
how we would define the desired state using Terraform config files. 
Terraform config files are written in a declarative language called HCL 
(HashiCorp Configuration Language), which, as discussed, is easy to 
understand and human-readable. The primary purpose of this language is 
to declare resources; these resources represent infrastructure objects. 
The combined definition of these resources makes up the desired 
infrastructure state.

To give you an example of how, as a DevSecOps
 engineer, Terraform configuration files might be used, let us consider 
an example where we want to define a simple VPC (virtual private cloud) 
using the AWS provider. That would look like this:

```bash
provider "aws" {
 region = "eu-west-2"
}

# Create aVPC
resource "aws_vpc" "flynet_vpc" {
 cidr_block = "10.0.0.0/16"
 tags = {
  Name = "flynet-vpc"
 }
}

```

**What does the code do?** After defining our provider (which in this case is AWS),
 this resource block is used to define a VPC. We first define the 
resource by stating the resource type, which in this case is an 
"aws_vpc", and then what we will call this resource. This example is 
"flynet_vpc". Then begins our *resource block,* where
 we define our resource arguments. The arguments given will depend on 
what type of resource is being defined. For example, an aws_vpc will 
need a CIDR block (method for allocating IP addresses). We also define 
tags which can be used in AWS to help with the automation of resources, billing, access control, etc.

**Resource Relationships**

Sometimes,
 resources can depend on other resources. When defining a resource with 
dependencies, the resources it depends on will be referenced. For 
example, if you were assigned a task to define an AWS
 security group ingress rule, allowing SSH access from any source within
 the VPC, you would add the following code block to your configuration 
file.

```bash
resource "aws_security_group" "example_security_group" {
 name = "example-security-group"
 description = "Example Security Group"
 vpc_id = aws_vpc.flynet_vpc.id #Reference to theVPC created above (format: resource_type.resource_name.id)# Ingress rule allowingSSH access from any source within the VPC
 ingress {
  #Since we are allowingSSH traffic , from port and to port should be set to port 22
  from_port = 22
  to_port = 22
  protocol = "tcp"
  cidr_blocks = [aws_vpc.flynet_vpc.cidr_block]
 }
}

```

**What does the code do?** Here, you can see we have a resource block that defines an AWS
 security group (helps secure AWS environments by controlling how 
traffic is allowed into EC2 machines), which allows SSH access from any 
source within the VPC. You can see in the commented lines how this is 
configured and how resources can be referenced from within another 
resource block.

# Infrastructure Modularisation

As a DevSecOps
 engineer, you will likely work with a large, complex infrastructure. 
Another benefit of Terraform is that it allows for the modularisation of
 an infrastructure, that is, for the infrastructure to be broken down 
and defined as modular components rather than in a single place. This is
 common practice in larger organisations as it simplifies the management
 of complex infrastructure configurations. Let's take a look at what the
 above example configuration would look like. Below is a representation 
of a directory `/tfconfig` and the files within it, with a brief comment explaining the purpose of each file:

```bash
tfconfig/
 -flynet_vpc_security.tf #Like mentioned, instead of having all resources defined in one file, resources can be paired up and defined in separate modular files
 -other_module.tf
 -variables.tf #some values will be used across two or many infrastructure modules, so instead of declaring these repeatedly in each .tf file it makes sense to paramaterise them in a file called variables.tf. These variables can then be directly referenced in the .tf file.
 -main.tf #main.tf acts as the central configuration file where the defined modules are all referenced in one place

```

If we consider the example given above, if we were to define a vpc using this structure, it could be configured like so:

variables.tf

```yaml
variable "vpc_cidr_block" {
 description = "CIDR block for the VPC"
 type = string #Set the type of variable (string,number,bool etc)
 default = "10.0.0.0/16" # Can be changed as needed
}
```

We are defining a VPC the same way as we did at the beginning of this task, except now we are storing it in a `variables.tf`
 file. We are doing this so we can reuse/reference it. This could be 
referenced in any module.tf file, for example, below, we have a code 
block for a module named `flynet_vpc_security`:

flynet_vpc_security.tf

```yaml
cidr_block = var.vpc_cidr_block
#Variable can be referenced using var. followed by variable name
```

```
Finally, this module (and all other module tf files) would be collected and referenced in the main.tf file like so:
```

main.tf

```yaml
module "flynet_vpc_security" {
 source = "./flynet_vpc_security.tf"
 #where module is defined (relative to current file)
}

module "other_module" {
 source = "./Other_module.tf"
}
```

This level of organisation would be 
extreme, given how primitive the infrastructure setup is in our example.
 However, this was to show you how an infrastructure at scale might be 
configured in a larger organisation/company.

Terraform Workflow

**Understanding the Terraform Workflow**

The
 Terraform workflow generally follows four steps: Write, Initialise, 
Plan and Apply. To better understand this workflow and how it can 
benefit DevSecOps
 engineers while provisioning of infrastructure, let's consider an 
infrastructure at different points in development. When dealing with 
infrastructure provisioning, you tend to have different problems at 
different stages. To illustrate this, let's consider the Terraform 
workflow at three points in time:

- Day 1 (the infrastructure does not exist yet and needs to be provisioned from scratch)
- Day 2+ (The infrastructure exists, but some changes need to be made)
- Day N (an undefined point in time when you no longer need this infrastructure)

# Day 1

Let's
 take a look at what the Terraform workflow would look like on Day 1 of 
infrastructure provisioning. You have an empty environment with no 
infrastructure set up and need to define and provision this 
infrastructure. Using Terraform, you would follow this workflow:

- **Write:** In this part of the workflow you would define the desired state of your infrastructure in a Terraform configuration file. As discussed in the
previous task, these configuration files are used to define the desired
components, and these components can reference each other if they have a relation.
- **Initialise:** The next part of
the workflow is to initialise. The init command prepares your workspace
(the working directory where your Terraform configuration files are) so Terraform can apply your changes. This preparation includes things like downloading dependencies, for example, if your configuration file
defines 'aws' as the provider, during the initialisation, Terraform will download the aws provider plug-in. This is done using the following
command: `terraform init`
- **Plan:** After initialising your workspace, you should now plan your changes.
The planning stage considers what infrastructure is present currently
(with it being Day 1, there will be no infrastructure present) vs the
desired state and prepares a plan of actions which, if applied, will
make it so the infrastructure matches the desired state. It produces
this execution plan and will tell the user what components will be
added/destroyed in the process. This is done using the following
command: `terraform plan`
- **Apply:** Apply actions the steps (detailed in the plan) required to take the
infrastructure from the current state to the desired state. Terraform
works out which order these infrastructure resources should be created.
In our example from the previous task, we defined two resources: a VPC and a security group. Since the security group references the VPC and
is therefore dependent on it, Terraform would create the VPC first. This is done using the following command: <`terraform apply`

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/8f2325af86bb7978f2106f733caac33b.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/8f2325af86bb7978f2106f733caac33b.svg)

# Day 2+

Day
 2+ means any day after the infrastructure has been provisioned; what 
will the workflow look like when making changes to an existing 
infrastructure? Say, for instance, you wanted to add a component to your
 infrastructure.

- **Initialise**: `terraform init` should be the first command run after making any changes to an
infrastructure configuration. It will initialise the workspace just like when creating the infra from scratch.
- **Plan**: Terraform plan is not required but is best practice, especially in an
already existing infrastructure. The execution plan generated by the
plan command will show you exactly what is being removed or added to the infrastructure. This can catch any misconfigurations before they are
applied and break anything. The plan will assess the existing
infrastructure in this case and note that the existing components match
the desired state, so no changes need to be made, but the additional
component has not been created yet and will need to be created to match
the desired state, so will be listed as a resource that needs to be
added.
- **Apply**: Again, Terraform
will provision the infrastructure changes defined using the execution
plan made during the Plan phase (note that if you skip the planning
phase, Terraform will automatically create an execution plan as if you
had and will ask you to approve the plan before execution). The state
file will then be updated to reflect that the current state now matches
the desired state as the additional component has been
added/provisioned.

# Day N

Day
 N denotes a day in the future when the infrastructure is no longer 
needed. Maybe it was just a test environment, or the application it 
supports has been shelved. Now that this infrastructure is no longer 
needed, all that is required is to destroy it.

- **Destroy**: Running the `terraform destroy` command will take care of this. Functionally, the destroy command is
quite similar to the apply command in that it takes a plan (a destroy
plan which Terraform makes on running this command) and compares it to
what infrastructure currently exists and actions that plan instead of
provisioning/de-provisioning resources changes, it tears down all
resources.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/667e6e2b9cbac61df9d17ac8e0aabae9.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/667e6e2b9cbac61df9d17ac8e0aabae9.svg)

Cloudformation 101

﻿**
﻿
CloudFormation Overview**

CloudFormation is an Amazon Web Services (AWS)
 IaC tool for automated provision and resource management. Instead of 
manually configuring resources through the AWS Management Console or 
using the AWS Command Line Interface (CLI), you can use CloudFormation 
templates to describe your infrastructure in a "declarative" manner.

Declarative Infrastructure as Code

With CloudFormation, you express the desired state of your infrastructure using a JSON
 or YAML template. This template defines the resources, their 
configurations, and the relationships between them. CloudFormation 
provides and manages these resources, making managing and replicating 
your infrastructure easier.

# Templates and Stacks

A
 CloudFormation template is a text file that serves as a blueprint for 
your infrastructure. It contains sections that describe various AWS
 resources like EC2 instances, S3 buckets, and more. When you use a 
template to create resources, it forms a CloudFormation stack. Stacks 
are the fundamental units of CloudFormation, and they represent a 
collection of AWS resources that are created, updated, and deleted 
together.

Example

```bash
# CloudFormation Template
AWSTemplateFormatVersion: '2010-09-09'  # Version of the CloudFormation template syntax

Description: 'A simple CloudFormation template'  # Description of the template

Resources:  # Section whereAWS resources are defined
  MyEC2Instance:  # Logical name of the resource
    Type: 'AWS::EC2::Instance'  # Type ofAWS resource being created

    Properties:  # Properties specific to the resource type
      ImageId: 'ami-12345678'  # ID of the Amazon Machine Image (AMI) for theEC2 instance
      InstanceType: 't2.micro'  # Type ofEC2 instance
      KeyName: 'my-key-pair'  #SSH key pair for accessing the instance

  MyS3Bucket:  # Another resource example
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: 'my-s3-bucket'  # Name of theS3 bucket

Outputs:  # Section to define outputs for the template
  EC2InstanceId:  # Logical name for the output
    Description: 'ID of theEC2 instance'  # Description of the output
    Value: !Ref MyEC2Instance  # Reference to theEC2 instance resource
```

- **AWSTemplateFormatVersion:** This specifies the CloudFormation template version.
- **Description:** Provides a brief description of the template.
- **Resources:** This section defines the AWS resources to be created, such as EC2 instances or S3 buckets. Each resource has a logical name (MyEC2Instance, MyS3Bucket). Type indicates the AWS resource type. Properties hold configuration settings for the resource.
- **Outputs:** This section defines the output values displayed after creating the stack. Logical name, description, and a reference to a resource using `!Ref`.

**Notes:** CloudFormation Designer is a service for visually creating/validating these templates. Read more [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer-overview.html).

# CloudFormation Architecture

Similar
 to Terraform, CloudFormation follows a workflow for provision and 
management. To better understand the workflow, we need to understand the
 inner workings of CloudFormation and its Architecture.

Main and Worker Architecture

CloudFormation employs a main-worker architecture. The main, typically a CloudFormation service running in AWS,
 interprets and processes the CloudFormation template. It manages the 
overall stack creation, update, or deletion orchestration. The worker 
nodes, distributed across AWS regions, are responsible for carrying out 
the actual provisioning of resources.

# Template Processing Flow

![https://tryhackme-images.s3.amazonaws.com/user-uploads/61a7523c029d1c004fac97b3/room-content/10cd2efae7292cd42ba523ba3625c3c8.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/61a7523c029d1c004fac97b3/room-content/10cd2efae7292cd42ba523ba3625c3c8.svg)

- **Template Submission:** users submit a CloudFormation template, written in JSON or YAML, to the CloudFormation service. The template specifies the
desired AWS resources and their configurations. This can be stored in an [S3](https://aws.amazon.com/s3/) bucket, for example.
- **Template Validation:** the CloudFormation service validates the submitted template to ensure its syntax is correct and it follows AWS resource specifications.
- **Processing by the Main Node:** the main node processes the template, creating a set of instructions
for resource provisioning. It determines the order in which resources
should be created based on dependencies.
- **Resource Provisioning:** the main node communicates with worker nodes distributed across different AWS regions. Worker nodes carry out the actual provisioning of resources stated by the instructions provided by the main.
- **Stack Creation/Update:** the resources are created or updated in the specified order, forming a
stack. The stack represents the complete set of provisioned resources.

Event-Driven Model

CloudFormation
 operates on an event-driven model. Events are generated during stack 
creation, update, or deletion processes, and CloudFormation logs these 
events. Users can monitor these events to track the progress of stack 
operations or identify any issues.

Rollback and Rollback Triggers

If an error occurs during the stack creation or update process, CloudFormation can automatically trigger a [rollback](https://docs.aws.amazon.com/autoscaling/ec2/userguide/instance-refresh-rollback.html),
 reverting the stack to its previous state. Rollback triggers can be 
defined in the template to specify conditions under which a rollback 
should occur.

Cross-Stack References

CloudFormation
 supports cross-stack references, allowing resources from one stack to 
refer to resources in another. This is useful for managing complex 
applications and dependencies that span multiple stacks.

Understanding
 the architecture of CloudFormation provides insights into how the 
service efficiently manages the orchestration and provisioning of AWS resources, ensuring a reliable and consistent infrastructure deployment process.

CloudFormation Configuration & Use Cases

# Configuration and Concepts

Template Structure

CloudFormation templates consist of key sections:

- **AWSTemplateFormatVersion:** Specifies the AWS CloudFormation template version.
- **Description:** Describes the template.
- **Parameters:** You can input custom values when creating or updating a stack.
- **Resources:** Defines the AWS resources to be created or managed.
- **Outputs:** Describes the values that can be queried once the stack is created or updated.

Intrinsic Functions

CloudFormation
 templates support "intrinsic functions", which help you perform 
operations. Examples of intrinsic functions are referencing resources, 
performing calculations, and conditionally including resources:

```bash
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-12345678
      InstanceType: t2.micro

Outputs:
  InstanceId:
    Value: !Ref MyInstance

  PublicDnsName:
    Value: !GetAtt MyInstance.PublicDnsName

  SubstitutedString:
    Value: !Sub "Hello, ${MyInstance}"

```

- **Fn::Ref :** References the value of the specified resource.
- **Fn::GetAtt :** Gets the value of an attribute from a resource in the template.
- **Fn::Sub :** Performs string substitution.

Resource Dependencies

Resources in CloudFormation can have dependencies on each other. For example, an EC2
 instance might depend on a VPC being created first. CloudFormation 
automatically handles the order of resource creation and updates based 
on these dependencies.

Change Sets

Before
 making changes to a stack, CloudFormation lets you preview the changes 
using a Change Sets feature. This helps in understanding the impact of 
modifications before they are applied.

# Use Cases

There are many use cases for resource provisioning and management in AWS. Here are some examples:

Infrastructure Provisioning and Management

CloudFormation simplifies the process of creating and managing AWS resources. It ensures consistency and repeatability in infrastructure deployments, reducing the risk of configuration errors.

Application Lifecycle Management

CloudFormation
 is commonly used to manage the entire lifecycle of applications. This 
includes provisioning resources, deploying application code, and 
handling updates or rollbacks.

Multi-Environment Deployments

Deploying
 the same infrastructure across multiple environments (dev, test, 
production) is often necessary. CloudFormation allows you to use the 
same template with different parameter values for each environment.

Resource Scaling

As
 your application or workload grows, CloudFormation enables you to 
quickly scale your infrastructure by modifying the template or using [auto-scaling](https://aws.amazon.com/autoscaling/) capabilities.

CloudFormation provides a robust and scalable way to manage AWS
 resources through code, offering benefits in terms of automation, 
consistency, and collaboration in the cloud infrastructure setup and 
maintenance.

Terraform vs CloudFormation

# Terraform vs. CloudFormation

![https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/46b69b1f213ad744229dd1a273835633.svg](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/46b69b1f213ad744229dd1a273835633.svg)

CloudFormation

- **Vendor Lock-In:** AWS CloudFormation is tightly integrated with AWS services, making it the natural choice for AWS-centric environments.
- **Native Integration:** Seamlessly integrates with other AWS services, providing direct resource references and a unified management experience.
- **Service Coverage:** Provides comprehensive coverage of AWS services, often including support for new services shortly after release.
- **Learning Curve:** Learning CloudFormation may be easier for those familiar with AWS services.

Terraform

- **Cloud-Agnostic:** Terraform is cloud-agnostic, supporting multiple cloud providers, including AWS, Azure, Google Cloud, and more. This makes it a versatile choice for hybrid or multi-cloud deployments.
- **Community and Modules:** This has a large and active community, and using modules allows for reusable and shareable code.
- **State Management:** Terraform uses a state file to track the current state of infrastructure, providing a clear view of the deployed resources.
- **Language Flexibility:** The HashiCorp Configuration Language (HCL) used by Terraform is designed for readability and is more flexible than JSON or YAML.

# Use Cases

Terraform Use Cases

**1. Multi-Cloud Environments**

***Scenario*:** A company utilises its infrastructure with multiple cloud providers such as AWS, Azure, and GCP.

Reason for Terraform:

- Terraform has providers for various cloud platforms, making it easier to manage multi-cloud environments.
- A single Terraform configuration can span different cloud providers,
allowing consistent infrastructure as code (IaC) across the entire
infrastructure landscape.

**2. Community Modules and Providers:**

***Scenario*:** An organisation heavily relies on community-contributed modules and providers to enhance infrastructure provisioning.

Reason for Terraform:

- Terraform has a vibrant community that contributes reusable modules and providers for a wide range of services and platforms.
- Leveraging community-driven content can significantly speed up the development
process and provide best practices adopted by a broader audience.

AWS CloudFormation Use Cases

**1. Deep AWS Integration**

***Scenario*:**
 An enterprise's infrastructure is predominantly AWS-centric, and the 
team is deeply invested in AWS-specific services and features.

Reason for CloudFormation:

- AWS CloudFormation provides native integration with AWS services, making it well-suited for managing AWS-specific resources.
- Features like CloudFormation StackSets and Change Sets enhance the management of AWS-specific resources and deployments.

**2. Managed Service Integration:**

***Scenario*:** An organisation heavily utilises AWS-managed services, such as AWS Elastic Beanstalk or AWS OpsWorks.

Reason for CloudFormation:

- AWS CloudFormation integrates seamlessly with AWS-managed services,
offering simplified provisioning and management of these services.
- CloudFormation provides specific resource types for many AWS-managed services,
allowing for a higher level of abstraction in the templates.

Secure IaC

**Secure Cloud IaC Best Practices**

For Both CloudFormation and Terraform

- **Version Control:** store IaC code in version control systems like Git to track changes, facilitate collaboration, and maintain a version history.
- **Least Privilege Principle:** always assign the least permissions and scope for credentials and IaC
tools. Only grant the needed permissions for the actions to be
performed.
- **Parameterise Sensitive Data:** Use parameterisation to handle credentials or API keys and avoid hardcoding secrets directly into the IaC code.
- **Secure Credential Management:** leverage the cloud platform's secure credential management solutions or services to securely handle and store sensitive information, e.g., vaults for
secret management.
- **Audit Trails:** enable logging and
monitoring features to maintain an audit trail of changes made through
IaC tools. Use these logs to conduct reviews periodically.
- **Code Reviews:** implement code reviews to ensure IaC code adheres to best security
practices. Collaborative review processes can catch potential security
issues early.

Check out the [Source Code Security](https://tryhackme.com/room/sourcecodesecurity) room to learn more about this area.

For AWS CloudFormation

- **Use IAM Roles:** Assign [Identity and Access Management](https://aws.amazon.com/iam/?gclid=Cj0KCQiAm4WsBhCiARIsAEJIEzXouhhd93RvbhqE9xDx8UN65Y44Gq19qsHQf_D5yk9QkScSLgQwvDgaAtOWEALw_wcB&trk=35b38fd8-ca20-4fe2-b46d-16f845a47e34&sc_channel=ps&ef_id=Cj0KCQiAm4WsBhCiARIsAEJIEzXouhhd93RvbhqE9xDx8UN65Y44Gq19qsHQf_D5yk9QkScSLgQwvDgaAtOWEALw_wcB:G:s&s_kwcid=AL!4422!3!651612449969!e!!g!!amazon%20iam!19836376240!155574317508) (IAM) roles with the minimum required permissions to CloudFormation stacks. Avoid using long-term access keys when possible.
- **Secure Template Storage:** store CloudFormation templates in an encrypted [S3 bucket](https://aws.amazon.com/s3/) and restrict access to only authorised users or roles.
- **Stack Policies:** implement stack policies to control updates to stack resources and enforce specific conditions during updates.

For Terraform

- **Backend State Encryption:** enable backend state encryption to protect sensitive information stored in the Terraform state file.
- **Use Remote Backends:** store the Terraform state remotely using backends like Amazon S3 or Azure Storage. This enhances collaboration and provides better security.
- **Variable Encryption:** consider encrypting sensitive values using tools like HashiCorp Vault
or other secure key management solutions when using variables.
- **Provider Configuration:** Securely configure provider credentials using environment variables, variable files, or other secure methods.
