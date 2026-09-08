# 免费抖音竞品研究助手

按关键词或指定账号读取抖音公开作品样本，输出竞品矩阵、钩子结构、可见证据、差异机会和选题建议。它只看当前页面可见信号，不复制作品原文，不推断后台数据，也不声称掌握平台算法。

## 能做什么

- 研究一个公开账号页、一个或多个关键词搜索页的作品卡片。
- 对每个样本标注视频/图文、钩子结构、开场动作、受众承诺和证据来源。
- 提供基于样本结构的差异化测试方向与 3 条选题建议。
- `mock` 模式完全离线；`easy-webbridge` 模式复用用户已授权浏览器，只读并在结束时关闭本次会话。

## 开始使用

最小请求：

```json
{
  "runtime": "mock",
  "accountAlias": "fixture-tech-competitors",
  "accountUrl": "https://www.douyin.com/user/fixture",
  "keywords": ["AI工具"],
  "sampleLimit": 8
}
```

本地 mock：

```bash
node scripts/douyin-competitor-research-free.mjs collect \
  --request fixtures/request-valid.json \
  --input fixtures/visible-snapshot-success.json \
  --output ./output/competitors
node scripts/douyin-competitor-research-free.mjs analyze \
  --snapshot ./output/competitors/research-snapshot.json \
  --output ./output/competitors
```

真实浏览器：先安装并启动 [Easy WebBridge](https://github.com/xxjrq/easy-webbridge)，在目标浏览器完成抖音登录，再运行：

```bash
node scripts/douyin-competitor-research-free.mjs list
node scripts/douyin-competitor-research-free.mjs collect \
  --request ./request.json --output ./output/competitors
node scripts/douyin-competitor-research-free.mjs analyze \
  --snapshot ./output/competitors/research-snapshot.json \
  --output ./output/competitors
```

## 输出

- `research-snapshot.json`：带 runtime 标记的公开页面快照，不含原文。
- `competitor-research.json`：结构化竞品矩阵、钩子统计、证据、差异机会和选题建议。
- `competitor-research.md`：可读研究报告，适合人工审核。
- `run-diagnostic.json`：登录、验证码、空页面、浏览器选择或输入错误诊断。

## 边界

结果只代表指定页面在采集时刻的公开可见样本，不代表全网排名、播放效果、转化率或算法规律。脚本不会保存标题、简介、字幕、评论等原文，不读取 Cookie、Token 或后台接口，不执行互动和发布。页面要求登录或验证时，在浏览器中人工处理后重试。

MIT License，见 [LICENSE](LICENSE)。
