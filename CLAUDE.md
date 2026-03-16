# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**tutorial-any-repo** is a Claude Code skill that generates file-by-file code tutorial websites for any repository. It uses parallel agent teams, MkDocs Material theme, and deploys to GitHub Pages. Live demo: https://tkoniy.github.io/verl/

## Repository Structure

```
skills/tutorial-any-repo/SKILL.md   # Core skill definition (the entire logic)
.claude-plugin/marketplace.json     # Claude Code plugin marketplace metadata
```

The project has no build system, package manager, or test suite of its own — it is a single-skill plugin. The SKILL.md file contains the full 6-phase execution pipeline, agent prompt templates, and MkDocs configuration templates.

## Architecture

The skill executes a 6-phase pipeline when invoked:

1. **Explore & Plan** — Scan source files, create `tutorial/` directory structure, generate TODO.md tracker
2. **Foundation Documents** — Generate background knowledge and reading guide (parallel agents)
3. **Parallel Module Documentation** — Launch N agents simultaneously to write file-by-file tutorials
4. **Self-Review** — Verify completeness, spot-check quality, fix gaps
5. **Build Website** — Install MkDocs + plugins, generate mkdocs.yml, build static site
6. **Deploy to GitHub Pages** — Push to gh-pages branch, set up GitHub Actions CI/CD

Key design principles: full file coverage (every source file gets a doc), maximum parallelism for speed, progress tracking via TODO.md and Task system, consistent document format across all tutorials.

## Runtime Dependencies (installed by the skill at execution time)

```bash
pip install mkdocs mkdocs-material mkdocs-awesome-pages-plugin jieba
```

Deployment uses `mkdocs gh-deploy` and `gh` CLI.

## Requirements

- Claude Code CLI
- Python 3.8+
- `gh` CLI (GitHub CLI)
- Git with a GitHub remote configured
