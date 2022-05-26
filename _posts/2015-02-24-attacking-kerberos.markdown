---
title: "[TryHackMe][CompTIA_Pentest+][Attacking_Kerberos]"
layout: post
date: 2022-05-25 08:00
image: /assets/images/tryhackme.png
headerImage: false
tag:
- TryHackMe
- CompTIA_Pentest+
- Local-host vulnerabilities
category: blog
author: Safak AYDIN
description: Attacking_Kerberos
---

## Summary:

Learn how to abuse the Kerberos Ticket Granting Service inside of a Windows Domain Controller.

#### Tasks
- [Introduction](#introduction)
- [Enumeration w/ Kerbrute](#enumeration-w/-kerbrute)
- [Harvesting & Brute-Forcing Tickets w/ Rubeus](#harvesting-&-brute-forcing-tickets-w/-rubeus)
- [Kerberoasting w/ Rubeus & Impacket](#kerberoasting-w/-rubeus-&-impacket)
- [AS-REP Roasting w/ Rubeus](#as-rep-roasting-w/-rubeus)
- [Golden/Silver Ticket Attacks w/ mimikatz](#golden/silver-ticket-attacks-w/-mimikatz)

---

## Introduction

**Question :** What does TGT stand for ?

{% highlight html %}
Answer : Ticket Granting Ticket
{% endhighlight %}

**Question :** What does SPN stand for ?

{% highlight html %}
Answer : Service Principal Name
{% endhighlight %}

**Question :** What does PAC stand for ?

{% highlight html %}
Answer : Privilege Attribute Certificate
{% endhighlight %}

**Question :** What two services make up the KDC ?

{% highlight html %}
Answer : AS, TGS
{% endhighlight %}

## Enumeration w/ Kerbrute

![image](https://user-images.githubusercontent.com/80531900/170521501-ea85c969-77f7-4d95-afbc-55b96bdb47c0.png)

* Pre-requisite :
{% highlight html %}
# echo "Machine_IP   CONTROLLER.LOCAL >> /etc/hosts"
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/170521628-42d1a23c-a527-4659-936b-1cb0d684bc7c.png)

* Kerbrute installation : 
{% highlight html %}
# wget https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute_linux_amd64
# chmod +x kerbrute_linux_amd64
# mv kerbrute_linux_amd64 /usr/bin/kerbrute
# kerbrute -h
{% endhighlight %}

* Username Wordlist Import : 
{% highlight html %}
# wget https://raw.githubusercontent.com/Cryilllic/Active-Directory-Wordlists/master/User.txt
{% endhighlight %}

* Enumerating Users : 
{% highlight html %}
# kerbrute userenum --dc CONTROLLER.LOCAL -d CONTROLLER.LOCAL User.txt
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/170522935-cd3f7925-6a2f-4be4-ab54-f0a58723001f.png)

**Question :** How many total users do we enumerate ?

{% highlight html %}
Answer : 10
{% endhighlight %}

**Question :** What is the SQL service account name ?

{% highlight html %}
Answer : SQLService
{% endhighlight %}

**Question :** What is the second "machine" account name ?

{% highlight html %}
Answer : Machine2
{% endhighlight %}

**Question :** What is the third "user" account name ?

{% highlight html %}
Answer : User3
{% endhighlight %}

## Harvesting & Brute-Forcing Tickets w/ Rubeus

**Question :** Which domain admin do we get a ticket for when harvesting tickets ?

{% highlight html %}
Answer : Administrator
{% endhighlight %}

**Question :** Which domain controller do we get a ticket for when harvesting tickets ?

{% highlight html %}
Answer : CONTROLLER-1
{% endhighlight %}

## Kerberoasting w/ Rubeus & Impacket

**Question :** What is the HTTPService Password ?

{% highlight html %}
Answer : Summer2020
{% endhighlight %}

**Question :** What is the SQLService Password ?

{% highlight html %}
Answer : MYPassword123#
{% endhighlight %}

## AS-REP Roasting w/ Rubeus

**Question :**  What hash type does AS-REP Roasting use ? 

{% highlight html %}
Answer : Kerberos 5 AS-REP etype 23
{% endhighlight %}

**Question :** Which User is vulnerable to AS-REP Roasting ?

{% highlight html %}
Answer : User3
{% endhighlight %}

**Question :** What is the User's Password ?

{% highlight html %}
Answer : Password3
{% endhighlight %}

**Question :** Which Admin is vulnerable to AS-REP Roasting ?

{% highlight html %}
Answer : Admin2
{% endhighlight %}

**Question :** What is the Admin's Password ?

{% highlight html %}
Answer : P@$$W0rd2
{% endhighlight %}

## Golden/Silver Ticket Attacks w/ mimikatz

**Question :** What is the SQLService NTLM Hash ?

{% highlight html %}
Answer : cd40c9ed96265531b21fc5b1dafcfb0a
{% endhighlight %}

**Question :** What is the Administrator NTLM Hash ? 

{% highlight html %}
Answer : 2777b7fec870e04dda00cd7260f7bee6
{% endhighlight %}

