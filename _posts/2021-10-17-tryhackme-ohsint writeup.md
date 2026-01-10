---
layout: post
title: TryHackMe writeup - OhSINT
date: 2021-10-16 15:00:18
summary: This is my writeup for the TryHackMe challenge OhSINT
categories: TryHackMe
thumbnail: ohsint
tags:
 - TryHackMe
 - writeup
---
A downloadable task file is given with this challenge. It contains an image as shown below. ![WindowsXP.jpg](/assets/WindowsXP.jpg)
On running exiftool, we find the name of a person `OWoodflint`.
![exiftool](/assets/ohsint-exiftool.png)
A quick google search gives us a twitter account, where the person has shared a BSSID.
> From my house I can get free wifi ;D  
> Bssid: B4:5D:50:AA:86:41 - Go nuts!
 
On going to wigle.net/ and typing the BSSID into advanced search, we get the person's location and SSID.
 
Going back to google search of OWoodflint, we get the github account and a wordpress blog. In github we get his email ID. From the blog we get his holiday location and password.  

1. What is this users avatar of?  
    cat
2. What city is this person in?  
    London
3. Whats the SSID of the WAP he connected to?  
    UnileverWiFi
4. What is his personal email address?  
    OWoodflint@gmail.com
5. What site did you find his email address on?  
    Github
6. Where has he gone on holiday?  
    New York
7. What is this persons password?  
    pennYDr0pper.!