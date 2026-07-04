---
title: "[科研工具] Paper Tracker — 顶级化学期刊每日论文追踪系统"
description: >-
  每日自动追踪顶级化学期刊最新论文，通过邮箱和 CrossRef 获取元数据，支持中英双语翻译。
  Daily tracking of latest papers from top chemistry journals with email-driven metadata fetching and bilingual Chinese/English translation.
author: 陈建棋
date: 2026-06-29 13:47:34 +0800
categories: [Projects, Research]
tags: [python, paper-tracking, chemistry, automation, translation, llm, crossref]
---

## 项目简介

**Paper Tracker** 是一个每日自动追踪顶级化学期刊最新论文的工具。通过读取期刊 Alert 邮件、提取 DOI、调用 CrossRef API 获取元数据，并使用 LLM 进行**中英双语翻译**，最终以 Web UI 和 Markdown 文件两种形式呈现。

---

## 追踪期刊列表

| 缩写 | 全称 | 出版商 |
|------|------|--------|
| JACS | Journal of the American Chemical Society | ACS |
| JCTC | Journal of Chemical Theory and Computation | ACS |
| Nature | Nature | Nature Publishing |
| Science | Science | AAAS |
| JCIM | Journal of Chemical Information and Modeling | ACS |
| Angew | Angewandte Chemie International Edition | Wiley |
| Nat. Chem. | Nature Chemistry | Nature Publishing |
| Nat. Catal. | Nature Catalysis | Nature Publishing |
| JACS Au | JACS Au | ACS |
| JOC | Journal of Organic Chemistry | ACS |
| JCP | Journal of Chemical Physics | AIP |
| JPCA | Journal of Physical Chemistry A | ACS |
| ACS Catal. | ACS Catalysis | ACS |
| Org. Lett. | Organic Letters | ACS |

> 覆盖 **14 本** 化学及相关领域顶级期刊，涵盖 ACS、Nature、Wiley、AIP 等主要出版商。

---

## 功能特性

- **邮件驱动** — 通过 POP3/IMAP 读取期刊 Alert 邮件
- **DOI 提取** — 从邮件 HTML 中提取 DOI，通过 CrossRef API 补全元数据
- **中英双语** — 使用 LLM（OpenAI 兼容 API）自动翻译标题与摘要
- **Web UI** — 支持按日期范围和期刊浏览、搜索、筛选论文
- **Markdown 导出** — 论文按日期组织为 `.md` 文件
- **定时任务** — 周期性检查邮件、翻译、补全摘要
- **YAML 配置** — 所有设置集中在单一配置文件

---

## 快速开始

```bash
git clone https://github.com/jqChen1566/paper-tracker.git
cd paper-tracker
pip install -r requirements.txt
cp config.example.yaml config.yaml
# 编辑 config.yaml 填入邮箱和 LLM API 配置
python app.py
# 浏览器打开 http://localhost:5000
```

---

🔗 **GitHub**: [jqChen1566/paper-tracker](https://github.com/jqChen1566/paper-tracker)
