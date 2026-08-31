# pi-apply-patch

Codex-style `apply_patch` tool extension for the [pi coding agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent). It registers a freeform grammar patch tool for OpenAI GPT-family models and swaps out `write` / `edit` while those models are active.

## Behavior

The extension registers one LLM-callable tool: `apply_patch`. The tool accepts Codex patch envelopes and applies file additions, updates, deletions, and moves after resolving file paths against the current workspace.

| Case | Result |
|------|--------|
| OpenAI GPT model active, directly or through `pi-model-relay-e2ee` | replaces `write` and `edit` with `apply_patch` |
| Non-GPT model active | restores the original `write` and `edit` toolset |
| Raw freeform patch input | accepted and applied |
| JSON `{ "input": "..." }` patch input | accepted and applied |
| Invalid update/delete in a multi-file patch | rejected during preflight before any file is changed |
| Multiple operations targeting one resolved path | rejected during preflight |
| Absolute or parent-escaping path | accepted and resolved by Node path semantics |

## Tool

### `apply_patch`

Use this tool to edit files with the Codex patch format.

```text
*** Begin Patch
*** Add File: hello.txt
+Hello world
*** Update File: src/app.py
@@ def greet():
-print("Hi")
+print("Hello, world!")
*** Delete File: obsolete.txt
*** End Patch
```

With Pi 0.84.3 or newer, the OpenAI Responses API receives this as a custom freeform grammar tool, not as a JSON function tool. Earlier Pi versions do not expose the constrained-sampling extension API required for that wire format.

## Installation

The package targets the [`pi`](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) coding agent. Pi loads extensions from `~/.pi/agent/extensions/`, project `.pi/extensions/`, or via the `--extension` / `-e` CLI flag.

```bash
# 1. Install the maintained fork
pi install git:github.com/alexei-ciobanu/pi-apply-patch

# 2. Or clone the maintained fork manually
git clone https://github.com/alexei-ciobanu/pi-apply-patch ~/.pi/agent/extensions/pi-apply-patch
cd ~/.pi/agent/extensions/pi-apply-patch && npm install

# 3. Development / one-shot test
pi -e /path/to/pi-apply-patch/src/index.ts
```

After installation, restart pi or run `/reload` inside an interactive session.

## Development

```bash
npm install
npm test
npm run typecheck
npm run check
npm pack --dry-run
pi -e ./src/index.ts
```

The test suite uses vitest. TypeScript is strict, Node-only, and uses ESM imports with `.js` suffixes.

## Origin

Ported from `packages/coding-agent/src/core/extensions/builtin/gpt-apply-patch.ts` in `code-yeongyu/senpi-mono`. The patch grammar and tool descriptions mirror Codex.

This repository is Alexei Ciobanu's maintained fork of [`code-yeongyu/pi-apply-patch`](https://github.com/code-yeongyu/pi-apply-patch). Upstream remains the attribution source; this fork carries the deployed compatibility and TUI fixes.

## License

[MIT](LICENSE).

## Related

- [senpi](https://github.com/code-yeongyu/senpi) — the fork/runtime these extensions are extracted from.
- [Ultraworkers Discord](https://discord.gg/PUwSMR9XNk) — community link from the senpi README.
- [Dori](https://sisyphuslabs.ai) — the product powered by senpi under the hood.

## Acknowledgements

- **Mario Zechner** ([@badlogic](https://github.com/badlogic)) — author of [pi-mono](https://github.com/badlogic/pi-mono) and the pi-coding-agent extension API this package targets.
- **OpenAI Codex** — reference `apply_patch` tool grammar and patch language.
