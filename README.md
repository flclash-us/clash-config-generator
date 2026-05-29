# OpenWrt 路由器代理配置完整指南 mktp97

[中文版] 在 OpenWrt 路由器上一键部署 Clash，实现全设备透明代理。

## 环境要求

- OpenWrt 21.02 或更高版本
- 至少 8MB Flash + 128MB RAM
- 已开启 SSH 访问

## 安装步骤

### Step 1: 更新软件包
opkg update
opkg install luci git git-http

### Step 2: 安装 Clash
wget https://github.com/frainzy1477/clash/releases/download/v1.18.0/clash-linux-arm64.gz
gunzip clash-linux-arm64.gz
mv clash-linux-arm64 /usr/bin/clash
chmod +x /usr/bin/clash
mkdir -p /etc/clash

### Step 3: 配置并启动
vi /etc/clash/config.yaml  # 填入你的配置
# /etc/rc.local 添加: clash -d /etc/clash &

## 透明代理配置

dns:
  enable: true
  listen: 0.0.0.0:53
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  nameserver:
    - 223.5.5.5
  fallback:
    - 1.1.1.1
  fallback-filter:
    geoip: true
    geoip-code: CN

## 常见问题

Q: Clash 启动报错？A: 检查 config.yaml 格式和 YAML 缩进。
Q: 透明代理无效？A: 确认 iptables 规则已添加。

## 许可证

MIT License

推荐工具

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行的 Clash 图形化客户端
- [ClashMI](https://clashmi.site/) - 轻量级 Clash 客户端，支持多平台
- [FlClash](https://flclash.us/) - 现代代理工具，支持多种协议