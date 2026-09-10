# tot-lite

The free tier of **`/tot`** — a Claude Code skill for deep, adversarially-tested reasoning on high-stakes prompts.

`tot-lite` runs **Stage 1 only**: a Tree of Thought pass — at least 7 distinct branches, each evaluated, then synthesized into one "golden path." Full quality, nothing shortened or simplified for this tier.

It does **not** run Stage 2 ("Robots Fight" — a 3-persona adversarial debate that pressure-tests the golden path across 3 rubric-weighted rounds and revises it before finalizing). That's in the full paid version, **`/tot`** (RKlab).

## Install

Copy [`​.claude/skills/tot-lite/SKILL.md`](.claude/skills/tot-lite/SKILL.md) into your own project's `.claude/skills/tot-lite/SKILL.md`. No dependencies — it's a plain instructions file, works anywhere a Claude session can reason in multiple passes (full parallel-subagent fidelity in Claude Code; sequential/simulated mode elsewhere, e.g. claude.ai).

## When to use it

Reserve this for prompts where being wrong or sloppy is expensive — architecture decisions, hard bugs, irreversible calls, security-sensitive design, research synthesis. Not for everyday prompts.

## Soft-spot flags

`tot-lite`'s output includes honest, inline flags naming specific untested aspects of its own answer (e.g. an unstated assumption, an untested edge case) — never a claim that the answer is *probably wrong*, just what hasn't been checked. Where a real matching case study exists showing the full version catching that kind of gap, the flag links to it.

## Full version

`/tot` (paid, one-time purchase) adds the Robots Fight adversarial-debate stage — see [link to Gumroad listing] for the full version and published case studies.

## License

MIT-style — free to use, copy, and modify. "tot" and "/tot" are trademarks of RKlab; this covers the name/branding only, not this file's content.
