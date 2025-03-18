---
title: Ubuntu系统安装crawl4ai
date: 2025-03-18
lastmod: 2025-03-18
tags:
  - Ubuntu
  - python
  - 爬虫
categories:
  - 工具
image: /image/Ubuntu系统安装crawl4ai/Ubuntu系统安装crawl4ai.jpg
top: 
hideFromHomePage: 
share: true
draft: false
---

# 安装前提
**需要python开发环境**，[点击此处查看如何配置](https://rotosaries.github.io/posts/ubuntu系统配置python开发环境/)
# 使用虚拟环境(推荐)

## 创建虚拟环境
```bash
python3 -m venv venv_crawl4ai
```
`venv_crawl4ai`：虚拟环境名称
创建成功后会在当前目录下生成一个以`venv_crawl4ai`为名称的文件夹，它就是创建成功的虚拟环境
## 激活虚拟环境
在虚拟环境所在目录下，运行以下命令即可激活虚拟环境：
```bash
source venv_crawl4ai/bin/activate
```

- 命令提示符变为`(venv_crawl4ai) rotos@RotosDev:~$`：即代表已经进入该虚拟环境
- 退出虚拟环境：输入`deactivate`即可退出
- 删除虚拟环境：直接删除虚拟环境所对应的文件夹`venv_crawl4ai`即可
# 安装Crawl4AI核心包
```bash
pip install crawl4ai
```
注意：若遇到网络问题，可尝试更换网络环境或使用镜像源
# 运行安装后设置

安装完成后，运行以下命令以完成环境配置：
```bash
crawl4ai-setup
```
此命令会安装必要的 Playwright 浏览器（如 Chromium、Firefox 等），并检查操作系统级别的依赖（如`libnss3`、`libgbm-dev`等）。

# 验证安装

```bash
crawl4ai-doctor
```
此命令会检查浏览器安装状态、依赖项完整性和环境配置。
# 脚本测试

创建一个简单的 Python 脚本（如 `test_crawl.py`），并运行以下代码以验证crawl4ai是否正常使用：
```python
import asyncio
from crawl4ai import AsyncWebCrawler

async def main():
    async with AsyncWebCrawler() as crawler:
        result = await crawler.arun(url="https://www.example.com")
        print(result.markdown[:300])  # 打印提取的前 300 个字符

if __name__ == "__main__":
    asyncio.run(main())
```
运行脚本：
```bash
python test_crawl.py
```
如果一切正常，脚本会输出`https://www.example.com`网页的前300字符。

---
# 声明与注意事项
截至本文发布日期，上述安装方案在 Ubuntu 24.04.1 LTS 环境中实测验证有效。若后续因以下可能的原因导致操作失效果：

1. 系统级依赖缺失
2. Playwright浏览器安装失败

建议通过以下途径自行解决：  
- 查看[Playwright 官方文档](https://www.wenxiaobai.com/chat/200006#)或[crawl4ai GitHub仓库](https://github.com/unclecode/crawl4ai/)获取最新指南