# agent-cli-creator

English | [中文](./README.md)

Tell an AI agent in one sentence what you keep doing on a webpage, and it'll turn that into a CLI tool. The generated CLI can be called by your agent any time, driving your real Chrome login session directly — no API, no token juggling.

This repo *is* the skill that teaches an agent how to build such a CLI. Install it, then say "Build me a CLI for example.com" to your agent. Working examples built with this exact skill live in [better-world-ai/x-cli](https://github.com/better-world-ai/x-cli).

DEMO (a CLI being born):

https://github.com/user-attachments/assets/c1d04187-972a-4b8a-b243-df085281fc77

## Prerequisites

To let the agent actually drive your browser, install [kimi-webbridge](https://www.kimi.com/features/webbridge). It has two parts:

1. **Browser extension** — the agent's entry point for controlling the browser. Once installed, every click, input, and read is forwarded through it, and your existing Chrome login sessions get reused automatically.
   - English: <https://www.kimi.com/features/webbridge>
   - 中文：<https://www.kimi.com/zh-cn/features/webbridge>

2. **Local skill** that teaches the agent how to use the extension above. Install:

   ```bash
   curl -fsSL https://cdn.kimi.com/webbridge/install.sh | bash
   ```

## Install the skill

```bash
npx skills add better-world-ai/agent-cli-creator
```

<details>
<summary>No Node.js? Manual install</summary>

Copy this repo's contents (`SKILL.md` + `references/`) into your agent's skills directory under an `agent-cli-creator/` subdirectory (for Claude Code that's `~/.claude/skills/agent-cli-creator/`). Not sure where it goes? Paste this README section to your agent — it'll figure it out.

</details>

Once installed, just say "Build me a CLI for example.com" in conversation to trigger it.

## How to use

1. Start kimi-webbridge and log into the target site in Chrome.
2. Tell your agent, e.g.:
   > "Build me a CLI for example.com. I want to pull the homepage feed and post comments."
3. The agent asks a few questions first (which language, what the first 1–3 features are), then goes off to analyze the site, scaffold the project, and implement the commands — pausing at key checkpoints to confirm with you.
4. You end up with a tool used like this:
   ```bash
   example-cli login-status
   example-cli home --limit 10
   example-cli post --content "hello"
   ```

## Working examples

[better-world-ai/x-cli](https://github.com/better-world-ai/x-cli) collects a set of CLIs built with this exact skill — AI image generation, China rentals (58同城, 安居客), UK/US/EU rentals, hotel & flight booking, gaokao admissions, and more. Each scenario has a copy-paste-ready prompt script in [x-cli/recipes/](https://github.com/better-world-ai/x-cli/tree/main/recipes).

## License

MIT — see [LICENSE](./LICENSE).
