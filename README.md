# AdguardFilter

**更合理 AdGuard 规则，轻松改善你的使用体验 - 专注于拦截追踪器和 HTTPDNS**

禁用常见软件内置 DNS，禁用 MIUI 反炸，禁用 MIUI 安装器 API，将 DNS 请求牢牢地把握自己手里。

人工亲测减少误杀可能，和 CatWrt 一样优秀！[⚠️ 误杀报告](https://github.com/miaoermua/AdguardFilter/issues/new?assignees=&labels=&projects=&template=hosts-report.md&title=)

AdGuard Home: DNS 黑名单 - 添加黑名单 - 添加一个自定义列表

```url
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/rule.txt
```

## 完整版

因为不影响存量用户 rule.txt 为标准规则，因为 Apple & MicroSoft 较多域名，所以单独增加了白名单规则，遵循官方给出的白名单规则。如需要添加不仅仅需要添加黑名单还需要添加白名单才可以正常使用，否则由 Apple 提供的服务将无法使用 (如: iCloud,Find,App Store,Apple Music……)。

黑名单列表: `https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/bad_apple.txt`

白名单列表: `https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/whitelist.txt`

## 去广告

只实现了关于微信广告，酷安广告，友盟的封禁。

## 跟踪器

去除了明显特征的跟踪器域名，米家可用。

## 内置 DNS

为什么屏蔽 APP 内置 DNS？因为内置 DNS 会绕过 AdGuard Home，去请求 APP 内置的 HTTPDNS / DoH，不利于我们追踪设备的 DNS 请求。对于我们而言，虽然可以获得 APP 厂商的 CDN 调度，但是厂商可以从 DNS 请求的角度，为用户打标签，获得更多角度的你（悄悄告诉你，在正常情况下，你使用 APP 内置浏览器访问别的网站，DNS 请求 也是走这个 HTTPDNS 哦？也就是说，你通过内置浏览器访问什么站，厂商也是知道的，同样可以作为你这个用户数据的一部分）。

注意：APP 启动后需要等待内置 DNS 超时，回落到 System DNS，这需要一定时间（在此期间 APP 可能几乎不可用）。

## BiliBili

为什么手机看视频不卡，电脑刷视频卡，电脑访问容易命中 PCDN 节点，这些节点质量参差不齐，可能会导致看 冷门视频/直播 严重卡顿，通过规则后将 PCDN 域名封禁 `xy*.x*.x*.*xy-mcdn.bilivideo.com` 就会和手机端一样请求诸如 `upos-city-*cos.bilivideo.com` 这类官方 CDN 或者教育网 CDN，速度和质量有保证，在一般情况下，可以很好的缓解命中低质量 CDN 节点带来的卡顿，不保证高峰期依旧流畅。

*缺点*: 有很大几率不能缓存视频，因为解析下载的地址一般不会跟随播放器重定向。
