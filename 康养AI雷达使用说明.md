# 康养 AI 信息雷达

已准备好的配置文件是 `data/config.kangyang-ai.json`。它默认生成中文日报，并从权威卫生机构、医学与数字医疗期刊、全球新闻、中国新闻，以及相关社区中筛选内容。

## 默认选题范围

- 医疗人工智能、临床研究与数字疗法
- 老年健康、长寿、长期照护与银发经济
- 中国康养/医疗 AI 动态，以及国际监管、公共卫生和产品进展

每日最多保留 12 条，按“临床与科研、医疗 AI 与产品、康养与老龄化、政策与公共卫生”均衡编排；AI 评分低于 7 分的内容会被过滤。

## 启用前只需补齐

1. 在 `.env` 中填写 DeepSeek API 密钥。默认使用 `deepseek-v4-flash` 和官方 OpenAI 兼容端点；若改用其他服务商，需要同步修改配置中的 `provider`、`model` 和 `api_key_env`。
2. 创建企业微信群机器人，并把其 Webhook 地址保存为 `HORIZON_WEBHOOK_URL`。配置已使用企业微信的 Markdown 消息格式，日报会以一条消息推送。
3. 若用 GitHub 自动运行，将此项目推送到自己的私有或公开仓库，在仓库 Secrets 中保存模型密钥；不要把密钥写进配置文件。

## 本地试跑

将配置复制为 `data/config.json`，把 `.env.kangyang-ai.example` 复制为 `.env` 后填入密钥。安装依赖后执行 `uv run horizon --hours 24`。结果保存在 `data/summaries/`，可发布的日报会写入 `docs/`。

## 自动化建议

项目自带 GitHub Actions 工作流，会在温哥华当地时间早上 7:00 运行，并发布到 GitHub Pages。它会额外判断夏令时，避免一年中有半年的推送时间偏移一小时。
