---
title: 'How to add alias to your Linux'
date: Sat, 24 Oct 2020 09:43:16 +0000
draft: false
tags: ['alias', 'aliases', 'bash', 'Linux', 'Ubuntu', 'customize']
categories: ['Linux', 'Ubuntu', 'Customization']
aliases: ['/how-to-add-alias-to-your-linux']
---

Using a Linux Operating System, there is a high level of customization, depending on your preferences or needs.

One important thing is to create alias to the most common commands in order to optimize the time you use. In mi case, I love to use ".." instead of "cd .." or "update" to update all my Ubuntu software pending updates.

Here I put my list of aliases, it is not big but it is what I mostly use in the servers I have with Linux.

To install them, you first have to edit the file `~/.bash_alises` like this:

    root@rhea:~# vi ~/.bash_aliases

And insert this lines:

```
alias l="ls -lh --color"
alias rm="rm -i"
alias ..="cd .."
alias ...="cd ../.."
alias update='sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade'
alias clean='sudo apt-get autoclean && sudo apt-get autoremove && sudo apt-get clean'
```

Then you can update the alises used in your current session:

```
root@rhea:~# source ~/.bash_aliases
root|rhea:~$
```

And from that moment, you can use them.
