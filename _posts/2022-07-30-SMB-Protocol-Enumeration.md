---
layout: post
title: SMB Protocol Enumeration
date: 2022-07-30 04:58:27 +0530
author: Aarcha Paul
summary: 
categories: cheatsheet
thumbnail: 
tags:
 - enumeration
 - reconnaisance
 - bugbounty
 - oscp
---

## What is SMB Protocol?
SMB stands for Server Message Block, which usually works on port 445. It used to be called Common Internet File System previously which was included in Microsoft Windows NT 4.0 in 1996. It is a file sharing protocol used for sharing file and peripherals (e.g. printers) between computers in a network. One of the most famous attacks EternalBlue was done by exploiting SMB protocol.

## Working
SMB follows a client-server protocol. Clients using SMB connect to a supporting server using NetBIOS over TCP/IP, IPX/SPX, or NetBEUI. The initial establishment of the connection between client and server is required for exchanging information.  Subsequent data transport is controlled by TCP protocol. Once the connection is established, the client can open, read/write, and access files similar to the file system on a local computer.

## Enumeration Methods
There are many different tools available to enumerate vulnerable SMB service. The main aim is to check if file reading, writing or uploading access is available. 
1. **smbclient :** smbclient is a client that is part of the Samba software suite. It communicates with a LAN Manager server, offering an interface similar to that of the ftp  program. Usage - `smbclient -L //ip-address` and enter a blank password
2. smbmap : This tool was based on a python library PySMB but has since switched to Impacket. This tool was designed with pen testing in mind, and is intended to simplify searching for potentially sensitive data across large networks. Usage - `smbmap -H ip-address` 
3. crackmapexec : This tool is noteworthy because it shows undelying OS. 
4. **Metasploit :** The popular tool metasploit has an auxillary module called scanner. This can be used for to enumerate smb vulnerabilities.
	`use auxiliary/scanner/smb/smb_version`
	`set RHOSTS ip-address`
	`options`
	`run`
5. **nmap scripts :** Nmap has many built-in scripts to enumerate smb vulnerabilities. If you have nmap installed, it can be viewed in `/usr/share/nmap/scripts` directory.
	`cd /usr/share/nmap/scripts; ls |  grep smb`

![](https://www.infosecademy.com/wp-content/uploads/2021/01/image-23.png)
