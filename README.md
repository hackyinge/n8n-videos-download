# 🚀 Video Download API (Douyin & TikTok)

[![Docker](https://img.shields.io/badge/Docker-Supported-blue.svg?logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-GPL%20v3-green.svg)](https://github.com/evil0ctal/douyin_tiktok_download_api)
[![Status](https://img.shields.io/badge/Status-Running-brightgreen.svg)]()

一个基于 [douyin_tiktok_download_api](https://github.com/evil0ctal/douyin_tiktok_download_api) 深度优化的本地视频下载服务，支持抖音 (Douyin) 与 TikTok 视频的高效解析与下载。

---

## ✨ 核心特性

- **多平台支持**：完美支持抖音 Web 端、TikTok Web 端及 App 端解析。
- **Docker 化部署**：一键启动，环境隔离，无需担心依赖冲突。
- **自动 Token 维护**：内置 msToken 与 ttwid 自动生成/分发机制。
- **高性能**：基于 FastAPI 构建，响应迅速，支持高并发解析。

---

## 🛠️ 快速开始 (本地部署)

### 1. 环境准备
确保您的机器已安装：
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Docker Compose

### 2. 启动服务
在项目根目录下执行以下命令：

```bash
# 启动容器
docker-compose up -d
```

### 3. 访问服务
服务启动后，可以通过以下地址访问 Web 界面或 API 文档：
- **Web UI**: [http://localhost:8000](http://localhost:8000)
- **API Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)

---

## ⚙️ 关键配置说明

项目通过根目录下的 `config.yaml` 进行统一管理。

### 🔑 修改 Cookie (重要)
为了保证解析成功率（特别是大规模抓取），建议在 `config.yaml` 中配置您个人的 Cookie：

1. 打开浏览器访问 [抖音](https://www.douyin.com/) 或 [TikTok](https://www.tiktok.com/)。
2. 按 `F12` 打开开发者工具 -> `Network` -> 刷新页面。
3. 找到任意请求，复制 `Headers` 中的 `Cookie` 字段。
4. 将其粘贴至 `config.yaml` 对应节点的 `Cookie` 字段中。

### 🔄 同步配置
在修改根目录的 `config.yaml` 后，请运行以下同步指令以更新容器配置：

```bash
# 同步配置到子服务目录
cp config.yaml douyin_tiktok_download_api/douyin_web/config.yaml && \
cp config.yaml douyin_tiktok_download_api/tiktok_web/config.yaml && \
cp config.yaml douyin_tiktok_download_api/tiktok_app/config.yaml

# 重启容器使配置生效
docker-compose restart
```

---

## ❓ 常见问题排查 (Troubleshooting)

- **AttributeError / KeyError**: 
  - 确保 `config.yaml` 中包含完整的 `douyin` 和 `tiktok` 节点。
  - 确保 `msToken` 节点下存在 `User-Agent` 字段。
- **ValueError: Unknown scheme for proxy**:
  - 如果不使用代理，请确保 `proxies` 下的 `http` 和 `https` 字段为 **留空**（不要写成 `""`）。
- **Mac 无法访问**:
  - 本项目已针对 Mac 环境将 `network_mode: host` 修改为端口映射模式 (`8000:80`)。

---

## 📜 免责声明
本项目仅供学术研究和技术交流使用，请勿用于任何商业用途或非法获取他人隐私。使用者在利用本项目进行任何操作时，需遵守当地法律法规及平台方服务协议。

---

> *“简单、高效、优雅的视频下载利器。”* 🚀
