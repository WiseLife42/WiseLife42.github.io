---
title: "[TryHackMe][CompTIA_Pentest+][Network_Services]"
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
description: Network_Services
---

## Summary:

Learn about, then enumerate and exploit a variety of network services and misconfigurations.

#### Tasks
- [Understanding SMB](#understanding-smb)
- [Enumerating SMB](#enumerating-smb)
- [Exploiting SMB](#exploiting-smb)
- [Understanding Telnet](#understanding-telnet)
- [Enumerating Telnet](#enumerating-telnet)
- [Exploiting Telnet](#exploiting-telnet)
- [Understanding FTP](#understanding-ftp)
- [Enumerating FTP](#enumerating-ftp)
- [Exploiting FTP](#exploiting-ftp)

---

## Understanding SMB

**Question :** What does SMB stand for ?

{% highlight html %}
Answer : Server Message Block
{% endhighlight %}

**Question :** What type of protocol is SMB ?

{% highlight html %}
Answer : response-request
{% endhighlight %}
    
**Question :** What do clients connect to servers using ?

{% highlight html %}
Answer : TCP/IP
{% endhighlight %}
    
**Question :** What systems does Samba run on ?

{% highlight html %}
Answer : Unix
{% endhighlight %}

## Enumerating SMB

![image](https://user-images.githubusercontent.com/80531900/171834346-50f10c1c-c13f-4923-bdd1-98c998d9c7eb.png)

**Question :** Conduct an nmap scan of your choosing, How many ports are open?

{% highlight html %}
Answer : 3
{% endhighlight %}

**Question :** What ports is SMB running on ?

{% highlight html %}
Answer : 139/445
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834389-15c1137c-f95a-4eb5-9e9f-a30f7f404bee.png)

![image](https://user-images.githubusercontent.com/80531900/171834413-1df7ba93-a0be-4d03-98d1-60761caeec92.png)

**Question :** Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name ?

{% highlight html %}
Answer : WORKGROUP
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834440-ad777dd3-6321-4475-91a9-a9b6dc317063.png)

**Question :** What comes up as the name of the machine ?

{% highlight html %}
Answer : POLOSMB
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834467-e8dc5b34-1a87-4c84-af38-bebbeb4cdb4a.png)

**Question :** What operating system version is running ?    

{% highlight html %}
Answer : 6.1
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834493-6e563a52-30ac-45e2-ae8e-fbb116ea4814.png)

**Question :** What share sticks out as something we might want to investigate ?

{% highlight html %}
Answer : profiles
{% endhighlight %}

## Exploiting SMB

**Question :** What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port ?

{% highlight html %}
Answer : smbclient //10.10.10.2/secret -U suit -p 445
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834570-fed8c190-43ef-4359-af3a-61454beba3f2.png)

**Question :** Does the share allow anonymous access ? Y/N ?

{% highlight html %}
Answer : Y
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834598-86d398bb-6cef-4aff-b343-859d4eb44c36.png)

![image](https://user-images.githubusercontent.com/80531900/171834615-8b31f3ee-a273-451d-b426-97a246847068.png)

**Question :** Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to ?

{% highlight html %}
Answer : John Cactus
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834646-20566c93-6b14-4a24-a802-0794b52f75f7.png)

**Question :** What service has been configured to allow him to work from home ? 

{% highlight html %}
Answer : ssh
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834701-2bb4e049-3748-4990-8010-da1bf96df81c.png)

**Question :** Okay! Now we know this, what directory on the share should we look in ? 

{% highlight html %}
Answer : .ssh
{% endhighlight %}

**Question :** This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us ?

![image](https://user-images.githubusercontent.com/80531900/171834724-f495a406-57e4-4231-ae38-e7afd3e45bbe.png)

{% highlight html %}
Answer : id_rsa
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834759-ae7f2748-309d-4790-b2e0-ab81d6ba388f.png){: class="bigger-image" }

![image](https://user-images.githubusercontent.com/80531900/171834779-c127cecf-8db1-455b-9502-1063283e42eb.png)

**Question :** What is the smb.txt flag ?

{% highlight html %}
Answer : THM{smb_is_fun_eh?}
{% endhighlight %}

## Understanding Telnet

**Question :** What is Telnet?

{% highlight html %}
Answer : application protocol
{% endhighlight %}

**Question :** What has slowly replaced Telnet ?

{% highlight html %}
Answer : ssh
{% endhighlight %}

**Question :** How would you connect to a Telnet server with the IP 10.10.10.3 on port 23 ? 

{% highlight html %}
Answer : telnet 10.10.10.3 23
{% endhighlight %}

**Question :** The lack of what, means that all Telnet communication is in plaintext ?

{% highlight html %}
Answer : encryption
{% endhighlight %}

## Enumerating Telnet

![image](https://user-images.githubusercontent.com/80531900/171834934-3619bc6b-96ea-4ae2-aa2c-6cf71462e9fc.png)

**Question :** How many ports are open on the target machine ?

{% highlight html %}
Answer : 1
{% endhighlight %}

**Question :** What port is this ?

{% highlight html %}
Answer : 8012
{% endhighlight %}

**Question :** This port is unassigned, but still lists the protocol it's using, what protocol is this ?

{% highlight html %}
Answer : tcp
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834978-a74e2b39-0555-4606-8ce0-538f213434c3.png)

**Question :** Now re-run the nmap scan, without the -p- tag, how many ports show up as open ? 

{% highlight html %}
Answer : 0
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171834994-c56acfe2-8ac1-46e7-9ad9-c0a57e5227b9.png)

**Question :** Based on the title returned to us, what do we think this port could be used for ? 

{% highlight html %}
Answer : a backdoor
{% endhighlight %}

**Question :** Who could it belong to ? Gathering possible usernames is an important step in enumeration.

{% highlight html %}
Answer : Skidy
{% endhighlight %}

## Exploiting Telnet

**Question :** Great! It's an open telnet connection! What welcome message do we receive ? 

{% highlight html %}
Answer : SKIDY'S BACKDOOR.
{% endhighlight %}

**Question :** Let's try executing some commands, do we get a return on any input we enter into the telnet session ? (Y/N)

{% highlight html %}
Answer : N
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835103-e2050add-3e09-477c-8674-5bf5b0efc5af.png)

![image](https://user-images.githubusercontent.com/80531900/171835127-5f10129c-98ed-4f20-ab10-27c5d8736521.png)

**Question :** Now, use the command "ping [local THM ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835163-1e5b7cab-5ec8-407a-b797-f08bc79a3cf0.png)

![image](https://user-images.githubusercontent.com/80531900/171835177-92a0c72b-3e56-4e9f-a36c-92e2fac5e362.png)

**Question :** What word does the generated payload start with ?

{% highlight html %}
Answer : mkfifo
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835237-5482e962-6265-47aa-901a-b700ac69321a.png)

**Question :** What would the command look like for the listening port we selected in our payload ?

{% highlight html %}
Answer : nc -lvp 4444
{% endhighlight %}

**Question :** Success! What is the contents of flag.txt ?

{% highlight html %}
Answer : THM{y0u_g0t_th3_t3ln3t_fl4g}
{% endhighlight %}

## Understanding FTP

**Question :** What communications model does FTP use ?

{% highlight html %}
Answer : client-server
{% endhighlight %}

**Question :** What's the standard FTP port ?

{% highlight html %}
Answer : 21
{% endhighlight %}

**Question :** How many modes of FTP connection are there?    

{% highlight html %}
Answer : 2
{% endhighlight %}

## Enumerating FTP

![image](https://user-images.githubusercontent.com/80531900/171835264-ae37ca94-97cd-49cf-a774-a265b9fbcac4.png)

**Question :** How many ports are open on the target machine ?

{% highlight html %}
Answer : 2
{% endhighlight %}

**Question :** What port is ftp running on ? 

{% highlight html %}
Answer : 21
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835288-2f106ec1-d702-4e04-a0f6-d41c8efef3e8.png)

**Question :** What variant of FTP is running on it ?  

{% highlight html %}
Answer : vsftpd
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835303-74dfdba1-6fbf-4da9-8380-06b0b67b8e4e.png)

**Question :** What is the name of the file in the anonymous FTP directory?

{% highlight html %}
Answer : PUBLIC_NOTICE.txt
{% endhighlight %}

**Question :** What do we think a possible username could be ?

{% highlight html %}
Answer : mike
{% endhighlight %}

## Exploiting FTP

![image](https://user-images.githubusercontent.com/80531900/171835335-3d88da2d-f075-4ff0-9f6c-ee8bba0539c5.png){: class="bigger-image" }

**Question :** What is the password for the user "mike" ?

{% highlight html %}
Answer : password
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171835385-1d79244d-1559-4bbf-96a6-92d262f0717f.png)

**Question :** What is ftp.txt?

{% highlight html %}
Answer : THM{y0u_g0t_th3_ftp_fl4g}
{% endhighlight %}
