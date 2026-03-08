# binance-square-profile-analyzer

> 币安广场用户主页内容抓取与创作风格分析工具 | 完全未登录态运行 | 17维度深度分析

## 简介

通过 3 个公开 API 端点，在**无需登录、无需 API Key**的情况下，抓取任意币安广场用户的全部历史帖子并生成深度分析报告。

实测：成功抓取无邪Infinity（@wuxie）2000条帖子，CZ 全部 67 条帖子（总浏览量 2.45 亿），Richard Teng 508 条帖子。

## 核心 API

| API 端点 | 功能 | 方法 |
|----------|------|------|
| `v1/friendly/pgc/search/query/intended` | 用户名搜索/模糊匹配 | GET |
| `v3/friendly/pgc/user/client` | 用户 Profile 信息 | POST |
| `v2/friendly/pgc/content/queryUserProfilePageContentsWithFilter` | 用户帖子列表（分页） | GET |

## 三种使用模式

### 1. profile — 查看用户概览
```bash
python3 scripts/binance_profile_analyzer.py profile "CZ"
```
返回：粉丝数、帖子数、简介、认证状态等。

### 2. fetch — 抓取全部帖子数据
```bash
python3 scripts/binance_profile_analyzer.py fetch "CZ" --output ./data
```
输出：`posts_<username>.csv` + `posts_<username>.json`

### 3. analyze — 抓取 + 深度分析报告
```bash
python3 scripts/binance_profile_analyzer.py analyze "CZ" --output ./report
```
输出：完整 Markdown 分析报告 + CSV/JSON 数据

## 17 维度分析报告

| 维度 | 内容 |
|------|------|
| 用户概览 | 粉丝/关注/帖子/点赞/分享 |
| 内容数据总览 | 总浏览量、平均互动率 |
| 发布频率 | 周均/月均发帖数 |
| 内容类型分布 | 短帖/长文/视频/直播占比 |
| 语言分布 | 中/英/其他 |
| 情绪倾向 | 看多/看空/中性 |
| 多媒体使用 | 含图率、含视频率 |
| 常用 Hashtag | Top 20 |
| 常提及币种 | Top 15 |
| 常提及用户 | Top 15 |
| 高频关键词 | Top 30 |
| 热门帖子（浏览量） | Top 10 |
| 热门帖子（互动率） | Top 10 |
| 发布时间分析 | 按小时/星期分布 |
| 月度发帖趋势 | 活跃周期可视化 |
| 内容长度分析 | 均值/中位数/最长最短 |
| 打赏统计 | 收打赏帖子及金额 |

## 目录结构

```
binance-square-profile-analyzer/
├── SKILL.md                          # OpenClaw Skill 说明文件
├── scripts/
│   └── binance_profile_analyzer.py   # 核心脚本
└── references/
    └── api_reference.md              # API 接口文档
```

## 依赖

```bash
pip install requests
```
仅需标准库 + requests，无其他依赖。

## 注意事项

- 完全未登录态运行，不需要 Cookie 或 API Key
- 支持模糊搜索（如输入 "Yi He" 自动匹配 "YiHe"）
- 建议抓取间隔 0.3s（默认），避免触发频率限制
- 单次最多抓取 2000 条（API 分页上限）

---

作者：**无邪Infinity** + **芒果**

---

## 💰 赞助支持

如果这个项目对你有帮助，欢迎赞助支持！

**BSC（BEP-20）钱包地址：**
```
0x3B74BE938caB987120C3661C8e3161CD838e5a1A
```
支持 USDT / BNB / 任意 BEP-20 代币。感谢每一位支持者 🙏

> 作者：**无邪Infinity** | Binance Square [@wuxie](https://www.binance.com/en/square/profile/wuxie) | X [@wuxie149](https://x.com/wuxie149)

