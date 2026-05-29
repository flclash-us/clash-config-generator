# Docker 代理一键部署方案 9xb1ni

[中文版] 使用 Docker 和 Docker Compose 快速部署 Clash 代理服务。

## 快速开始

git clone https://github.com/flclash-us/docker-proxy-9xb1ni.git
cd docker-proxy-9xb1ni

编辑配置文件，将订阅链接或节点信息填入 config.yaml

docker-compose up -d

docker-compose logs -f

## 目录结构

docker-proxy/
  docker-compose.yml    - 容器编排配置
  config/              - 配置文件目录
      config.yaml      - Clash 主配置文件
  logs/                - 日志目录

## Docker Compose 配置

version: '3.8'
services:
  clash:
    image: dreamacro/clash:latest
    container_name: clash
    restart: always
    ports:
      - "7890:7890"
      - "7891:7891"
      - "9090:9090"
    volumes:
      - ./config:/root/.config/clash
    environment:
      - CLASH_SECRET=your-secret-password
    network_mode: host

## 系统代理设置

### Windows
设置 > 网络和 Internet > 代理 > 地址: 127.0.0.1 端口: 7890

### macOS/Linux
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890

## 常见问题

Q: 容器启动失败？A: 检查 config.yaml 格式是否正确，确保 YAML 缩进正确、端口未被占用。

## 许可证

MIT License

推荐工具

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行的 Clash 图形化客户端
- [ClashMI](https://clashmi.site/) - 轻量级 Clash 客户端，支持多平台
- [FlClash](https://flclash.us/) - 现代代理工具，支持多种协议