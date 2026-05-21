# AIGC 降重工具链 — 项目介绍

## 概述

本项目提供一套完整的 AIGC 降重工具链，用于降低学术论文的 AIGC 检测率。基于 Claude Code Skill + Python 配套脚本，通过系统性替换 AI 高频用词、拆解套话句式、古典书面语→口语化转换等手段，将 AIGC 检测率从原始 79.98% 降至 20% 以下。

## 组成部分

### 1. Claude Code Skill

位于 `.claude/skills/aigc-dedup/` 目录下的 Claude Code 技能，包含：

- **skill.md** — 核心降重规则与工作流
- **domain-stem.md** — 理工科领域特定规则（76 组 STEM 句式对）
- **domain-humanities.md** — 文科领域特定规则（20 组经济句式 + 14 类 AI 模板）
- **history.md** — 各版本迭代记录

### 2. 配套脚本

位于 `.claude/skills/aigc-dedup/scripts/`：

- **l4_check.py** — 16 项 AIGC 特征自查引擎
- **l5_iterative.py** — 自动迭代降重流水线

## 快速开始

```bash
# 安装依赖
pip install -r requirements.txt

# 运行自查
python3 .claude/skills/aigc-dedup/scripts/l4_check.py input.docx

# 运行迭代降重
python3 .claude/skills/aigc-dedup/scripts/l5_iterative.py input.docx output.docx
```

## 使用 Skill

在 Claude Code 中使用 `/aigc-dedup` 激活技能。
