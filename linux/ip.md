---
layout: default
title: ip
---

# ip

macOS 原生没有 `ip` 命令需要通过 [brew](../macOS/brew) 安装

```shell
brew install iproute2mac
```

```shell
ip addr
```

## Route 路由

在 Linux 中，route 是 ip 的子命令，而 macOS 中 [route](../macos/route) 是独立的命令。

### 查看路由规则

```shell
ip route
route # for macOS
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
