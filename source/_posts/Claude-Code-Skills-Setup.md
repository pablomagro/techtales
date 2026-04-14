---
title: Claude Code - Skills Setup
date: 2026-04-15 00:00:00
tags:
  - Claude
  - AI
  - CLI
categories:
  - AI
---

[Claude Code](https://claude.ai/code) is Anthropic's official CLI for Claude. It can be extended with **skills** — reusable slash commands that give Claude structured workflows for common tasks like debugging, testing, code review, and more.

## Installing Skills

Skills are installed via `npx skills`. The `-g` flag installs them globally (available in all projects) and `-y` auto-confirms.

### Sequential Thinking

Systematic step-by-step reasoning with the ability to revise and branch thoughts.

```bash
npx skills add mrgoonie/claudekit-skills@sequential-thinking -g -y
```

Invoke with: `/sequential-thinking`

### Superpowers Bundle (14 skills)

A curated bundle covering the most common development workflows.

```bash
npx skills add obra/superpowers -g -y
```

### Context7 — Live Library Documentation

Fetches up-to-date documentation for libraries and frameworks in real time.

```bash
# Install the skill
npx skills add upstash/context7@context7-mcp -g -y
npx skills add intellectronica/agent-skills@context7 -g -y

# Activate the MCP server
claude mcp add context7 -- npx -y @upstash/context7-mcp@latest
```

Invoke with: `/context7`

## Official Claude Plugin

### Code Simplifier

Reviews changed code for reuse, quality, and efficiency, then fixes issues found.

```bash
claude plugin install code-simplifier
```

Invoke with: `/simplify`

## Quick Reference — All Skills

| Skill | Command |
|---|---|
| Sequential Thinking | `/sequential-thinking` |
| Brainstorming | `/brainstorming` |
| Writing Plans | `/writing-plans` |
| Executing Plans | `/executing-plans` |
| Test-Driven Development | `/test-driven-development` |
| Systematic Debugging | `/systematic-debugging` |
| Subagent Development | `/subagent-driven-development` |
| Parallel Agents | `/dispatching-parallel-agents` |
| Git Worktrees | `/using-git-worktrees` |
| Verification | `/verification-before-completion` |
| Code Review (request) | `/requesting-code-review` |
| Code Review (receive) | `/receiving-code-review` |
| Finish Branch | `/finishing-a-development-branch` |
| Context7 Docs | `/context7` |
| Code Simplifier | `/simplify` |

## Extra Tools

### markitdown — Document Reader

Converts files (PDF, Word, PowerPoint, Excel, HTML, CSV, JSON, Images, Audio, YouTube URLs, EPubs, ZIP) to Markdown so Claude can read them.

```bash
pipx install 'markitdown[all]'

# For scanned PDFs (OCR support)
sudo apt install tesseract-ocr
```

Usage inside a Claude Code session:

```bash
markitdown path/to/file.pdf
```
