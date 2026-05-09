---
title: Claude Code - Useful Commands and Keywords
date: 2026-05-10 00:00:00
tags:
  - Claude
  - AI
  - CLI
  - Productivity
categories:
  - AI
---

[Claude Code](https://claude.ai/code) ships with several built-in commands and keywords that improve how you interact with it day-to-day. Here are the ones worth knowing.

---

## `ultrathink` — Deeper Reasoning on Demand

Typing `ultrathink` anywhere in your message tells Claude to reason more thoroughly before responding. It's useful when a task is genuinely complex — architecture decisions, tricky bugs, multi-file refactors — and a shallow first pass would waste time.

```
ultrathink Can you provide suggestions to improve this project?
```

There is a family of these keywords, each triggering a progressively deeper thinking budget:

| Keyword | Reasoning depth |
|---|---|
| `think` | Light extended thinking |
| `think hard` | Moderate |
| `think harder` | Deep |
| `ultrathink` | Maximum |

Use them selectively. On straightforward tasks they add latency with no benefit.

---

## `/effort` — Control How Hard Claude Works

`/effort` sets the effort level Claude applies to responses. Useful when you want faster, lighter answers for exploratory work, or maximum thoroughness for critical changes.

```
/effort low      # faster, lighter responses
/effort auto     # default — Claude decides based on task complexity
```

Running `/effort` with no argument shows the current setting. Toggle it back to `auto` when you want Claude to self-pace again.

---

## `/insights` — Analyze Your Usage Patterns

`/insights` analyzes your recent sessions and generates a usage report — both a console summary and a full HTML report saved locally.

```
/insights
```

Output example:

```
32 sessions · 592 messages · 337h · 88 commits
Report URL: file:///home/pablo/.claude/usage-data/report.html
```

The report covers:

- **Project areas** — which projects got the most attention and what was done
- **Interaction style** — how you batch tasks, redirect Claude, and delegate
- **Friction analysis** — recurring failure modes with examples from your own sessions (wrong scope, regressions, auth blockers)
- **Suggestions** — CLAUDE.md additions, features to try, copyable prompts
- **On the horizon** — ambitious autonomous workflows matched to your patterns

The friction analysis is the most actionable part. A wrong-scope mistake in a single session feels like a one-off; seeing it happen 16 times across a month makes it worth fixing in CLAUDE.md.

---

## `/clear` — Reset the Conversation Context

`/clear` wipes the current conversation context and starts fresh. Use it when:

- The context has grown too large and responses are slowing down
- You are switching to an unrelated task in the same session
- Claude has gone off-track and a clean slate is faster than correcting it

```
/clear
```

A related command is `/compact`, which summarizes the conversation history instead of discarding it — useful when you want to continue a long session without losing the thread entirely.

---

## Combining Them

These commands complement each other in practice. A typical flow might look like:

1. Start a complex task with `ultrathink` to get a thorough plan upfront
2. Switch to `/effort auto` for the implementation work
3. Use `/clear` between unrelated tasks to keep context clean
4. Run `/insights` periodically to spot patterns and improve your workflow

Small adjustments — adding the right keyword, clearing context at the right moment — add up over dozens of sessions.
