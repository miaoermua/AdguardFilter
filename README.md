# AdguardFilter

**更合理 AdGuard 规则，轻松改善你的使用体验 - 专注于拦截追踪器和 HTTPDNS**

[![Stars](https://m3-markdown-badges.vercel.app/stars/3/3/miaoermua/AdguardFilter)](https://github.com/miaoermua/AdguardFilter)
[![Issues](https://m3-markdown-badges.vercel.app/issues/1/2/miaoermua/AdguardFilter)](https://github.com/miaoermua/AdguardFilter/issues)
[![Support](https://ziadoua.github.io/m3-Markdown-Badges/badges/Sponsor/sponsor1.svg)](https://www.miaoer.net/sponsor)
[![COPYING](https://ziadoua.github.io/m3-Markdown-Badges/badges/LicenceMIT/licencemit1.svg)](https://github.com/miaoermua/CatWrt/blob/main/LICENSE)

禁用常见软件内置 DNS，禁用 MIUI 反炸，禁用 MIUI 安装器 API，定期更新网络安全舆情，将 DNS 请求牢牢地把握自己手里。

使用人工亲测减少误杀可能，和 CatWrt 一样优秀！[⚠️ 误杀报告](https://github.com/miaoermua/AdguardFilter/issues/new?assignees=&labels=&projects=&template=hosts-report.md&title=)，欢迎大家 PR 修改参与到项目中来。


AdGuard Home: DNS 黑名单 - 添加黑名单 - 添加一个自定义列表

```url
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/rule.txt
```



不足之处可以使用 AdGuard DNS filter 这个默认规则进行补充，此 repo 最大限度保证可用性，DNS 样本数据仅来自：Apple，Xiaomi，OnePlus(Unlock Bootloader) 的部分内容……无法覆盖全部，必然会有没覆盖的厂商和漏网之鱼。

另外如果使用了 Apple 的规则，请确定你有定期帮忙去看看苹果会不会更新白名单域名这样的事，众所周知苹果也有草台班子，你也不想的苹果设备会遇到奇奇怪怪的问题～。

部分规则必定会参考到其他规则库，如有冒犯请见谅。

## 完整版

为了不影响存量用户 `rule.txt` 为标准规则，因为 Apple & Microsoft 较多域名，因此我们单独增加了白名单规则，遵循官方给出的白名单规则。如需要添加不仅仅需要添加黑名单还需要添加白名单才可以正常使用，
否则由 Apple 提供的服务将无法使用 (如: iCloud, Find, App Store, Apple Music ……)。

黑名单列表: `https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/bad_apple.txt`

白名单列表: `https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/whitelist.txt`

不建议使用 `adobe.txt` 这个规则，纯自用。

## 特色
### 去广告

只实现了关于微信广告，酷安广告，友盟，雷神加速器的广告 SDK 封禁。

### 跟踪器

去除了明显特征的跟踪器域名，米家可用。

### 内置 DNS

为什么屏蔽 APP 内置 DNS？因为内置 DNS 会绕过 AdGuard Home，去请求 APP 内置的 HTTPDNS / DoH，不利于我们追踪设备的 DNS 请求。对于我们而言，虽然可以获得 APP 厂商的 CDN 调度，但是厂商可以从 DNS 请求的角度，为用户打标签，获得更多角度的你（悄悄告诉你，在正常情况下，你使用 APP 内置浏览器访问别的网站，DNS 请求 也是走这个 HTTPDNS 哦？也就是说，你通过内置浏览器访问什么站，厂商也是知道的，同样可以作为你这个用户数据的一部分）。

*注意*：APP 启动后需要等待内置 DNS 超时，回落到 System DNS，这需要一定时间（在此期间 APP 可能几乎不可用）。

### BiliBili

为什么手机看 B 站不卡，电脑刷 B 站卡，电脑访问容易命中 PCDN 节点，这些节点质量参差不齐，可能会导致看 冷门视频/直播 严重卡顿，
通过规则后将 PCDN 域名封禁 `xy*.x*.x*.*xy-mcdn.bilivideo.com` 就会和手机端一样请求诸如 `upos-city-*cos.bilivideo.com` 这类官方 CDN 或者教育网 CDN，速度和质量有保证，在一般情况下，可以很好的缓解命中低质量 CDN 节点带来的卡顿，不保证高峰期依旧流畅。

*缺点*: 有几率不能缓存视频，因为解析下载的地址一般不会跟随播放器重定向，如遇到缓存视频问题可以临时加白，实测大部分情况不影响。

另外推荐将 B 站的部分域名通过 DNS 重写为 `A` ，使用 IPv4 较大可能将 B 站“使用 IPv6 卡顿”的问题进行缓解。
