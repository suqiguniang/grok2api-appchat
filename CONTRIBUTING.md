# Contributing

感谢你愿意改这个项目。

## 基本原则

- 不要提交真实的 `token.json`
- 不要提交真实的 `config.toml`
- 不要把域名、Cookie、代理、API key、服务器 IP 写死到源码里
- 所有部署相关的私货都应该留在运行时配置，而不是仓库里

## 开发建议

1. 新功能优先保持 OpenAI 兼容接口不破坏现有字段。
2. 配置项改动要同步更新 `config.defaults.toml` 和 `README.md`。
3. 如果修改了镜像、启动方式或目录结构，也要同步更新 `docker-compose.yml` 和文档。
4. 新增公开发布内容时，先检查是否会泄露个人部署信息。

## 提交前检查

建议至少检查下面这些内容：

```bash
rg -n "token|cf_clearance|proxy|api_key|app_key|http://|https://" .
```

重点确认：

- 示例值是否还是示例值
- 文档里是否误放了你的域名
- 默认密码是否仍是占位值
- 没有把 `data/config.toml` 和 `data/token.json` 放进提交

## Issue / PR 建议

- 标题直接写问题，不要写成聊天句子
- 如果是接口兼容问题，请附最小请求示例
- 如果是生图问题，请说明：
  - 网页端是否能生图
  - 文本接口是否正常
  - 当前项目是否仍走旧的 imagine websocket 链路

## 许可证和来源

这个项目来自上游开源项目的整理版。

- 许可证见 `LICENSE`
- 来源说明见 `NOTICE.md`
