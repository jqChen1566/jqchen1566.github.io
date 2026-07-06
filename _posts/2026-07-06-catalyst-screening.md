---
title: "[科研工具] Catalyst Screening — AutoML驱动的催化剂智能筛选系统"
description: >-
  基于 RDKit 分子描述符 + AutoGluon AutoML 的催化剂产率预测工具，面向本科化学实验课程。
  An AutoML-powered molecular descriptor calculation and catalyst yield prediction tool for undergraduate chemistry lab courses.
author: 陈建棋
date: 2026-07-06 20:47:25 +0800
categories: [Projects, Computational Chemistry]
tags: [python, automl, rdkit, catalyst, machine-learning, cheminformatics, autogluon]
---

## 项目简介

**Catalyst Intelligent Screening System** 是一个面向本科化学实验课程的智能催化剂筛选工具。学生在 Excel 中填写候选催化剂的 SMILES 结构式，双击运行程序即可自动完成分子描述符计算、AutoML 建模和产率预测——**无需任何编程基础**。

该项目服务于"安息香缩合催化剂迭代优化"实验，将传统的手动试错替换为数据驱动的智能筛选。

---

## 核心功能

| 模块 | 说明 |
|------|------|
| 🔬 分子描述符计算 | RDKit 自动计算 ~25 个分子描述符（3D 构象、Gasteiger 电荷、%Vbur 等） |
| 🤖 AutoML 建模 | AutoGluon 自动尝试 RF、XGBoost、LightGBM、CatBoost、KNN、神经网络 |
| 📊 结果可视化 | 催化剂产率排序 + 描述符重要性图 + 模型性能报告 |

---

## 工作流程

```
SMILES 输入 → RDKit 描述符计算 → AutoGluon 训练/预测 → 可视化输出
```

1. **描述符计算** — 将 SMILES 结构式转为 ~25 个分子描述符，包含 ETKDGv3 + MMFF 力场优化的 3D 构象
2. **模型训练** — AutoGluon TabularPredictor 自动尝试多种模型，5 折交叉验证，以 RMSE 为优化目标
3. **预测输出** — 候选催化剂按预测产率排序，含不确定性估计，特征重要性图揭示关键分子性质

---

## 输出文件

| 文件 | 内容 |
|------|------|
| `prediction_results.xlsx` | 催化剂产率预测排名及不确定性 |
| `feature_importance.png` | 分子描述符重要性柱状图 |
| `model_performance.txt` | 模型 R²、RMSE、MAE 及排行榜 |
| `descriptors_all.xlsx` | 全部分子的计算描述符 |

---

## 技术栈

| 组件 | 选型 |
|------|------|
| 分子描述符 | RDKit |
| AutoML 框架 | AutoGluon |
| 模型 | RF / XGBoost / LightGBM / CatBoost / KNN / NN |
| 打包分发 | PyInstaller (单文件 .exe) |
| 语言 | Python 3.10+ |

---

🔗 **GitHub**: [jqChen1566/catalyst_screening](https://github.com/jqChen1566/catalyst_screening)
