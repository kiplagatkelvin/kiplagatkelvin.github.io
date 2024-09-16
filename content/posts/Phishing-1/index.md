---
title: "Phishing"
dscription: This is a blog on how emails work and wat it takes for ono to be phished.
date: 2024-01-13
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Sea full of phishes" # Here you can write a small summary of the post if needed
tags: [Phishing]
categories: [Purple Team]
---

# PHISHING


**Email Delivery**

A handful of protocols are involved with the "magic" that takes place when you hit SEND in an email client.

By now, you should already know that certain protocols were created to handle specific network-related tasks, such as email.

There are 3 specific protocols involved to facilitate the outgoing and incoming email messages, and they are briefly listed below.

- **SMTP** (**Simple Mail Transfer Protocol)** It is utilized to handle the sending of emails.
- **POP3 (Post Office Protocol)** Is responsible transferring email between a client and a mail server.
- **IMAP (Internet Message Access Protocol)**  ****Is responsible transferring email between a client and a mail server.

You should have noticed that both **POP3** and **IMAP** have the same definition. But there are differences between the two.

The difference between the two is listed below: (credit [AOL](https://help.aol.com/articles/what-is-the-difference-between-pop3-and-imap) -- [*You got mail!*](https://www.youtube.com/watch?v=gFBLiHpkcOk))

**POP3**

- Emails are downloaded and stored on a single device.
- Sent messages are stored on the single device from which the email was sent.
- Emails can only be accessed from the single device the emails were downloaded to.
- If you want to keep messages on the server, make sure the setting "Keep
email on server" is enabled, or all messages are deleted from the server once downloaded to the single device's app or software.

**IMAP**

- Emails are stored on the server and can be downloaded to multiple devices.
- Sent messages are stored on the server.
- Messages can be synced and accessed across multiple devices.

Now let's talk about how email travels from the sender to the recipient.

To best illustrate this, see the oversimplified image below:

![https://assets.tryhackme.com/additional/phishing1/email-network-flow-4.png](https://assets.tryhackme.com/additional/phishing1/email-network-flow-4.png)

Below is an explanation of each numbered point from the above diagram:

1. Alexa composes an email to Billy (`billy@johndoe.com`) in her favorite email client. After she's done, she hits the send button.
2. The **SMTP** server needs to determine where to send Alexa's email. It queries **DNS** for information associated with `johndoe.com`.
3. The **DNS** server obtains the information `johndoe.com` and sends that information to the **SMTP** server.
4. The **SMTP** server sends Alexa's email across the Internet to Billy's mailbox at `johndoe.com`.
5. In this stage, Alexa's email passes through various **SMTP** servers and is finally relayed to the destination **SMTP** server.
6. Alexa's email finally reached the destination **SMTP** server.
7. Alexa's email is forwarded and is now sitting in the local **POP3/IMAP** server waiting for Billy.
8. Billy logs into his email client, which queries the local **POP3/IMAP** server for new emails in his mailbox.
9. Alexa's email is copied (**IMAP**) or downloaded (**POP3**) to Billy's email client.

Lastly, each protocol has its associated default ports and recommended ports. For example, **SMTP** is port 25.

**Email Headers**

Great! We know how an email travels from point A to point B and all the protocols involved in the process.

This task is to understand the components of what makes up an email message when it arrives in an inbox.

This understanding is necessary if you wish to analyze potentially malicious emails manually.

Before we begin, we need to understand that there are two parts to an email:

- the email **header** (information about the email, such as the email servers that relayed the email)
- the email **body** (text and/or HTML formatted text)

The syntax for email messages is known as the [**Internet Message Format**](https://datatracker.ietf.org/doc/html/rfc5322) (**IMF**).

Let's look at email headers first.

What do you look for when analyzing a potentially malicious email?

Let's start with the following email header fields:

1. **From** - the sender's email address
2. **Subject** - the email's subject line
3. **Date** - the date when the email was sent
4. **To** - the recipient's email address

This is usually clearly visible in any email client. Let's look at an example of these fields in the below image.

**Warning**: This is a snippet from an actual email. The email in the below image is from a honeypot Yahoo email address. Don't engage/interact with the email addresses or IP addresses revealed in this room.

![https://assets.tryhackme.com/additional/phishing1/email-headers-1b.png](https://assets.tryhackme.com/additional/phishing1/email-headers-1b.png)

**Note**: The numbers in the above image correspond to the email header fields bullet list above.

Another method to obtain the same email header information, and more, is by viewing the '**raw**' email details.

When looking at an email header in detail, it can be intimidating at first, but it's not so bad if you know what to look for.

**Note**:
 Depending on your email client, whether a web client or a desktop app, 
the steps to view these email header fields will vary, but the concept 
is the same.

Review this Knowledge Base (KB) article from Media Temple on viewing the raw/full email headers in various email clients [here](https://mediatemple.net/community/products/grid/204644060/how-do-i-view-email-headers-for-a-message).

In the below image, you can see how to view this information within Yahoo.

![https://assets.tryhackme.com/additional/phishing1/email-raw-headers-menu-2.png](https://assets.tryhackme.com/additional/phishing1/email-raw-headers-menu-2.png)

Below is a snippet of the raw message for the email sample.

![https://assets.tryhackme.com/additional/phishing1/email-raw-headers-2b.png](https://assets.tryhackme.com/additional/phishing1/email-raw-headers-2b.png)

**Note**: The above image shows some, not all, of the information within an email's header.

You can review this email in the `Email Samples` directory on the Desktop within the attached virtual machine. The email is titled `email1.eml`.

From the above image, there are other email header fields of interest.

1. **X-Originating-IP** The IP address of the email was sent from (this is known as an [**X-header**](https://help.returnpath.com/hc/en-us/articles/220567127-What-are-X-headers-))
2. **Smtp.mailfrom**/**header.from** - The domain the email was sent from (these headers are within **Authentication-Results**)
3. **Reply-To** - This is the email address a reply email will be sent to instead of the **From** email address

To clarify, in the email in the sample above, the **Sender** is newsletters@ant.anki-tech.com, but if a recipient replies to the email, the response will go to reply@ant.anki-tech.com, which is the **Reply-To**, and **NOT** to newsletters@ant.anki-tech.com.

Below is an additional resource from Media Temple on how to analyze email headers:

- [https://mediatemple.net/community/products/all/204643950/understanding-an-email-header](https://mediatemple.net/community/products/all/204643950/understanding-an-email-header)

**Email Body**

The email body is the part of the email which contains the text (plain or HTML formatted) the sender wants you to view.

Below is an example of a text-only email.

![https://assets.tryhackme.com/additional/phishing1/email-text-2.png](https://assets.tryhackme.com/additional/phishing1/email-text-2.png)

Below is an example of the HTML formatted email.

![https://assets.tryhackme.com/additional/phishing1/email-html-2.png](https://assets.tryhackme.com/additional/phishing1/email-html-2.png)

The above email contains an image (which was blocked by the email client) and embedded hyperlinks.

HTML is what makes it possible to add these elements to an email.

To view an email's HTML code is the same approach shown below, but it may vary depending on the webmail client.

In the example below, the screenshot is from [Protonmail](https://protonmail.com/).

![https://assets.tryhackme.com/additional/phishing1/email-source-code-2.png](https://assets.tryhackme.com/additional/phishing1/email-source-code-2.png)

A snippet of the HTML code is shown below.

![https://assets.tryhackme.com/additional/phishing1/email-html-code.png](https://assets.tryhackme.com/additional/phishing1/email-html-code.png)

In this specific email web client, Protonmail, the option to switch back to HTML is called "**View rendered HTML**".

![https://assets.tryhackme.com/additional/phishing1/email-render-html.png](https://assets.tryhackme.com/additional/phishing1/email-render-html.png)

Again, it will be different for other webmail clients.

Lastly, emails may contain attachments. The same premise applies; you can view an email's attachment from an email's HTML format or by viewing the source code.

Let's look at a few examples below.

The following example is an HTML formatted email from "Netflix" with an attachment. The web client is Yahoo!

![https://assets.tryhackme.com/additional/phishing1/email-with-attachment.png](https://assets.tryhackme.com/additional/phishing1/email-with-attachment.png)

1. The email body has an image.
2. The email attachment is a PDF document.

Now let's view this attachment within the source code.

![https://assets.tryhackme.com/additional/phishing1/email-with-attachment-2.png](https://assets.tryhackme.com/additional/phishing1/email-with-attachment-2.png)

From the above example, we can see the headers associated with this attachment:

- **Content-Type** is **application/pdf**.
- **Content-Disposition** specifies it's an **attachment**.
- **Content-Transfer-Encoding** tells us it's **base64** encoded.

With the base64 encoded data, you can decode it and save it to your machine.

Warning:
 When interacting with attachments, proceed with caution and make sure 
you don't double-click an email's attachment by accident.

**Note**:
 Headers specific to 'content' can be found in various locations within 
an email message source code, and they're not only associated with 
attachments. For example, **Content-Type** can be **text/html,** and **Content-Transfer-Encoding** can have other values, such as **8bit**.

**Types of Phishing**

Now that we covered the
 general concepts regarding emails and how they travel from sender to 
recipient, we can now talk about how this method of communication is 
used for nefarious purposes.

Different types of malicious emails can be classified as one of the following:

- [**Spam**](https://www.proofpoint.com/us/threat-reference/spam) - unsolicited junk emails sent out in bulk to a large number of recipients. The more malicious variant of Spam is known as **MalSpam**.
- [**Phishing](https://www.proofpoint.com/us/threat-reference/phishing)**  ****emails sent to a target(s) purporting to be from a trusted entity to lure individuals into providing sensitive information.
- [**Spear phishing](https://www.proofpoint.com/us/threat-reference/spear-phishing) -** takes phishing a step further by targeting a specific individual(s) or organization seeking sensitive information. ****
- [**Whaling](https://www.rapid7.com/fundamentals/whaling-phishing-attacks/)**  is similar to spear phishing, but it's targeted specifically to C-Level high-position individuals (CEO, CFO, etc.), and the objective is the
same.
- [**Smishing**](https://www.proofpoint.com/us/threat-reference/smishing) - takes phishing to mobile devices by targeting mobile users with specially crafted text messages.
- [**Vishing**](https://www.proofpoint.com/us/threat-reference/vishing) - is similar to smishing, but instead of using text messages for the
social engineering attack, the attacks are based on voice calls.

When it comes to phishing, the modus operandi is usually the same depending on the objective of the email.

For example, the objective can be to harvest credentials, and another is to gain access to the computer.

Below are typical characteristics phishing emails have in common:

- The **sender email name/address** will masquerade as a trusted entity ([**email spoofing**](https://www.proofpoint.com/us/threat-reference/email-spoofing))
- The email subject line and/or body (text) is written with a **sense of urgency** or uses certain keywords such as **Invoice**, **Suspended**, etc.
- The email body (HTML) is designed to match a trusting entity (such as Amazon)
- The email body (HTML) is poorly formatted or written (contrary from the previous point)
- The email body uses generic content, such as Dear Sir/Madam.
- **Hyperlinks** (oftentimes uses URL shortening services to hide its true origin)
- A [malicious attachment](https://www.proofpoint.com/us/threat-reference/malicious-email-attachments) posing as a legitimate document

**PHISHING IN ACTION**

**Cancel your PayPal order**

The email sample in this task will highlight the following techniques:

- **Spoofed email address**
- **URL shortening services**
- **HTML to impersonate a legitimate brand**

Here are some quick observations about this email sample:

1. This is an unusual email recipient address. This is not the email address associated with the Yahoo account.
2. This mismatch should immediately stand out. The sender's details
(service@paypal.com) don't match the sender's email address
(gibberish@sultanbogor.com).
3. The subject line hints that you made a purchase or a transaction of some
sort. If you don't recall this account, then it will grab your
attention. This social engineering tactic is to prompt you to interact
with the email with haste.

![https://assets.tryhackme.com/additional/phishing2.0/email1-details.png](https://assets.tryhackme.com/additional/phishing2.0/email1-details.png)

Now let's look at the contents of the email body.

**Email Body Text (Image 1)**:

![https://assets.tryhackme.com/additional/phishing2.0/email-body-1.png](https://assets.tryhackme.com/additional/phishing2.0/email-body-1.png)

**The second half of the same email body text (Image 2)**:

![https://assets.tryhackme.com/additional/phishing2.0/email-body-2b.png](https://assets.tryhackme.com/additional/phishing2.0/email-body-2b.png)

The email body compliments the sender information and subject line. The email was designed as a legitimate email from PayPal.

There aren't any attachments associated with this email. The only interactive element in this email is the **Cancel the order** button/link.

Let's investigate that further by reviewing the raw HTML source for the email...

**Email Hyperlinks**:

![https://assets.tryhackme.com/additional/phishing2.0/cancel-order.png](https://assets.tryhackme.com/additional/phishing2.0/cancel-order.png)

The
 link uses URL shortening services. It is not a good idea to click on 
the link if you don't know where the link is taking you.

Luckily, there are online tools that we can use to let us know the destination of a shortened URL.

![https://assets.tryhackme.com/additional/phishing2.0/email1-url-shortener.png](https://assets.tryhackme.com/additional/phishing2.0/email1-url-shortener.png)

Strange. This link redirects to google.com.

**Note**: Tools to expand shortened URLs will be discussed in the Phishing Emails 3 room.

**Track your package**

This email sample will highlight the following techniques:

1. **Spoofed email address**
2. **Pixel tracking**
3. Link manipulation

Here are some quick observations about this email sample:

1. The email is tailored to appear that it's sent from a mail distribution center of some sort.
2. The subject line adds to the pretense with a 'tracking number.'
3. The link in the email body matches the subject line.

![https://assets.tryhackme.com/additional/phishing2.0/email2-details.png](https://assets.tryhackme.com/additional/phishing2.0/email2-details.png)

**Note**: In this email sample, Yahoo blocked the images from automatically loading. Any guesses as to why?

Typically
 one can hover the cursor over a link to see where the link is pointing 
to, but in this sample, that technique won't work because Yahoo disabled
 links in the email.  We can look at the raw source code for the email and find out.

**Email Hyperlinks**:

![https://assets.tryhackme.com/additional/phishing2.0/email2-hyperlinks.png](https://assets.tryhackme.com/additional/phishing2.0/email2-hyperlinks.png)

Here we see an image file, and it's explicitly called **Tracking.png**. These trackers send information back to the spammer's server.

There are many reasons for spammers to embed tracking pixels (very small images) into their spam emails. To read more about this concept, refer to this post on The Verge [here](https://www.theverge.com/22288190/email-pixel-trackers-how-to-stop-images-automatic-download).

Now we can understand why Yahoo automatically blocked the images in this email. Many email providers do the same.

Back
 to the hyperlink, the link is pointing to a shady-looking domain. The 
only distribution center this domain can be associated with is malware, 
but further analysis is the only way to confirm that definitely.

**Select your email provider to view document**

This email sample will highlight the following techniques:

- Urgency
- HTML to impersonate a legitimate brand
- Link manipulation
- Credential harvesting
- Poor grammar and/or typos

Let's take a closer look...

![https://assets.tryhackme.com/additional/phishing2.0/email6-details2.png](https://assets.tryhackme.com/additional/phishing2.0/email6-details2.png)

Here are some quick observations about this email sample:

1. The email was sent on Thursday, July 15th, 2021.
2. A sense of urgency is introduced in this email. Notice that the link to download the fax document expires on the same day.
3. There is an action to perform. In this case, a button to download the fax.

![https://assets.tryhackme.com/additional/phishing2.0/email6-phish1b.png](https://assets.tryhackme.com/additional/phishing2.0/email6-phish1b.png)

The
 above image shows the victim is redirected to a page created to pass as
 OneDrive. Notice that the URL is not anything Microsoft-related.

There
 are two more links for the victim to interact with. The victim has to 
click either button to obtain the fax document that is set to expire.

![https://assets.tryhackme.com/additional/phishing2.0/email6-phish2b.png](https://assets.tryhackme.com/additional/phishing2.0/email6-phish2b.png)

The
 victim is directed to yet another site. This one was crafted to 
resemble Adobe. Again, notice the URL. It doesn't look like it's related
 to Adobe.

Also, notice the page title in the tab. It's called "Share Point Online", which is a Microsoft product.  There are a couple of grammatical errors as well.

The victim has options to sign in with the email provider of their choice.

![https://assets.tryhackme.com/additional/phishing2.0/email6-phish3.png](https://assets.tryhackme.com/additional/phishing2.0/email6-phish3.png)

Our victim chose to log in with Outlook because, per the instructions, "*To read the document, please enter with the valid email credentials that this file was sent to.*"; the email was viewed in Outlook.

![https://assets.tryhackme.com/additional/phishing2.0/email6-phish4.png](https://assets.tryhackme.com/additional/phishing2.0/email6-phish4.png)

In
 this sample, we can tell that fake credentials were entered, but even 
if the victim would have entered valid credentials, the error message 
would be the same. This scenario happens 
because the victim is not really authenticating to an email provider. 
Instead, the credentials that were entered now reside on the criminal's 
server. The criminal's objective to harvest credentials has been met.

Lastly, notice more grammatical errors. All this work they put into this, you would think they would run a spell check.

This
 email sample was obtained from Any Run. If you wish to interact with 
the email and see the full analysis, refer to the link below.

- Analysis: [https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#](https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#)

**Please update your payment details**

This email sample will highlight the following techniques:

- Spoofed email address
- Urgency
- HTML to impersonate a legitimate brand
- Poor grammar and/or typos
- **Attachments**

Here are some quick observations about this email sample:

1. This email is made to appear that it's from Netflix Billing, but the sender address is z99@musacombi.online.
2. Here is the element of urgency. The account was suspended, so the victim must act quickly.
3. There is more of this sense of urgency in the email body.

![https://assets.tryhackme.com/additional/phishing2.0/email3-details.png](https://assets.tryhackme.com/additional/phishing2.0/email3-details.png)

Also, notice the different misspellings of the word Netflix. Not sure what was the purpose of that.

Typically, you'll see this technique when it comes to [typosquatting](https://www.csoonline.com/article/3600594/what-is-typosquatting-a-simple-but-effective-attack-technique.html), but that wasn't the case here.

![https://assets.tryhackme.com/additional/phishing2.0/email3-typos.png](https://assets.tryhackme.com/additional/phishing2.0/email3-typos.png)

Ok,
 here is the meat and potatoes of this email. Apparently, the victim 
needs to open the attachment (PDF) to update their Netflix account.

![https://assets.tryhackme.com/additional/phishing2.0/email3-body-attachment.png](https://assets.tryhackme.com/additional/phishing2.0/email3-body-attachment.png)

Notice the phone number for 'Netflix'. At first glance, that is an unusual phone number to send to a US-based victim.

![https://assets.tryhackme.com/additional/phishing2.0/email3-attachment2.png](https://assets.tryhackme.com/additional/phishing2.0/email3-attachment2.png)

The attachment contains an embedded link titled 'Update Payment Account'.

**Your recent purchase**

This email sample will highlight the following techniques:

- Spoofed email address
- Recipient is BCCed
- Urgency
- Poor grammar and/or typos
- Attachments

Here are some quick observations about this email sample:

1. This email is made to appear that it's from Apple Support, but the sender's address is gibberish@sumpremed.com.
2. This email wasn't sent directly to the victim's inbox but rather BCCed ([Blind Carbon Copy](https://www.technology.pitt.edu/help-desk/how-to-documents/using-blind-carbon-copy-bcc-feature-protect-privacy-email-addresses)). The recipient email looks like another spoofed email to appear as a legitimate Apple email address.
3. Here is the element of urgency. Action is required on behalf of the victim.

![https://assets.tryhackme.com/additional/phishing2.0/email5-details2.png](https://assets.tryhackme.com/additional/phishing2.0/email5-details2.png)

There are a few noticeable typos in both the sender and recipient email addresses: **donoreply** and **payament**.

This particular email doesn't necessarily have an email body. It's totally blank. The email simply contains an attachment.

![https://assets.tryhackme.com/additional/phishing2.0/email5-attachment.png](https://assets.tryhackme.com/additional/phishing2.0/email5-attachment.png)

This file extension you may not be familiar to you. A .[DOT](https://www.reviversoft.com/en/file-extensions/dot) file is page layout template files associated with Microsoft Word.

![https://assets.tryhackme.com/additional/phishing2.0/email5-attachment2.png](https://assets.tryhackme.com/additional/phishing2.0/email5-attachment2.png)

The
 above image shows what is contained within the attachment. You can see 
that the file contains a large image to resemble an App Store receipt.

Notice the link contains certain keywords related to Apple: **apps** and **ios**.

**DHL Express Courier Shipping notice**

This email sample will highlight the following techniques:

- Spoofed email address
- HTML to impersonate a legitimate brand
- Attachments

Here are some quick observations about this email sample:

1. The sender's email doesn't match the company that is being impersonated, which in this case is DHL.
2. The subject line gives the impression that there is a package DHL will ship for you.
3. The HTML in the email body was designed to look like it was sent from DHL.

![https://assets.tryhackme.com/additional/phishing2.0/email4-details.png](https://assets.tryhackme.com/additional/phishing2.0/email4-details.png)

Looking at the source code for the email, the link to view the email as a web page doesn't contain an actual destination URL.

![https://assets.tryhackme.com/additional/phishing2.0/email4-body-1.png](https://assets.tryhackme.com/additional/phishing2.0/email4-body-1.png)

...

![https://assets.tryhackme.com/additional/phishing2.0/email4-body-2.png](https://assets.tryhackme.com/additional/phishing2.0/email4-body-2.png)

The only element the victim can interact with in this email is the email attachment, which, in this case is an Excel document.

![https://assets.tryhackme.com/additional/phishing2.0/email4-attachment.png](https://assets.tryhackme.com/additional/phishing2.0/email4-attachment.png)

The image below shows what is contained within the attachment.

![https://assets.tryhackme.com/additional/phishing2.0/email4-attachment2.png](https://assets.tryhackme.com/additional/phishing2.0/email4-attachment2.png)

The attachment runs a payload that throws an error.

![https://assets.tryhackme.com/additional/phishing2.0/email4-attachment3.png](https://assets.tryhackme.com/additional/phishing2.0/email4-attachment3.png)

**Phishing Analysis Tools**

**Email header analysis**

Some of the pertinent 
information that we need to collect can be obtained visually from an 
email client or web client (such as Gmail, Yahoo!, etc.). But some information, such as the sender's IP address and reply-to information, can only be obtained via the email header.

In [Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe), we saw how to obtain this information manually by sifting through an email's source code.

Below we'll look at some tools that will help us retrieve this information.

First up to bat is a tool from Google that can assist us with analyzing email headers called **Messageheader** from the Google Admin Toolbox.

Per the [site](https://toolbox.googleapps.com/apps/main/), "*Messageheader
 analyzes SMTP message headers, which help identify the root cause of 
delivery delays. You can detect misconfigured servers and mail-routing 
problems*".

**Usage**: Copy and paste the entire email header and run the analysis tool.

- **Messageheader**: [https://toolbox.googleapps.com/apps/messageheader/analyzeheader](https://toolbox.googleapps.com/apps/messageheader/analyzeheader)

![https://assets.tryhackme.com/additional/phishing2/messageheader.png](https://assets.tryhackme.com/additional/phishing2/messageheader.png)

Another tool is called **Message Header Analyzer**.

- **Message Header Analyzer**: [https://mha.azurewebsites.net/](https://mha.azurewebsites.net/)

![https://assets.tryhackme.com/additional/phishing2/mha.png](https://assets.tryhackme.com/additional/phishing2/mha.png)

Lastly, you can also use [mailheader.org](https://mailheader.org/).

![https://assets.tryhackme.com/additional/phishing2/mailheader.png](https://assets.tryhackme.com/additional/phishing2/mailheader.png)

Even
 though not covered in the previous Phishing rooms, a Message Transfer 
Agent (MTA) is software that transfers emails between sender and 
recipient. Read more about MTAs [here](https://csrc.nist.gov/glossary/term/mail_transfer_agent). Since we're on the subject, read about MUAs (Mail User Agent) [here](https://csrc.nist.gov/glossary/term/mail_user_agent).

**Note**:
 The option on which tool to use rests ultimately on you. It is good to 
have multiple resources to refer to as each tool might reveal 
information that another tool may not reveal.

The tools below can help you analyze information about the sender's IP address:

- IPinfo.io: [https://ipinfo.io/](https://ipinfo.io/)

Per the [site](https://ipinfo.io/), "*With
 IPinfo, you can pinpoint your users’ locations, customize their 
experiences, prevent fraud, ensure compliance, and so much more*".

![https://assets.tryhackme.com/additional/phishing2/ipinfo.png](https://assets.tryhackme.com/additional/phishing2/ipinfo.png)

- URLScan.io: [https://urlscan.io/](https://urlscan.io/)

Per the [site](https://urlscan.io/about/), "*urlscan.io
 is a free service to scan and analyse websites. When a URL is submitted
 to urlscan.io, an automated process will browse to the URL like a 
regular user and record the activity that this page navigation creates. 
This includes the domains and IPs contacted, the resources (JavaScript, 
CSS, etc) requested from those domains, as well as additional 
information about the page itself. urlscan.io will take a screenshot of 
the page, record the DOM content, JavaScript global variables, cookies 
created by the page, and a myriad of other observations. If the site is 
targeting the users one of the more than 400 brands tracked by 
urlscan.io, it will be highlighted as potentially malicious in the scan 
results*".

![https://assets.tryhackme.com/additional/phishing2/urlscan.png](https://assets.tryhackme.com/additional/phishing2/urlscan.png)

Notice
 that urlscan.io provides a screenshot of the URL. This screenshot is 
provided, so you don't have to navigate to the URL in question 
explicitly.

You can use other tools that provide the same functionality and more, such as [URL2PNG](https://www.url2png.com/) and [Wannabrowser](https://www.wannabrowser.net/).

- Talos Reputation Center: [https://talosintelligence.com/reputation](https://talosintelligence.com/reputation)

![https://assets.tryhackme.com/additional/phishing2/talos.png](https://assets.tryhackme.com/additional/phishing2/talos.png)

**Email body analysis**

Now it's time to direct
 your focus to the email body. This is where the malicious payload may 
be delivered to the recipient either as a link or an attachment.

Links can be extracted manually, either directly from an HTML formatted email or by sifting through the raw email header.

Below is an example of obtaining a link manually from an email by right-clicking the link and choosing **Copy Link Location**.

![https://assets.tryhackme.com/additional/phishing2/copy-link.png](https://assets.tryhackme.com/additional/phishing2/copy-link.png)

The same can be accomplished with the assistance of a tool. One tool that can aid us with this task is URL Extractor.

- URL Extractor: [https://www.convertcsv.com/url-extractor.htm](https://www.convertcsv.com/url-extractor.htm)

You can copy and paste the raw header into the text box for **Step 1: Select your input**.

![https://assets.tryhackme.com/additional/phishing2/url-extractor.png](https://assets.tryhackme.com/additional/phishing2/url-extractor.png)

The extracted URLs are visible in **Step 3**.

![https://assets.tryhackme.com/additional/phishing2/url-extractor-2.png](https://assets.tryhackme.com/additional/phishing2/url-extractor-2.png)

You may also use [CyberChef](https://gchq.github.io/CyberChef/) to extract URLs with the Extract URLs recipe.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/a31606afb772b8f87eebf0ff59f00fce.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/a31606afb772b8f87eebf0ff59f00fce.png)

Tip:
 It's important to note the root domain for the extracted URLs. You will
 need to perform an analysis on the root domain as well.

After
 extracting the URLs, the next step is to check the reputation of the 
URLs and root domain. You can use any of the tools mentioned in the 
previous task to aid you with this.

If the email has an 
attachment, you'll need to obtain the attachment safely. Accomplishing 
this is easy in Thunderbird by using the Save button.

![https://assets.tryhackme.com/additional/phishing2/save-attachment.png](https://assets.tryhackme.com/additional/phishing2/save-attachment.png)

After
 you have obtained the attachment, you can then get its hash. You can 
check the file's reputation with the hash to see if it's a known 
malicious document.

Obtain the file's SHA256 hash

```
user@machine$ sha256sum Double\ Jackpot\ Slots\ Las\ Vegas.dotc650f397a9193db6a2e1a273577d8d84c5668d03c06ba99b17e4f6617af4ee83  Double Jackpot Slots Las Vegas.dot
```

There are many tools available to help us with this, but we'll focus on two primarily; they are listed below:

- Talos File Reputation: [https://talosintelligence.com/talos_file_reputation](https://talosintelligence.com/talos_file_reputation)

Per the [site](https://talosintelligence.com/talos_file_reputation), "*The
 Cisco Talos Intelligence Group maintains a reputation disposition on 
billions of files. This reputation system is fed into the AMP, 
FirePower, ClamAV, and Open-Source Snort product lines. The tool below 
allows you to do casual lookups against the Talos File Reputation 
system. This system limits you to one lookup at a time, and is limited 
to only hash matching. This lookup does not reflect the full 
capabilities of the Advanced Malware Protection (AMP) system*".

![https://assets.tryhackme.com/additional/phishing2/talos-file-rep.png](https://assets.tryhackme.com/additional/phishing2/talos-file-rep.png)

![https://assets.tryhackme.com/additional/phishing2/talos-file-rep-2.png](https://assets.tryhackme.com/additional/phishing2/talos-file-rep-2.png)

- VirusTotal: [https://www.virustotal.com/gui/](https://www.virustotal.com/gui/)

Per the [site](https://www.virustotal.com/gui/), "Analyze suspicious files and URLs to detect types of malware, automatically share them with the security community."

![https://assets.tryhackme.com/additional/phishing2/virustotal.png](https://assets.tryhackme.com/additional/phishing2/virustotal.png)

![https://assets.tryhackme.com/additional/phishing2/virustotal-2.png](https://assets.tryhackme.com/additional/phishing2/virustotal-2.png)

Another tool/company worth mentioning is [Reversing Labs](https://www.reversinglabs.com/), which also has a [file reputation service](https://register.reversinglabs.com/file_reputation).

**Malware Sandbox**

Luckily as Defenders, 
we don't need to have malware analysis skills to dissect and reverse 
engineer a malicious attachment to understand the malware better.

There
 are online tools and services where malicious files can be uploaded and
 analyzed to better understand what the malware was programmed to do. These services are known as malware sandboxes.

For
 instance, we can upload an attachment we obtained from a potentially 
malicious email and see what URLs it attempts to communicate with, what 
additional payloads are downloaded to the endpoint, persistence 
mechanisms, Indicators of Compromise (IOCs), etc.

Some of these online malware sandboxes are listed below.

- Any.Run: [https://app.any.run/](https://app.any.run/)

Per the [site](https://app.any.run/), "*Analyze
 a network, file, module, and the registry activity. Interact with the 
OS directly from a browser. See the feedback from your actions 
immediately*".

![https://assets.tryhackme.com/additional/phishing2/any-run.png](https://assets.tryhackme.com/additional/phishing2/any-run.png)

- Hybrid Analysis: [https://www.hybrid-analysis.com/](https://www.hybrid-analysis.com/)

Per the site, *"This
 is a free malware analysis service for the community that detects and 
analyzes unknown threats using a unique Hybrid Analysis technology*."

![https://assets.tryhackme.com/additional/phishing2/hybrid-analysis.png](https://assets.tryhackme.com/additional/phishing2/hybrid-analysis.png)

- [https://www.joesecurity.org/](https://www.joesecurity.org/)

Per the site, "*Joe
 Sandbox empowers analysts with a large spectrum of product features. 
Among them: Live Interaction, URL Analysis & AI based Phishing 
Detection, Yara and Sigma rules support, MITRE ATT&CK matrix, AI 
based malware detection, Mail Monitor, Threat Hunting & 
Intelligence, Automated User Behavior, Dynamic VBA/JS/JAR 
instrumentation, Execution Graphs, Localized Internet Anonymization and 
many more*".

![https://assets.tryhackme.com/additional/phishing2/joe-security.png](https://assets.tryhackme.com/additional/phishing2/joe-security.png)

We will interact with these services in the upcoming Phishing cases.

**PhishTool**

A tool that will help with automated phishing analysis is [PhishTool](https://www.phishtool.com/).

Yes, I saved this for last! What is PhishTool?

Per the site, "*Be
 you a security researcher investigating a new phish-kit, a SOC analyst 
responding to user reported phishing, a threat intelligence analyst 
collecting phishing IoCs or an investigator dealing with email-born 
fraud.*

*PhishTool combines threat intelligence, OSINT, email
 metadata and battle tested auto-analysis pathways into one powerful 
phishing response platform. Making you and your organisation a 
formidable adversary - immune to phishing campaigns that those with 
lesser email security capabilities fall victim to.*"

Note: There is a free community edition you can download and use. :)

I uploaded a malicious email to PhishTool and connected VirusTotal to my account using my community edition API key.

Below are a few screenshots of the malicious email and the PhishTool interface.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/0dcc25c992ddfdfc60532f6fb9416a70.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/0dcc25c992ddfdfc60532f6fb9416a70.png)

From the image above, you can see the PhishTool conveniently grabs all the pertinent information we'll need regarding the email.

- Email sender
- Email recipient (in this case, a long list of CCed email addresses)
- Timestamp
- Originating IP and Reverse DNS lookup

We can obtain information about the SMTP relays, specific X-header information, and IP info information.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9665b8957923a892e721a0e02e42ea9f.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9665b8957923a892e721a0e02e42ea9f.png)

Below is a snippet of Hop 1 of 6 (SMTP relays).

![https://assets.tryhackme.com/additional/phishing2/phish-smtp.png](https://assets.tryhackme.com/additional/phishing2/phish-smtp.png)

Notice that the tool notifies us that '**Reply-To no present**' although it provides the alternative header information, **Return-Path**.

To
 the right of the PhishTool dashboard, we can see the email body. There 
are two tabs across the top that we can toggle to view the email in text
 format or its HTML source code.

Text view:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/94366a297a0abb9b7f680e006c421b45.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/94366a297a0abb9b7f680e006c421b45.png)

HTML view:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e5eb24859d263b8d233f52c1502aaed4.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e5eb24859d263b8d233f52c1502aaed4.png)

The bottom two panes will display information about attachments and URLs.

The right pane will show if any URLs were found in the email. In this case, no emails were found.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/a737376ca1243a926f7a41a765cb7a1e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/a737376ca1243a926f7a41a765cb7a1e.png)

The left pane will show information about the attachment. This particular malicious email has a zip file.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/685f9bb5291973038d55aca7c09ffd1e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/685f9bb5291973038d55aca7c09ffd1e.png)

We can automatically get feedback from VirusTotal since our community edition API key is connected.

Here we can grab the zip file name and its hashes without manually interacting with the malicious email.

There
 is an ellipsis at the far right of the above image. If that is clicked,
 we are provided additional actions that we can perform with the 
attachment.

Below is a screenshot of the additional options sub-menu.

![https://assets.tryhackme.com/additional/phishing2/phish-options.png](https://assets.tryhackme.com/additional/phishing2/phish-options.png)

Let's look at the Strings output.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e1f11b62dbd9ed415177bdbc44a13d2d.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e1f11b62dbd9ed415177bdbc44a13d2d.png)

Next, let's look at the information from VirusTotal.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5c0556b15a803638a2d289915edc8946.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5c0556b15a803638a2d289915edc8946.png)

Since
 the VirusTotal API key is the free community edition, an analyst can 
manually navigate to VirusTotal and do a file hash search to view more 
information about this attachment.

Lastly, any submissions you 
upload to PhishTool, you can flag as malicious and resolve with notes. 
Similar to how you would if you were a SOC Analyst.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/31728d39e79f36340ab8bcdd740940d6.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/31728d39e79f36340ab8bcdd740940d6.png)

The attachment file name and file hashes will be marked as malicious. Next, click on **Resolve**.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/64c5e32e65919e17e352161594fbb627.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/64c5e32e65919e17e352161594fbb627.png)

In the next screen, an analyst can mark the email based on dropdown selections. Refer to the GIF below.

![https://assets.tryhackme.com/additional/phishing2/resolve-case.gif](https://assets.tryhackme.com/additional/phishing2/resolve-case.gif)

**Note**:
 I didn't perform further analysis on the domain name or the IP address.
 Neither did I perform any research regarding the root domain the email 
originated from. The attachment can further be analyzed by uploading it 
to a malware sandbox to see what exactly it's doing, which I did not do.
 Hence the reason why additional Flag artifacts and Classifications 
codes weren't selected for this malicious email. :)

To expand on classification codes briefly, not all phishing emails can be categorized as the same. A classification
 code allows us to tag a case with a specific code, such as Whaling 
(high-value target). Not all phishing emails will target a high-value 
target, such as a Chief Financial Officer (CFO).

**Phishing Prevention**

**SPF (Sender Policy Framework)**

What is the **Sender Policy Framework** (**SPF**)?

Per [dmarcian](https://dmarcian.com/what-is-spf/), "*Sender Policy Framework (SPF)
 is used to authenticate the sender of an email. With an SPF record in 
place, Internet Service Providers can verify that a mail server is 
authorized to send email for a specific domain. An SPF record is a DNS 
TXT record containing a list of the IP addresses that are allowed to 
send email on behalf of your domain.*"

Below is a visual workflow for SPF.

![https://assets.tryhackme.com/additional/phishing4/dmarcian-spf.png](https://assets.tryhackme.com/additional/phishing4/dmarcian-spf.png)

**Note:** Credit to dmarcian for the above image.

How does a basic SPF record look like?

`v=spf1 ip4:127.0.0.1 include:_spf.google.com -all`

An explanation for the above record:

- `v=spf1` -> This is the start of the SPF record
- `ip4:127.0.0.1` -> This specifies which IP (in this case version IP4 & not IP6) can send mail
- `include:_spf.google.com` -> This specifies which domain can send mail
- `all` -> non-authorized emails will be rejected

Refer to the SPF Record Syntax on dmarcian [here](https://dmarcian.com/spf-syntax-table/) and [here](https://dmarcian.com/what-is-the-difference-between-spf-all-and-all/).

Let's look at Twitter's SPF record using dmarcian's SPF Surveyor [tool](https://dmarcian.com/spf-survey/).

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/66c0270a75718fd985664b223e549cde.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/66c0270a75718fd985664b223e549cde.png)

Refer to this resource on [dmarcian](https://dmarcian.com/create-spf-record/) on how to create your own SPF records.

Let's look at another sample.

The image below is from [Google Admin Toolbox Messageheader](https://toolbox.googleapps.com/apps/messageheader/), which was used to analyze a malicious email.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5d9bea5f9fd4e1409d4cb28bfdfea94e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5d9bea5f9fd4e1409d4cb28bfdfea94e.png)

The above image shows the status of an SPF record check. It reports back as **softfail**.

**Note**: Even though this task uses [dmarcian](https://dmarcian.com/) for SPF-related information and online checks, many other companies do the same.

 **DKIM (DomainKeys Identified Mail)**

What is **DKIM**?

Per [dmarcian](https://dmarcian.com/what-is-dkim/), "*DKIM
 stands for DomainKeys Identified Mail and is used for the 
authentication of an email that’s being sent. Like SPF, DKIM is an open 
standard for email authentication that is used for DMARC alignment. A 
DKIM record exists in the DNS, but it is a bit more complicated than 
SPF. DKIM’s advantage is that it can survive forwarding, which makes it 
superior to SPF and a foundation for securing your email.*"

How does a DKIM record look like?

`v=DKIM1;
 k=rsa; 
p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxTQIC7vZAHHZ7WVv/5x/qH1RAgMQI+y6Xtsn73rWOgeBQjHKbmIEIlgrebyWWFCXjmzIP0NYJrGehenmPWK5bF/TRDstbM8uVQCUWpoRAHzuhIxPSYW6k/w2+HdCECF2gnGmmw1cT6nHjfCyKGsM0On0HDvxP8I5YQIIlzNigP32n1hVnQP+UuInj0wLIdOBIWkHdnFewzGK2+qjF2wmEjx+vqHDnxdUTay5DfTGaqgA9AKjgXNjLEbKlEWvy0tj7UzQRHd24a5+2x/R4Pc7PF/y6OxAwYBZnEPO0sJwio4uqL9CYZcvaHGCLOIMwQmNTPMKGC9nt3PSjujfHUBX3wIDAQAB`

An explanation of the above record:

- `v=DKIM1`> This is the version of the DKIM record. This is optional.
- `k=rsa` -> This is the key type. The default value is RSA. RSA is an encryption algorithm (cryptosystem).
- `p=` -> This is the public key that will be matched to the private key, which was created during the DKIM setup process.

Refer to the DKIM resource [here](https://dmarcian.com/dkim-selectors/) and [here](https://help.returnpath.com/hc/en-us/articles/222481088-DKIM-DNS-record-overview) for additional information.

The below image is a snippet of an email header for an email flagged as spam that contained a potentially malicious attachment.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/334dbef5ba955a23b7e84629b85eb26a.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/334dbef5ba955a23b7e84629b85eb26a.png)

**DMARC (Domain-Based Message Authentication, Reporting, and Conformance)**

What is **DMARC**?

Per [dmarcian](https://dmarcian.com/start-dmarc/), "*DMARC,
 (Domain-based  Message Authentication Reporting, & Conformance) an 
open source standard, uses a concept called alignment to tie the result 
of two other open source standards, SPF (a published list of servers 
that are authorized to send email on behalf of a domain) and DKIM (a 
tamper-evident domain seal associated with a piece of email), to the 
content of an email. If not already deployed, putting a DMARC record 
into place for your domain will give you feedback that will allow you to
 troubleshoot your SPF and DKIM configurations if needed.*"

How does a basic DMARC record look like?

`v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com`

An explanation of the above record:

- `v=DMARC1` -> Must be in all caps, and it's not optional
- `p=quarantine` -> If a check fails, then an email will be sent to the spam folder (DMARC Policy)
- `rua=mailto:postmaster@website.com` -> Aggregate reports will be sent to this email address

Refer to the DMARC resources [here](https://dmarcian.com/dmarc-record/) and [here](https://dmarc.org/overview/) for additional information on DMARC tags. Review the following resource about DMARC [Alignment](https://dmarcian.com/alignment/).

Let's use the **Domain Health Checker** from [dmarcian.com](https://dmarcian.com/domain-checker/) and check the DMARC status of **microsoft.com**.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9b94a157faf86848b26093efb30c2126.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9b94a157faf86848b26093efb30c2126.png)

And the results are...

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/72bc9ea8efe179361c958a951f9db9fb.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/72bc9ea8efe179361c958a951f9db9fb.png)

Microsoft passed all checks. We can drill down into **DMARC**, **SPF**, or **DKIM** to get more details.

**DMARC**:

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/d0b2fc15e23d1466ff98efc98afef61e.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/d0b2fc15e23d1466ff98efc98afef61e.png)

In the details above, we can see that all emails that fail the DMARC check will be rejected.

**S/MIME (Secure/Multipurpose Internet Mail Extensions)**

What is [**S/MIME**](https://docs.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo)?

Per Microsoft, "*S/MIME
 (Secure/Multipurpose internet Mail Extensions) is a widely accepted 
protocol for sending digitally signed and encrypted messages*."

As you can tell from the definition above, the 2 main ingredients for S/MIME are:

1. **Digital Signatures**
2. **Encryption**

Using [Public Key Cryptography](https://www.ibm.com/docs/en/ztpf/2023?topic=concepts-public-key-cryptography), S/MIME guarantees data integrity and nonrepudiation.

- If Bob wishes to use S/MIME, then he'll need a digital certificate. This digital certificate will contain his public key.
- With this digital certificate, Bob can "sign" the email message with his private key.
- Mary can then decrypt Bob's message with Bob's public key.
- Mary will do the same (send her certificate to Bob) when she replies to his email, and Bob complete the same process on his end.
- Both will now have each other's certificates for future correspondence.

The illustration below will help you understand how public key cryptography works.

![https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/27cb0b439d172324f453e57c9cbf7ac0.png](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/27cb0b439d172324f453e57c9cbf7ac0.png)
