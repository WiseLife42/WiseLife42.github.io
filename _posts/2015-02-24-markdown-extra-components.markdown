---
title: "[TryHackMe][CompTIA_Pentest+][Attacktive_Directory]"
layout: post
date: 2022-05-25 08:00
image: /assets/images/tryhackme.png
headerImage: false
tag:
- TryHackMe
- CompTIA_Pentest+
- Local-Host vulnerabilities
category: blog
author: Safak AYDIN
description: Attacktive_Directory
---

## Summary:

Learn the basics of Active Directory and how it is used in the real world today.

#### Tasks
- [Setup](#setup)
- [Welcome to Attacktive Directory](#welcome-to-attacktive-directory)
- [Enumerating Users via Kerberos](#enumerating-users-via-kerberos)
- [Abusing Kerberos](#abusing-kerberos)
- [Back to the Basics](#back-to-the-basics)
- [Elevating Privileges within the Domain](#elevating-privileges-within-the-domain)
- [Flag Submission Panel](#flag-submission-panel)

---

## Setup

{% highlight html %}
# apt install bloodhound neo4j -y
# sudo git clone https://github.com/SecureAuthCorp/impacket.git /opt/impacket
# sudo pip3 install -r /opt/impacket/requirements.txt
# cd /opt/impacket/ 
# sudo pip3 install .
# sudo python3 setup.py install
{% endhighlight %}

## Welcome to Attacktive Directory

**Question :** What tool will allow us to enumerate port 139/445?

{% highlight html %}
Answer : enum4linux
{% endhighlight %}

**Question :** What is the NetBIOS-Domain Name of the machine?

{% highlight html %}
Answer : THM-AD
{% endhighlight %}

**Question :** What invalid TLD do people commonly use for their Active Directory Domain?

{% highlight html %}
Answer : .local
{% endhighlight %}

---

## Enumerating Users via Kerberos

**Question :** What command within Kerbrute will allow us to enumerate valid usernames?

{% highlight html %}
Answer : userenum
{% endhighlight %}

**Question :** What notable account is discovered? (These should jump out at you)

{% highlight html %}
Answer : svc-admin
{% endhighlight %}

**Question :** What is the other notable account is discovered? (These should jump out at you)

{% highlight html %}
Answer : backup
{% endhighlight %}

---

## Abusing Kerberos

**Question :** We have two user accounts that we could potentially query a ticket from. Which user account can you query a ticket from with no password?

{% highlight raw %}
Answer : svc-admin
{% endhighlight %}

**Question :** Looking at the Hashcat Examples Wiki page, what type of Kerberos hash did we retrieve from the KDC? (Specify the full name)

{% highlight raw %}
Answer : Kerberos 5 AS-REP etype 23
{% endhighlight %}

**Question :** What mode is the hash?

{% highlight raw %}
Answer : 18200
{% endhighlight %}

**Question :** Now crack the hash with the modified password list provided, what is the user accounts password?

{% highlight raw %}
Answer : management2005
{% endhighlight %}

---

## Back to the Basics

**Question :** What utility can we use to map remote SMB shares?

{% highlight raw %}
Answer : smbclient
{% endhighlight %}

**Question :** Which option will list shares?

{% highlight raw %}
Answer : -L
{% endhighlight %}

**Question :** How many remote shares is the server listing?

{% highlight raw %}
Answer : 6
{% endhighlight %}

**Question :** There is one particular share that we have access to that contains a text file. Which share is it?

{% highlight raw %}
Answer : backup
{% endhighlight %}

**Question :** What is the content of the file?

{% highlight raw %}
Answer : YmFja3VwQHNwb29reXNlYy5sb2NhbDpiYWNrdXAyNTE3ODYw
{% endhighlight %}

**Question :** Decoding the contents of the file, what is the full contents?

{% highlight raw %}
Answer : backup@spookysec.local:backup2517860
{% endhighlight %}

---

## Elevating Privileges within the Domain

**Question :** What method allowed us to dump NTDS.DIT?

{% highlight raw %}
Answer : DRSUAPI
{% endhighlight %}

**Question :** What is the Administrators NTLM hash?

{% highlight raw %}
Answer : 0e0363213e37b94221497260b0bcb4fc
{% endhighlight %}

**Question :** What method of attack could allow us to authenticate as the user without the password?

{% highlight raw %}
Answer : Pass The Hash
{% endhighlight %}

**Question :** Using a tool called Evil-WinRM what option will allow us to use a hash?

{% highlight raw %}
Answer : -H
{% endhighlight %}

---

## Flag Submission Panel

**Question :** svc-admin 

{% highlight raw %}
Answer : TryHackMe{K3rb3r0s_Pr3_4uth}
{% endhighlight %}

**Question :** backup

{% highlight raw %}
Answer : TryHackMe{B4ckM3UpSc0tty!}
{% endhighlight %}

**Question :** Administrator

{% highlight raw %}
Answer : TryHackMe{4ctiveD1rectoryM4st3r}
{% endhighlight %}

---

[1]: https://daringfireball.net/projects/markdown/
[2]: https://www.fileformat.info/info/unicode/char/2163/index.htm
[3]: https://www.markitdown.net/
[4]: https://daringfireball.net/projects/markdown/basics
[5]: https://daringfireball.net/projects/markdown/syntax
[6]: https://kune.fr/wp-content/uploads/2013/10/ghost-blog.jpg
