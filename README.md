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

## Case studies: Robots Fight in action

Real examples of Stage 2 (the paid tier) catching something a single-pass Stage 1 answer missed — all pulled from actual `/tot` runs, none invented for marketing. Each is tagged by the soft-spot category it belongs to; `tot-lite`'s own inline flags link here when your output shows the same category of gap.

<a id="unstated-assumption"></a>
### Unstated assumption
A sale-structure plan assumed a subscription meaningfully gated access to a file. Robots Fight caught that a canceled subscriber keeps their copy forever — the assumption was wrong, and the pricing model was rebuilt around it before shipping.

<a id="claims-overreach"></a>
### Claims overreach
A legal draft leaned on trademarking a product name to stop copying. Robots Fight caught that trademark only protects the *name*, not the *content* — a renamed clone would have been untouched. The license was rewritten to say exactly what it can and can't stop.

<a id="proportionality-mismatch"></a>
### Proportionality mismatch
A first draft called for five separate systems — a marketplace, a subscription engine, watermarking infrastructure, a hosted server — for a single text-file product. Robots Fight caught that this was built like a company's product line, not a solo creator's file. Rebuilt around one purchase, on existing commerce tools.

<a id="stakeholder-incentive-blindness"></a>
### Stakeholder-incentive blindness
A free-tier upsell draft used sharper, more urgent language to drive conversions. Robots Fight caught that this would make skeptical users trust the tool *less*, not buy it more — rebuilt around honest, existence-gated disclosure instead.

<a id="internal-inconsistency"></a>
### Internal inconsistency
A pricing draft called its launch discount a "founding price." Robots Fight caught that this was the exact urgency language an earlier rule on the same project had already banned — the label was dropped for a plain, disclosed price-change mechanism.

<a id="evidence-gap"></a>
### Evidence gap
A refund policy assumed the free lite tier already proved the paid tier's value to buyers. Robots Fight caught that this was an unverified assumption — lite never runs the paid stage at all — and the policy was rewritten on honest, checkable grounds.

<a id="edge-case-blindness"></a>
### Edge-case blindness
A refund policy said "all sales final" as if that settled the matter. Robots Fight caught that a buyer can bypass a stated policy entirely via a card-network chargeback — the policy was rewritten to say plainly what it does and doesn't cover.

## Full version

`/tot` (paid, one-time purchase) adds the Robots Fight adversarial-debate stage — see [link to Gumroad listing] for the full version.

## License

MIT-style — free to use, copy, and modify. "tot" and "/tot" are trademarks of RKlab; this covers the name/branding only, not this file's content.
