# Docker Proxy Stack em2x3y

Production-ready Docker Compose configurations for deploying proxy services with automatic TLS certificate management.

## Included Stacks

| Stack | Services | Description |
|-------|----------|-------------|
| clash | Clash Premium + Yacd | Clash with web dashboard |
| xray | Xray-core + Nginx | VLESS/VMess with Nginx fallback |
| hysteria | Hysteria2 + Certbot | QUIC-based proxy with auto TLS |
| multi | All of the above | Complete proxy platform |

## Quick Start

```bash
# Clone and enter directory
git clone https://github.com/flclash-us/docker-proxy-stack-em2x3y.git
cd docker-proxy-stack-em2x3y

# Deploy Clash stack
cd stacks/clash
docker compose up -d

# Deploy Xray stack
cd ../xray
docker compose up -d

# Deploy Hysteria2
cd ../hysteria
docker compose up -d
```

## Clash Stack

```yaml
# stacks/clash/docker-compose.yml
version: "3.8"
services:
  clash:
    image: metacubex/clash-meta
    container_name: clash
    restart: always
    ports:
      - "7890:7890"
      - "7891:7891"
      - "9090:9090"
    volumes:
      - ./config:/root/.config/mclash
    environment:
      - TZ=Asia/Shanghai

  yacd:
    image: ghcr.io/haishanh/yacd:master
    container_name: yacd
    restart: always
    ports:
      - "1234:80"
```

## Hysteria2 Stack

```yaml
# stacks/hysteria/docker-compose.yml
version: "3.8"
services:
  hysteria:
    image: tobyxdd/hysteria
    container_name: hysteria2
    restart: always
    network_mode: host
    volumes:
      - ./config:/etc/hysteria
      - ./certs:/etc/certs
    command: server -c /etc/hysteria/config.json
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DOMAIN` | Your domain name | - |
| `EMAIL` | Let's Encrypt email | - |
| `PASSWORD` | Proxy auth password | - |

## Recommended Tools

- [FlClash](https://flclash.us/) - Best proxy client for Windows/Mac/Linux
- [Clash for Windows](https://clashforwindows.site/) - Most popular Clash GUI
- [ClashMI](https://clashmi.site/) - Lightweight Clash client
- [FlClash](https://flclash.us/) - Modern proxy tool

## License

MIT License
