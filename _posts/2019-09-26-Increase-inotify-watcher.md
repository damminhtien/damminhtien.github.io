---
title: Increasing the amount of inotify watchers
tags: Linux
---

@Author: damminhtien :whale:

@LastUpdate: 16/11/2019

Sometime you code on VSCode editor and get troubles with **the limit of watchers in linux**, the error seem like "Unable to wathc for file changes 
in this large workspace". The content below will help you debug :) 

TDLR;

## How to
If you are not interested in the technical details and only want to get Listen to work:

If you are running Debian, RedHat, or another similar Linux distribution, run the following in a terminal:

```bash
$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

If you are running ArchLinux, run the following command instead (see here for why):

```bash
$ echo fs.inotify.max_user_watches=524288 | sudo tee /etc/sysctl.d/40-max-user-watches.conf && sudo sysctl --system
```

Then paste it in your terminal and press on enter to run it.

## The technical details
Listen uses inotify by default on Linux to monitor directories for changes. It's not uncommon to encounter a system limit on the number of files you can monitor. For example, Ubuntu Lucid's (64bit) inotify limit is set to 8192.

You can get your current inotify file watch limit by executing:

```bash
$ cat /proc/sys/fs/inotify/max_user_watches
```

When this limit is not enough to monitor all files inside a directory, the limit must be increased for Listen to work properly.

You can set a new limit temporary with:

```bash
$ sudo sysctl fs.inotify.max_user_watches=524288
$ sudo sysctl -p
```
If you like to make your limit permanent, use:

```bash
$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
$ sudo sysctl -p
```

You may also need to pay attention to the values of max_queued_events and max_user_instances if Listen keeps on complaining.

## More info
Manual of [inotify(7)](http://linux.die.net/man/7/inotify)

Blog post: [limit of inotify (archive.org)](https://web.archive.org/web/20161106193425/http://blog.sorah.jp/2012/01/24/inotify-limitation)
