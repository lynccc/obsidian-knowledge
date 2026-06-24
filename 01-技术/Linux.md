---
aliases: [linux, 系统, 服务器]
tags: [技术, Linux, 系统, 运维]
created: 2026-06-24 15:27
source: 奶茶一号整理
related: [[Docker]], [[服务器运维]]
---

# 🐧 Linux

## 核心概念

- **一切皆文件** — 设备、进程、网络都是文件
- **权限** — 读(r)、写(w)、执行(x)
- **进程** — 运行中的程序
- **Shell** — 命令行解释器（bash、zsh）

## 常用命令

```bash
# 文件操作
ls -la                      # 列出文件（含隐藏）
cd /path                    # 切换目录
pwd                         # 当前路径
mkdir -p dir                # 创建目录
cp -r src dst               # 复制
mv src dst                  # 移动/重命名
rm -rf dir                  # 删除（危险！）

# 查看文件
cat file                    # 查看全部
less file                   # 分页查看
head -n 10 file             # 前10行
tail -f file                # 实时追踪

# 权限
chmod 755 file              # 设置权限
chown user:group file       # 设置所有者

# 进程
ps aux                      # 查看进程
top                         # 实时监控
kill -9 pid                 # 强制结束进程

# 网络
netstat -tlnp               # 查看端口
curl url                    # HTTP请求
ping host                   # 测试连通性

# 磁盘
df -h                       # 磁盘使用
du -sh dir                  # 目录大小
```

## 常用技巧

### 管道和重定向
```bash
cmd1 | cmd2                 # 管道：cmd1 输出作为 cmd2 输入
cmd > file                  # 重定向到文件（覆盖）
cmd >> file                 # 追加到文件
cmd 2>&1                    # 错误输出合并
```

### 后台运行
```bash
cmd &                       # 后台运行
nohup cmd &                 # 后台运行，断开终端不停止
screen -S name              # 创建会话
screen -r name              # 恢复会话
```

## 相关笔记

- [[Docker]] — 容器化
- [[服务器运维]] — 部署和维护

---

*由奶茶一号整理 🧋*
