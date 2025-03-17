---
title: Ubuntu系统配置python开发环境
date: 2025-03-17
lastmod: 2025-03-17
tags:
  - Ubuntu
  - python
categories:
  - 工具
image: /image/Ubuntu系统配置python开发环境/Ubuntu系统配置python开发环境.jpg
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
# 安装Python、pip和虚拟环境工具
```bash
sudo apt install python3 python3-pip python3-venv -y
```
## 验证python和pip是否安装成功
```bash
python3 --version
pip3 --version
```
输出示例：
```bash
Python 3.12.3
pip 24.0 from /usr/lib/python3/dist-packages/pip (python 3.12)
```

# 创建并激活虚拟环境
## 创建虚拟环境
创建虚拟环境目录（例如 `myenv`）：
```bash
python3 -m venv ~/myenv
```
`myenv`：虚拟环境名称
## 激活虚拟环境
```bash
source ~/myenv/bin/active
```
激活后命令行提示符前显示环境名称（如 `(myenv) rotos@RotosDev:~$`）。
## 退出虚拟环境
退出虚拟环境：输入`deactivate`即可退出

```bash
deactive
```
## 删除虚拟环境
删除虚拟环境：直接删除虚拟环境所对应的文件夹`myenv`即可

```bash
rm -rf ~/myenv
```
# 配置pip镜像源加速(推荐)
这里是**永久配置镜像源**，你也可以选择配置临时镜像源，这里不再给出具体方案，可自行搜索解决。
## 创建配置文件目录和文件
```bash
mkdir -p ~/.pip
vim ~/.pip/pip.conf
```
## 在文件中输入以下内容（以清华源为例）
```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

---
# 声明与注意事项
截至本文发布日期，上述安装方案在 Ubuntu 24.04.1 LTS 环境中实测验证有效。若后续因以下可能的原因导致操作失效：

1. 镜像源服务器临时故障（建议更换其他镜像源）

建议通过以下途径自行解决：  
- 访问镜像源官网（如[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)）获取最新配置。