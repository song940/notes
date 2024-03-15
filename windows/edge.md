---
layout: default
title: Microsoft Edge
parent: Windows
---

# Microsoft Edge

## NewTab

Microsoft Edge 的新标签页非常烦人还不能在浏览器设置中修改或关闭，

我注意到在 `edge://policy` 中有相关设置，但是需要 MDM 才能配置，

我找到了一种通过注册表的方式加入 MDM，然后就可以修改新标签页地址了：

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Enrollments\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF] 
"EnrollmentState"=dword:00000001 
"EnrollmentType"=dword:00000000 
"IsFederated"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF]
"Flags"=dword:00d6fb7f
"AcctUId"="0x000000000000000000000000000000000000000000000000000000000000000000000000"
"RoamingCount"=dword:00000000
"SslClientCertReference"="MY;User;0000000000000000000000000000000000000000"
"ProtoVer"="1.2"

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge]
"NewTabPageLocation"="https://google.com"
```

注意 `google.com` 可以修改为任意你喜欢的网站地址,如果你想要空标签页可以写 `about:blank`

将上面的内容保存为 `msedge-newtab.reg` 然后打开就可以导入注册表，重启生效。

![](https://assets.den.dev/images/postmedia/edge-blank-new-tab/edge-updated-new-tab.png)

+ <https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies#newtabpagelocation>