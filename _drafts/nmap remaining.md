nmap remaining 


## Host Discovery
The `-p` switch determines the type of ping to perform.

 **-PI**      ICMP ping                   
 **-Po**      No ping                     
 **-PS**      SYN ping                    
 **-PT**      TCP ping                    

### Perform a Ping Only Scan

nmap -sn [target]
### Do Not Ping

nmap -Pn [target]
### TCP SYN Ping

nmap -PS [target]
### TCP ACK Ping

nmap -PA [target]
### UDP Ping

nmap -PU [target]
### SCTP INIT Ping

nmap -PY [target]
### ICMP Echo Ping

nmap -PE [target]

### ICMP Timestamp Ping

nmap -PP [target]
### ICMP Address Mask Ping

nmap -PM [target]
### IP Protocol Ping

nmap -PO [target]
### ARP ping

nmap -PR [target]
### Traceroute

nmap --traceroute [target]
### Force Reverse DNS Resolution

nmap -R [target]
### Disable Reverse DNS Resolution

nmap -n [target]
### Alternative DNS Lookup

nmap --system-dns [target]
### Manually Specify DNS Server
Can specify a single server or multiple.

nmap --dns-servers [servers] [target]
### Create a Host List

nmap -sL [targets]

## Timing and Performance
The `-t` switch determines the speed and stealth performed.

 Nmap Switch  Description                 
:------------:----------------------------
 **-T0**      Serial, slowest scan        
 **-T1**      Serial, slow scan           
 **-T2**      Serial, normal speed scan   
 **-T3**      Parallel, normal speed scan 
 **-T4**      Parallel, fast scan         

Not specifying a `T` value will default to `-T3`, or normal speed.

## Firewall Evasion Techniques

### Firewall/IDS Evasion and Spoofing
 Nmap Switch  Description                 
:------------:----------------------------

### Fragment Packets

nmap -f [target]
### Specify a Specific MTU

nmap --mtu [MTU] [target]
### Use a Decoy

nmap -D RND:[number] [target]
### Idle Zombie Scan

nmap -sI [zombie] [target]
### Manually Specify a Source Port

nmap --source-port [port] [target]
### Append Random Data

nmap --data-length [size] [target]
### Randomize Target Scan Order

nmap --randomize-hosts [target]
### Spoof MAC Address

nmap --spoof-mac [MAC0vendor] [target]
### Send Bad Checksums

nmap --badsum [target]

  
## Advanced Scanning Functions

### TCP SYN Scan

nmap -sS [target]
### TCP Connect Scan

nmap -sT [target]
### UDP Scan

nmap -sU [target]
### TCP NULL Scan

nmap -sN [target]
### TCP FIN Scan

nmap -sF [target]

### Xmas Scan

nmap -sA [target]
### TCP ACK Scan

nmap -sA [target]
### Custom TCP Scan

nmap --scanflags [flags] [target]
### IP Protocol Scan

nmap -sO [target]
### Send Raw Ethernet Packets

nmap --send-eth [target]
### Send IP Packets

nmap --send-ip [target]
## Timing Options

### Timing Templates

nmap -T[0-5] [target]
### Set the Packet TTL

nmap --ttl [time] [target]
### Minimum NUmber of Parallel Operations

nmap --min-parallelism [number] [target]
### Maximum Number of Parallel Operations

nmap --max-parallelism [number] [target]
### Minimum Host Group Size

nmap --min-hostgroup [number] [targets]
### Maximum Host Group Size

nmap --max-hostgroup [number] [targets]
### Maximum RTT Timeout

nmap --initial-rtt-timeout [time] [target]
### Initial RTT Timeout

nmap --max-rtt-timeout [TTL] [target]
### Maximum Number of Retries

nmap --max-retries [number] [target]
### Host Timeout

nmap --host-timeout [time] [target]
### Minimum Scan Delay

nmap --scan-delay [time] [target]
### Maxmimum Scan Delay

nmap --max-scan-delay [time] [target]
### Minimum Packet Rate

nmap --min-rate [number] [target]
### Maximum Packet Rate

nmap --max-rate [number] [target]
### Defeat Reset Rate Limits

nmap --defeat-rst-ratelimit [target]

### Periodically Display Statistics

nmap --stats-every [time] [target]

## Compare Scans

`ndiff [scan1.xml] [scan2.xml]`: Comparison Using Ndiff
`ndiff -v [scan1.xml] [scan2.xml]`: Ndiff Verbose Mode
`ndiff --xml [scan1.xml] [scan2.xml]`: XML Output Mode

## Troubleshooting and Debugging

### Debugging

nmap -d [target]
### Display Port State Reason

nmap --reason [target]
### Only Display Open Ports

nmap --open [target]
### Trace Packets

nmap --packet-trace [target]
### Display Host Networking

nmap --iflist
### Specify a Network Interface

nmap -e [interface] [target]


