---
layout: post
title: 
date: 2022-08-13 21:13:45 +0530
author: Aarcha Paul
summary: 
categories: TryHackMe
thumbnail: jekyll
tags:
  - TryHackMe
  - writeup
---
This is the Write-Up about OWASP Top 10 Room in TryHackMe:

## Introduction
Learn one of the OWASP vulnerabilities every day for 10 days in a row. A new task will be revealed every day, where each task will be independent from the previous one. These challenges will cover each OWASP topic:

- Day 1) Injection
- Day 2) Broken Authentication
- Day 3) Sensitive Data Exposure
- Day 4) XML External Entity
- Day 5) Broken Access Control
- Day 6) Security Misconfiguration
- Day 7) Cross-site Scripting
- Day 8) Insecure Deserialization
- Day 9) Components with Known Vulnerabilities
- Day 10) Insufficent Logging & Monitoring

The challenges are designed for beginners and assume no previous knowledge of security. Some tasks will have you learning by doing, often through hacking a virtual machine. Before start to do the challanges, Connect to TryHackMe network with OpenVPN to get IP address for each virtual machine.

## Day 1 : Injection

To complete the questions below, Deploy virtual machine and navigate to http://MACHINE_IP/evilshell.php

![evilshell.php](/assets/evilshell_php.png)

### Challenge :

Questions :
1. What strange text file is in the website root directory?
2. How many non-root/non-service/non-daemon users are there? 
3. What user is this app running as? 
4. What is the user's shell set as? 
5. What version of Ubuntu is running? 
6. Print out the MOTD. What favorite beverage is shown? 

### Explanation :

Default website root directory of most Linux is `var/www/html` , first use `pwd` command to know current directory position. after that use `ls` command to list inside `var/www/html`. Besides `evilshell.php` there is another strange file.
![/var/www/html](/assets/var_www_html.png)

User account information in Linux machine stored in `/etc/passwd directory`. I use `awk` instead of cat to give simpler output :

`awk -F':' '/x/{print $1}' /etc/passwd`

![/etc/passwd](/assets/etc_passwd.png)

in `/etc/passwd` output there are no non-root/non-service/non-daemon users. To check which user is running this application is with `whoami` command
![whoami](/assets/whoami.png)

User’s shell stored in /etc/passwd with user information, because we already knew which user that running this application we can use cat and grep.

`cat /etc/passwd | grep www-data`

![user info](/assets/userinfo.png)

OS version in Linux stored in file named `lsb-release`, `os-release` or `*-release` (* depends on Distribution i.e. redhat). For this case, let’s use `os-release` with this command `cat /etc/os-release`.
![os-release](/assets/os-release.png)

MoTD (Message of The Day) message can be customized based on needs by modifying the file or script within the motd directory. They give hint for last question and it says `00-header`, which is one of the motd files. use    `locate 00-header` to know the directory (and i’m really sure if it’s in `/etc/update-motd.d/00-header`) then use cat command.
![MoTD](/assets/motd.png)

## Day 2 : Broken Authentication

    To see this in action go to `http://MACHINE_IP:8888`

![register page](/assets/register-page.png)

### Challenge :

Questions :
1. What is the flag that you found in darren's account?
2. Now try to do the same trick and see if you can login as arthur.
3. What is the flag that you found in arthur's account? 

### Explanation :

When first try to register with username “darren”, it will be show an error page because username already registered.

But if we register with username “ darren” (with space in starting), it will display login page which means registration process succeed. Try to login with “ darren” , you will logged on as “darren” with flag in web page.
![logged in as “ darren”](/assets/darren.png)

Do the same technique with user “ arthur” , if succeed logged in as “arthur”, it will show the flag in web page.
arthur

## Day 3 : Sensitive Data Exposure

Deploy machine and navigate to machine’s IP in web browser
![web page](/assets/webpage.png)

### Challenge :

Questions :
1. Have a look around the webapp. The developer has left themselves a note indicating that there is sensitive data in a specific directory. What is the name of the mentioned directory? 2. Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data? 3. Use the supporting material to access the sensitive data. What is the password hash of the admin user? 4. Crack the hash.
What is the admin's plaintext password? 5. Login as the admin. What is the flag? 

### Explanation :

TryHackMe gives a hint if we have to take a look source code in /login, edit url to `http://MACHINE_IP/login` , then inspect the page to see the source code and there is some interesting notes.
![inspect login page](/assets/inspect-login.png)

Inside `http://MACHINE_IP/assets` there is a file named `webapp.db`, download that file and see what’s inside.  
![/assets](/assets/assets.png)

After open `webapp.db` file with `sqlite3`, there are some users information such a user ID, username and password (in hash).  
![webapp.db](/assets/webapp_db.png)

Because password for admin user in hash form, decrypt it using hash cracker in `https://crackstation.net/` the result will show the type of encryption used and plaintext password.  
Login with user `admin` and there is a flag.
![admin](/assets/admin.png)

## Day 4 : XML External Entity
Deploy a machine and go to the `http://[IP_MACHINE]`

xxe page

### Challenges :

