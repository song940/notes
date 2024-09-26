---
layout: default
title: 網絡管理
parent: Linux
nav_order: 2
---

# Linux 網絡管理

在 Linux 中有大量管理网络的工具:

+ [ip](ip)
+ [dig](dig)
+ [ping](ping)
+ [netstat](netstat)
+ [tcpdump](tcpdump)
+ [ifconfig](ifconfig)
+ [iptables](iptables)
+ [traceroute](traceroute)

## NetworkManager

```shell
~# apt install networkmanager
~# pacman -S networkmanager
```

Enable NetworkManager:

```shell
~# systemctl enable NetworkManager
~# systemctl start NetworkManager
```

Setup

```shell
~$ nmcli
~$ nmtui
```

## WiFi Menu

```shell
apt install netctl
```

```shell
wifi-menu
```
