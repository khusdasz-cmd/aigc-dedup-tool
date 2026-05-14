# AIGC 降重工具链

中文论文 AIGC 检测降重方案。通过系统性文本改写降低 PaperYY、PaperPass 等检测器的 AIGC 疑似率。

## 概述

本项目包含两大部分：

### 1. Claude Code Skill（核心）

位于 `.claude/skills/aigc-dedup/`，作为 Claude Code IDE 插件的可调用技能运行。支持：

- **论文类型自动识别** — 根据信号词自动判定理工科/社科/文科，加载对应领域模板
- **三级降重深度** — L1 词汇替换 → L2 句式拆解 → L3 结构性重写
- **双检测器覆盖** — 针对 PaperYY 和 PaperPass 的检测特征分别优化
- **自动化迭代管线** — 配套 Python 脚本实现改写→自检→加码→再改写闭环

### 2. 配套自检工具（`scripts/`）

- **`l4_check.py`** — 16 项 AIGC 自检引擎，对 docx 文件运行后输出按类别汇总的问题报告（文言单字、AI高频词、套话句式、密集引用等）
- **`l5_iterative.py`** — 自动迭代降重管线，支持 T1/T2/T3/Adaptive 四级模式 + 自适应收敛

## 快速开始

```bash
# 检查一篇文档的 AIGC 问题
python3 scripts/l4_check.py input.docx

# 自动迭代降重
python3 scripts/l5_iterative.py input.docx output.docx
```

## 技能使用

在 Claude Code 中激活该 skill：

```
帮我降重这段话 /aigc-dedup
AI疑似率太高了，帮我处理一下
```

Skill 会自动检测论文学科类型并加载对应规则。

## 文档结构

```
.claude/skills/aigc-dedup/
├── skill.md               # 主技能文件 — 操作指令 + 检测规则 + 自查清单
├── domain-stem.md         # 理工科专用规则（化学/材料/工程）
├── domain-humanities.md   # 社科/文科专用规则（经济/管理/法学）
├── history.md             # 完整迭代历史（仅参考，运行时加载）
└── scripts/
    ├── l4_check.py        # AIGC 自检引擎
    └── l5_iterative.py    # 自动迭代降重管线

CLAUDE.md                  # 通用降重规则（与 skill 配合使用）
AIGC降重项目介绍.md         # 项目介绍（简历用）
```

## 迭代效果

| 阶段 | 策略 | 检测结果 |
|------|------|---------|
| V1 | 词汇替换 | 20.4% (PaperYY) |
| V2 | 句式拆散 | 15.61% (PaperPass) |
| V3-V4 | L3深度 + 增量 | ~13.5% (PaperYY) |
| V5-V6 | 全篇正则 + 自动化 | 44.36% (PaperPass) |
| V7-V8 | 靶向修复→系统性覆盖 | 43.67%→收敛 |
| V9-V12 | 自动迭代 + 手动混合 | 28.7% (PaperYY) |
