---
layout: post
title:  Generating a new SSH key and adding it to the ssh-agent
date:   2017-04-20 21:59:00 +0800
categories: ssh linux
description: "How to Generating a new SSH"
---

 1. Greate a ssh-keygen  
~~~~
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
~~~~

 2. Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.  
~~~
ssh-add ~/.ssh/id_rsa
~~~

from:[Generating a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