-Question in Task 14 and Task 15 can be answered by reading supporting material-Questions : 
1. Try to display your own name using any payload. 
2. See if you can read the /etc/passwd 
3. What is the name of the user in /etc/passwd 
4. Where is falcon's SSH key located? 
5. What are the first 18 characters for falcon's private key

### Explanation :

First try to display our name using payload[1] in web pages. type or paste the payload[1] in input field.
Payload[1]

And here’s the output after executed the payload
Output from Payload[1]

Use payload[2] to read /etc/passwd in the machine and find the user in /etc/passwd
Payload[2]

Content in/etc/passwdshown after executed payload[2] in input field.
output from payload[2]

Use payload[2] to read user falcon’s ssh key. By default, the private key is stored in ~/. ssh/id_rsa within your user’s home directory, edit payload[2] change /etc/passwd to /home/falcon/.ssh/id_rsa.

    More info about private key

Payload[2] — Read SSH Key

After executed payload[2] in input field, it will shown user falcon’s SSH Key.
ssh key

## Day 5 : Broken Access Control
IDOR

    Deploy a machine and go to the http://[IP_MACHINE]

Login Page

### Challenges :

Questions :
1. Deploy the machine and go to http://[ip_machine] - Login with the username being noot and the password test1234.
2. Look at other users notes. What is the flag?

### Explanation :

First, after deploy the machine try to login with provided credential which is username : noot and password : test1234. there is a note in user noot page I am noot!.
user noot page

    “Some applications create an id on client-side and then send the in create request to server. This id value can be number such as “-1”, “0” or anything. The existing id values change with the previously created objects’ id. So you can delete / edit other users’ objects using IDOR vulnerability.” — bugcrowd.com

On the user noot’s url there is a parameter/note.php?note=1 based on material and quotes above about IDOR, parameter value can be changed to another value such as “-1”, “0” or anything to create request to server, change parameter note=1 to note=0 and there is a flag.

## Day 6 : Security Misconfiguration

Security misconfigurations include:

    Poorly configured permissions on cloud services, like S3 buckets
    Having unnecessary features enabled, like services, pages, accounts or privileges
    Default accounts with unchanged passwords
    Error messages that are overly detailed and allow an attacker to find out more about the system
    Not using HTTP security headers, or revealing too much detail in the Server: HTTP header

This vulnerability can often lead to more vulnerabilities, such as default credentials giving you access to sensitive data, XXE or command injection on admin pages.

    Deploy the VM, and hack in by exploiting the Security Misconfiguration!

Pensive Notes webapp

    ### Challenges :

Question : 
1. Hack into the webapp, and find the flag! 

### Explanation :

This Challenge focusing on Default accounts with unchanged passwords, the simple way to find web app default username and password is by Googling it.
as simple as that

    NinjaJc01/PensiveNotes-README.md — app’s documentation usually stored in readme file

After get default credential which is pensive:PensiveNotes login with it and there is a flag, or try to change default password with new password and try to login with the new password, it works!

## Day 7 : XSS (Cross-site Scripting)

Cross-site scripting, also known as XSS is a security vulnerability typically found in web applications. It’s a type of injection which can allow an attacker to execute malicious scripts and have it execute on a victim’s machine. XSS is possible in Javascript, VBScript, Flash and CSS.

    Deploy the VM

Register first, because it will needed when perform stored XSS
XSS Playground

### Challenges :

Questions : 1. Go to http://MACHINE_IP/reflected and craft a reflected XSS payload that will cause a popup saying "Hello". 
2. On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address. 
3. Now navigate to http://MACHINE_IP/stored and make an account. Then add a comment and see if you can insert some of your own HTML. 
4. On the same page, create an alert popup box appear on the page with your document cookies. 
5. Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript. 

### Explanation :

Reflected XSS

    Reflected XSS — the malicious payload is part of the victims request to the website. The website includes this payload in response back to the user. To summarise, an attacker needs to trick a victim into clicking a URL to execute their malicious payload.

First, craft a reflected XSS payload that will cause a popup saying "Hello", for this case i use alert and the payload is like this :

<script>alert(“Hello”)</script>

if the payload executed from search field in reflected xss playground web page, it will display an alert pop-up with the 1st flag in it.

Because this is reflected xss, the payload will shown in url.
url

On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address. for this case the payload will inclode javascript window.location.hostname to returns the domain name of the web host, the payload would be like this :

    More info about Javascript window loaction

<script>alert(“window.location.hostname”)</script>

if the payload successfully executed, it will shown the 2nd flag in alert pop-up, and the url will shown the payload too.
url payload 2nd flag

Stored XSS

    Stored XSS — the most dangerous type of XSS. This is where a malicious string originates from the website’s database. This often happens when a website allows user input that is not sanitised (remove the “bad parts” of a users input) when inserted into the database.

When perform Stored XSS, it required to have an account and see if HTML script can inserted in comment section. Try to input the comment with HTML script. for this scenario just put the simple script :

<h3>Hello</h3>

It will shown in the comment section, but with different size also there is a 3rd flag.
comment section

Next is create an alert popup box with javascript cookie, create the alert payload and add document.cookie inside alert.

    More information about Javascript cookie

