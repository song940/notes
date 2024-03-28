---
layout: default
title: pacman
parent: Linux
---

# pacman

pacman is a package manager for Unix-like operating systems such as Linux, macOS, and Windows.
pacman 是 Arch Linux 的包管理器，用于安装、更新和删除软件包。

## 同步操作

**Sy** - Synchronize

    pacman -Syu
更新所有软件包

**S** - Install

    pacman -S package-name
安装软件包

**Ss** - Search sync databases

    pacman -Ss package-name
搜索软件包

**Syy** - Force refresh

    pacman -Syy
强制完全刷新包数据库

**Q** - Query

    pacman -Q
查看已安装的软件包

**Qi** - Query information

    pacman -Qi package-name
查看特定软件包的信息

**Ql** - Query list

    pacman -Ql package-name
查看特定软件包的文件

**R** - Remove

    pacman -R package-name
卸载软件包（但保留其配置文件）

**Rn** - Remove with no config

    pacman -Rn package-name
卸载软件包并删除其配置文件

**Sc** - Clean cache

    pacman -Sc
删除未安装的软件包缓存

**Scc** - Clean all cache

    pacman -Scc
删除所有软件包缓存

**Qo** - Query owns

    pacman -Qo /path/to/file
查找哪个包提供特定文件

**F** - Find

    pacman -F filename
查找文件属于哪个包

**--force** - Force action

    pacman -S --force package-name
强制重新安装软件包

