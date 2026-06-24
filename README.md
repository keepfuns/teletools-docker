# TeleTools

基于 Telegram MTProto 协议的多功能消息监控与自动化管理工具，提供 Web 管理界面，支持 Docker 一键部署。

## 功能描述

- **消息监控** - 监听频道/群组/用户消息，支持关键词匹配、排除关键词过滤
- **媒体下载** - 匹配消息中的图片/视频/音频/文档自动下载到本地，支持断点续传
- **消息转发** - 将匹配消息转发到指定目标，支持超级转发
- **文件重命名** - 支持正则表达式替换文件名，支持从消息文本提取命名
- **定时推送** - 按 Cron 表达式定时发送消息到指定频道/群组/用户
- **音乐搜索** - 内置聆澜音乐源，设置秘钥后可通过 Bot 搜索歌曲
- **实时日志** - 日志通过 WebSocket 实时推送至浏览器，支持分级过滤
- **QR 登录** - 支持 QR 码扫码登录和手机号验证码登录
- **系统监控** - 实时展示 CPU、内存、磁盘使用量

## 快速开始

### 获取 Telegram API 凭证
- 访问 [my.telegram.org](https://my.telegram.org)
- 登录你的 Telegram 账号
- 进入 API Development Tools
- 创建新的应用程序，获取 `API_ID` 和 `API_HASH`

### Docker Run 部署

```
docker run -d \
--name teletools \
-p 8026:8026 \
-v /path/to/data:/app/data \
-v /path/to/downloads:/app/downloads \
-v /path/to/logs:/app/logs \
-e API_ID=your_api_id \
-e API_HASH=your_api_hash \
-e LICENSE_KEY=your_license_key \
-e PROXY_URL=your_proxy_url \
-e TZ=Asia/Shanghai \
--restart unless-stopped \
keepfuns/teletools:latest
```

### Docker Compose 部署

```
version: "3.8"
services:
  teletools:
    image: keepfuns/teletools:latest
    container_name: teletools
    ports:
      - "8026:8026"
    volumes:
      - ./data:/app/data
      - ./downloads:/app/downloads
      - ./logs:/app/logs
    environment:
      - API_ID=your_api_id
      - API_HASH=your_api_hash
      - LICENSE_KEY=your_license_key
      - PROXY_URL=your_proxy_url
      - TZ=Asia/Shanghai
    restart: unless-stopped
```

启动后访问 http://localhost:8026

## 环境变量

| 变量 | 必填 | 说明 |
|------|------|------|
| API_ID | 是 | Telegram API ID |
| API_HASH | 是 | Telegram API Hash |
| LICENSE_KEY | 是 | 软件许可证密钥 |
| PROXY_URL | 否 | 代理地址 (socks5/http) |
| DATA_DIR | 否 | 数据目录 (默认 ./data) |
| DOWNLOADS_DIR | 否 | 下载目录 (默认 ./downloads) |
| LOGS_DIR | 否 | 日志目录 (默认 ./logs) |
| TZ | 否 | 时区 (默认 Asia/Shanghai) |

## 许可证安装

 - 部署成功后查看日志，找到 `机器指纹` 
 - 发送 [开发者](https://t.me/luluprivatechatbot) 获取许可证秘钥
 - 设置环境变量 `LICENSE_KEY` 后重启

## 赞赏
- 如果您欣赏本项目，欢迎为它点亮一颗⭐️
- `1元1证`，尊重劳动成果，感谢您的支持🙏
<br/><br/>
<span><img src="assets/zhifubao.png" alt="支付宝" width="20%" align="left">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="assets/weixin.png" alt="微信 " width="20%" align="left"></span>
