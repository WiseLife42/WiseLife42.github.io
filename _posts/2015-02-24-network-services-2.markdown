---
title: "[TryHackMe][CompTIA_Pentest+][Network_Services_2]"
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
description: Network_Services_2
---

## Summary:

Enumerating and Exploiting More Common Network Services & Misconfigurations.

#### Tasks
- [Understanding NFS](#understanding-nfs)
- [Enumerating NFS](#enumerating-nfs)
- [Exploiting NFS](#exploiting-nfs)
- [Understanding SMTP](#understanding-smtp)
- [Enumerating SMTP](#enumerating-smtp)
- [Exploiting SMTP](#exploiting-smtp)
- [Understanding MySQL](#understanding-mysql)
- [Enumerating MySQL](#enumerating-mysql)
- [Exploiting MySQL](#exploiting-mysql)

---

## Understanding NFS

**Question :** What does NFS stand for ? 

{% highlight html %}
Answer : Network File System
{% endhighlight %}

**Question :** What process allows an NFS client to interact with a remote directory as though it was a physical device ?

{% highlight html %}
Answer : Mounting
{% endhighlight %}

**Question :** What does NFS use to represent files and directories on the server ?

{% highlight html %}
Answer : file handle
{% endhighlight %}

**Question :** What protocol does NFS use to communicate between the server and client ?

{% highlight html %}
Answer : RPC
{% endhighlight %}

**Question :** What two pieces of user data does the NFS server take as parameters for controlling user permissions ? Format: parameter 1 / parameter 2

{% highlight html %}
Answer : user id / group id
{% endhighlight %}

**Question :** Can a Windows NFS server share files with a Linux client ? (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

**Question :** Can a Linux NFS server share files with a MacOS client ? (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

**Question :** What is the latest version of NFS ?

{% highlight html %}
Answer : 4.2
{% endhighlight %}

## Enumerating NFS

![image](https://user-images.githubusercontent.com/80531900/171988815-4fa9c15e-9b36-436c-8845-d19a1b5930ba.png)

**Question :** Conduct a thorough port scan scan of your choosing, how many ports are open ?

{% highlight html %}
Answer : 7
{% endhighlight %}

**Question :** Which port contains the service we're looking to enumerate ?

{% highlight html %}
Answer : 2049
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171988819-2d0afa38-e022-4a1a-af5b-a6a7f27214f9.png)

**Question :** Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share ?

{% highlight html %}
Answer : /home
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171988824-6239019f-dbc8-4d44-a4c8-f750f5ce4054.png)

**Question :** Then, use the mount command we broke down earlier to mount the NFS share to your local machine. Change directory to where you mounted the share- what is the name of the folder inside ?

{% highlight html %}
Answer : cappucino
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171988827-085615a3-f1b1-4ea4-9cb4-3a599d869b90.png)

**Question :** Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server ?

{% highlight html %}
Answer : .ssh
{% endhighlight %}

**Question :** Which of these keys is most useful to us ?

{% highlight html %}
Answer : id_rsa
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171988838-e2802ea7-9af6-4e29-8c58-94f26943f570.png)

**Question :** Can we log into the machine using ssh -i <key-file> <username>@<ip> ? (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

## Exploiting NFS
    
* Download file : https://github.com/polo-sec/writing/blob/master/Security Challenge Walkthroughs/Networks 2/bash
    
![image](https://user-images.githubusercontent.com/80531900/171988982-73a65b4e-7784-4df8-9001-6b65af50e36e.png)

**Question :** Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +[permission] bash". What letter do we use to set the SUID bit set using chmod ?
    
{% highlight html %}
Answer : s 
{% endhighlight %}
    
**Question :** What does the permission set look like? Make sure that it ends with -sr-x.

{% highlight html %}
Answer : -rwsr-sr-x 
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171988998-fecf3833-3128-4466-b443-de43ec86620f.png)

**Question :** Great! If all's gone well you should have a shell as root! What's the root flag ?

{% highlight html %}
Answer : THM{nfs_got_pwned}
{% endhighlight %}

## Understanding SMTP

**Question :** What does SMTP stand for ?

{% highlight html %}
Answer : Simple Mail Transfer Protocol
{% endhighlight %}

**Question :** What does SMTP handle the sending of ? (answer in plural)

{% highlight html %}
Answer : emails
{% endhighlight %}

**Question :** What is the first step in the SMTP process ?

{% highlight html %}
Answer : SMTP handshake
{% endhighlight %}

**Question :** What is the default SMTP port ?

{% highlight html %}
Answer : 25
{% endhighlight %}

**Question :** Where does the SMTP server send the email if the recipient's server is not available ?

{% highlight html %}
Answer : smtp queue
{% endhighlight %}

**Question :** On what server does the Email ultimately end up on ?

{% highlight html %}
Answer : POP/IMAP
{% endhighlight %}

**Question :** Can a Linux machine run an SMTP server ? (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

**Question :** Can a Windows machine run an SMTP server ? (Y/N)

{% highlight html %}
Answer : Y
{% endhighlight %}

## Enumerating SMTP
    
![image](https://user-images.githubusercontent.com/80531900/171989013-3bf171cc-fa54-475f-b15a-9101effee25b.png)

**Question :** First, lets run a port scan against the target machine, same as last time. What port is SMTP running on ?

{% highlight html %}
Answer : 25
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989014-e687b1f9-dbec-46e3-8827-1d10053ba045.png)

**Question :** What command do we use to do this ? 

{% highlight html %}
Answer : msfconsole
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989025-23906705-e129-4cb4-883e-a5fe624769cf.png){: class="bigger-image" }

**Question :** Let's search for the module "smtp_version", what's it's full module name ? 

{% highlight html %}
Answer : auxiliary/scanner/smtp/smtp_version
{% endhighlight %}

**Question :** Great, now- select the module and list the options. How do we do this ?

{% highlight html %}
Answer : options
{% endhighlight %}

**Question :** Have a look through the options, does everything seem correct? What is the option we need to set ?

{% highlight html %}
Answer : RHOSTS
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989042-c2aa5889-b881-4abb-a927-bce95efe2718.png)

**Question :** Set that to the correct value for your target machine. Then run the exploit. What's the system mail name ?

{% highlight html %}
Answer : polosmtp.home
{% endhighlight %}

**Question :** What Mail Transfer Agent (MTA) is running the SMTP server? This will require some external research.

{% highlight html %}
Answer : Postfix
{% endhighlight %}

![image](https://user-images.githubusercontent.com/80531900/171989045-aa016976-1026-4e3b-8f99-53abd35846bc.png){: class="bigger-image" }
    
* Download : https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt

**Question :** Let's search for the module "smtp_enum", what's it's full module name ?

{% highlight html %}
Answer : auxiliary/scanner/smtp/smtp_enum
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989089-8dc791e0-4b99-4dff-8880-e6cc9fde36c8.png){: class="bigger-image" }

**Question :** What option do we need to set to the wordlist's path ?

{% highlight html %}
Answer : USER_FILE
{% endhighlight %}

**Question :** Once we've set this option, what is the other essential paramater we need to set ?

{% highlight html %}
Answer : RHOSTS
{% endhighlight %}

**Question :** Okay! Now that's finished, what username is returned ?

{% highlight html %}
Answer : administrator
{% endhighlight %}

## Exploiting SMTP
    
![image](https://user-images.githubusercontent.com/80531900/171989094-e1e06902-0432-4574-bfe6-21eba3eadf7a.png)
  
![image](https://user-images.githubusercontent.com/80531900/171989098-68aafdf5-29d7-49d2-b747-9153e84c6fb3.png)

**Question :** What is the password of the user we found during our enumeration stage ?

{% highlight html %}
Answer : alejandro
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989112-0595face-c2ab-41c7-b4bb-2c6594b8092d.png)

**Question :** Great! Now, let's SSH into the server as the user, what is contents of smtp.txt

{% highlight html %}
Answer : THM{who_knew_email_servers_were_c00l?}
{% endhighlight %}

## Understanding MySQL

**Question :** What type of software is MySQL ?

{% highlight html %}
Answer : relational database management system
{% endhighlight %}

**Question :** What language is MySQL based on ?

{% highlight html %}
Answer : SQL
{% endhighlight %}

**Question :** What communication model does MySQL use ?

{% highlight html %}
Answer : client-server
{% endhighlight %}

**Question :** What is a common application of MySQL ?

{% highlight html %}
Answer : back end database
{% endhighlight %}

**Question :** What major social network uses MySQL as their back-end database ? This will require further research.

{% highlight html %}
Answer : Facebook
{% endhighlight %}

## Enumerating MySQL
    
![image](https://user-images.githubusercontent.com/80531900/171989121-1a8b0ae0-b9ee-411f-8f84-cb1a3c1a7e69.png)

**Question :** As always, let's start out with a port scan, so we know what port the service we're trying to attack is running on. What port is MySQL using ?

{% highlight html %}
Answer : 3306
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989146-c627b078-1cdc-4ba6-a6af-df89bdc483e9.png)
    
![image](https://user-images.githubusercontent.com/80531900/171989153-edca5b69-70e7-4a80-86a9-2477d03c99df.png){: class="bigger-image" }

**Question :** Search for, select and list the options it needs. What three options do we need to set? (in descending order).

{% highlight html %}
Answer : PASSWORD/RHOSTS/USERNAME
{% endhighlight %}

**Question :** Run the exploit. By default it will test with the "select version()" command, what result does this give you ?

{% highlight html %}
Answer : 5.7.29-0ubuntu0.18.04.1
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989181-21570108-d58f-479d-b847-db70d3d82f4b.png)

**Question :** Change the "sql" option to "show databases". how many databases are returned ?

{% highlight html %}
Answer : 4
{% endhighlight %}

## Exploiting MySQL
    
![image](https://user-images.githubusercontent.com/80531900/171989192-9198adfd-c998-4b1f-afd2-7bc28c1c7eb3.png){: class="bigger-image" }

**Question :** First, let's search for and select the "mysql_schemadump" module. What's the module's full name ?

{% highlight html %}
Answer : auxiliary/scanner/mysql/mysql_schemadump
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989201-cf71310d-5c20-401a-b99f-427e70086221.png)

![image](https://user-images.githubusercontent.com/80531900/171989207-bba70794-986c-4c29-a23d-f1f04a2d665b.png)

**Question :** What's the name of the last table that gets dumped ?

{% highlight html %}
Answer : x$waits_global_by_latency
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989224-03fb33fa-4736-4404-b1ff-77802dd640ce.png){: class="bigger-image" }

**Question :** Awesome, you have now dumped the tables, and column names of the whole database. But we can do one better... search for and select the "mysql_hashdump" module. What's the module's full name ?

{% highlight html %}
Answer : auxiliary/scanner/mysql/mysql_hashdump
{% endhighlight %}

**Question :** Again, I'll let you take it from here. Set the relevant options, run the exploit. What non-default user stands out to you ?

{% highlight html %}
Answer : carl
{% endhighlight %}

**Question :** What is the user/hash combination string ?

{% highlight html %}
Answer : carl:*EA031893AA21444B170FC2162A56978B8CEECE18
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989236-d9621ac7-0f59-4fae-ae20-dd5bae3873d6.png)

**Question :** Now, we need to crack the password! Let's try John the Ripper against it using: "john hash.txt" what is the password of the user we found ?

{% highlight html %}
Answer : doggie
{% endhighlight %}
    
![image](https://user-images.githubusercontent.com/80531900/171989239-08c03359-6b53-45ea-b4cb-1534bdfbaad6.png)

**Question :** What's the contents of MySQL.txt

{% highlight html %}
Answer : THM{congratulations_you_got_the_mySQL_flag}
{% endhighlight %}
