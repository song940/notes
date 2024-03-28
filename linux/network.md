---
layout: default
title: Linux Network
parent: Linux
---

# Network

## ip 命令

**ip** - 显示或操纵路由、设备、策略路由和隧道。

**ip link** - 显示或修改网络设备的属性。

**ip addr** - 显示或修改地址的属性。

**ip route** - 显示或修改路由表。

    ip route add 192.168.1.0/24 via 192.168.2.1
添加一个新路由。

    ip route del 192.168.1.0/24 via 192.168.2.1
删除一个路由。

## traceroute 命令

**traceroute** - 显示数据包到主机的路径。

    traceroute 192.168.1.1
显示数据包到192.168.1.1的路径。

## ping 命令

**ping** - 发送 ICMP ECHO_REQUEST 到网络主机。

    ping 192.168.1.1
向192.168.1.1发送ping请求。

## ifconfig 命令

**ifconfig** - 显示或配置一个网络接口。

    ifconfig eth0
显示eth0的配置。

## iptables 命令

**iptables** - 管理IPv4包过滤规则。

## tcpdump 命令

**tcpdump** - 捕获并显示网络流量。

    tcpdump -i eth0
在eth0上捕获流量。

    tcpdump -i eth0 'host 192.168.1.1'
只捕获与192.168.1.1有关的流量。

    tcpdump -i eth0 'host 192.168.1.1 or 192.168.3.1'
捕获与192.168.1.1或192.168.3.1有关的流量。

## dig 命令

**dig** - DNS查找实用程序。

    dig google.com
查询google.com的DNS记录。

    dig google.com +trace
追踪google.com的DNS查询路径。

    dig google.com @1.1.1.1
使用1.1.1.1作为DNS服务器查询google.com。

