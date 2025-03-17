---
title: Ubuntu系统使用Homebrew安装Nushell
date: 2025-02-21
lastmod: 2025-03-16
tags:
  - Ubuntu
  - Shell
categories:
  - 工具
image: /image/Ubuntu系统使用Homebrew安装Nushell/Ubuntu系统使用Homebrew安装Nushell.jpg
top: false
hideFromHomePage: false
share: true
draft: false
---

# 安装前提

更新软件包索引确保获取最新版本：
```bash
sudo apt update
```
# 安装软件包管理器Homebrew

Ubuntu推荐使用[Homebrew](https://brew.sh/)
## 安装编译依赖
```bash
sudo apt install -y build-essential curl file git
```
这些依赖包含编译器工具链、下载工具和版本控制系统
## 执行安装脚本
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
注意：若遇到网络问题，可尝试更换网络环境或使用镜像源
## 配置环境变量
```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
```
若使用zsh，请将`.bashrc`改为`.zshrc`
## 重新加载.bashrc文件
```bash
source ~/.bashrc
```
## 验证安装
```bash
brew --version
```
正常应显示版本信息（如：Homebrew 4.4.20）
# 安装Nushell
## 通过brew安装
```bash
brew install nushell
```
## 验证安装
```bash
nu --version
```
成功安装会显示类似：0.102.0
# 使用说明
## 启动Nushell
```bash
nu
```
输入`exit`可退出返回原shell环境
## 兼容性说明
重要注意事项：

- Nushell与传统Bash存在语法差异
- 部分Bash脚本可能需要修改才能运行
- 系统级脚本（如apt）建议仍在Bash中执行

**故这里推荐手动启动NuShell**，你也可以选择将其配置成默认的shell，这里不再给出具体方案，可自行搜索解决。

---

# 声明与注意事项
截至本文发布日期，上述安装方案在 Ubuntu 22.04.5 LTS 环境中实测验证有效。若后续因可能的以下原因导致操作失效：

1. 官方软件包更新引发的兼容性问题
2. 第三方仓库结构调整或脚本变更
3. 系统环境差异导致的意外错误

建议通过以下途径自行解决：  
- 查看 [Homebrew官方文档](https://brew.sh/) 或 [Nushell GitHub仓库](https://github.com/nushell/nushell) 获取最新指南