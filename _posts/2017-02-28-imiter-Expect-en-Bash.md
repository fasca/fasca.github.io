---
layout: post
title: Imiter Expect en Bash
date: 2017-02-28 14:30:00
tags:
  - backend
  - system
description: Imiter Expect en Bash
categories: system backend
serie: programmation
published: true
---

Exemple:

````bash
var=$(cat file.txt)
sleep 2
echo "login"
sleep 1
echo "password"
sleep 1
echo "echo \"${var}\" > /tmp/toto.txt"
sleep 1
echo "exit"
````
pour executer ce scirpt sur du telnet exemple:

sh script.sh | telenet @IP
