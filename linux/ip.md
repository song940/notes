---
layout: default
title: ip
parent: Linux
---

# ip

ip is a command-line utility for networking.

显示或操纵路由、设备、策略路由和隧道

macOS 原生没有 `ip` 命令需要通过 [brew](../macos/brew) 安装.

```shell
brew install iproute2mac
```

## ip addr

显示或修改地址的属性

```shell
ip addr
```

## ip link

显示或修改网络设备的属性。

## ip route

显示或修改路由表

在 Linux 中，route 是 ip 的子命令，而 macOS 中 [route](../macos/route) 是独立的命令。

### 查看路由规则

```shell
ip route
route # for macOS
```

### 添加一个新路由

```shell
ip route add 192.168.1.0/24 via 192.168.2.1
```

### 删除一个路由

```shell
ip route del 192.168.1.0/24 via 192.168.2.1
```

### 删除默认路由

```shell
sudo ip route delete default
sudo route delete default # for macOS
```

### 添加默认路由

添加新的默认路由

```shell
sudo ip route add default dev utun7
sudo route add default -interface utun7 # for macOS
```
