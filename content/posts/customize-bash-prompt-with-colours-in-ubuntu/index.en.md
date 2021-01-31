---
title: 'Customize Bash Prompt with colours in Ubuntu'
date: Wed, 01 Apr 2020 21:06:21 +0000
draft: false
tags: ['colours', 'customize', 'Linux', 'prompt', 'Ubuntu']
categories: ['Linux', 'Ubuntu', 'Customization']
aliases: ['/customize-bash-prompt-with-colours-in-ubuntu']
---

There are lot of people that simply like to customize the appearence of the terminal, is my case. When you use a terminal during a lot of time, it usually helps to have a prompt more visible than the default one.

## Backup

First of all, you should make a backup of the configuration file in order to fall back in case it is necessary. The file is at the user $HOME, so first step is to go the directory.

```
cd ~
cp -p .bashrc .bashrc-backup
```

## Adding the new configuration

Now, is the moment to edit the file .bashrc and add the new configuration to have the customized prompt.

I am used to use the _vi_ editor to modify the configuration.

    vi .bashrc

Once open the file, you should go to the end of the file. The way to do it in vi is using the key combination "Shift+G". Once the cursor is positioned at the end, start edit mode in _vi_ using the "o" key. Add next configuration at the end of the file.

```
########################################
# background color using ANSI escape
########################################
bgBlack="\[$(tput setab 0)\]" # black
bgRed="\[$(tput setab 1)\]" # red
bgGreen="\[$(tput setab 2)\]" # green
bgYellow="\[$(tput setab 3)\]" # yellow
bgBlue="\[$(tput setab 4)\]" # blue
bgMagenta="\[$(tput setab 5)\]" # magenta
bgCyan="\[$(tput setab 6)\]" # cyan
bgWhite="\[$(tput setab 7)\]" # white


########################################
# foreground color using ANSI escape
########################################
fgBLack="\[$(tput setaf 0)\]" # black
fgRed="\[$(tput setaf 1)\]" # red
fgGreen="\[$(tput setaf 2)\]" # green
fgYellow="\[$(tput setaf 3)\]" # yellow
fgBlue="\[$(tput setaf 4)\]" # blue
fgMagenta="\[$(tput setaf 5)\]" # magenta
fgCyan="\[$(tput setaf 6)\]" # cyan
fgWhite="\[$(tput setaf 7)\]" # white


########################################
# text editing options
########################################
txBold="\[$(tput bold)\]"   # bold
txHalf="\[$(tput dim)\]"    # half-bright
txUnderline="\[$(tput smul)\]"   # underline
txEndUnder="\[$(tput rmul)\]"   # exit underline
txReverse="\[$(tput rev)\]"    # reverse
txStandout="\[$(tput smso)\]"   # standout
txEndStand="\[$(tput rmso)\]"   # exit standout
txReset="\[$(tput sgr0)\]"   # reset attributes

# root
PS1="[\t] $fgRed\u$txReset|$fgYellow\h$txReset:$fgCyan\W$txReset\$ "

# user
PS1="[\t] $fgCyan\u$txReset|$fgMagenta\h$txReset:$fgGreen\w$txReset\$ "
```

The last command "PS1=..." is the definition of the prompt. In this line you could change the colour variables as you want.

Once finished the edition of the file, you shoud exit the vi edition mode (ESC), and save the file (:wq).

## Update current terminal

In order to update the prompt of your current terminal, you should execute the _source_ command.

    source .bashrc

And that is, now you should have the terminal customized.

![](./images/colour_prompt-1.webp)

## Rollback the configuration

To return to the previous configuration, you should copy the backup file.

```
cd ~
cp .bashrc-backup .bashrc
```
