# AdguardFilter

自用 Adguard 规则

禁用常见软件内置 DNS，禁用 MIUI 安装器 API，将 DNS 权力把握自己手里。

AdGuard Home: DNS 黑名单 - 添加黑名单 - 添加一个自定义列表 

```url
https://cdn.jsdelivr.net/gh/miaoermua/AdguardFilter@main/rule.txt
```

较快更新选我！

```url
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/rule.txt
```

## 内置 DNS

为什么屏蔽内置 DNS，因为内置 DNS 会绕过 Adguard 缓存去远端服务器请求，在 Adguard 具有远端 DNS 缓存后显得有写鸡肋而且 DNS 日志不在 Adguard 不安全！

## BiliBili

为什么手机看视频不卡，电脑刷视频卡，电脑频繁使用廉价的 PCDN 服务，PCDN 质量不行跑的业务非常多导致用户看视频卡顿明显，无论是 4k 还是 1080p 都非常卡顿，通过规则后将 PCDN 域名封禁 `xy*.x*.x*.*xy-mcdn.bilivideo.com` 就会和手机一样请求 `upos-city-*cos.bilivideo.com` 或者 `cn-gdcity-isp-*-*.bilivideo.com` 速度和质量有保证。