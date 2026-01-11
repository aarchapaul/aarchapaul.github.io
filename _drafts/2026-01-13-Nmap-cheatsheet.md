---
layout: post
title: Nmap cheatsheet
date: 2026-01-13 19:47:08 +0530
author: Aarcha Paul
summary: Nmap cheatsheet
categories: cheatsheet
thumbnail:
tags:
  - enumeration
  - bugbounty
---

# Nmap cheatsheet

**References:** 
## intro
- ARP [address resolution protocol]   -> programs use IP addr [logical addr] to send/recieve data but comm actually happens over physical layer using MAC addr. ARP translates IP addr to MAC addr. 
- Done with CAM table
- `arp-scan -l` 	gives virtual MAC addr
- then ping all ip addresses
- gateway IPs ignore, scan rest with nmap

## imp commands
```
nmap -sV -sS -sC 10.10.0.3 -p 22,80,443
```

```
nmap -T4 -p- 10.10.10.3  [initial scan faster]
nmap -sC -sV -oN scan.txt -p 22,80.443,21 10.10.10.3  [more detailed scan]
```

```
nmap -sV -p- --max-retries 0 -oN initialscan.txt [ip]
```

### UDP nmap
It’s always good to check the top UDP ports. OffSec seems to like the “hidden UDP gems” SNMP and TFTP.

```
nmap -sU --top-ports 20 -o nmap-udp.out -vvv $RHOST
```

## table of switches
| Type of scan | Command |
| --- | ---|
| Multiple Targets | `nmap [ip-1] [ip-2]` |
| quick scan of top x ports | `nmap -F [ip] --top-ports [no-of-ports]` |
| if within same range | `nmap 10.0.2.5,7` |
| to scan an enitre range of ip addr | `nmap 10.0.2.1-254` |
| ping scan [to find which devices are turned on and off] | `nmap -sn 10.0.2.1/24` |
| TCP Connect/Full open scan [uses 3 way handshaking] | `nmap -sT  10.0.2.5` |
| Stealth/Half open/Syn scan [avoid detection by firewall/IDS] | arp-scan -l	`nmap -sS [ip-addresses]` |
| ACK Probe [detect firewall / IDS] |  `nmap -sA $ip`    If RST packet recieved from target, no filtering; if no response, then traffic is being filtered |
| scan a specific port | `nmap -p [port-no] 10.0.1.2` |
| service detection (useful to find and search for vulns associated with) | `-sV` |
| OS detection | `-O` |
| Aggressive Scanning [enables os detection, version detection, script scanning and traceroute] | `nmap -A` |
| UDP Scanning | `-sU` No flags for UDP packets; if port open no respone, else msg given ICMP port unreachable |
| Script scan [`usr/share/nmap/scripts`: location in kali] | `nmap -sC `, `nmap -p22 --script "default, safe" `|
| NMAP Output | normal o/p -> `nmap -F scanme.nmap.org -oN normal.txt` , XML format -> `nmap -F scanme.nmap.org -oX <filename>` can be used in webmap , script kiddie format -> `nmap -F scanme.nmap.org -oS <filename>`	uses leetspeak , grepable format -> `nmap -F scanme.nmap.org -oG <filename>`multiple formats -> `nmap -F scanme.nmap.org -oA <filename>`	create files in gnmap, nmap and xml formats |
| --- | ---|

## Nmap Scripting
![nmap-script-scan](Attachments%F0%9F%96%BC/nmap-script-scan.png)
- 
- vuln is a common script
- nmap –script=ssh-brute [site] 
- `nmap –script=ssh-brute –script-args userdb=userslist.txt,passdb=passlist.txt`    bruteforcing using custom wordlist

---

# nmap cheatsheet

- Basic scans: 
> - `nmap <hostip>` - Scan Single IPs
> - `nmap <hostip1> <hostip2>` - Scan Specific IPs 
> - `nmap 192.168.1.1-254` - Scan a Range
> - `nmap scanme.domain.name` - Scan a domain
> - `nmap 192.168.1.0/24` - Scan using CIDR notation
> - `nmap -iL targets.txt` - Scan targets from a file
> - `nmap -iR 100` - Scan 100 random hosts
> - `nmap --exclude 192.168.1.1` - Excude listed host

