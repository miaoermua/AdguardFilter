# AdguardFilter

**A more practical AdGuard rule set for blocking trackers and app-provided DNS services.**

[![Stars](https://m3-markdown-badges.vercel.app/stars/3/3/miaoermua/AdguardFilter)](https://github.com/miaoermua/AdguardFilter)
[![Issues](https://m3-markdown-badges.vercel.app/issues/1/2/miaoermua/AdguardFilter)](https://github.com/miaoermua/AdguardFilter/issues)
[![Support](https://ziadoua.github.io/m3-Markdown-Badges/badges/Sponsor/sponsor1.svg)](https://www.miaoer.net/sponsor)
[![LICENSE](https://ziadoua.github.io/m3-Markdown-Badges/badges/LicenceMIT/licencemit1.svg)](https://github.com/miaoermua/CatWrt/blob/main/LICENSE)

This project:

- reduces common app-level DNS bypasses;
- disables the MIUI "anti-bricking" and MIUI installer APIs;
- blocks selected advertising and tracking domains;
- is updated periodically based on network-security reports and testing.

The rules are manually tested as much as possible to reduce false positives. If a rule breaks a service, please open a [false-positive report](https://github.com/miaoermua/AdguardFilter/issues/new?assignees=&labels=&projects=&template=hosts-report.md&title=).

## Regional coverage

This list is not a complete global DNS blocklist.

A substantial portion of the rules—roughly half—targets products and services commonly used in mainland China, including Xiaomi/MIUI, Chinese app SDKs, Chinese advertising networks, Bilibili PCDN domains, and similar ecosystem traffic. The basic list therefore should not be treated as a replacement for an international DNS filter.

It does include Apple and Microsoft-related rules and can coexist with rules for other regions, but coverage varies by country, vendor, and app. International services are only covered where a specific rule or whitelist entry is present. For example, the Apple rules cover known Apple infrastructure and require matching whitelist entries for normal operation.

If you use another DNS filter at the same time, review which list owns each blocked domain. Conflicting blocklists can make troubleshooting and false-positive reports misleading.

## AdGuard Home setup

In AdGuard Home:

1. Open **Filters**.
2. Open **DNS blocklists**.
3. Select **Add blocklist**.
4. Choose **Add a custom list**.
5. Paste one of the URLs below.

You can use `miaoermua/AdguardFilter` as the custom-list name.

### Basic rules

```text
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/rule.txt
```

The basic list is the recommended starting point. It aims to block common tracking, advertising SDK, and app-level DNS behavior while keeping more broadly required domains available.

### Full rules

The full setup is only for users who also need the Apple/Microsoft-oriented rules in `bad_apple.txt` and the corresponding entries in `whitelist.txt`.

Add the blocklist:

```text
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/bad_apple.txt
```

Add the whitelist:

```text
https://raw.githubusercontent.com/miaoermua/AdguardFilter/main/whitelist.txt
```

Both lists must be enabled together. Otherwise, Apple services may stop working, including iCloud, Find My, the App Store, Apple Music, and related services.

The list cannot cover every vendor or every app. Current samples come mainly from Apple, Xiaomi, and OnePlus unlock-related software, with some additional community and security-report sources. The default AdGuard DNS filter may be added as a supplement when broader international coverage is needed.

Apple whitelist entries should be reviewed periodically because Apple may change its service endpoints. The whitelist also records known Apple infrastructure rather than promising complete or permanent compatibility.

## Main features

### Advertising

The rules block selected advertising SDK and ad-delivery domains, including traffic associated with WeChat advertising, CoolApk advertising, UMeng, and Thunder Accelerator.

### Tracking

The rules remove domains with clear tracking signatures. Xiaomi/MIUI service functionality is tested where possible.

### App-provided DNS

Apps sometimes send DNS, HTTPDNS, or DoH/DoT requests themselves instead of using the device system resolver. Blocking these requests makes the app fall back to normal system DNS through AdGuard, making DNS activity easier to audit.

This may have a downside: after an app starts, it may wait for the blocked built-in DNS request to time out before falling back to system DNS. During that delay, an app or a network-dependent feature may appear unavailable. Some domains are deliberately exempted when blocking them would cause a practical usability problem.

### Bilibili PCDN

On mobile, Bilibili may use different CDNs than a desktop client. Low-quality PCDN endpoints may cause stuttering for less popular videos or live streams.

This project includes rules that reduce matching to PCDN-style domains such as `xy*.x*.x*.*xy-mcdn.bilivideo.com`, encouraging official or education-network CDN endpoints where applicable.

This is a traffic-routing preference, not a guarantee that peak-time playback will be smooth. Cached downloads may occasionally fail because the final media URL does not follow the expected player redirect. Add the affected domain to a temporary exception if this happens.

You can also use AdGuard DNS rewrites to resolve supported Bilibili domains to IPv4 `A` records. This may reduce playback problems on IPv6 networks, but it is not guaranteed to work for every region or ISP.

## Maintenance policy

- `rule.txt` is the basic list.
- `whitelist.txt` contains whitelist entries used by the full Apple setup.
- `bad_apple.txt` contains the full Apple-oriented blocklist.
- `adobe.txt` is provided for personal use and is not generally recommended.

The project preserves source comments and original DNS rule lines until they are deliberately updated. Original domain records should not be rewritten as a side effect of translating or maintaining documentation.

Some domains originate from community reports or public security reporting rather than a vendor's official threat disclosure. Blocking is considered reasonable when the domain has no confirmed purpose or criticality and is unlikely to break a known application feature. Every reported false positive is reviewed for usability impact.

## Compatibility checklist

Before enabling the full set:

- test iCloud, App Store, Apple Music, Find My, and device update services;
- review existing blocklists for conflicting overrides;
- use a temporary whitelist when testing a suspected false positive;
- keep a fallback resolver available;
- re-check the whitelist after Apple publishes changes to service endpoints.

## Contributing

Pull requests and false-positive reports are welcome. Please include the affected domain, app or service, device/OS, resolver, and steps to reproduce. Avoid reporting only that a domain exists: explain how the block affects real behavior.
