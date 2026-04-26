# Karpathy Coding Workflow for Codex

A Codex-specific skill that makes AI coding feel less like autocomplete and more like a careful senior engineer doing real work in a real repo.

Use it when you want Codex to clarify the target, read the code before editing, build a correctness harness, choose the simplest working design, remove dead code, verify the result, and leave behind a diff that is easy to review.

This is not a generic prompt pack for every assistant. It is written for Codex's skill system, Codex-style repo work, `SKILL.md` discovery, `agents/openai.yaml` metadata, local `.codex/skills` installs, terminal-driven verification, and final reports that name the exact evidence behind the change. Claude, Cursor, or other agents may adapt the ideas, but the packaged skill and install path are built for Codex.

This project is community-made and is not affiliated with, sponsored by, or endorsed by Andrej Karpathy.

It is especially useful for:

- Bug fixes that need reproduction before patching.
- Refactors where abstraction bloat is the main risk.
- Performance work where correctness must survive optimization.
- Unfamiliar codebases where hidden assumptions are expensive.
- Code review and cleanup passes where the final diff needs to be tight.

## What It Teaches Codex To Do

- Convert fuzzy requests into `Goal`, `Context`, `Constraints`, `Done when`, and `Non-goals`.
- Search and inspect the repo before writing code.
- Prefer tests, reproductions, fixtures, smoke checks, or benchmarks over guessing.
- Push back when the requested solution conflicts with repo evidence.
- Implement the smallest correct change before adding abstractions.
- Delete obsolete code and avoid unrelated churn.
- Report exactly what changed, what was verified, and what risk remains.

## Install With npx for Codex

For a public GitHub repo, users do not need this skill to be published as its own npm package. The `skills` CLI is run through `npx`, and it installs the skill directly from GitHub.

Users can install it globally with:

```bash
npx --yes skills add alyhas/karpathy-coding-workflow-for-codex --global
```

Full GitHub URL form also works:

```bash
npx --yes skills add https://github.com/alyhas/karpathy-coding-workflow-for-codex --global
```

The GitHub source uses the repository name, `karpathy-coding-workflow-for-codex`. After install, Codex discovers the skill by the internal `name` in `SKILL.md`: `karpathy-coding-workflow`.

If this skill is ever moved into a larger multi-skill repository, Codex users can target it by name:

```bash
npx --yes skills add alyhas/codex-skills --skill karpathy-coding-workflow --global
```

Restart Codex after installation so the skill list refreshes.

## Use

Invoke it explicitly:

```text
Use $karpathy-coding-workflow to fix this bug. Reproduce it first, implement the smallest correct fix, and keep the diff tight.
```

More examples:

```text
Use $karpathy-coding-workflow to refactor this module. Push back if my requested abstraction is overkill.
```

```text
Use $karpathy-coding-workflow to optimize this path. Keep a correctness harness and do not sacrifice readability.
```

```text
Use $karpathy-coding-workflow to review my uncommitted changes and focus on real regressions.
```

## Make This Repo npx-Ready

This repository is ready to publish as:

```text
git@github.com:alyhas/karpathy-coding-workflow-for-codex.git
```

Keep this structure:

```text
karpathy-coding-workflow-for-codex/
  SKILL.md
  README.md
  agents/
    openai.yaml
  assets/
    review-checklist.md
    task-brief-template.md
  references/
    karpathy-derived-principles.md
```

The important requirement is that `SKILL.md` is at the repository root for a single-skill repo. The `agents/openai.yaml` file is optional metadata, but this repo includes it so Codex can show a better name, short description, and default prompt. The README intentionally documents Codex usage first; do not market this as a universal Claude/Cursor/all-agent skill unless you create separate install instructions and adapt the workflow language for those tools.

Publish it:

```bash
git init
git add .
git commit -m "Publish Karpathy Coding Workflow skill"
git branch -M main
git remote add origin git@github.com:alyhas/karpathy-coding-workflow-for-codex.git
git push -u origin main
```

Then test the install command from a clean terminal:

```bash
npx --yes skills add alyhas/karpathy-coding-workflow-for-codex --global --copy
```

Verify it appears in the global skill list:

```bash
npx --yes skills list --global
```

Use `--copy` when you want the installed files copied into the agent skill directory instead of symlinked.

## Local Development Install

From this folder on Windows PowerShell:

```powershell
$dest = "$env:USERPROFILE\.codex\skills\karpathy-coding-workflow"
New-Item -ItemType Directory -Force $dest | Out-Null
Copy-Item -Path ".\*" -Destination $dest -Recurse -Force
Test-Path "$dest\SKILL.md"
```

Validate the skill:

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py" .
```

## Contents

- `SKILL.md`: trigger metadata and the main operating workflow.
- `agents/openai.yaml`: UI metadata and a default prompt for Codex.
- `assets/task-brief-template.md`: compact task framing for fuzzy work.
- `assets/review-checklist.md`: final review checklist before reporting completion.
- `references/karpathy-derived-principles.md`: source principles for maintaining the skill.

## License

MIT. See [LICENSE](LICENSE).
