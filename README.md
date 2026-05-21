# TG-Monitor

Telegram 消息监控工具。

## 主要功能

### 监控转发

- 可以同时监控多个 Telegram 频道、群组、机器人、用户的消息，并自动转发对应目标
- 配置 ID、用户名、名称等任一标识皆可匹配来源和目标
- 每个监控源可设置独立的`关键词/排除关键词`，灵活过滤消息
- 支持文本、图片、视频、音频、文档等多种媒体格式的原样转发
- 自动检测频道是否开启`禁止转发`，强制启用重构发送模式
- 重构发送模式自动提取消息中的超链接和按钮链接，以文字形式追加

### 定时发送

- 基于标准 Cron 表达式精确控制消息发送时间（如每天 2 点：`0 2 * * *`）
- 支持向频道、群组、用户定时发送文本消息
- 支持手动立即执行任意定时任务

### 下载管理

- 监控命中规则的媒体文件（图片、视频、音频、文档等）自动下载
- 支持并发下载（默认 `3` 个），超限任务自动排队等待
- 支持自定义重命名规则（正则替换）
- 下载进度实时追踪，支持 `WebSocket` 推送

### 通知推送

- 通过 `Telegram Bot API` 推送事件通知
- 支持监控命中通知和定时发送完成通知
- 自动适配 `SOCKS5` 和 `HTTP` 代理，失败时自动降级直连

## 运行步骤

### 1. 获取 Telegram API 凭证

- 访问 [my.telegram.org](https://my.telegram.org)
- 登录你的 Telegram 账号
- 进入 API Development Tools
- 创建新的应用程序，获取 `api_id` 和 `api_hash`

### 2. Docker Compose 部署（推荐）

在项目目录下创建 `docker-compose.yml`：

```yaml
services:
  tg-monitor:
    image: keepfuns/tg-monitor:latest
    container_name: tg-monitor
    restart: always
    ports:
      - "8026:8026"
    volumes:
      - ./data:/app/data
      - ./logs:/app/logs
      - ./downloads:/app/downloads
    environment:
      - API_ID=你的API_ID
      - API_HASH=你的API_HASH
      # - PROXY_URL=socks5://127.0.0.1:1080  # 可选
```

### 3. 环境变量说明

| 变量 | 必填 | 默认值 | 说明 |
|------|------|--------|------|
| API_ID | 是 | - | Telegram API ID |
| API_HASH | 是 | - | Telegram API Hash |
| PROXY_URL | 否 | 空 | 代理地址（socks5:// 或 http://） |
| DATA_DIR | 否 | ./data | 数据存储目录 |
| DOWNLOADS_DIR | 否 | ./downloads | 文件下载目录 |
| LOGS_DIR | 否 | ./logs | 日志文件目录 |

### 4. 许可证安装

 * 部署成功后查看日志，找到 `机器指纹` 发给 [开发者](https://t.me/luluprivatechatbot) 生成许可证文件 `license.key`
 * 将生成的 `license.key` 放入容器 `/app/data/` 目录后重启

## 赞赏
- 如果您欣赏本项目，欢迎为它点亮一颗⭐️
- `1元1证`，尊重劳动成果，感谢您的支持🙏
<br/><br/>
<span><img src="assets/zhifubao.png" alt="支付宝" width="20%" align="left">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="assets/weixin.png" alt="微信 " width="20%" align="left"></span>