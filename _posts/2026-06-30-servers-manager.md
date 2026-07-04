---
title: "[运维工具] ServersManager — 轻量级无Agent局域网服务器监控面板"
description: >-
  基于 Python Flask 的轻量级服务器监控面板，通过 SSH 无 Agent 采集 CPU、内存、磁盘、温度等指标，支持 Gaussian/ORCA 计算任务追踪。
  A lightweight, agentless LAN server monitoring dashboard with SSH-based metrics collection and computational chemistry job tracking.
author: 陈建棋
date: 2026-06-30 18:59:30 +0800
categories: [Projects, DevOps]
tags: [python, flask, ssh, server-monitoring, dashboard, linux]
---

## 项目简介

**ServersManager** 是一个轻量级、无 Agent 的局域网服务器监控面板。通过 SSH 远程采集 Linux 服务器的 CPU 使用率、内存、磁盘、温度及运行任务，**无需在目标机器上安装任何 Agent**。

作为计算化学方向的学生，我还特别加入了 Gaussian/ORCA 任务的自动发现与完成通知功能，方便监控计算集群上的作业状态。

---

## 功能特性

- **无 Agent 架构** — 仅需 SSH 访问权限，无需在监控目标上安装软件
- **实时监控** — CPU、内存、磁盘使用率、CPU 温度、硬件规格
- **任务追踪** — 自动发现 Gaussian/ORCA 计算化学作业及其他高负载进程
- **多标签面板** — Servers / Tasks / Disks / Specs / Sync / Cluster 六个视图
- **用户过滤** — 按 Owner 筛选服务器卡片，适合大规模集群
- **任务完成通知** — Gaussian/ORCA 作业完成时弹出 Toast 提示并记录日志
- **灵活监控方式** — 支持 SSH（全指标）、ping（仅在线状态）、TCP 端口检测
- **系统服务部署** — 附带 systemd unit 文件

---

## 技术栈

| 组件 | 选型 |
|------|------|
| 后端框架 | Python Flask |
| SSH 连接 | Paramiko |
| 前端 | Bootstrap + Chart.js |
| 部署 | systemd / Docker |

---

## 快速开始

```bash
git clone https://github.com/jqChen1566/ServersManager.git
cd ServersManager
pip install -r requirements.txt
cp config.example.json config.json
# 编辑 config.json 填入服务器列表和 SSH 凭据
python app.py
# 浏览器打开 http://<本机IP>:5000
```

---

🔗 **GitHub**: [jqChen1566/ServersManager](https://github.com/jqChen1566/ServersManager)
