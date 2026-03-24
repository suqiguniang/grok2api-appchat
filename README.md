# grok2api-appchat

一个已清理敏感信息、可直接公开发布的 Grok 到 OpenAI 兼容网关项目。

这个版本来自一套线上可运行的 Rust 版部署快照，已经去掉部署私货，只保留可复用源码、管理后台和默认配置模板，方便你二次维护并发布到自己的 GitHub 仓库。

## 主要功能

- Rust + Axum，支持单二进制和 Docker 部署
- OpenAI 兼容接口
  - `/v1/chat/completions`
  - `/v1/responses`
  - `/v1/images/generations`
  - `/v1/images/generations/nsfw`
  - `/v1/models`
  - `/v1/files/*`
- 内置管理后台
  - Token 管理
  - 配置管理
  - 缓存管理
  - 下游接口开关
  - 在线调试页

## 项目结构

```text
grok2api-appchat/
├─ src/
├─ static/
├─ docker/
├─ data/
│  └─ token.json.example
├─ config.defaults.toml
├─ docker-compose.yml
├─ Dockerfile
├─ NOTICE.md
└─ LICENSE
```

## 快速开始

### 1. 本地运行

```bash
mkdir -p data
cp config.defaults.toml data/config.toml
cp data/token.json.example data/token.json

cargo build --release
SERVER_HOST=0.0.0.0 SERVER_PORT=8000 ./target/release/grok2api-appchat
```

### 2. Docker 运行

```bash
mkdir -p data
cp config.defaults.toml data/config.toml
cp data/token.json.example data/token.json

docker build -t grok2api-appchat:latest .
docker compose up -d
```

默认后台地址：

- `http://127.0.0.1:8000/admin`

## 首次部署必须检查

- `app.app_key`
  后台登录密码，默认占位值是 `change-me`，上线前必须改
- `app.api_key`
  下游 Bearer Token，建议设置
- `app.app_url`
  服务的外部访问地址。生产环境必须改成真实外网 URL
- `grok.base_proxy_url`
  上游请求代理
- `grok.asset_proxy_url`
  图片/视频资源代理
- `grok.cf_clearance`
  需要 Cloudflare Cookie 时填写

## Token 文件格式

项目默认示例：

```json
{
  "ssoBasic": []
}
```

把你自己的 `sso` Token 按项目原有格式导入即可。不要把真实 Token、Cookie、代理地址提交到仓库。

## 公开发布前建议

1. 不要提交 `data/config.toml`
2. 不要提交 `data/token.json`
3. 不要在源码里写死域名、Cookie、代理、API key
4. 把 `docker-compose.yml` 的镜像名改成你自己的仓库名
5. 把 README 里的仓库地址、镜像地址改成你自己的

## GitHub Actions

项目自带 GHCR 发布工作流。

- push 到 `main` 时发布 `latest`
- push tag 时发布对应版本 tag

镜像名自动使用当前 GitHub 仓库名，不绑定任何固定账号。

## 开发与协作

- 变更记录见 [CHANGELOG.md](CHANGELOG.md)
- 贡献说明见 [CONTRIBUTING.md](CONTRIBUTING.md)
- 上游来源说明见 [NOTICE.md](NOTICE.md)

## 致谢

这个公开版基于以下上游项目整理：

- `XeanYu/grok2api-rs`
- `chenyme/grok2api`

更多信息见 [NOTICE.md](NOTICE.md)。

## 免责声明

仅供学习与研究。请自行评估合规、服务条款、账号安全和风控风险。
