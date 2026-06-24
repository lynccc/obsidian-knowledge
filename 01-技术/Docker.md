---
aliases: [容器, Docker容器]
tags: [技术, Docker, 容器, DevOps]
created: 2026-06-24
source: 奶茶一号整理
related: [[Linux]], [[服务器运维]]
---

# 🐳 Docker

## 核心概念

- **容器** — 轻量级的隔离环境，共享宿主机内核
- **镜像** — 只读模板，用于创建容器
- **Dockerfile** — 构建镜像的脚本
- **Docker Compose** — 多容器编排工具

## 常用命令

```bash
# 镜像操作
docker images              # 列出镜像
docker pull <image>        # 拉取镜像
docker build -t <name> .   # 构建镜像
docker rmi <image>         # 删除镜像

# 容器操作
docker ps                  # 查看运行中的容器
docker ps -a               # 查看所有容器
docker run -d <image>      # 后台运行容器
docker stop <container>    # 停止容器
docker rm <container>      # 删除容器
docker logs <container>    # 查看日志
docker exec -it <container> bash  # 进入容器
```

## Docker Compose 示例

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    restart: unless-stopped
```

## 最佳实践

- 使用 `.dockerignore` 排除不需要的文件
- 多阶段构建减小镜像体积
- 使用 `alpine` 版本镜像更轻量
- 容器不要存储状态数据

## 相关笔记

- [[Linux]] — 基础系统
- [[服务器运维]] — 部署相关
- [[Node.js]] — 常用 Docker 场景

---

*由奶茶一号整理 🧋*
