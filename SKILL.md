# 币安广场创作者主页分析 Skill (binance-square-profile-analyzer)

## 简介
这是一个用于抓取并分析币安广场（Binance Square）用户主页内容的 Skill。它可以帮助你了解特定创作者的写作风格、活跃度、互动数据以及创作偏好。**该 Skill 完全在未登录状态下运行，无需任何 API Key 或登录凭证。**

## 核心功能
1. **智能用户搜索**：支持通过关键词或模糊用户名搜索匹配币安广场用户。
2. **全量帖子抓取**：自动翻页抓取用户的所有历史帖子（支持限制抓取数量或按类型筛选）。
3. **深度内容分析**：
   - **基础数据**：总浏览量、点赞数、评论数、综合互动率等。
   - **发布习惯**：按小时、星期、月份的活跃度分布。
   - **内容偏好**：帖子类型（长文/短帖/视频）、情感倾向、多媒体使用比例。
   - **关键词与提及**：常用 Hashtag、常提及的币种、常提及的其他用户、高频词汇。
   - **热门内容**：按浏览量和互动率排序的 Top 10 帖子列表。

## 目录结构
```text
binance-square-profile-analyzer/
├── SKILL.md                              # 技能说明文件
├── scripts/
│   └── binance_profile_analyzer.py       # 核心抓取与分析脚本
└── references/
    └── api_reference.md                  # API 接口文档
```

## 使用方法

### 1. 查看用户概览 (profile)
仅获取用户的基本信息（粉丝数、帖子数、简介等），不抓取帖子。

```bash
python3 /home/ubuntu/skills/binance-square-profile-analyzer/scripts/binance_profile_analyzer.py profile "CZ"
```

### 2. 抓取用户帖子 (fetch)
仅抓取用户的帖子数据，并保存为 CSV 和 JSON 格式，不进行深度分析。

```bash
python3 /home/ubuntu/skills/binance-square-profile-analyzer/scripts/binance_profile_analyzer.py fetch "CZ" --output ./data
```

**可选参数：**
- `--filter` / `-f`: 筛选帖子类型（`ALL`, `ORIGINAL`, `QUOTE`, `LIVE`），默认 `ALL`。
- `--max-posts` / `-m`: 限制最大抓取帖子数（例如：`--max-posts 100`）。

### 3. 抓取并生成分析报告 (analyze)
抓取用户帖子并生成详细的 Markdown 分析报告。这是最常用的命令。

```bash
python3 /home/ubuntu/skills/binance-square-profile-analyzer/scripts/binance_profile_analyzer.py analyze "CZ" --output ./analysis_report
```

**输出文件包含：**
- `analysis_report_[username].md`: 详细的 Markdown 分析报告。
- `posts_[username].csv`: 帖子原始数据的 CSV 文件。
- `posts_[username].json`: 帖子原始数据的 JSON 文件。
- `analysis_[username].json`: 分析结果的 JSON 数据。
- `profile_[username].json`: 用户基本信息。

## 输出数据字段说明

在生成的 `posts_*.csv` 中，包含以下关键字段：
- `post_id`: 帖子唯一 ID
- `content_type`: 帖子类型 (short_post, long_article, video)
- `title`: 标题（仅长文有）
- `body_text`: 纯文本内容
- `language`: 语言
- `tendency`: 情感倾向 (neutral, bullish, bearish)
- `hashtags`: 包含的标签
- `trading_pairs`: 提及的交易对/币种
- `view_count`, `like_count`, `comment_count`, `share_count`, `quote_count`: 互动数据
- `create_time`: 发布时间 (UTC)

## 注意事项
- 该脚本通过公开 API 抓取数据，建议在连续抓取大量数据时适当控制频率。
- 如果搜索关键词包含空格，请使用引号包裹，例如 `"Richard Teng"`。
- 对于发帖量极大的用户（如数千条），抓取可能需要几分钟时间，请耐心等待。