<script>alert(document.cookie)</script>

When the payload successfully executed, it will shown alert pop up box with the 4th flag
alert popup

DOM XSS

    DOM-Based XSS — DOM stands for Document Object Model and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. A web page is a document and this document can be either displayed in the browser window or as the HTML source.

Last is to Change “XSS Playground” to “I am a hacker” by adding a comment and using Javascript. here is the payload :
Inspect page to know the id for “XSS Playground”

<script>document.querySelector('#thm-title').textContent = 'I am a hacker'</script>

Some good source about the payload above :

    HTML DOM querySelector() — The querySelector() method only returns the first element that matches the specified selectors

    CSS Selector — #thm-title Selects the element with id=”thm-title”

    HTML DOM Text Content Property — If you set the textContent property, any child nodes are removed and replaced by a single Text node containing the specified string

After the payload executed, the pages will change into ‘I am a hacker’ on the top left side and the 5th flag will appear.
defaced page

## Day 8 : Insecure Deserialization
Insecure Deserialization

    Deploy the VM, navigate to http://MACHINE_IP, create an account on the machine through sign-up (Join us) menu.

Home Page

### Challenges :

Questions : 
1. 1st flag (cookie value)? 
2. 2nd flag (admin dashboard)?

### Explanation :

Cookies
Cookies

Tiny pieces of data, these are created by a website and stored on the user’s computer. Websites use these cookies to store user-specific behaviours like items in their shopping cart or session IDs.

After create an account and logged in, user will be directed to profile page
profile page

Right-Click the Page and press “Inspect”, Go to Application tab > Storage > Cookies. There are registrationTimestamp, username, password, sessionId, and userType.
cookie

notice the value in sessionId, there are == at the end of the line, this indicates base64 encode, which means the string can be decoded use this command and there is a flag.

echo -PUT THE STRING HERE- | base64 -d

decode

Modify the cookie value by change userType from user to admin and refresh the page.

After refresh the page, the page will redirect to admin dashboard and there is a 2nd flag.
admin dashboard

RCE (Remote Code Execution)

    One of the most dangerous types of computer vulnerabilities. It allows an attacker to remotely run malicious code within the target system on the local network or over the Internet — Kaspersky Encyclopedia

To do this action, back to user first by change the userType in inspect from admin to user.
set back to user

In the user profile page, click “Exchange your vim” URL [1], A cookie is encoded and stored within the browser. When visit the feedback form [2], the value of this cookie is decoded and then deserialized.
Use profile page

Set netcat listener on attacker machine (Kali Linux) using netcat -nvlp 4444 and create payload with source code from CMNatic.
rce.py

Modify the source code to replace your “YOUR_TRYHACKME_VPN_IP” with your TryHackMe VPN IP.
fill IP address

After that run the python3 rce.py to execute the payload and the output will be encoded with base64, paste the output string to encodePayload value in cookie browser.
user profile cookie in feedback page

Refresh the page, and look at the netcat listener that has been set up before, there must be a shell, and find flag.txt to get the flag
we are in

## Day 9 : Components With Known Vulnerabilities

    Deploy the VM, navigate to http://MACHINE_IP

online cse bookstore

    ### Challenges :

Question : 
1. How many characters are in /etc/passwd (use wc -c /etc/passwd to get the answer) 

### Explanation :

From the home page there are some information such a site created using PHP and MySQL and the webapps using Bootstrap. The hint says its a bookstore application and check for recent unauthenticated bookstore app rce’s. Find the exploit in exploit-db.com or searchsploit if using kali terminal.
exploit-db

There are 3 recent exploit for ‘book store’, but based on the hint above there is only 1 match, that is Online Book Store 1.0 — Unauthenticated Remote Code Execution and it has an exploit that can be downloaded. Because the exploit is a python file, excecute it withpython3 47887.py and the output will show how to use this exploit.
usage info

Modify the command to add an url in the end of line like thispython3 47887.py http://10.10.143.112 after that, execute again the payload and the shell will appear.
we are in

Use wc -c /etc/passwdto get the answer.

## Day 10 : Insufficient Logging and Monitoring

    Download the log and analysing this sample log file.

log

### Challenges :

Question : 
1. What IP address is the attacker using? 
2. What kind of attack is being carried out? 

### Explanation :

Categorize or Read the log by column :

1. HTTP Respond — More info (HTTP Respond Code) 
2. Respond Info
3. IP Address (Source) 
4. Username
5. Timestamp
6. Action / Activity

Respond 200 OK means status response code indicates that the request has succeeded, in this case is login activity and every IP address with respond code 200 has different username.

Respond 401 Unauthorized means error status response code indicates that the request has not been applied because it lacks valid authentication credentials for the target resource.

From the log IP49.99.13.16 try to login with superuser cred such root, admin, and etc. but the respond code is 401 which means it lacks valid authentication credentials and the possibility is because wrong password.

IP 49.99.13.16 submitting many passwords or passphrases with the hope of eventually guessing correctly and this action indicates the IP 49.99.13.16 did Brute Force Attack. More info about Brute-force Attack.

Finish, MR. Anomali