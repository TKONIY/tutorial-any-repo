# tutorial-any-repo

> Automatically generate a file-by-file code tutorial website for **any** repository — powered by Claude Code's parallel agent system.

## What It Does

Given any codebase, this skill will:

1. **Explore** the entire repository structure and inventory every source file
2. **Plan** a TODO tracker mapping every file to a tutorial document
3. **Launch parallel agent teams** to write detailed code explanations simultaneously
4. **Self-review** all generated docs for completeness and quality
5. **Build** a searchable static website with MkDocs Material theme
6. **Deploy** to GitHub Pages automatically

The result is a fully navigable tutorial website where every source file has a corresponding explanation document with code snippets, architecture diagrams, and cross-references.

## Example Output

**Live demo**: [https://tkoniy.github.io/verl/](https://tkoniy.github.io/verl/)

This skill was used to generate a 411-page tutorial for the [verl](https://github.com/volcengine/verl) reinforcement learning framework (397 Python files):

- Background knowledge docs (RL, RLHF, PPO, distributed training)
- Three reading paths: Quick Start, Complete Learning, Topic-based
- File-by-file code walkthroughs with key snippets
- Module overview pages with ASCII architecture diagrams
- LaTeX-rendered mathematical formulas
- Full-text search with Chinese/English support

[![verl tutorial screenshot](https://img.shields.io/badge/Live_Demo-verl_Tutorial-blue?style=for-the-badge)](https://tkoniy.github.io/verl/)

## Installation

### Via Claude Code Plugin Manager

```bash
/plugin marketplace add TKONIY/tutorial-any-repo
/plugin install tutorial-any-repo
```

### Manual Installation

Copy the skill to your Claude Code skills directory:

```bash
# Personal scope (available in all projects)
mkdir -p ~/.claude/skills/tutorial-any-repo
curl -o ~/.claude/skills/tutorial-any-repo/SKILL.md \
  https://raw.githubusercontent.com/TKONIY/tutorial-any-repo/main/skills/tutorial-any-repo/SKILL.md

# Or project scope (shared with collaborators)
mkdir -p .claude/skills/tutorial-any-repo
curl -o .claude/skills/tutorial-any-repo/SKILL.md \
  https://raw.githubusercontent.com/TKONIY/tutorial-any-repo/main/skills/tutorial-any-repo/SKILL.md
```

## Usage

```bash
# Generate tutorial for current directory in English
/tutorial-any-repo

# Specify a target directory
/tutorial-any-repo ./my-project

# Specify language (English, Chinese, Japanese, etc.)
/tutorial-any-repo ./my-project Chinese
```

## How It Works

The skill executes in 6 phases:

```
Phase 1: Explore & Plan
  └─ Scan codebase → Create directory structure → Build TODO tracker

Phase 2: Foundation Documents
  └─ Background knowledge + Reading guide (parallel agents)

Phase 3: Parallel Module Documentation
  └─ Launch N agents simultaneously, one per module
  └─ Each agent: Read source → Write tutorial docs
  └─ Large modules split across multiple agents

Phase 4: Self-Review
  └─ Completeness check → Quality spot-check → Fix issues

Phase 5: Build Website
  └─ MkDocs Material + Chinese search + LaTeX + auto-navigation

Phase 6: Deploy
  └─ GitHub Pages + GitHub Actions CI/CD
```

### Key Features

| Feature | Description |
|---------|-------------|
| **Full coverage** | Every source file gets a tutorial document — no exceptions |
| **Parallel agents** | Multiple agents write docs simultaneously for speed |
| **Progress tracking** | TODO.md + Task system keeps you informed |
| **Auto-navigation** | MkDocs awesome-pages plugin generates sidebar from directory structure |
| **Math support** | LaTeX rendering via MathJax for mathematical formulas |
| **Search** | Full-text search with CJK language support (jieba) |
| **Dark mode** | Material theme with light/dark toggle |
| **CI/CD** | GitHub Actions workflow for automatic redeployment |

## Tutorial Document Format

Each generated tutorial doc follows a consistent structure:

```markdown
# `filename.py` — Short description

## File Overview
What this file does and its role in the project.

## Key Code Walkthrough
### 1. Core Class/Function
(code snippet with explanation)

## Core Classes & Functions
| Name | Type | Description |
|------|------|-------------|
| ... | ... | ... |

## Relationship to Other Modules
How this file connects to the rest of the codebase.

## Summary
```

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI
- Python 3.8+ (for MkDocs)
- `gh` CLI (for GitHub Pages deployment)
- Git repository with GitHub remote

## License

MIT
