# 👨‍🎨 Binance Square Profile Analyzer — 币安广场创作者主页分析 Skill

[![Version](https://img.shields.io/badge/version-1.1.0-blue)](https://github.com/wxie0815-arch/binance-square-profile-analyzer)
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Compatible-green)](https://openclaw.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> 抓取并分析币安广场创作者的用户主页，深入了解其写作风格、活跃度、互动数据和创作偏好。无需登录凭证，支持17个维度的深度分析。

## 🎯 功能概述

`binance-square-profile-analyzer` 是一个独立的分析工具，同时也是 `binance-square-oracle` 的核心数据来源（L6层），用于生成用户写作风格指纹。

## ✨ 核心特性

- **智能用户搜索**：通过关键词或模糊用户名搜索匹配币安广场用户。
- **全量帖子抓取**：自动翻页抓取用户的所有历史帖子（最多2000条）。
- **17维度深度分析**：生成包含发布习惯、内容偏好、关键词、热门内容等维度的详细分析报告。
- **无需认证**：所有抓取均在未登录状态下通过公开API完成。
- **多格式输出**：支持将数据保存为 CSV、JSON，并生成 Markdown 格式的分析报告。

## 🚀 快速开始

### 安装

```bash
gh repo clone wxie0815-arch/binance-square-profile-analyzer
cd binance-square-profile-analyzer
```

### 命令行使用

```bash
# 抓取用户 "CZ" 的帖子并生成完整分析报告
python3 scripts/binance_profile_analyzer.py analyze "CZ" --output ./report

# 仅抓取用户 "CZ" 的前50条帖子数据
python3 scripts/binance_profile_analyzer.py fetch "CZ" --max-posts 50 --output ./data

# 仅获取用户 "CZ" 的基本信息
python3 scripts/binance_profile_analyzer.py profile "CZ"
```

### 作为模块使用

```python
import sys
sys.path.insert(0, 'scripts')
from binance_profile_analyzer import fetch_user_profile, fetch_user_posts, analyze_content

# 获取用户信息
profile = fetch_user_profile("CZ")

# 抓取帖子
posts = fetch_user_posts(profile["square_uid"], max_posts=50)

# 分析内容
analysis = analyze_content(posts, profile)
```

详细的命令行参数和输出文件说明，请参考 `SKILL.md`。

## 🔗 相关 Skill

| Skill | 说明 | 仓库 |
|-------|------|------|
| `binance-square-oracle` | 集成此分析功能的完整预言机 | [wxie0815-arch/binance-square-oracle](https://github.com/wxie0815-arch/binance-square-oracle) |

## 📄 许可证

MIT License

---

## 💰 赞助支持

如果这个项目对您有帮助，欢迎赞助支持！

**BSC（BEP-20）钱包地址：**
`0x3B74BE938caB987120C3661C8e3161CD838e5a1A` 

支持 USDT / BNB / 任意 BEP-20 代币。感谢每一位支持者 🙏

**作者：** 无邪Infinity | 币安广场 [@wuxie](https://www.binance.com/en/square/profile/wuxie) | X [@wuxie149](https://x.com/wuxie149)
