---
layout: post
title: 
date: 2022-09-24 18:39:13 +0530
author: Aarcha Paul
summary: 
categories: TryHackMe
thumbnail: jekyll
tags:
 - regex
 - Regular Expressions
---
# Regex commands for beginners

Regular expressions, also known as regex, are a powerful tool for working with text. They allow you to search for, match, and manipulate specific patterns of characters within a body of text.

Here are a few basic regex commands that every beginner should know:

1.  `^` - Matches the start of a line. For example, the regex `^Hello` would match the string "Hello" at the beginning of a line.
2.  `$` - Matches the end of a line. For example, the regex `World$` would match the string "World" at the end of a line.
3.  `.` - Matches any single character (except a newline). For example, the regex `H.llo` would match the strings "Hello", "Hillo", and "Hxllo", but not "Hollo".
4.  `**` - Matches zero or more occurrences of the preceding character or group. For example, the regex "H*llo" would match the strings "Hello", "Hllo", and "Hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhllo".
5.  `+` - The plus symbol (+) matches one or more occurrences of the preceding character or group. For example, the regex `H+llo` would match the strings "Hello" and "Hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhllo", but not "Hllo".
6.  `?` - The question mark (?) matches zero or one occurrence of the preceding character or group. For example, the regex `H?llo` would match the strings "Hello" and "Hllo", but not "Hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhllo".
7.  `[ ]` - Brackets enclose a character set, which matches any single character within the set. For example, the regex `H[ae]llo` would match the strings "Hello" and "Hallo", but not "Hxllo".
8.  `[^ ]` - When the caret symbol is placed within brackets, it negates the character set. For example, the regex `H[^ae]llo` would match the string "Hxllo", but not "Hello" or "Hallo".
9.  `|` - The pipe symbol (|) represents a logical OR. For example, the regex `H(e|a)llo` would match the strings "Hello" and "Hallo".
10.  `\d` - The backslash and "d" combination matches any single digit. For example, the regex `\d\d\d-\d\d-\d\d\d\d` would match a string in the format "XXX-XX-XXXX", where "X" is a digit.

These are just a few basic regex commands that can help you get started working with regular expressions. With practice and a bit of creativity, you can use these commands to perform a wide range of tasks, such as searching for and replacing specific patterns of text within a document, validating forms, and more.