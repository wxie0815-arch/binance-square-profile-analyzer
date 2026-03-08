# Binance Square Profile API Reference

本文档记录了 `binance-square-profile-analyzer` Skill 所使用的币安广场公开 API 接口。这些接口均支持在**未登录态**下访问。

## 1. 搜索意图与用户建议 (Search Intent)

用于在不知道用户确切 username 时，通过关键词获取用户名建议。

- **URL**: `https://www.binance.com/bapi/composite/v1/friendly/pgc/search/query/intended`
- **Method**: GET
- **Query Parameters**:
  - `searchStr`: 搜索关键词（例如："CZ" 或 "Yi He"）
- **Response Data (部分)**:
  ```json
  {
    "code": "000000",
    "data": {
      "suggestionsList": ["CZ", "cz_binance"]
    }
  }
  ```

## 2. 用户主页信息 (User Profile)

获取用户的详细资料，包括粉丝数、简介、认证状态等。此接口需要准确的 `username`。

- **URL**: `https://www.binance.com/bapi/composite/v3/friendly/pgc/user/client`
- **Method**: POST
- **Body**:
  ```json
  {
    "username": "CZ",
    "getFollowCount": true,
    "queryFollowersInfo": true,
    "queryRelationTokens": true
  }
  ```
- **关键返回字段**:
  - `squareUid`: 用户的唯一 ID，**用于后续抓取帖子**
  - `displayName`: 显示名称
  - `biography`: 个人简介
  - `verificationType`: 认证类型 (0=未认证, 1=创作者, 2=官方)
  - `totalFollowerCount`: 粉丝总数
  - `totalListedPostCount`: 帖子总数
  - `totalLikeCount`: 累计获赞数

## 3. 用户帖子列表 (User Posts List)

获取用户主页的帖子列表，支持分页和类型筛选。

- **URL**: `https://www.binance.com/bapi/composite/v2/friendly/pgc/content/queryUserProfilePageContentsWithFilter`
- **Method**: GET
- **Query Parameters**:
  - `targetSquareUid`: 目标用户的 squareUid（从 Profile API 获取）
  - `timeOffset`: 分页游标。第一页传 `-1`，后续页传上一页返回的 `timeOffset`
  - `filterType`: 筛选类型。支持 `ALL` (全部), `ORIGINAL` (原创), `QUOTE` (引用), `LIVE` (直播)
- **Response Data 结构**:
  ```json
  {
    "code": "000000",
    "data": {
      "timeOffset": 1759928312999,
      "isExistSecondPage": true,
      "contents": [
        {
          "id": 293895202581969,
          "contentType": 1,
          "bodyTextOnly": "帖子纯文本内容...",
          "viewCount": 3193722,
          "likeCount": 5181,
          "commentCount": 1810,
          "shareCount": 150,
          "lan": "en",
          "tendency": 0
          // ... 更多字段
        }
      ]
    }
  }
  ```

## 关键请求头 (Headers)

调用以上所有 API 时，建议携带以下 Headers 以模拟真实浏览器请求：

```json
{
  "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
  "Accept": "*/*",
  "clienttype": "web",
  "lang": "en",
  "Origin": "https://www.binance.com",
  "Referer": "https://www.binance.com/en/square"
}
```
