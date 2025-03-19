---
title: Ubuntu系统配置Vue开发环境
date: 2025-03-19
lastmod: 2025-03-19
tags:
  - Ubuntu
  - vue
categories:
  - 工具
image: /image/Ubuntu系统配置Vue开发环境/Ubuntu系统配置Vue开发环境.jpg
top: 
hideFromHomePage: 
share: true
draft: false
---

# 安装前提

更新软件包索引确保获取最新版本：
```bash
sudo apt update
```
安装必要的工具：curl、git：
```bash
sudo apt install -y curl git
```

# 安装 Node.js 和 npm

## 安装nvm
推荐使用 `nvm`（Node 版本管理工具），避免直接通过`apt`安装旧版：
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
注意：若遇到网络问题，可尝试更换网络环境或使用镜像源
### 重新加载.bashrc文件
```bash
source ~/.bashrc
```
### 验证安装
```bash
nvm -v
```
## 安装 npm和Node.js（以 LTS 版本为例）
```bash
nvm install --lts
```

### 验证安装
```bash
node -v
npm -v
```

## 配置 npm 镜像源（可选，国内用户推荐）
```bash
npm config set registry https://registry.npmmirror.com
```
# 安装官方命令行工具 Vue CLI
## 全局安装 Vue CLI

```bash
npm install -g @vue/cli
```
## 验证安装
```bash
vue --version
```
# 创建并运行 Vue 项目
## 创建新项目
```bash
vue create my-vue-app
```
使用 Vue CLI 创建项目，按提示选择配置，默认配置（Vue 3 + Babel + ESLint）或手动选择特性（如 Router、Vuex、TypeScript）
## 进入项目并启动开发服务器
```bash
cd my-vue-app
npm run serve
```
开发服务器默认运行在 `http://localhost:8080`
**注意：若遇到端口冲突可以在`vue.config.js`文件中调整端口号**
示例如下：
```JavaScript
module.exports = {
  devServer: {
    port: 8081  // 更换为可用端口
  }
}
```

---
# 声明与注意事项
截至本文发布日期，上述安装方案在 Ubuntu 24.04.1 LTS 环境中实测验证有效。若后续因以下可能的原因导致操作失效：

1. 镜像源服务器临时故障（建议更换其他镜像源）

建议通过以下途径自行解决：  
- 访问镜像源官网（如[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)）获取最新配置。