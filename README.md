# Clash 配置文件生成器

> 一键生成 Clash/Mihomo 配置文件 | YAML 配置模板 | 规则生成工具 | 订阅链接转换

[![Stars](https://img.shields.io/github/stars/flclash-us/clash-config-generator?style=flat)](https://github.com/flclash-us/clash-config-generator)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

---

## 🚀 功能特性

- ✅ **一键生成** - 输入订阅链接，自动生成完整配置
- ✅ **多协议支持** - SS/SSR/V2Ray/Trojan/Hysteria 等
- ✅ **规则模板** - 内置多种分流规则模板
- ✅ **自定义规则** - 支持添加自定义分流规则
- ✅ **配置优化** - 自动优化 DNS、TUN 等高级设置

---

## 📖 使用方法

### 在线生成

访问在线生成器：
- [Clash for Windows](https://clashforwindows.site/config-generator)
- [Clash 资源站](https://flclash.us/tools/config)

### 本地使用

```bash
# 克隆仓库
git clone https://github.com/flclash-us/clash-config-generator.git
cd clash-config-generator

# 安装依赖
pip install -r requirements.txt

# 运行生成器
python generator.py --subscription "你的订阅链接"
```

---

## 🔧 配置模板

### 基础模板

```yaml
# 基础配置
port: 7890
socks-port: 7891
mixed-port: 7892
allow-lan: true
bind-address: '*'
mode: rule
log-level: info
external-controller: 127.0.0.1:9090

# DNS 配置
dns:
  enable: true
  listen: 0.0.0.0:53
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  nameserver:
    - https://1.1.1.1/dns-query
    - https://8.8.8.8/dns-query

# 代理提供者
proxy-providers:
  my-subscription:
    type: http
    url: "订阅链接"
    interval: 3600
    path: ./providers/my-sub.yaml
    health-check:
      enable: true
      interval: 600
      url: http://www.gstatic.com/generate_204

# 代理组
proxy-groups:
  - name: "🚀 节点选择"
    type: select
    use:
      - my-subscription
    proxies:
      - DIRECT

  - name: "📹 国外媒体"
    type: select
    proxies:
      - "🚀 节点选择"
      - DIRECT

  - name: "Ⓜ️ 微软服务"
    type: select
    proxies:
      - DIRECT
      - "🚀 节点选择"

# 规则
rules:
  - DOMAIN-SUFFIX,google.com,🚀 节点选择
  - DOMAIN-SUFFIX,youtube.com,🚀 节点选择
  - DOMAIN-SUFFIX,netflix.com,🚀 节点选择
  - DOMAIN-SUFFIX,microsoft.com,Ⓜ️ 微软服务
  - GEOIP,CN,DIRECT
  - MATCH,🚀 节点选择
```

---

## 📋 规则集合

### 推荐规则源

```yaml
rule-providers:
  reject:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./ruleset/reject.yaml

  proxy:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
    path: ./ruleset/proxy.yaml

  direct:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./ruleset/direct.yaml

  private:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
    path: ./ruleset/private.yaml

  gfw:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml

  greatfire:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/greatfire.txt"
    path: ./ruleset/greatfire.yaml

  tld-not-cn:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml

  telegramcidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt"
    path: ./ruleset/telegramcidr.yaml

  cncidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
    path: ./ruleset/cncidr.yaml

  lancidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
```

---

## 🔗 相关资源

| 资源 | 链接 |
|------|------|
| Clash for Windows | [clashforwindows.site](https://clashforwindows.site) |
| Clash 资源站 | [flclash.us](https://flclash.us) |
| Android 教程 | [clashmi.site](https://clashmi.site) |

---

<p align="center">
  快速生成专业配置，轻松科学上网 🚀
</p>