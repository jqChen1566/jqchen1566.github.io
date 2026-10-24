---
title: "[计算化学] fBlockKit — f 区强关联体系的计算工具箱"
description: >-
  fBlockKit 面向镧系、锕系与强关联体系，提供 ORCA/OpenMolcas 输入生成与输出表征分析，结论附带可追溯来源。
  fBlockKit is a toolkit for f-block and strongly correlated systems: input generation for ORCA/OpenMolcas and provenance-carrying characterisation analysis.
author: 陈建棋
date: 2026-10-24 00:10:00 +0800
categories: [Projects, Computational Chemistry]
tags: [f-block, lanthanide, actinide, orca, openmolcas, python, toolkit]
---

## 项目简介

**fBlockKit** 是一个面向 f 区强关联体系的计算工具箱，处理计算流程的两端：一端把体系信息转换为可运行的输入文件，另一端把程序输出转换为带来源标注的分析报告。计算本身仍由用户在本地或集群上提交，工具箱不接管作业调度。

项目当前版本为 v0.1.0（2026-09-30），采用 Apache-2.0 许可，要求 Python 3.11 及以上，运行时依赖 PyYAML、Jinja2 与 NumPy。

---

## 设计目标

f 区计算流程的碎片化体现在三个环节：输入文件的参数组合多，输出文件的解读依赖经验，结论的来源难以追溯。fBlockKit 针对这三点做了取舍：

- 输入生成以问答式菜单完成，每个参数给出默认值，回车即可接受；
- 输出分析以规则引擎完成，不引入机器学习模型；
- 每条结论附带程序手册引文、文献 DOI 与 BibTeX，或实测记录。

---

## 功能

### 输入生成

- 从体系画像生成 ORCA 输入：方法链、基组与 ECP、活性空间、收敛设置，并附运行指引（菜单 3、4）；
- 专用生成器：DeltaSCF/MOM 激发态 SCF（27）、RAS/ORMAS 模型空间（28）、多起点与虚频重启（29、30）、带判定条件的多参考配方（6）；
- OpenMolcas 磁链模板：SA-CASSCF / RASSI / SINGLE_ANISO；
- 外部程序输入：pysisyphus 势能面探索（32）、MOKIT/automr（44）。

### 表征分析

- 检查报告与 SCF 救援：轨道成分、活性空间分析、多参考诊断、振荡与轨迹检查、错误解警告（1、9）；
- 基于 FCIDUMP 的精确活性空间分析：四态熵、环境自旋熵、原子项检查（12）；
- 轨道选择：AVAS（14）、轨道画像（15）、跨结构映射（17）、WASP 初猜迁移（18）、偶极矩选择（19、20）、APC 排序（21）、ASS1ST（22、23）、QICAS（24）、AEGISS（25）、TNASS（26）；
- 晶体场拟合（10）与点电荷估计（11），跨级别解一致性检查（7），CASSCF 态数据与跃迁（31）；
- 磁性与光谱：Judd-Ofelt 强度（34）、pNMR 位移（35）、弛豫与 QTM（36）、超精细与 EFG（40）、磁热效应（41）、隧穿弛豫预测（46）、XAS/RIXS（37）、AILFT（38）、多核磁性（39）；
- 外部程序结果读取：xTB 批量计算（42）、CREST 构象系综（43）、MOKIT/automr（45）、pysisyphus（33）。

---

## 设计原则

- **确定性规则引擎**：决策层不含机器学习，不联网，不上传文件；
- **来源可追溯**：报告中的结论对应手册章节与 URL、文献 DOI 与 BibTeX，或实测记录；
- **只读输入**：所有产物写入新文件（`*.fbk.md`、`*.fbk.json`、`*.fbk.inp`）；
- **可重放**：交互会话可录制为脚本，重放得到字节级一致的报告。

---

## 安装与使用

提供三种安装形式：

- Windows 绿色包：下载 `fblockkit-<version>-windows-x64.zip`，解压后运行 `fblockkit.exe`，无需安装 Python；
- pip：`pip install fblockkit`；
- 源码：在仓库内执行 `pip install .`。

最常见的两种用法是检查已有输出与生成新输入：

```text
# 检查 ORCA 或 Gaussian 输出
fblockkit
# 选择菜单 1，输入输出文件路径

# 重放一段会话
fblockkit run session.txt
```

报告为 Markdown 格式，章节编号与手册菜单一一对应，便于按编号查找说明。

---

## 适用边界

v0.1 处于早期开发阶段，接口与报告格式可能随版本变化。工具箱不执行计算，生成输入后的运行与收敛判断仍由用户负责。规则引擎的结论受内置规则覆盖范围限制，超出范围的体系需要结合原始输出复核。

fBlockKit 由 Jianqi Chen、Wen Zeng、Guanghui Song 开发，暨南大学化学与材料学院。项目受暨南大学省级大学生创新创业训练计划（S202610559049）支持。

---

## 链接

- GitHub：[jqChen1566/fblockkit](https://github.com/jqChen1566/fblockkit)
- 许可：Apache-2.0
