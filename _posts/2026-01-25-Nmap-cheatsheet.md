---
layout: post
title: Nmap cheatsheet
date: 2026-01-25 19:47:08 +0530
author: Aarcha Paul
summary: Nmap cheatsheet
categories: cheatsheet
thumbnail:
tags:
  - enumeration
  - bugbounty
---

# Nmap cheatsheet

## Quick use commands
`nmap -T4 -p- [ip]`: Runs a quick scan over all ports in IP  
`nmap -sC -sV -oN scan.txt -p [open ports] [ip]`: Performs more detailed scan and store results in scan.txt file  
`nmap -sV -sS -sC [ip] -p [open ports]`: Runs in-depth scan on the specified ports
`nmap -sV -p- --max-retries 0 -oN [outputfile.txt] [ip]`: 
`nmap -sU --top-ports 20 -o nmap-udp.out -vvv [ip]`: Checks the top 20 UDP ports (likely to find SNMP, TFTP)

## Scan flags  
-sC : scan using nmap scripts stored in usr/share/nmap/scripts in kali  
-sV : service detection (useful to find and search for vulns associated with)  
-sS : Stealth/Half open/Syn scan [avoid detection by firewall/IDS]  
-sT : TCP Connect/Full open scan [uses 3 way handshaking]  
-sA: ACK scan  
-sF: FIN scan   
-sI: IDLE scan  
-sL: DNS scan (a.k.a. list scan)  
-sN: NULL scan  
-sO: Protocol scan    
-sP: Ping scan  
-sR: RPC scan  
-sW: Windows scan    
-sX: XMAS scan  

## Full list  
`nmap [ip-1] [ip-2]`: Scan multiple targets  
`nmap -F [ip] --top-ports [no-of-ports]`: quick scan of top x ports  
`nmap [ip],7`: scan IPs if within same range  
`nmap [ip]`: Scan an enitre range of ip addresses  
`nmap 192.168.1.1-254`: Scan a Range  
`nmap scanme.domain.name`: Scan a domain  
`nmap 192.168.1.0/24`: Scan using CIDR notation  
`nmap -iL targets.txt`: Scan targets from a file  
`nmap -iR 100`: Scan 100 random hosts  
`nmap --exclude [ips]`: Excude listed host  
`nmap -sn [ip]/24`: ping scan [to find which devices are turned on and off]  
`nmap -sT [ip]`: TCP Connect/Full open scan [uses 3 way handshaking]  
`nmap -sS [ip-addresses]`: Stealth/Half open/Syn scan [avoid detection by firewall/IDS]  
`nmap -sA [ip]`: ACK Probe [detect firewall / IDS]. If RST packet recieved from target, no filtering; if no response, then traffic is being filtered  
`nmap -sP 10.7.1.0/24`: ping multiple ips at once  
`nmap -O [ip]`: OS Detection  
`nmap -A [ip]`: Aggressive Scanning (OS Detection + Version Detection + Script Scanning + traceroute)  
`nmap -sV [ip]`: Service version detection  
`nmap -D [decoy ip] [ip]`: Add Decoy  
`nmap -6 [target]`: Scan an IPv6 Target  
`nmap -F [target]`: Perform a Fast Scan  
`nmap -sU -sT -p U:[ports],T:[ports] [ips]`: Scan ports by specific protocol  
`nmap -r [target]`: Perform a Sequential Port Scan  
`nmap -O --osscan-guess [target]`: Attempt to Guess an Unknown OS  
`nmap -sR [target]`: Perform a RPC Scan  

## NMAP Output types
-oN: normal format  
-oX: XML format; can be used in webmap  
-oS: script kiddie format; uses leetspeak  
-oG: grepable format  
-oA: multiple formats; create files in gnmap, nmap and xml formats  

## Nmap Script scan
`nmap --script ssl-enum-ciphers -p [port] [ip]`: Using nmap script ssl-enum-ciphers to check SSL. Location in kali `usr/share/nmap/scripts`  
`nmap --script "default, safe" [ip]`: Uses the default scripts to scan IP  
`nmap –script=ssh-brute [ip] `: scans IP using nmap built-in script ssh-brute  
`nmap –script=ssh-brute –script-args userdb=userslist.txt,passdb=passlist.txt`: bruteforcing using custom wordlist  
`nmap --script [script.nse] [target]`: Execute Individual Scripts  
`nmap --script [expression] [target]`: Execute Multiple Scripts  
`nmap --script [category] [target]`: Execute Scripts by Category  
`nmap --script [category1,category2,etc]`: Execute Multiple Script Categories  
`nmap --script [script] --script-trace [target]`: Troubleshoot Scripts  
`nmap --script-updatedb`: Update the Script Database  


