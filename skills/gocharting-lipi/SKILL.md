---
name: gocharting-lipi
description: "Use this skill whenever the user wants a script for GoCharting charts, in GoCharting's Lipi language: converting an indicator or strategy script written in any other language into Lipi, writing a new Lipi indicator or strategy from a plain description, fixing a Lipi script after the GoCharting editor reported an error, or writing the public description of a Lipi script for publishing. Use it even when the user does not say \"Lipi\", for example \"make this indicator work on GoCharting\", \"port my strategy code to GoCharting\" or \"write a 150-character description for my GoCharting script\". It works from its own bundled Lipi reference and makes no network calls."
license: Apache-2.0
metadata:
  version: "0.5.1"
  docs-pack: "cad1b17ca07d"
  prompts: "convert p21, create p101, describe p201"
---

# GoCharting Lipi

Lipi is GoCharting's language for chart indicators and strategies. This skill does what GoCharting's hosted AI script tools do, with the
same instructions and the same reference, inside your own agent.

**This skill cannot compile.** GoCharting's online script editor does. Every script you give the user ends with this step: paste it into the
GoCharting script editor; if the editor reports an error, paste the error back here, and you fix the script (`references/fix-errors.md`).
Never say a script compiles or works; say it is ready to paste and check.

## Pick the workflow, then read its file in full

| The user wants | Read |
|---|---|
| Code in another language turned into Lipi | `references/workflow-convert.md` |
| A new Lipi script from a description of what it should do | `references/workflow-create.md` |
| The public description of an existing Lipi script (for publishing) | `references/workflow-describe.md` |
| An error from the GoCharting editor fixed | `references/fix-errors.md` |

Every script answer also follows `references/self-check.md` (before you answer) and `references/output.md` (how you answer).

## The Lipi reference (bundled; read it, never guess)

- `references/lang/index.md`: every function, variable, type, constant and keyword, with its signature and one line on what it does,
  grouped by namespace. Look up every name you use here first; a name that is not in it does not exist in Lipi.
- `references/lang/core.md`: the language manual (syntax, types, scopes, execution model). Read the parts your script needs.
- `references/lang/ns/<namespace>.md`: full detail for one namespace (`ta`, `talib`, `array`, `label`, `line`, `box`, `table`,
  `strategy`, `input`, `str`, `math` and the rest; `global.md` holds names without a namespace). Read the file for each namespace you use.

The reference is Lipi 2 reference 2.7, generated 2026-10-25, compiler build df7b3b14. It is the only source of truth for names and signatures here.
