# AIGC 降重工具链

> 系统性降低 AIGC 检测率的工具链，基于 Claude Code Skill + Python 配套脚本。

## 结构

本仓库包含两部分：

### 1. Claude Code Skill (`.claude/skills/aigc-dedup/`)

核心降重规则库，在 Claude Code 中通过 `/aigc-dedup` 激活。

### 2. 配套自查脚本 (`.claude/skills/aigc-dedup/scripts/`)

- **l4_check.py** — 16 项 AIGC 特征自查
- **l5_iterative.py** — 自动迭代降重流水线

## 快速开始

`$'`bash
pip install -r requirements.txt
python .claude/skills/aigc-dedup/scripts/l4_check.py input.docx
python .claude/skills/aigc-dedup/scripts/l5_iterative.py input.docx output.docx
`$'`

## 目录结构

`$'`
├── .claude/skills/aigc-dedup/
│   ├── skill.md
│   ├── domain-stem.md
│   ├── domain-humanities.md
│   ├── history.md
│   └── scripts/
│       ├── l4_check.py
│       └── l5_iterative.py
├── aigc-dedup-overview.md
├── CLAUDE.md
├── README.md
├── LICENSE
└── requirements.txt
`$'`
