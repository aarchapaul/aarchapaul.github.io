---
layout: post
title: 25 Windows Commands you NEED to know
date: 2023-01-07 11:31:08 +0530
author: Aarcha Paul
summary: 
categories: 
thumbnail: windows
tags:
 - windows
---
# 25 Windows Commands you NEED to know

As a Windows user, there are certain commands that you should familiarize yourself with in order to perform various tasks more efficiently. These commands can be run from the command prompt, which is a command-line interpreter that allows you to enter commands into the command-line interface of your operating system.

Here are the **25** Windows commands that you should know:

 1. `dir` - This command allows you to view the files and directories in a directory. By using the `/p` option, you can view the files and directories one page at a time, which is useful for large directories.
 2. `cd` - The `cd` command allows you to change your current directory. For example, if you want to switch to the Documents directory, you would enter `cd Documents` into the command prompt.
 3. `copy` - This command allows you to copy files from one location to another. For example, if you want to copy a file named `file.txt` from the `C:\Users\User\Desktop` directory to the `C:\Users\User\Documents` directory, you would enter `copy C:\Users\User\Desktop\file.txt C:\Users\User\Documents` into the command prompt.
 4. `xcopy` - The `xcopy` command is similar to the `copy` command, but it has more options and is better suited for copying entire directories.
 5. `ping` - The `ping` command allows you to test the connection between your computer and another device on a network. For example, if you want to ping a website, you can enter `ping www.website.com` into the command prompt. This command is useful for troubleshooting network issues.    
 6. `ipconfig` - This command displays your computer's network configuration, including its IP address, subnet mask, and default gateway. The `/all` option displays even more information about your network configuration such as DNS server, IPv6 address and MAC address. 
 7. `findstr` - The `findstr` command allows you to search for a specific string of text within a file or set of files. For example, if you want to search for the word `error` in all the .txt files in the `C:\Users\User\Desktop` directory, you would enter `findstr error C:\Users\User\Desktop*.txt` into the command prompt.
 8. `ipconfig /release` and `ipconfig /renew` - These commands allow you to release and renew your IP address, respectively. This can be useful if you're having connectivity issues and need to refresh your IP address. These will reach out to the DHCP server and gett you a fresh new address and refresh every single interface on your computer. If you dont want that, specify the interface after command eg. `ipconfig /release "Wi-Fi"`. 
 9. `ipconfig /displaydns` and `ipconfig /flushdns` - The `ipconfig /displaydns` command displays the contents of your DNS resolver cache, while the `ipconfig /flushdns` command clears the contents of your DNS resolver cache. These commands can be useful if you are having issues with your network.
 10. `clip` - This is very handy to copy the output of a command to your clipboard. For example, `ipconfig /displaydns | clip` will copy the output of the DNS resolver cache to your clipboard, which you can paste into your favorite text editor.
 11. `nslookup` - The `nslookup` command allows you to query DNS servers for information about a specific domain or IP address. E.g. `nslookup google.com` will give you the IP address of google. You can also check for other types of records like MX, TXT, AAAA, etc.
 12. `cls` - The `cls` command clears the screen of the command prompt window.
 13. `getmac /v` - This command displays your computer's MAC address and other network-related information.
 14. `powercfg /energy` - This command generates a report that shows you how to improve your computer's energy efficiency.
 15. `powercfg /batteryreport` - The `powercfg /batteryreport` command generates a report that provides information about your computer's battery usage. 
 16. `assoc` - The assoc command displays or modifies the file associations for a particular file extension. For example, if the default app for opening mp4 files in your system is Windows Media Player, you can change it to VLC Media player by using the command `assoc .mp4=VLC.vlc` 
 17. `chkdsk /f` and `chkdsk /r` - These commands check your computer's hard drive for errors and attempt to fix them. The `/f` option checks for and fixes errors that can be fixed without restarting your computer, while the `/r` option checks for and fixes errors that can only be fixed by restarting your computer.
 18. `sfc /scannow` - This command scans all protected system files on your computer and replaces any that are corrupt or missing.
 19. `DISM /Online /Cleanup /CheckHealth`, `DISM /Online /Cleanup /ScanHealth`, and `DISM /Online /Cleanup /RestoreHealth` - These commands are used to troubleshoot and repair problems with your Windows installation. The `CheckHealth` command checks the health of your system, the `ScanHealth` command scans for corruption and attempts to fix any issues it finds, and the `RestoreHealth` command restores the health of your system by repairing any issues it finds.
 20. `tasklist` and `taskkill` - The `tasklist` command displays a list of all running processes on your computer, while the `taskkill` command allows you to terminate a specific process.
 21. `netsh` - is the older version of the `ipconfig` command. there are many possible variations to use netsh with.  Running this command `netshwlan show wlanreport` will create a report about your wireless network. `netsh interface show interface` will display information about your network interface. You can even turn off the Windows defender firewall witha single command `netsh advfirewall set allprofiles state off`. Super cool, isn't it? 
 22. `tracert` - Shows the path taken to a website along each route it takes to get there and how long it takes. It can be a little slow so running it with the flag `-d` will speed it up by not resolving the domain names.
 23. `netstat` - Will show the devices connected to you and the devices you are connecting to. It will also show which ports are open on your system by running the flag `-af`.
 24. `route print` - shows the route table of your system, a.k.a which paths it takes to connect to any website. 
 25. `shutdown` - This comand will power off your computer. But running it by adding a few more flags `shutdown /r /fw /f /t 0` like this, it will restart into the system BIOS. 

These are just a few of the many Windows commands that you should know. By learning and using these commands, you can perform tasks more efficiently and become more comfortable using the command-line interface of your operating system.