---
title: "[科研工具] chemoton-network-map — Chemoton 反应网络的 GRRM 风格结构图"
description: >-
  将 SCINE Chemoton/VizChemoton 导出的反应网络渲染为 JSmol 结构图：节点为三维球棍模型，能量为同分异构体相对值。
  Render reaction networks exported by SCINE Chemoton/VizChemoton as GRRM-style JSmol structure maps, with isomer-relative energies in kJ/mol.
author: 陈建棋
date: 2026-10-24 00:30:00 +0800
categories: [Projects, Computational Chemistry, Visualization]
tags: [chemoton, scine, reaction-network, jsmol, visualization, python]
---

## 项目简介

**chemoton-network-map** 把 SCINE Chemoton / VizChemoton 导出的反应网络渲染成 GRRM 风格的结构图：每个节点是一个 JSmol 三维球棍模型，极小点为红色，过渡态为蓝色；节点标注 `EQn`/`TSn` 编号与同分异构体相对能量（kJ/mol）。

工具只负责选点、布局与绘制，不重新计算能量。

---

## 输入

读取 VizChemoton 的标准导出：

- `compounds.json`：xyz 坐标（Bohr）与能量（kJ/mol）；
- `reactions.csv`：反应边。

---

## 选点模式

- **目标中心 BFS**：给定目标产物 SMILES，在物种图上取邻域；
- **碳数过滤**：保留碳原子数不超过 N 的节点，用确定性的 Steiner 树连接低能极小点，再补入过渡态。

过渡态按反应对去重，使用 RMS 指纹，保留至多 `k` 个不同过渡态；关联边与组成边一并保留。

---

## 布局与渲染

- 结构与两行标签占用互斥槽位，绘制前对矩形做两两重叠检查；
- JSmol 16.5.3（HTML5）在无头 Firefox 中渲染每个结构；
- 过渡态的 2.0–2.35 Å 部分键用 `connect` 绘制；
- 输出 600 dpi PNG、矢量 PDF、SVG，以及包含节点、能量、边与来源参数的 JSON。

---

## 使用

```bash
pip install -r requirements.txt
python setup_jsmol.py

# 目标中心选点
python netmap.py --db path/to/export --target "C1CCC1" --name cyclobutane

# 碳数过滤
python netmap.py --db path/to/export --start "agg:C=O+C=O" --max-carbon 2 --radius 4 --cap 90 --name h2co_c2
```

`setup_jsmol.py` 下载官方 Jmol 发布包，校验 MD5 后解压 JSmol 资源；JSmol 按 LGPL 分发，不在仓库中再分发。

---

## 已知限制

- 能量来自搜索数据库的 DFTB3 电子能，未重新评估；不同组成的同分异构体相对值不可直接比较；
- 箭头为直线且绘制在结构层下方，长边可能被结构遮挡而显示为断开；
- 布局是通用图布局，不是反应坐标布局，过渡态不强制落在两个极小点的连线上；
- JSmol 颜色命令必须使用带引号十六进制颜色的 `{element}` 选择器；直接写 `color C "#..."` 会被解析为注释，并把背景涂成该颜色；
- 无头 Firefox 截图无法捕获 JSmol 画布，渲染器通过 `toDataURL` 导出画布像素。

---

## 链接

- GitHub：[jqChen1566/chemoton-network-map](https://github.com/jqChen1566/chemoton-network-map)
- 许可：MIT
