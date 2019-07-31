---
title: Useful packages for developer - A highlight list packages you must install on Ubuntu
---
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
