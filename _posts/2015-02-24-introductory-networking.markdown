---
title: "[TryHackMe][CompTIA_Pentest+][Introductory_Networking]"
layout: post
date: 2022-05-25 08:00
image: /assets/images/tryhackme.png
headerImage: false
tag:
- TryHackMe
- CompTIA_Pentest+
- Network-based vulnerabilities
category: blog
author: Safak AYDIN
description: Introduction_Networking
---

## Summary:

An introduction to networking theory and basic networking tools.

#### Tasks
- [The OSI Model: An Overview](#the-osi-model-:-an-overview)
- [Encapsulation](#encapsulation)
- [The TCP/IP Model](#the-tcp-ip-model)
- [Ping](#ping)
- [Traceroute](#traceroute)
- [WHOIS](#whois)
- [Dig](#dig)

---

## The OSI Model: An Overview

**Question :** Which layer would choose to send data over TCP or UDP ?

{% highlight html %}
Answer : 4
{% endhighlight %}

**Question :** Which layer checks received packets to make sure that they haven't been corrupted ?

{% highlight html %}
Answer : 2
{% endhighlight %}

**Question :** In which layer would data be formatted in preparation for transmission ?

{% highlight html %}
Answer : 2
{% endhighlight %}

**Question :** Which layer transmits and receives data ?

{% highlight html %}
Answer : 1
{% endhighlight %}

**Question :** Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format ?

{% highlight html %}
Answer : 6
{% endhighlight %}

**Question :** Which layer tracks communications between the host and receiving computers ?

{% highlight html %}
Answer : 5
{% endhighlight %}

**Question :** Which layer accepts communication requests from applications ?

{% highlight html %}
Answer : 7
{% endhighlight %}

**Question :** Which layer handles logical addressing ?

{% highlight html %}
Answer : 3
{% endhighlight %}

**Question :** When sending data over TCP, what would you call the "bite-sized" pieces of data? 

{% highlight html %}
Answer : Segments
{% endhighlight %}

[Research] Which layer would the FTP protocol communicate with ?

{% highlight html %}
Answer : 7
{% endhighlight %}

**Question :** Which transport layer protocol would be best suited to transmit a live video ?

{% highlight html %}
Answer : UDP
{% endhighlight %}

## Encapsulation

**Question :** How would you refer to data at layer 2 of the encapsulation process (with the OSI model) ?

{% highlight html %}
Answer : Frames
{% endhighlight %}

**Question :** How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected ?

{% highlight html %}
Answer : Datagrams
{% endhighlight %}

**Question :** What process would a computer perform on a received message ?

{% highlight html %}
Answer : De-encapsulation
{% endhighlight %}

**Question :** Which is the only layer of the OSI model to add a trailer during encapsulation ?

{% highlight html %}
Answer : Data Link
{% endhighlight %}

**Question :** Does encapsulation provide an extra layer of security (Aye/Nay) ?

{% highlight html %}
Answer : Aye
{% endhighlight %}

## The TCP/IP Model

**Question :** Which model was introduced first, OSI or TCP/IP ?

{% highlight html %}
Answer : TCP/IP
{% endhighlight %}

**Question :** Which layer of the TCP/IP model covers the functionality of the Transport layer of the OSI model (Full Name) ?

{% highlight html %}
Answer : Transport
{% endhighlight %}

**Question :** Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model (Full Name) ?

{% highlight html %}
Answer : Application
{% endhighlight %}

**Question :** The Network Interface layer of the TCP/IP model covers the functionality of two layers in the OSI model. These layers are Data Link, and?.. (Full Name) ?

{% highlight html %}
Answer : Physical
{% endhighlight %}

**Question :** Which layer of the TCP/IP model handles the functionality of the OSI network layer ?

{% highlight html %}
Answer : Internet
{% endhighlight %}

**Question :** What kind of protocol is TCP ?

{% highlight html %}
Answer : Connection-based
{% endhighlight %}

**Question :** What is SYN short for ?

{% highlight html %}
Answer : Synchronise
{% endhighlight %}

**Question :** What is the second step of the three way handshake ?

{% highlight html %}
Answer : SYN/ACK
{% endhighlight %}

**Question :** What is the short name for the "Acknowledgement" segment in the three-way handshake ?

{% highlight html %}
Answer : ACK
{% endhighlight %}

# Networking Tools

## Ping

![image](https://user-images.githubusercontent.com/80531900/171719689-57ec9c05-fde7-4412-8c92-7b4f834d7a12.png)

![image](https://user-images.githubusercontent.com/80531900/171719725-54e2e1c7-83a3-4358-8cdc-ad7a96a69cb5.png)

**Question :** What command would you use to ping the bbc.co.uk website ?

{% highlight html %}
Answer : ping bbc.co.uk
{% endhighlight %}

**Question :** What is the IPv4 address ?

{% highlight html %}
Answer : 217.160.0.152
{% endhighlight %}

**Question :** What switch lets you change the interval of sent ping requests ?

{% highlight html %}
Answer : -i
{% endhighlight %}

**Question :** What switch would allow you to restrict requests to IPv4 ?

{% highlight html %}
Answer : -4
{% endhighlight %}

**Question :** What switch would give you a more verbose output ?

{% highlight html %}
Answer : -v
{% endhighlight %}

## Traceroute

![image](https://user-images.githubusercontent.com/80531900/171719770-a1a3cabe-a2bf-4116-83f0-7f0c56714d7e.png)

**Question :** Can you see the path your request has taken ?

![image](https://user-images.githubusercontent.com/80531900/171719792-f8d4c916-2f36-4469-83c3-ffbbcdaed317.png)

**Question :** What switch would you use to specify an interface when using Traceroute ?

{% highlight html %}
Answer : -i
{% endhighlight %}

**Question :** What switch would you use if you wanted to use TCP SYN requests when tracing the route ?

{% highlight html %}
Answer : -T
{% endhighlight %}

**Question :** [Lateral Thinking] Which layer of the TCP/IP model will traceroute run on by default (Windows) ?

{% highlight html %}
Answer : Internet
{% endhighlight %}

## WHOIS

**Question :** Perform a whois search on facebook.com

![image](https://user-images.githubusercontent.com/80531900/171719826-0263859f-ea8f-4e87-891a-03dbe596135f.png)

![image](https://user-images.githubusercontent.com/80531900/171719850-0edf2e9c-cf04-4625-8950-db1862b52ae9.png)

**Question :** What is the registrant postal code for facebook.com ?

{% highlight html %}
Answer : 94025
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171719880-29c40fff-4d61-40e5-b016-4d551b8e5e0e.png)

**Question :** When was the facebook.com domain first registered (Format: DD/MM/YYYY) ?

{% highlight html %}
Answer : 29/03/1997
{% endhighlight %}

**Question :** Perform a whois search on microsoft.com

![image](https://user-images.githubusercontent.com/80531900/171719896-0797116f-7a00-44c1-8f72-1bdcb46d6e86.png)

**Question :** Which city is the registrant based in ?

{% highlight html %}
Answer : Redmond
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171719925-318004c8-4232-4e3c-b974-8420dafa0fb0.png)

**Question :** [OSINT] What is the name of the golf course that is near the registrant address for microsoft.com ?

{% highlight html %}
Answer : Bellevue Golf Course
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171719950-1917f6d0-2f0b-41ca-bbe8-ed0a7373f2a4.png)

**Question :** What is the registered Tech Email for microsoft.com ?

{% highlight html %}
Answer : msnhst@microsoft.com
{% endhighlight %}

## Dig

**Question :** What is DNS short for ?

{% highlight html %}
Answer : Domain Name System
{% endhighlight %}

**Question :** What is the first type of DNS server your computer would query when you search for a domain?

{% highlight html %}
Answer : Recursive
{% endhighlight %}

**Question :** What type of DNS server contains records specific to domain extensions (i.e. .com, .co.uk*, etc)* ?

{% highlight html %}
Answer : Top-Level Doamin
{% endhighlight %}

**Question :** Where is the very first place your computer would look to find the IP address of a domain ?

{% highlight html %}
Answer : Local Cache
{% endhighlight %}

**Question :** [Research] Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one ?

{% highlight html %}
Answer : 8.8.4.4
{% endhighlight %}

**Question :** If a DNS query has a TTL of 24 hours, what number would the dig query show ?

{% highlight html %}
Answer : 86400
{% endhighlight %}
