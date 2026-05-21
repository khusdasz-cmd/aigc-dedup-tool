# AIGC 降重工具链

> 系统性降低 AIGC 检测率的工具链，基于 Claude Code Skill + Python 配套脚本。

## 结构

本仓库包含两部分：

### 1. Claude Code Skill (`.claude/skills/aigc-dedup/`)

核心降重规则库，在 Claude Code 中通过 `/aigc-dedup` 激活。

### 2. 配套自查脚本

- **l4_check.py** — 16 项 AIGC 特征自查
- **l5_iterative.py** — 自动迭代降重流水线

## 快速开始（脚本方式）

```bash
pip install -r requirements.txt
python .claude/skills/aigc-dedup/scripts/l4_check.py input.docx
python .claude/skills/aigc-dedup/scripts/l5_iterative.py input.docx output.docx
```

## Claude Code 用户使用说明

如果你已经在使用 Claude Code，激活本工具链只需两步：

### 1. 加载 Skill

在对话中直接输入 `/aigc-dedup` 即可激活降重技能。首次使用时会提示安装，确认即可。

### 2. 开始降重

激活后，把你需要降重的论文段落发给 Claude，它会自动按以下流程处理：

1. 标记 AI 高频用词并给出替换建议
2. 拆解 AI 套话句式
3. 将古典书面语转为口语化表达
4. 输出改写后的完整段落

默认使用 L2（中度降重），对检测率要求高的场景可要求使用 L3（深度降重）。

## 目录结构

```
├── .claude/skills/aigc-dedup/
│   ├── skill.md              # 核心降重规则与工作流
│   ├── domain-stem.md        # 理工科领域规则
│   ├── domain-humanities.md  # 文科领域规则
│   ├── history.md            # 迭代记录
│   └── scripts/
│       ├── l4_check.py       # AIGC 自查引擎
│       └── l5_iterative.py   # 迭代降重流水线
├── aigc-dedup-overview.md
├── CLAUDE.md
├── README.md
├── LICENSE
└── requirements.txt
```
