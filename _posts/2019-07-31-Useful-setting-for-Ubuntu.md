---
title: Useful packages for developer - A highlight list packages you must install on Ubuntu
---

@Author: damminhtien

@LastUpdate: 21/10/2019

## 1. Up arrow on keybroad to search bash history
*Reference this [link](https://askubuntu.com/questions/59846/bash-history-search-partial-up-arrow)*
Open your .bashrc file:
```bash
sudo gedit ~/.bashrc
```
Add 2 line of code at end of this file:
```bash
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
```
Activate them:
```bash
source ~/.bashrc
```
Done :D

## 2. Install 'thefuck' package to automate correct errors
The Fuck on it's offical repository is describled as a magnificent app, that can corrects errors in pervious commands.

The Fuck was written by python 3, so it's easy to customize code.

Requirements:
* python (3.4+)
* pip
* python-dev

Installation
* On Ubuntu / Mint:
  ```bash
  sudo apt update
  sudo apt install python3-dev python3-pip python3-setuptools
  sudo pip3 install thefuck
  ```
* On OS X:
  ```bash
  brew install thefuck
  ```
* On other systems:
  ```
  pip install thefuck
  ```
It is recommended that you replace this command in your .bash_profile, .bashrc, .zshrc or other startup scripts:
```bash
eval $(thefuck --alias)
evel $(thefuck --alias FUCK)
```