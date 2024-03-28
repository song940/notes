---
layout: default
title: Shadowsocks
---

# Shadowsocks

Shadowsocks is a free and open-source SOCKS5 proxy server.

Shadowsocks（通常简称为“SS”）是一个开源的安全传输协议，也常被视为一个加密代理工具。它是为了解决国家间互联网访问受限问题而设计的，但随着时间的推移，它也变得流行于互联网安全和隐私保护领域。以下是 Shadowsocks 的工作原理简介：

1. **加密与解密**:
   - 当用户的设备上的 Shadowsocks 客户端要访问一个互联网地址时，它首先会将原始数据（例如，您想访问的网站的URL）进行加密。
   - 在目标服务器返回数据时，Shadowsocks 服务端会将其加密，然后再发送到客户端，客户端收到后再进行解密。

2. **SOCKS5 代理**:
   - Shadowsocks 的数据传输建立在 [SOCKS5](socks5) 是一个网络层代理协议，可以处理任何类型的网络通信，不限于 HTTP。
   - 当客户端想要访问一个网址时，它会先将请求发送到 Shadowsocks 服务端，而不是直接发送到目标服务器。

3. **端到端通信**:
   - 从用户的角度看，数据从客户端发送到 Shadowsocks 服务端，然后从 Shadowsocks 服务端发送到目标服务器。返回的数据也遵循相同的路径。
   - 由于数据在传输过程中是加密的，所以在数据流向其目的地的过程中，任何中间人都无法读取或修改这些数据。

4. **混淆**:
   - 为了进一步增加安全性和避免被侦测，Shadowsocks 还支持流量混淆。这使得 Shadowsocks 生成的流量更难以被区分，从而更难以被检测和封锁。

5. **灵活的部署**:
   - 用户可以选择自己部署 Shadowsocks 服务端，或使用第三方服务提供的服务器。这为用户提供了在全球范围内使用服务的灵活性。

Shadowsocks 的核心原理是建立一个加密的通道，使得数据在传输过程中不被中间人读取或修改。通过使用 SOCKS5 代理和其他混淆技术，它可以帮助用户安全、私密地浏览互联网，绕过网络封锁。

+ https://github.com/shadowsocks
+ https://github.com/gwuhaolin/blog/issues/12
+ https://github.com/shadowsocks/go-shadowsocks2

称 Shadowsocks 的 ss-local 和 ss-remote 为客户端和服务端是不合适的，因为 ss-local 即是 ss 客户端也是 socks5 服务端, 比较严谨的方式可以称之为 远端和近端(本地端)。
