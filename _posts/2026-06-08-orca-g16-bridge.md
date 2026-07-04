---
title: "[计算化学] orca_g16_bridge — ORCA SCF + Gaussian 16 几何优化桥接器"
description: >-
  让 Gaussian 16 驱动几何优化，但每一步用 ORCA 计算 SCF 能量与梯度。结合 Gaussian 的稳健优化器与 ORCA 的快速 SCF。
  Let Gaussian 16 drive geometry optimization while ORCA computes SCF energy and gradient at each step.
author: 陈建棋
date: 2026-06-08 20:02:19 +0800
categories: [Projects, Computational Chemistry]
tags: [orca, gaussian, dft, geometry-optimization, python, computational-chemistry]
---

## 项目简介

**orca_g16_bridge** 是一个 Python 桥接脚本，实现了 **Gaussian 16 几何优化器 + ORCA SCF 计算** 的混合工作流：

- **Gaussian 的几何优化器更稳健**（trust-radius 算法、冗余内坐标）
- **ORCA 的 SCF 更快**（尤其对 DFT 计算）

该脚本作为 Gaussian 的 `External` 接口，在每一步几何优化中调用 ORCA 计算能量和梯度，再返回给 Gaussian 判断收敛。

---

## 工作原理

```
┌─────────────────────────────────────────┐
│              Gaussian 16                 │
│  ┌───────────────────────────────────┐  │
│  │  Geometry Optimizer (Opt)         │  │
│  │  - 检查收敛性                      │  │
│  │  - 生成新几何结构                  │  │
│  │  - Trust-radius / 冗余内坐标       │  │
│  └──────────────┬────────────────────┘  │
│           geometry (通信文件)            │
│                 ↓                       │
│  ┌──────────────────────────────────┐   │
│  │  orca_g16_bridge (本脚本)         │   │
│  │  - 解析 Gaussian 传入的结构       │   │
│  │  - 调用 ORCA 计算 SCF 能量/梯度   │   │
│  │  - 返回结果给 Gaussian            │   │
│  └──────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

---

## 快速开始

### 1. 编写 Gaussian 输入文件

```gjf
%nprocshared=8
%mem=16GB
%chk=molecule.chk
#P B3LYP/Def2SVP Opt External="/path/to/orca_g16_bridge/orca_scf.py"

Water molecule - ORCA SCF + Gaussian Optimizer

0 1
O      0.000000    0.000000    0.117349
H      0.000000    0.756950   -0.469396
H      0.000000   -0.756950   -0.469396
```

### 2. 运行

```bash
g16 molecule.gjf
```

> 脚本会自动检测 `%nprocshared` 和 `%mem` 并传递给 ORCA，还会自动将 Gaussian 的基组名称（如 `Def2SVP`）映射为 ORCA 格式（`def2-svp`）。

---

## 适用场景

- 需要使用 Gaussian 稳健优化器但偏好 ORCA 速度的 DFT 计算
- 过渡金属配合物的几何优化（Gaussian 的 trust-radius 算法对此类体系更稳定）
- 需要 ORCA 特有泛函/方法但希望用 Gaussian 做结构优化的场景

---

🔗 **GitHub**: [jqChen1566/orca_g16_bridge](https://github.com/jqChen1566/orca_g16_bridge)
