# GoCharting Lipi

An agent skill for **[Lipi](https://gocharting.com/docs/scripting/)**, the scripting language of [GoCharting](https://gocharting.com) charts. It does the same three jobs
as GoCharting's hosted AI script tools, with the same instructions and the same Lipi reference, inside your own AI agent:

- **Convert** an indicator or strategy script from any other language to Lipi.
- **Create** a Lipi indicator or strategy from a plain description of what it should do.
- **Describe** a Lipi script: the public description GoCharting's script library asks for when you publish.

It also fixes a script when the GoCharting editor reports an error.

## Examples

- "Make this indicator work on GoCharting: <paste your code>"
- "Write a GoCharting strategy: buy when the 9 EMA crosses above the 21 EMA, 2% stop loss"
- "Write the 150-character publish description for my GoCharting script"

## Install

| Agent | How |
|---|---|
| Claude Code | `/plugin install gocharting-lipi --marketplace GoChartingOSS/gocharting-lipi`; or copy `skills/gocharting-lipi` into `.claude/skills/` |
| claude.ai, Claude Desktop | upload a ZIP whose top level is the `gocharting-lipi` folder (Settings, Skills; code execution on) |
| Codex, Cursor, Copilot, Gemini CLI, Antigravity | copy `skills/gocharting-lipi` into `.agents/skills/` or `~/.agents/skills/`; or install this repository as a plugin |
| Grok Build | copy `skills/gocharting-lipi` into `.grok/skills/` or `~/.grok/skills/` (Grok Build also reads Claude Code's skill folders) |

## What it does not do

- **Network: none.** It makes no network call and contains no executable: it is instructions plus GoCharting's Lipi reference.
- **It cannot compile.** Paste each script into the GoCharting script editor; if it reports an error, paste the error back and the skill fixes it.
- **It executes no trades.** It writes scripts. A strategy script you later run in GoCharting may place orders there: review and test it first.
- Scripts and descriptions are written by AI. Review and test before use. Not financial advice.

## Before you convert or share

- Convert only code you have the right to convert. Not code you received only in protected, invite-only, encrypted, obfuscated or compiled form,
  unless you wrote it or its owner allows it. Converting does not change the original's licence: follow it when you share the result.
- The skill keeps a licence or author notice from the top of the original, and marks each script as written by AI. Keep both when you share it.
- A script that compiles has passed a syntax check, nothing more. Test it against the original before you rely on it.
- Do not paste passwords, keys or other secrets: your agent sends what you paste to its model provider.
- Rights holders: legal@gocharting.com.

## Links

- GoCharting: https://gocharting.com
- Lipi documentation: https://gocharting.com/docs/scripting/
- GoCharting for developers: https://gocharting.com/developers

## Privacy

The skill sends nothing anywhere itself, and no GoCharting service is involved. Your agent still sends the conversation (your code included) to its
own model provider, unless you run a local model, and an installer may collect its own usage data; their terms apply. GoCharting's privacy policy:
https://gocharting.com/legal/privacy

## Support

support@gocharting.com

GoCharting Inc. maintains this repository and does not accept contributions (CONTRIBUTING.md). Security reports: SECURITY.md.

## Licence

Apache-2.0, the whole package. See LICENSE and NOTICE (trademarks, no affiliation, no warranty, not financial advice).

Version 0.5.1, published by GoCharting Inc.. Generated from GoCharting's AI script tools; do not edit by hand.
