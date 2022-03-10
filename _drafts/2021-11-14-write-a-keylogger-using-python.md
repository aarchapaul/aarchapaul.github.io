---
layout:     post
title:      Write a Keylogger program using Python
date:       2021-11-14 15:31:19
author:     Aarcha Paul
summary:    How to Make a Keylogger in Python
categories: jekyll
thumbnail:  jekyll
tags:
 - python
---

## How to Make a Keylogger in Python
A keylogger is a type of surveillance technology used to monitor and record each keystroke typed on a specific computer's keyboard. In this tutorial, you will learn how to write a keylogger in Python.

You are maybe wondering, why a keylogger is useful ? Well, when a hacker (or a script kiddie) uses this for unethical purposes, he/she will register everything you type in the keyboard including your credentials (credit card numbers, passwords, etc.).

The goal of this tutorial is to make you aware of these kind of scripts as well as learning how to implement such malicious scripts on your own for educational purposes, let's get started!

First, we gonna need to install a module called keyboard, go to the terminal or the command prompt and write:

This module allows you to take full control of your keyboard, hook global events, register hotkeys, simulate key presses and much more, and it is small module though.

So, the Python script will do the following:

    Listen to keystrokes in the background.
    Whenever a key is pressed and released, we add it to a global string variable.
    Every N minutes, report the content of this string variable either to a local file (to upload to FTP server or Google Drive API) or via email.

Let us start by import the necessary modules:

If you choose to report key logs via email, then you should set up a Gmail account and make sure that:

- Less secure app access is on (we need to enable it because we will log in using smtplib in Python).
- 2-Step Verification is off.

Now let's initialize our parameters:
Note: Obviously, you need to put your correct gmail credentials, otherwise reporting via email won't work.


