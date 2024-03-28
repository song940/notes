---
layout: default
title: Clash
---

# Clash

[Clash Github](https://github.com/Dreamacro/clash)   
[Clash Official Documentation](https://lancellc.gitbook.io/clash)

Clash 是一个功能全面的网络流量处理工具。

## 入流量

为了实现流量的规则决策，需要接管流量。根据不同的协议，我们有以下方式：

- [HTTP/HTTPS](network/http) 协议
- [Socks5](network/socks5) 协议
- Tproxy 协议
- Redir 协议
- [TUN](network/tun) 模式

在传统方法中，我们需要确切知道哪些 IP 地址需要代理（黑名单）或不需要代理（白名单）。

- 使用黑名单方法通常需要通过 gfwlist 生成 ipset 地址池。
- 使用白名单方法则是将国内站点加入到 ipset。

白名单允许特定流量直接通行，而其余流量将走代理。
黑名单的缺点是地址列表庞大，查找效率较低，且某些较为冷门的网站可能未被列入，导致被遗漏。
两种方法都需要预先解析准确的 IP 地址，而且需要防止DNS污染，因此成本较高、效率较低。

相比之下，使用 TUN + fake ip 的方式会更简单且高效。

![](https://oss.whaleluo.top/blog/img/202307091530969.png)

`utun` 是 Clash 创建的虚拟网卡。流量进入后，会根据 IP 地址查找相应的域名，并根据规则判断是否使用代理。

```yaml
tun:
  enable: true
  stack: system
  dns-hijack:
    - any:53
    - tcp://any:53
# interface-name: br0
auto-route: true
auto-detect-interface: true
```

为了避免回环问题，我们可以使用 fake ip 作为 DNS 服务。

```yaml
dns:
  enable: true
  ipv6: true
  listen: :1053
  use-hosts: true
  enhanced-mode: fake-ip
  default-nameserver:
    - 223.5.5.5
    - 114.114.114.114
  nameserver:
    - 223.5.5.5
    - 114.114.114.114
#   - tls://1.12.12.12
#   - tls://223.5.5.5:853
#   - tls://dns.rubyfish.cn:853
#   - https://doh.pub/dns-query
#   - https://dns.alidns.com/dns-query
#   - https://119.29.29.29/dns-query
  fake-ip-range: 198.18.0.1/16
  fake-ip-filter:
    - "*.lan"
    - "*.direct"
    - "unifi"
  fallback-filter:
    geoip: true
    geoip-code: CN
    ipcidr:
      - 240.0.0.0/4
    domain:
      - "+.google.com"
      - "+.facebook.com"
      - "+.youtube.com"
      - "+.twitter.com"
  fallback:
    - 8.8.8.8
    - 208.67.222.222
    - tls://8.8.4.4:853
#   - https://1.0.0.1/dns-query
    - https://dns.google/dns-query
    - https://dns.cloudflare.com/dns-query
#   - https://public.dns.iij.jp/dns-query

```

例如，当你访问 google.com 时，首先会请求本地53端口进行 DNS 解析，然后 dnsmasq 将请求转发给 clash 的 DNS。Clash DNS 会从私有地址池（198.18.0.1/16）中返回一个 IP 并保存域名与 IP 的映射关系以备后用。


| DOMAIN     | IP           |
| ----       | ----         |
| google.com | 198.18.0.128 |
| baidu.com  | 198.18.0.6   |

Clash DNS 返回 `198.18.0.1/16` 的私有地址，然后这个流量就会根据路由表找到网卡

```shell
$ ip route
default via 111.196.56.1 dev pppoe-wan
10.8.0.0/24 dev tun0 scope link  src 10.8.0.1
10.10.10.0/24 dev n2n0 scope link  src 10.10.10.1
111.196.56.1 dev pppoe-wan scope link  src 111.196.61.172
172.16.0.0/24 via 10.10.10.2 dev n2n0
192.168.3.0/24 dev wg0 scope link
192.168.6.0/24 dev wg0 scope link
192.168.8.0/24 dev br-lan scope link  src 192.168.8.1
198.18.0.0/16 dev utun scope link  src 198.18.0.1
```

我们可以看到，流量会发送到 utun 这个网络设备上：

```shell
~# ip addr
18: utun: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 9000 qdisc mq state UNKNOWN qlen 500
    link/[65534]
    inet 198.18.0.1/16 scope global utun
       valid_lft forever preferred_lft forever
    inet6 fe80::9272:3919:426a:4a04/64 scope link flags 800
       valid_lft forever preferred_lft forever
```

## Rules 规则

接收到流量后，我们可以基于以下模式进行决策：

- Direct (直连)
- Rule (规则)
- Global (全局)

**Direct** 就是所有进来的流量都不经过代理，直接从本地发送和接收。
**Global** 代表所有「进站」流量都走代理。
**Rule** 是基于入站流量的特性，如域名、IP 地址和端口来匹配的。


规则是根据入站的流量特征进行匹配的条件，包括域名、IP 地址、端口 等等。

```yaml
rules:
  - DST-PORT,53,PROXY
  - DST-PORT,22,DIRECT
  - DOMAIN-SUFFIX,api.openai.com
  - RULE-SET,reject,REJECT
```

判断流量是否符合某一规则有很多方法可以用：

+ DST-PORT 判断目的端口
+ RULE-SET 匹配规则集


#### Rule Provider

规则集是将特定规则组合在一个文件中，集中管理。

```yaml
# OpenAI
payload:
  - DOMAIN-SUFFIX,api.openai.com
  - DOMAIN-SUFFIX,cdn.openai.com
  - DOMAIN-SUFFIX,chat.openai.com
  - DOMAIN-SUFFIX,auth0.openai.com
  - DOMAIN-SUFFIX,platform.openai.com
```

有这样的东西就可以允许大家在网络上整理一些规则以订阅

### 出站协议

#### Proxy Provider

和 Rule Provider 类似，Proxy Provider 也是将特定规则集中管理，允许服务提供商发布这些规则供用户订阅。

```yaml
proxy-providers:
  freefq:
    type: http
    path: proxies/freefq.yaml
    url: "https://rawgit.lsong.org/song940/freefq/release/proxies/freefq.yaml"
    interval: 3600
    health-check:
      enable: true
      interval: 600
      url: http://www.gstatic.com/generate_204

```

### Install 安装部署

我这里以 *OpenWRT* 为例，实际上其他系统也差不多

1. Download [Clash Premium](https://github.com/Dreamacro/clash/releases/tag/premium) from github.com
2. `gunzip -c` to `/usr/bin`
3. Put your config files to `/etc/clash`, make sure mode is *fakeip* in config file.
```shell
~$ git clone https://github.com/song940/freefq.git /etc/clash
```
4. start up clash
```shell
~$ opkg update
~$ opkg install kmod-tun
~$
~$ chmod +x /usr/bin/clash
~$ clash -d /etc/clash
```
首次启动会下载 *mmdb* 数据库文件，It'll take a moment，同时观察一下端口情况是否 *port in used*, 确保正常启动。
5. copy startup script to `/etc/init.d/clash`, run `service clash start` and `service clash enable`
```shell
~$ service clash start
~$ service clash enable
```
6. clash dns listen *1053*, add `127.0.0.1#1053` to *DNS forwardings* and *Size of DNS query cache* set `0` to disable cache.
```patch
# /etc/config/dhcp
config dnsmasq
  ...
  option domainneeded '1'
  option leasefile '/tmp/dhcp.leases'
  option ednspacket_max '1232'
  option nonegcache '1'
  ...
+ list server '127.0.0.1#1053'
+ option cachesize '0'
```
7. Set *input* and *forwarding* from `reject` to `allow` in OpenWRT's *Firewall Zone Settings*.
8. Reboot the Router.
