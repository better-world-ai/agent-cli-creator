# agent-cli-creator

A Claude Code [skill](https://code.claude.com/docs/en/skills) that guides an AI coding agent through building a website-automating CLI tool backed by the [kimi-webbridge](https://www.kimi.team/features/webbridge) browser daemon.

The skill encodes a 5-phase workflow — prerequisites check, requirements interview, **mandatory site archaeology**, iterative implementation, and a companion skill for the resulting CLI. Site archaeology is non-negotiable: the agent finds the real API endpoints inside the user's logged-in browser session before writing any business logic, so the CLI is built on verified contracts instead of guesswork.

## Install

```bash
npx skills add better-world-ai/agent-cli-creator
```

This drops the skill into your Claude Code skills directory (typically `~/.claude/skills/agent-cli-creator/`). After install, ask Claude:

> "帮我做一个针对 example.com 的 CLI"
> "create a CLI for example.com using kimi-webbridge"

Claude will detect the intent and invoke the skill.

## When it triggers

The skill's frontmatter listens for phrases like:

- "create a CLI for X site" / "build a tool to automate X"
- "针对 X 网站做一个 CLI" / "把 X 网站做成命令行工具"
- Any request to drive a specific website programmatically via an AI agent

## What it produces

A CLI that:

- Drives a real Chrome session via the kimi-webbridge daemon (so the user's own login cookies are reused — no separate auth flow)
- Has a uniform JSON output contract: `{"ok": true, "data": ...}` / `{"ok": false, "error": {"code": "...", "message": "..."}}`
- Ships with a *companion skill* that teaches future AI agents how to use the CLI (not just how it was built)

Working examples following this exact pattern live in [better-world-ai/x-cli](https://github.com/better-world-ai/x-cli) — 12 CLIs covering image generation, Chinese property search (58同城, 安居客), US/UK/EU rentals, hotel/flight booking, etc.

## Requirements

- A Claude Code, Codex, or compatible agent (`npx skills` supports 51+ agents)
- The [Kimi Desktop App](https://www.kimi.team/features/webbridge), which bundles the kimi-webbridge daemon

## Repository contents

| Path | Purpose |
|---|---|
| `SKILL.md` | Skill manifest + 5-phase workflow |
| `references/site-exploration.md` | Site archaeology protocol — how to discover API endpoints from the browser |
| `references/go-layout.md` | Canonical Go project layout |
| `references/login-handling.md` | Pattern for `login-status` commands |
| `references/companion-skill-template.md` | Template for the companion skill produced in Phase 5 |

## License

MIT — see [LICENSE](LICENSE).
