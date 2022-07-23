---
layout: post
title: Broken Access Control
date: 2022-07-23 20:26:17
author: Aarcha Paul
summary: A quick introduction to Broken Access Control vulnerability
categories: 
thumbnail: jekyll
tags:
 - enumeration 
 - reconnaisance 
 - OWASP top 10 
---
# Broken Access Control

Broken Access Control has become the most common web application vulnerability according to OWASP Top 10 list in 2021. Hence it is important to not only understand this type of vulnerability but also how to prevent it.

Access control involves a website granting some users access to content and function. It requires defining who can view and/or modify data or configurations within a system or application. The first step in implementing access control is defining a policy for the particular system or application. We need to understand who/what should and shouldn’t have access to view or edit an object. Once the policy is created and we know who should have access to a system and, more importantly, what level of access they should have, we next need to design the implementation.

When there are flaws in policy implementation, Broken Access Control occurs. Broken Access Control leads to unauthorized access, use, modification, or disclosure of data. If the control around this page isn’t secured properly, a malicious actor can gain unauthorized access and create, modify, or delete users.

## Types of Access Control Vulnerabilities
Broken authentication vulnerabilities can be categorized as:
1. **Vertical Privilege Escalation**: Vertical access controls are used to restrict access to crucial functions not available to other users in the organization. For example, broken vertical access controls can be explored to access functions that ordinary users can’t access, such as modifying and deleting user accounts. A few types of vertical privilege escalation attacks are Unprotected Sensitive Functionality, Parameter-based attacks and Broken access control due to platform misconfiguration. 
2. **Horizontal Privilege Escalation**: Horizontal access controls enable different application users to access similar resource types. These mechanisms restrict access to the resources only to the group of users allowed to access the resource. For instance, a banking application lets clients view their transactions’ records but not of other users. Broken horizontal access controls enable attackers to access resources belonging to other users and are caused by Improper ID controls. 
3. **Context-Dependent Privilege Escalation**: Often, attackers compromise privileged users to turn horizontal privilege escalation attacks into vertical privilege escalation. For instance, hackers may use broken horizontal controls to retrieve the login credentials of another user. The attackers can then target administrative accounts, which gives them administrative rights to escalate privileges vertically. Some context-dependent privilege escalation attacks are [[Insecure Direct Object Reference]], Multi-step attacks, Attacks on referer-based mechanisms and Attacks on geographical location-based mechanisms

## Exploiting Broken Access Control
To better understand Broken Access Control, let’s quickly cover the structure of a URL:
![](https://miro.medium.com/max/875/0*Lp7m1xCyKm3VB2kf.jpg)

As pictured above, we first have our protocol, which should always be HTTPS if the site processes sensitive data, like user logins. Next comes the domain and path of a subpage. After we’ve defined the path of the page we want to visit, sometimes we need to query a specific parameter. This always happens in the background, for example when we perform a search on a website.

In a website, there are some pages that only an administrator should be able to access. if an attacker gains access to another account by manipulating and fuzzing requests, then the website is vulnerable to Broken access control. For example, a website has a user account with parameter `www.target-site.com/note.php?note=1`. We can change the parameter `?note=1` to `?note=0` and gain access to an account with admin privileges.

Ideally, referencing a user ID like this shouldn’t actually contain the plaintext user ID. If you need the user ID to be passed in the URL, make sure it’s hashed at the least. And even if the user is able to find a page by fuzzing ID in URL, the website should prompt to authenticate the user.

## Prevention 
1. Deny everything by default: block all access by default and implement configuration to allow required access to users 
2. Logging failures & alerting admins: Enable logging of login failures and alert administrators when a certain threshold is met 
3. Disable webserver directory listing: Prevents users from being able to view the server directories and access potentially sensitive information 
4. Invalidate JSON Web Tokens (JWT) on logout
6. Insecure Id’s : Id's used in a URL must always br randomized. If an attacker can guess these id’s, and the supplied values are not validated to ensure the are authorized for the current user, the attacker can exercise the access control scheme freely to see what they can access. Web applications should not rely on the secrecy of any id’s for protection. 

## Conclusion
While the above considerations aren’t the only ones involved in implementing strong access control, they are some of the key components to securing access on a given web application. By implementing a default deny, protecting system files, invalidating tokens, and enabling sufficient logging, we are on our way to having a website with secure access control.