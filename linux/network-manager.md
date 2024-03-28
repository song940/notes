---
layout: default
title: NetworkManager
parent: Linux
---

# NetworkManager

## Install

```shell
~# apt install networkmanager
~# pacman -S networkmanager
```

Enable NetworkManager:

```shell
~# systemctl enable NetworkManager
~# systemctl start NetworkManager
```

## Setup

```shell
~$ nmcli
~$ nmtui
```

### WiFi Menu

```shell
apt install netctl
```

```shell
wifi-menu
```
