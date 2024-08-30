---
title: "Walking an application"
date: 2023-05-12
draft: false
summary: "Websecurity can sometimes be fun"
tags: [THM, websecurity]
categories: [TryHackMe]
---

## Walking an application


It is usually preferable to use in-built tools to review web application for security issues manually rather than using automated tools and scripts, since they may miss some vulnerabilities.

Some of the in-built tools that one can use include the following;

- **View Source** - Use your browser to view the human-readable source code of a website.
- **Inspector** - Learn how to inspect page elements and make changes to view usually blocked content.
- **Debugger** - Inspect and control the flow of a page's JavaScript
- **Network** - See all the network requests a page makes.

**View Source** - The page source is the human-readable code returned to our browser/client from the web server each time we make a request.

The returned code is made up of HTML(Hypertext markup language) and CSS(Cascading Style Sheets) and JavaScript,this code tells our browser what content to display, how to show it and adds an element of  interactivity with JavaScript.

**Steps on How to view a page source**

1. While viewing a website, you can right-click on the page, and you'll see an option on the menu that says View Page Source.
2. Most browsers support putting view-source: in front of the URL for example, **view-source:https://www.google.com/**
3. In your browser menu, you'll find an option to view the page source. This
option can sometimes be in sub-menus such as developer tools or more tools.

NB:It is usually not advisable to leave comments on a website as they may give actionable information to website viewers.

In this room, comments are enclosed in <!- - ……..- - >

and links to different pages in HTML are written in anchor tags (HTML elements that start with <a) and the link to be directed to is stored in the ‘href’ attribute.

On viewing the page source you will notice that in the comment there is a path to a new home page “`/new-home-beta`” that will provide you the first flag. Moreover there is a secret page “`/secret-page`” that contains the second flag .

As you continue down the source code analysis you will realize that there is a directory of high interest “`/assets`” , in the directory there is a file called flag.txt, that contains our third flag.Furthermore,at the bottom  of the source code, in the last comment section, the version of the website’s framework is given and a link to the framework’s website “`https://static-labs.tryhackme.cloud/sites/thm-web-framework`”.

After opening the link, in the change-log page different versions are displayed but in version1.3 there is a zipped file “/tmp.zip” which when on opened in the given link “[https://<ip address>.p.thmlabs.com](https://10-10-118-23.p.thmlabs.com/)/tmp.zip” in view source mode, our final flag is displayed.

**Developer tools** 

1. **Inspector -** it assists by providing us with a live representation of what is currently on the website,since the page source doesn’t always represent what is shown on a web page because CSS,java-script and user interaction can change the content and style of the page.

in the ACME IT support website,in the news tab. There is three articles but the third one is hidden fro only premium customers to view by a paywall, but this wall can be removed using the inspector tool. While using firefox browser,right click on the paywall then select inspect to open the inspector tool, locate the ‘DIV’ element with the premium-customer-blocker and click on it. In the inspector tool,the css style for the div class is displayed,on the display section change from block to none and you will be able to see the content of the premium customer and find your flag.

1. **Debugger -** this tool is intended for debugging java script , and again is an excellent tool for web developers wanting to work out why something might not be working, on the other hand for penetration testers,it gives them ability to dig deep into the java-script code.

on the ACME IT Support website,click on the contact page. When the page is refreshed, a red flash is displayed on the page at a fast rate,we need to use the debugger to capture the red flash which is located in the flash,min.js file of the website. we need to go to the file and analyze the code but it is obfuscated. Using the debugger tool we can be able to arrange the code in a proper manner by clicking n the ‘{}’ icon also called “pretty print”. At the bottom of the code there is a line flash[’ remove‘](); , we need to click on it to set a break point in order to capture the red flash on refreshing the page. The flash contains a flag.

1. **Network -**  this tool can be used to keep track of every external request a webpage makes.

**Ajax** is a method for sending and receiving network data in a web application background without interfering by changing the current web page.

In the ACME IT Support website,on the contact page try entering  data into the form and then click on the send message button, the data is submitted. on the  network tool in the developer tools, the message sent is shown and we can be able to see the response we got by clicking on the response tab to find the  flag.
