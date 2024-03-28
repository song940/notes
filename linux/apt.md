---
layout: default
title: APT
parent: Linux
---

# APT

```shell
apt update
```

## APT Source

For example ustc https://mirrors.ustc.edu.cn/help/debian.html

```shell
sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
```

/etc/apt/sources.list

```patch
deb http://mirrors.ustc.edu.cn/debian stable main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian stable main contrib non-free non-free-firmware
deb http://mirrors.ustc.edu.cn/debian stable-updates main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian stable-updates main contrib non-free non-free-firmware

# deb http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free non-free-firmware
```

## List Installed

```shell
apt list --installed
```
