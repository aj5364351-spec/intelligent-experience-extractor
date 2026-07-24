# Intelligent Experience Extractor — Never Debug the Same Problem Twice

> **Two hours debugging today. Two hours debugging the same thing three months from now. Not anymore.**
>
> An agent skill that captures every verified fix, outage, and optimization into a structured, searchable, reusable engineering experience — auto-redacted, deduplicated, and stored as plain Markdown in your project's repository.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Platform: Any](https://img.shields.io/badge/Platform-Claude%20Code%20%7C%20Codex%20%7C%20Cursor%20%7C%20Any-blue)]()

---

## The Problem

Most engineering lessons are lost the moment a terminal window closes. The fix you spent two hours debugging today will take another two hours three months from now — because neither you nor your AI assistant remembered it. Your knowledge evaporates with each session.

## The Solution

**Intelligent Experience Extractor** turns every verified engineering task into a permanent, structured record following a disciplined chain:

```
Problem → Root Cause → Solution → Verification → Prevention
```

It auto-redacts secrets before the preview even appears, cross-checks for duplicates, and never writes without authorization. All entries live in `.agent-knowledge/experiences.md` — human-readable, git-trackable, and shared with your entire team.

---

## Quick Start

### Install as a Claude Code / Codex skill

```bash
git clone https://github.com/aj5364351-spec/intelligent-experience-extractor \
  ~/.claude/skills/intelligent-experience-extractor
```

Restart your session. The skill loads automatically.

### Or drop it in as a standalone template

Copy `assets/knowledge-base-readme.md` into your project as `.agent-knowledge/README.md` and start recording experiences using the template in `assets/experience-entry.md`. Any AI agent with filesystem access can consume and maintain it.

---

## The Experience Chain

Every recorded experience follows five structured fields:

| Step | Question Answered |
|---|---|
| **Problem** | What observable error, behavior, or impact did the user see? |
| **Root Cause** | What direct causal chain does the evidence support? (Unknown parts are declared unknown.) |
| **Solution** | What minimal steps, config, or commands reproduce the fix? |
| **Verification** | What actually-run tests, builds, or checks confirmed the fix? |
| **Prevention** | What version pins, static checks, CI guards, or monitoring can reduce recurrence? |

---

## Hard Rules

- **No secrets in previews.** Redaction happens *before* the preview is displayed. Consistent placeholders (`<REDACTED_TOKEN>`, `<PRIVATE_HOST>`) are used.
- **No fabrication.** Commands, tests, metrics, file paths, and references are only recorded if they actually existed and were executed.
- **No unsolicited writes.** The default is *preview only*. Writing requires explicit user authorization or a persisted `auto-save=on` magic comment.
- **No duplicates.** Existing entries are searched before writing. New evidence updates old entries instead of creating near-duplicates.
- **Confidence is explicit.** Every entry carries a label: `已验证` (verified), `部分验证` (partially verified), or `推测` (speculative — user-requested only).

---

## Structure

```
intelligent-experience-extractor/
├── SKILL.md                          # Skill definition (Chinese, works with any language)
├── README.md                         # This file
├── LICENSE                           # MIT
├── .gitignore
├── agents/
│   └── openai.yaml                   # Cross-platform agent metadata
└── assets/
    ├── experience-entry.md           # Experience entry template
    └── knowledge-base-readme.md      # Knowledge base index template
```

---

## Platform-Agnostic by Design

Uses only directory listing, text search, file read, and file write — capabilities every competent agent already has. No hooks, no custom tools, no network calls, no database. The knowledge base is just Markdown on disk, fully git-trackable and human-readable.

---

## Language

The skill definition is written in Chinese. The templates ship in Chinese by default. The knowledge base content you write can be in any language — the structure is fully language-agnostic.

---

## Companion

This skill is an extension of **[Project Memory Curator](https://github.com/aj5364351-spec/project-memory-curator)** — the broader project memory system that manages project context, user preferences, runbooks, and architecture decisions across the same `.agent-knowledge/` directory.

| | Project Memory Curator | Intelligent Experience Extractor |
|---|---|---|
| **Scope** | Broad: context, preferences, decisions, runbooks, experiences | Narrow: troubleshooting & operations experiences |
| **Trigger** | Any engineering task | Debugging, build/deploy failures, CI/CD, config, performance, stability |
| **Entry Format** | Flexible fields per category | Rigid 5-field chain: `problem → cause → solution → verify → prevent` |
| **Redaction** | Manual review, user-facing | Automatic before preview |
| **Knowledge Base** | Same `.agent-knowledge/` | Same `.agent-knowledge/` — they coexist |

Install both for the complete workflow: Project Memory Curator as the hub, Intelligent Experience Extractor as the lab notebook.

---

## License

MIT © 2026 zorix