---
- Scans:
> - `nmap -sP 10.7.1.0/24` : ping multiple ips at once
> - `nmap -p <port(s)> <hostaddress` : scan specific ports
> - `nmap -sT <host>` : TCP (full open) scan - using full 3 way handshake
> - `nmap -sS -p <port(s)> <host>` - Stealthy scan (don't let TCP 3 way handshake complete to avoid getting caught.
> - `nmap -O <host>` : OS Detection
> - `nmap -A <host>`: OS Detection + Version Detection + Script Scanning + traceroute 
> - `nmap -sV <host>` : Service version detection
> - `nmap -D <decoy ip> <host>`: Add Decoy
> - `nmap --script ssl-enum-ciphers -p <port> <host>` : Check SSL

https://github.com/jasonniebauer/Nmap-Cheatsheet

width="560" height="600" src="https://github.com/jasonniebauer/Nmap-Cheatsheet/blob/master/README.md?plain=1"

# Nmap Cheat Sheet
Reference guide for scanning networks with Nmap.

## Basic Scanning Techniques
The `-s` switch determines the type of scan to perform.

| Nmap Switch | Description                 |
|:------------|:----------------------------|
| **-sA**     | ACK scan                    |
| **-sF**     | FIN scan                    |
| **-sI**     | IDLE scan                   |
| **-sL**     | DNS scan (a.k.a. list scan) |
| **-sN**     | NULL scan                   |
| **-sO**     | Protocol scan               |
| **-sP**     | Ping scan                   |
| **-sR**     | RPC scan                    |
| **-sS**     | SYN scan                    |
| **-sT**     | TCP connect scan            |
| **-sW**     | Windows scan                |
| **-sX**     | XMAS scan                   |

1. Scan a Single Target: `nmap [target]`
2. Scan Multiple Targets: `nmap [target1, target2, etc]`
3. Scan a List of Targets: `nmap -iL [list.txt]`
4. Scan a Range of Hosts: `nmap [range of IP addresses]`
5. Scan an Entire Subnet: `nmap [ip address/cdir]`
6. Scan Random Hosts:`nmap -iR [number]
7. Exclude Targets From a Scan: `nmap [targets] --exclude [targets]`
8. 

### Exclude Targets Using a List
```shell
nmap [targets] --excludefile [list.txt]
```

### Perform an Aggresive Scan
```shell
nmap -A [target]
```

### Scan an IPv6 Target
```shell
nmap -6 [target]
```

## Port Scanning Options

### Perform a Fast Scan
```shell
nmap -F [target]
```

### Scan Specific Ports
```shell
nmap -p [port(s)] [target]
```

Scan Ports by Name: `nmap -p [port name(s)] [target]`


### Scan Ports by Protocol
```shell
nmap -sU -sT -p U:[ports],T:[ports] [target]
```

### Scan All Ports
```shell
nmap -p 1-65535 [target]
```

### Scan Top Ports
```shell
nmap --top-ports [number] [target]
```

### Perform a Sequential Port Scan
```shell
nmap -r [target]
```

### Attempt to Guess an Unknown OS
```shell
nmap -O --osscan-guess [target]
```

### Service Version Detection
```shell
nmap -sV [target]
```

### Troubleshoot Version Scan
```shell
nmap -sV --version-trace [target]
```

### Perform a RPC Scan
```shell
nmap -sR [target]
```

## Discovery Options
**Host Discovery**
The `-p` switch determines the type of ping to perform.

| Nmap Switch | Description                 |
|:------------|:----------------------------|
| **-PI**     | ICMP ping                   |
| **-Po**     | No ping                     |
| **-PS**     | SYN ping                    |
| **-PT**     | TCP ping                    |

### Perform a Ping Only Scan
```shell
nmap -sn [target]
```

### Do Not Ping
```shell
nmap -Pn [target]
```

### TCP SYN Ping
```shell
nmap -PS [target]
```

### TCP ACK Ping
```shell
nmap -PA [target]
```

### UDP Ping
```shell
nmap -PU [target]
```

### SCTP INIT Ping
```shell
nmap -PY [target]
```

### ICMP Echo Ping
```shell
nmap -PE [target]
```
### ICMP Timestamp Ping
```shell
nmap -PP [target]
```

### ICMP Address Mask Ping
```shell
nmap -PM [target]
```

### IP Protocol Ping
```shell
nmap -PO [target]
```

### ARP ping
```shell
nmap -PR [target]
```

### Traceroute
```shell
nmap --traceroute [target]
```

### Force Reverse DNS Resolution
```shell
nmap -R [target]
```

### Disable Reverse DNS Resolution
```shell
nmap -n [target]
```

### Alternative DNS Lookup
```shell
nmap --system-dns [target]
```

### Manually Specify DNS Server
Can specify a single server or multiple.
```shell
nmap --dns-servers [servers] [target]
```

### Create a Host List
```shell
nmap -sL [targets]
```

## Port Specification and Scan Order

| Nmap Switch | Description                 |
|:------------|:----------------------------|

## Service/Version Detection

| Nmap Switch | Description                  |
|:------------|:-----------------------------|
| **-sV**     | Enumerates software versions |

## Script Scan

| Nmap Switch | Description             |
|:------------|:------------------------|
| **-sC**     | Run all default scripts |

## OS Detection

| Nmap Switch | Description                 |
|:------------|:----------------------------|

## Timing and Performance
The `-t` switch determines the speed and stealth performed.

| Nmap Switch | Description                 |
|:------------|:----------------------------|
| **-T0**     | Serial, slowest scan        |
| **-T1**     | Serial, slow scan           |
| **-T2**     | Serial, normal speed scan   |
| **-T3**     | Parallel, normal speed scan |
| **-T4**     | Parallel, fast scan         |

Not specifying a `T` value will default to `-T3`, or normal speed.

## Firewall Evasion Techniques

### Firewall/IDS Evasion and Spoofing
| Nmap Switch | Description                 |
|:------------|:----------------------------|

### Fragment Packets
```shell
nmap -f [target]
```

### Specify a Specific MTU
```shell
nmap --mtu [MTU] [target]
```

### Use a Decoy
```shell
nmap -D RND:[number] [target]
```

### Idle Zombie Scan
```shell
nmap -sI [zombie] [target]
```

### Manually Specify a Source Port
```shell
nmap --source-port [port] [target]
```

### Append Random Data
```shell
nmap --data-length [size] [target]
```

### Randomize Target Scan Order
```shell
nmap --randomize-hosts [target]
```

### Spoof MAC Address
```shell
nmap --spoof-mac [MAC|0|vendor] [target]
```

### Send Bad Checksums
```shell
nmap --badsum [target]
```
  
## Advanced Scanning Functions

### TCP SYN Scan
```shell
nmap -sS [target]
```

### TCP Connect Scan
```
nmap -sT [target]
```

### UDP Scan
```shell
nmap -sU [target]
```

### TCP NULL Scan
```shell
nmap -sN [target]
```

### TCP FIN Scan
```shell
nmap -sF [target]
```

### Xmas Scan
```shell
nmap -sA [target]
```

### TCP ACK Scan
```shell
nmap -sA [target]
```

### Custom TCP Scan
```shell
nmap --scanflags [flags] [target]
```

### IP Protocol Scan
```shell
nmap -sO [target]
```

### Send Raw Ethernet Packets
```shell
nmap --send-eth [target]
```

### Send IP Packets
```shell
nmap --send-ip [target]
```

## Timing Options

### Timing Templates
```shell
nmap -T[0-5] [target]
```

### Set the Packet TTL
```shell
nmap --ttl [time] [target]
```

### Minimum NUmber of Parallel Operations
```shell
nmap --min-parallelism [number] [target]
```

### Maximum Number of Parallel Operations
```shell
nmap --max-parallelism [number] [target]
```

### Minimum Host Group Size
```shell
nmap --min-hostgroup [number] [targets]
```

### Maximum Host Group Size
```shell
nmap --max-hostgroup [number] [targets]
```

### Maximum RTT Timeout
```shell
nmap --initial-rtt-timeout [time] [target]
```

### Initial RTT Timeout
```shell
nmap --max-rtt-timeout [TTL] [target]
```

### Maximum Number of Retries
```shell
nmap --max-retries [number] [target]
```

### Host Timeout
```shell
nmap --host-timeout [time] [target]
```

### Minimum Scan Delay
```shell
nmap --scan-delay [time] [target]
```

### Maxmimum Scan Delay
```shell
nmap --max-scan-delay [time] [target]
```

### Minimum Packet Rate
```shell
nmap --min-rate [number] [target]
```

### Maximum Packet Rate
```shell
nmap --max-rate [number] [target]
```

### Defeat Reset Rate Limits
```shell
nmap --defeat-rst-ratelimit [target]
```

## Output Options

| Nmap Switch | Description   |
|:------------|:--------------|
| ``-oN``     | Normal output |
| ``-oX``     | XML output    |
| ``-oA``     | Normal, XML, and Grepable format all at once |

### Save Output to a Text File
```shell
nmap -oN [scan.txt] [target]
```

### Save Output to a XML File
```shell
nmap -oX [scan.xml] [target]
```

### Grepable Output
```shell
nmap -oG [scan.txt] [target]
```

### Output All Supported File Types
```shell
nmap -oA [path/filename] [target]
```

### Periodically Display Statistics
```shell
nmap --stats-every [time] [target]
```

### 1337 Output
```shell
nmap -oS [scan.txt] [target]
```

## Compare Scans

### Comparison Using Ndiff
```shell
ndiff [scan1.xml] [scan2.xml]
```

### Ndiff Verbose Mode
```shell
ndiff -v [scan1.xml] [scan2.xml]
```

### XML Output Mode
```shell
ndiff --xml [scan1.xml] [scan2.xml]
```

## Troubleshooting and Debugging

### Debugging
```shell
nmap -d [target]
```

### Display Port State Reason
```shell
nmap --reason [target]
```

### Only Display Open Ports
```shell
nmap --open [target]
```

### Trace Packets
```shell
nmap --packet-trace [target]
```

### Display Host Networking
```shell
nmap --iflist
```

### Specify a Network Interface
```shell
nmap -e [interface] [target]
```

## Nmap Scripting Engine

### Execute Individual Scripts
```shell
nmap --script [script.nse] [target]
```

### Execute Multiple Scripts
```shell
nmap --script [expression] [target]
```

### Execute Scripts by Category
```shell
nmap --script [category] [target]
```

### Execute Multiple Script Categories
```shell
nmap --script [category1,category2,etc]
```

### Troubleshoot Scripts
```shell
nmap --script [script] --script-trace [target]
```

### Update the Script Database
```shell
nmap --script-updatedb
```


**Reference Sites**
- [X] [Nmap - The Basics](https://www.youtube.com/watch?v=_JvtO-oe8k8)  
- [ ] https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/  
- [ ] [Top 32 Nmap Command](https://www.cyberciti.biz/security/nmap-command-examples-tutorials/)  
- [ ] [Nmap Linux man page](https://linux.die.net/man/1/nmap)  
- [ ] [29 Practical Examples of Nmap Commands](https://www.tecmint.com/nmap-command-examples/)  
- [ ] https://medium.com/@infosecsanyam/nmap-cheat-sheet-nmap-scanning-types-scanning-commands-nse-scripts-868a7bd7f692
- [ ] https://www.cheatography.com/netwrkspider/cheat-sheets/nmap-cheatsheet/
- [ ] https://highon.coffee/blog/nmap-cheat-sheet/
- [ ] https://resources.infosecinstitute.com/nmap-cheat-sheet/
- [ ] https://www.andreafortuna.org/2018/03/12/nmap-my-own-cheatsheet/
- [ ] https://hackersonlineclub.com/nmap-commands-cheatsheet/
- [ ] https://www.stationx.net/nmap-cheat-sheet/
- [ ] http://nmapcookbook.blogspot.com/2010/02/nmap-cheat-sheet.html
