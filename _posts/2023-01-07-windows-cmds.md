---
layout: post
title: Windows Commands cheatsheet
date: 2023-01-07 11:31:08 +0530
author: Aarcha Paul
summary: 
categories: cheatsheet
thumbnail: windows
tags:
 - windows
---
# Windows Commands cheatsheet

<table>
   <colgroup>
      <col width="10%" />
      <col width="20%" />
      <col width="70%" />
   </colgroup>
   <thead>
      <tr>
         <th>Sl. no.</th>
         <th>Command</th>
         <th>Usage</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>1.</td>
         <td>dir</td>
         <td>View the files and directories in a directory. By using the `/p` option, you can view the files and directories one page at a time, which is useful for large directories.</td>
      </tr>
      <tr>
         <td>2.</td>
         <td>cd</td>
         <td>Change your current directory. E.g. to switch to the Documents directory, enter `cd Documents`</td>
      </tr>
      <tr>
         <td>3.</td>
         <td>copy</td>
         <td>Used to copy files from one location to another. E.g. if you want to copy a file named `file.txt` from the `C:\Users\User\Desktop` directory to the `C:\Users\User\Documents` directory, you would enter `copy C:\Users\User\Desktop\file.txt C:\Users\User\Documents` into the command prompt. </td>
      </tr>
      <tr>
         <td>4.</td>
         <td>xcopy</td>
         <td>Similar to the `copy` command, but it has more options and is better suited for copying entire directories.</td>
      </tr>
       <tr>
         <td>5.</td>
         <td>ping</td>
         <td>Test the connection between your computer and another device on a network. For example, if you want to ping a website, you can enter `ping www.website.com` into the command prompt. This command is useful for troubleshooting network issues.</td>
      </tr>
       <tr>
         <td>6.</td>
         <td>ipconfig</td>
         <td>Displays your computer's network configuration, including its IP address, subnet mask, and default gateway. The `/all` option displays even more information about your network configuration such as DNS server, IPv6 address and MAC address. </td>
      </tr>
       <tr>
         <td>7.</td>
         <td>findstr</td>
         <td>Search for a specific string of text within a file or set of files. E.g. if you want to search for the word `error` in all the .txt files in the `C:\Users\User\Desktop` directory, you would enter `findstr error C:\Users\User\Desktop*.txt` into the command prompt.</td>
      </tr>
       <tr>
         <td>8.</td>
         <td>`ipconfig /release` and `ipconfig /renew`</td>
         <td>Helps release and renew your IP address, respectively. Useful if you're having connectivity issues and need to refresh your IP address. These will reach out to the DHCP server and get you a fresh new address and refresh every single interface on your computer. If you dont want that, specify the interface after command eg. `ipconfig /release "Wi-Fi"`. </td>
      </tr>
       <tr>
         <td>9.</td>
         <td>`ipconfig /displaydns` and `ipconfig /flushdns`</td>
         <td>The `ipconfig /displaydns` command displays the contents of your DNS resolver cache, while the `ipconfig /flushdns` command clears the contents of your DNS resolver cache. These commands can be useful if you are having issues with your network.</td>
      </tr>
       <tr>
         <td>10.</td>
         <td>clip</td>
         <td>This is very handy to copy the output of a command to your clipboard. E.g. `ipconfig /displaydns | clip` will copy the output of the DNS resolver cache to your clipboard, which you can paste into your favorite text editor.</td>
      </tr>
       <tr>
         <td>11.</td>
         <td>nslookup</td>
         <td>Allows you to query DNS servers for information about a specific domain or IP address. E.g. `nslookup google.com` will give you the IP address of google. You can also check for other types of records like MX, TXT, AAAA, etc.</td>
      </tr>
       <tr>
         <td>12.</td>
         <td>cls</td>
         <td>Clears the screen of the command prompt window.</td>
      </tr>
       <tr>
         <td>13.</td>
         <td>getmac /v</td>
         <td>Displays your computer's MAC address and other network-related information.</td>
      </tr>
       <tr>
         <td>14.</td>
         <td>powercfg /energy</td>
         <td>Generates a report that shows you how to improve your computer's energy efficiency.</td>
      </tr>
       <tr>
         <td>15.</td>
         <td>powercfg /batteryreport</td>
         <td>Generates a report that provides information about your computer's battery usage. </td>
      </tr> 
       <tr>
         <td>16.</td>
         <td>assoc</td>
         <td>Displays or modifies the file associations for a particular file extension. E.g. if the default app for opening mp4 files in your system is Windows Media Player, you can change it to VLC Media player by using the command `assoc .mp4=VLC.vlc`</td>
      </tr>
        <tr>
         <td>17.</td>
         <td>`chkdsk /f` and `chkdsk /r`</td>
         <td>Check your computer's hard drive for errors and attempt to fix them. The `/f` option checks for and fixes errors that can be fixed without restarting your computer, while the `/r` option checks for and fixes errors that can only be fixed by restarting your computer.</td>
      </tr>
       <tr>
         <td>18.</td>
         <td>sfc /scannow</td>
         <td>Scans all protected system files and replaces any that are corrupt or missing.</td>
      </tr>
       <tr>
         <td>19.</td>
         <td>`DISM /Online /Cleanup /CheckHealth`, `DISM /Online /Cleanup /ScanHealth`, and `DISM /Online /Cleanup /RestoreHealth` </td>
         <td>Used to troubleshoot and repair problems with your Windows installation. The `CheckHealth` command checks the health of your system, the `ScanHealth` command scans for corruption and attempts to fix any issues it finds, and the `RestoreHealth` command restores the health of your system by repairing any issues it finds.</td>
      </tr>
      <tr>
         <td>20.</td>
         <td>tasklist</td>
         <td>Displays list of all running processes</td>
      </tr>
       <tr>
         <td>21.</td>
         <td>taskkill</td>
         <td>Terminate a specific process.</td>
      </tr>
       <tr>
         <td>22.</td>
         <td>netsh</td>
         <td>is the older version of the `ipconfig` command. there are many possible variations to use netsh with.  Running this command `netshwlan show wlanreport` will create a report about your wireless network. `netsh interface show interface` will display information about your network interface. You can even turn off the Windows defender firewall with a single command `netsh advfirewall set allprofiles state off`. </td>
      </tr>
      <tr>
         <td>23.</td>
         <td>tracert</td>
         <td>Shows the path taken to a website along each route it takes to get there and how long it takes. It can be a little slow so running it with the flag `-d` will speed it up by not resolving the domain names.</td>
      </tr>
      <tr>
         <td>24.</td>
         <td>netstat</td>
         <td>Shows the devices connected to you and the devices you are connecting to. It will also show which ports are open on your system by running the flag `-af`.</td>
      </tr>
      <tr>
         <td>25.</td>
         <td>route print</td>
         <td>shows the route table of your system, a.k.a which paths it takes to connect to any website.</td>
      </tr>
      <tr>
         <td>26.</td>
         <td>shutdown</td>
         <td>This comand will power off your computer. But running it by adding a few more flags `shutdown /r /fw /f /t 0` like this, it will restart into the system BIOS. </td>
      </tr>
   </tbody>
</table>
