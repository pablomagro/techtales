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

### PM Skills

Open-source library of 1,098 professional agent skills (markdown-based) spanning business domains (PRDs, postmortems) and everyday tasks (lease decoding, salary negotiation). Works with Claude, ChatGPT, Gemini, Cursor and Codex; no lock-in since skills are just text files.

```bash
npx pm-claude-skills add
```

Or install via `/plugin` inside Claude Code and search for **pm-skills**.

### Security Audit

[Cloudflare's security-audit skill](https://github.com/cloudflare/security-audit-skill) turns the agent into a security auditor: reconnaissance, coverage-led hunting, candidate validation, and independently verified findings, written out as `REPORT.md` / `FINDINGS-DETAIL.md`.

```bash
npx skills add https://github.com/cloudflare/security-audit-skill --skill security-audit -g -y
```

Trigger it with a prompt like `security audit this codebase`.

## Official Claude Plugin

### Code Simplifier

Reviews changed code for reuse, quality, and efficiency, then fixes issues found.

```bash
claude plugin install code-simplifier
```

Invoke with: `/simplify`

## MCP Plugins

### Context Mode — Reduce Context Window Usage

[Context Mode](https://github.com/mksglu/context-mode) is an MCP server that sandboxes tool output (98% reduction — a 315 KB session becomes 5.4 KB) and persists session memory across context compactions, so Claude doesn't forget which files it was editing.

```bash
/plugin marketplace add mksglu/context-mode
/plugin install context-mode@context-mode
```

Verify with `/context-mode:ctx-doctor`, check savings with `/context-mode:ctx-stats`.

### Engram — Persistent Memory

[Engram](https://openengram.ai/) is a self-hosted, open-source memory server (Apache 2.0): it extracts facts, preferences, and decisions from conversations, consolidates them nightly, and recalls them across sessions and even across different models (Claude, ChatGPT, Gemini).

```bash
# MCP server for Claude Desktop, Cursor, Windsurf, and any MCP client
git clone https://github.com/openengram/engram-mcp
```

Runs entirely on your machine — no cloud account required; used via `engram.remember(...)` / `engram.recall(...)`.

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
| Security Audit | prompt: "security audit this codebase" |
| Code Simplifier | `/simplify` |
| Context Mode | `/context-mode:ctx-stats` |
| Engram Memory | MCP tools: `remember` / `recall` |

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
