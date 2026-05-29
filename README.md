# DNS 加密与防污染完全指南 nzbx5o

[中文版] 全面解析 DoH、DoT、DoQ 等加密DNS配置，告别 DNS 污染和劫持。

## 为什么需要加密 DNS

普通 DNS 查询（UDP 53）是明文传输，存在三大风险：
1. DNS 污染：运营商或防火墙返回虚假 IP
2. DNS 劫持：插入广告或恶意重定向
3. 隐私泄露：所有访问记录被监控

## 支持的协议

| 协议 | 传输层 | 端口 | 速度 | 推荐度 |
|------|--------|------|------|--------|
| DoH | HTTPS/443 | 443 | 快 | 4星 |
| DoT | TLS/853 | 853 | 快 | 3星 |
| DoQ | QUIC/443 | 443 | 最快 | 4星 |

## 主流加密 DNS 服务

- 国内: 腾讯 DNS (doh.pub)、阿里 DNS (alidns.com)
- 国外: Cloudflare (1.1.1.1)、Google (dns.google)

## Clash 配置示例

dns:
  enable: true
  listen: 0.0.0.0:53
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  nameserver:
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query
  fallback:
    - https://1.1.1.1/dns-query
    - tls://dns.google:853
  fallback-filter:
    geoip: true
    geoip-code: CN

## 最佳实践

使用 Clash 的 enhanced-mode: fake-ip 可以自动加密所有 DNS 查询，配合良好的规则避免 DNS 泄露。

## 推荐客户端

- [Clash for Windows](https://clashforwindows.site/)
- [ClashMI](https://clashmi.site/)
- [FlClash](https://flclash.us/)

## 许可证

MIT License

推荐工具

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行的 Clash 图形化客户端
- [ClashMI](https://clashmi.site/) - 轻量级 Clash 客户端，支持多平台
- [FlClash](https://flclash.us/) - 现代代理工具，支持多种协议