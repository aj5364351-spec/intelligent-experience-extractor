# Intelligent Experience Extractor

> Capture verified engineering experiences from troubleshooting, builds, and deployments — sanitized, deduplicated, and ready for reuse.

**Intelligent Experience Extractor** is an agent skill that teaches AI coding assistants how to extract structured, reusable engineering knowledge from completed work. It follows a disciplined `problem → root cause → solution → verification → prevention` chain, automatically redacts sensitive data, checks for duplicates, and never writes without explicit authorization.

## Why

Most engineering lessons are lost the moment a terminal window closes. The fix you spent two hours debugging today will take another two hours three months from now — because neither you nor your AI assistant remembered it. This skill turns every verified fix into a permanent, searchable, and reusable record that lives in your project's repository as plain Markdown.

## What It Does

- **Before troubleshooting** — searches the project knowledge base for relevant past experiences (matched on error signatures, components, environment, and root cause)
- **After verification** — evaluates whether the completed work produced a durable lesson worth recording
- **Structured extraction** — distills the `symptom → root cause → solution → verification → prevention` chain from confirmed results only
- **Auto-redaction** — strips API keys, tokens, passwords, emails, private IPs, hostnames, and customer data before the preview is even shown
- **Deduplication** — scans existing entries for overlap before writing; suggests updates instead of duplicates
- **Preview-then-save** — shows a structured preview; the user chooses **Save**, **Edit**, or **Skip**

## The Experience Chain

Every recorded experience follows five fields:

| Step | Question Answered |
|---|---|
| **Problem** | What observable error, behavior, or impact did the user see? |
| **Root Cause** | What direct causal chain does the evidence support? (Unknown parts are declared unknown.) |
| **Solution** | What minimal steps, config, or commands reproduce the fix? |
| **Verification** | What tests, builds, or checks confirmed the fix? (Only actually-run verification.) |
| **Prevention** | What version pins, static checks, CI guards, or monitoring can reduce recurrence? |

## Hard Rules

- **No secrets in previews.** Redaction happens *before* the user sees the preview. Consistent placeholders (`<REDACTED_TOKEN>`, `<PRIVATE_HOST>`) are used.
- **No fabrication.** Commands, tests, metrics, file paths, issue numbers, and references are only recorded if they actually exist and were executed.
- **No unsolicited writes.** The default state is *preview only*. Writing requires explicit user authorization or a persisted `auto-save=on` magic comment.
- **No duplicates.** Existing entries are searched before writing. New evidence updates old entries rather than creating near-duplicates.
- **Confidence is explicit.** Every entry carries a confidence label: `已验证` (verified), `部分验证` (partially verified), or `推测` (speculative — only when the user explicitly requests it).

## Structure

```
intelligent-experience-extractor/
├── SKILL.md                          # The skill definition (Chinese-first, works with any language)
├── agents/
│   └── openai.yaml                   # Agent interface metadata
├── assets/
│   ├── experience-entry.md           # Experience entry template
│   └── knowledge-base-readme.md      # Knowledge base index template
├── README.md
├── LICENSE
└── .gitignore
```

## Platform-Agnostic by Design

Like its companion [Project Memory Curator](https://github.com), this skill uses only directory listing, text search, file read, and file write — capabilities every competent agent already has. No hooks, no custom tools, no network calls, no database. The knowledge base is just Markdown on disk, fully git-trackable and human-readable.

## Relationship to Project Memory Curator

| | Project Memory Curator | Intelligent Experience Extractor |
|---|---|---|
| **Scope** | Broad: project context, preferences, decisions, runbooks, and experiences | Narrow: specifically engineering troubleshooting & operations experiences |
| **Trigger** | Any engineering task (code, build, deploy, etc.) | Troubleshooting, build/deploy failures, CI/CD, config, performance, stability |
| **Entry Format** | Flexible fields per category | Rigid `problem → root cause → solution → verification → prevention` chain |
| **Redaction** | Manual review, user-facing | Automated before preview, with normalized placeholders |
| **Knowledge Base** | Same `.agent-knowledge/` directory | Same `.agent-knowledge/` directory — they coexist and complement each other |

## How to Use

### As a skill (Claude Code / Codex / compatible platforms)

Drop the entire `intelligent-experience-extractor/` directory into your skills directory (e.g., `.claude/skills/` or `.codex/skills/`). The agent will load it automatically when triggered by troubleshooting, build, deployment, or similar engineering scenarios.

### As a standalone knowledge base template

Copy `assets/knowledge-base-readme.md` into your project as `.agent-knowledge/README.md` and start recording experiences using the template in `assets/experience-entry.md`. Any AI agent capable of reading Markdown can consume and maintain it.

## Language

The skill definition is written in Chinese and defaults to the user's current language for new knowledge bases. All templates and structures are language-agnostic — entries can be written in any language.

## License

MIT
