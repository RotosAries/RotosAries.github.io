---
title: Ubuntu系统配置apt镜像源加速
date: 2025-03-16
lastmod: 2025-03-16
tags:
  - Ubuntu
  - apt
categories:
  - 系统配置
image: /image/Ubuntu系统配置apt镜像源加速/Ubuntu系统配置apt镜像源加速.jpg
top: 
hideFromHomePage: true
share: true
draft: false
---

# 查看 Ubuntu 系统版本

在配置镜像源之前，需要先确认您的 Ubuntu 系统版本，不同版本的配置文件路径和格式可能不同（**本文以Ubuntu 24.04.1 LTS为例**）。使用`lsb_release`命令查看版本信息：
```bash
lsb_release -a
```
输出示例：
```bash
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.1 LTS
Release:        24.04
Codename:       noble    #这个就是你的版本代号，找到与你版本适配的镜像源
```

# 备份原始的源配置文件

根据系统版本选择配置文件路径：
- **Ubuntu 24.04 及更新版本**：配置文件路径为`/etc/apt/sources.list.d/ubuntu.sources`（DEB822 格式）。
- **Ubuntu 22.04 LTS 及更早版本**：配置文件路径为 `/etc/apt/sources.list`（传统格式）。
```bash
# Ubuntu 22.04 及更早版本
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

# Ubuntu 24.04 及更新版本
sudo cp /etc/apt/sources.list.d/ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources.bak
```
# 编辑源配置文件

使用文本编辑器打开源配置文件：
```bash
# Ubuntu 22.04 及更早版本
sudo vim /etc/apt/sources.list

# Ubuntu 24.04 及更新版本
sudo vim /etc/apt/sources.list.d/ubuntu.sources
```
# 替换为国内镜像源
删除文件中的原始内容，根据版本代号（如 `jammy` 或 `noble`）选择合适的镜像源（这里以清华大学镜像源为例）。
## 清华大学镜像源（DEB822 格式，适用于 24.04 LTS）
```ini
Types: deb
URIs: https://mirrors.tuna.tsinghua.edu.cn/ubuntu/
Suites: noble noble-updates noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```
## 清华大学镜像源（传统单行格式，适用于 22.04 LTS）
```ini
# 默认注释了源码镜像以提高更新速度，需源码可取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
```
# 更新软件列表并升级系统
保存文件后，运行以下命令更新软件列表并升级系统：
```bash
sudo apt update && sudo apt upgrade -y
```
# 验证镜像源生效
执行以下命令检查软件源地址：
```bash
apt policy | grep http
```
输出中应包含配置的镜像地址（如 `mirrors.tuna.tsinghua.edu.cn`）。

---

# 声明与注意事项
截至本文发布日期，上述安装方案在 Ubuntu 24.04.1 LTS 环境中实测验证有效。若后续因以下可能的原因导致操作失效：

1. 镜像源服务器临时故障（建议更换其他镜像源）
2. 版本代号不匹配

建议通过以下途径自行解决：  
- 访问镜像源官网（如[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)）获取最新配置。