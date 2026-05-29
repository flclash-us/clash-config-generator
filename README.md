# Clash 配置模板完整版 0ng029

[中文版] 开箱即用的 Clash 配置模板集，涵盖基础配置、高级分流、游戏加速、流媒体优化四大场景。

## 特性

- 多种代理分组策略（自动选择、故障转移、负载均衡）
- 优化的 DNS 设置，支持 DoH/DoT/DoQ
- 完整的分流规则，覆盖主流网站和应用
- 平台专属配置（Windows / macOS / Android / iOS / OpenWrt）
- 持续更新的规则集，适配最新网络环境

## 快速开始

1. 根据使用场景选择对应模板
2. 编辑模板中的代理提供者（proxy-providers），填入订阅链接
3. 导入 Clash for Windows 开始使用

## 模板说明

| 模板文件 | 适用场景 | 规则数量 |
|---------|---------|---------|
| basic.yaml | 新手入门，最小配置 | ~50条 |
| advanced.yaml | 进阶用户，全功能 | ~500条 |
| gaming.yaml | 游戏加速，低延迟 | ~100条 |
| streaming.yaml | 流媒体解锁（Netflix/YouTube/HBO） | ~200条 |

## 配置结构详解

port: 7890
socks-port: 7891
allow-lan: false
mode: rule
log-level: info

dns:
  enable: true
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  nameserver:
    - https://dns.alidns.com/dns-query
    - https://doh.pub/dns-query
  fallback:
    - https://1.1.1.1/dns-query

proxy-groups:
  - name: "Proxy"
    type: select
    proxies: [Auto, DIRECT]
  - name: "Auto"
    type: url-test
    proxies: [HK-1, JP-1, US-1]
    url: "http://www.gstatic.com/generate_204"
    interval: 300

rules:
  - DOMAIN-SUFFIX,google.com,Proxy
  - DOMAIN-KEYWORD,github,Proxy
  - DOMAIN-SUFFIX,cn,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,Auto

## 推荐客户端

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行
- [ClashMI](https://clashmi.site/) - 轻量级多平台
- [FlClash](https://flclash.us/) - 现代代理工具

## 常见问题

Q: 订阅链接无法导入？
A: 确保使用 Clash for Windows 最新版，订阅链接需 base64 编码或直接使用原始 YAML URL。

Q: 节点全部超时？
A: 检查系统代理是否正确设置为 127.0.0.1:7890，或更换 DNS 服务器。

## 许可证

MIT License

推荐工具

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行的 Clash 图形化客户端
- [ClashMI](https://clashmi.site/) - 轻量级 Clash 客户端，支持多平台
- [FlClash](https://flclash.us/) - 现代代理工具，支持多种协议