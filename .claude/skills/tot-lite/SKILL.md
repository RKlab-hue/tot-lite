---
name: "tot-lite"
description: "Free lite tier of /tot. Tree of Thought only (at least 7 distinct branches → evaluate → synthesize → golden path) — the adversarial 'Robots Fight' debate stage is not included in this tier. Use for architecture decisions, hard debugging, irreversible calls, security-sensitive design, or research synthesis where a single-pass exploration is enough. For a result pressure-tested by 3 adversarial personas across 3 rubric-weighted rounds before finalizing, see /tot (full version)."
---

# ToT Lite

This is the free lite tier of `/tot`. It runs **Stage 1 (Tree of Thought) only, at full quality** — the same branch count, evaluation, and synthesis as the full version. Nothing in Stage 1 is degraded, shortened, or simplified for this tier.

It does **not** run Stage 2 ("Robots Fight" — an adversarial 3-persona, 3-round debate that pressure-tests the golden path and revises it before finalizing). That stage exists only in the full paid version of `/tot`.

Scope: reserve this for prompts where being wrong or sloppy is expensive — architecture/design decisions, hard bugs, irreversible or high-blast-radius calls, security-sensitive design, research synthesis. Do not invoke for routine requests; the multi-branch fan-out is not worth the cost otherwise.

## Execution mode — check this first

This skill runs differently depending on what the current environment actually supports. Determine which mode applies before starting:

- **Parallel mode** (Agent/subagent tool with background execution is available — e.g. Claude Code, Cowork): every branch is a real, independent subagent call, batched so they run concurrently. Preferred whenever available.
- **Sequential mode** (no subagent tool, or a single-session environment like claude.ai): simulate independence deliberately — generate each branch in its own clearly-delimited pass, explicitly discarding/ignoring earlier passes' content while writing the next one. Say so plainly in the output ("running in sequential mode — branches are simulated independently, not truly concurrent") rather than implying subagents ran when they didn't.

## Tree of Thought

### 1. Branch generation
Produce **at least 7 distinct branches** (more is fine if the problem space genuinely supports it — don't pad with near-duplicates just to hit a number). Each branch is a self-contained solution/approach built around one genuinely different core idea or mechanism. In parallel mode, spawn one subagent per branch with only the original prompt. In sequential mode, generate each branch in its own pass per the independence discipline above.

Before finalizing the branch set, sanity-check spread: if two branches are really the same mechanism with different names, replace one of them with a genuinely different approach.

### 2. Evaluate
For each branch, write explicit pros and cons. Do not skip weak branches — a branch's cons are what make synthesis possible.

### 3. Drop pass (before synthesis)
A branch is dropped from synthesis **only** if one of these is true, quoted explicitly:
- it contradicts an explicit hard constraint stated in the original prompt, or
- the branch's own reasoning admits it doesn't work.

Otherwise it stays in play — benefit of the doubt. State the quote and reason for every drop.

### 4. Synthesize
Merge the elements from surviving branches that make the result more efficient, more trustworthy, and less reliant on guesswork. Pull specific mechanisms/decisions across branches, not whole branches. Say explicitly which branches were NOT incorporated and why.

### 5. Golden path
Output the synthesized result as one coherent solution. This is the final answer for this tier.

## Soft-spot disclosure (required — do not skip)

Before presenting the golden path as final, scan it against this fixed taxonomy and flag anything that applies. This is the lite tier's honesty mechanism — it is disclosure, not a sales pitch, and the rules below are not optional.

**Taxonomy** (flag only what genuinely applies — do not force a fit):
- Unstated assumption — the golden path quietly depends on something never tested against alternatives
- Claims overreach — states something with more legal/technical/factual force than it can back up
- Edge-case blindness — hasn't been pressure-tested against a "what if this breaks" scenario
- Proportionality mismatch — solution's complexity/cost isn't checked against actual problem scale
- Internal inconsistency — the plan's mechanisms contradict its own stated philosophy/goal
- Stakeholder-incentive blindness — doesn't account for how a specific affected party would actually react/exploit it
- Evidence gap — a claim is asserted but not checked against verifiable grounding

**Hard copy rule (never violate this):**
- A flag may name what is *untested* in the category above. It must **never** imply the answer is *probably wrong*, use urgency language ("don't risk it," "before it's too late"), scarcity/social-proof language ("other users caught this"), or a countdown/limited-time framing.
- Acceptable: *"Soft spot flagged: [category] — [specific untested element in this answer]."*
- Not acceptable: *"This part might be wrong"* / *"Answers like this are often wrong"* / any framing whose persuasive force comes from doubt about this specific answer rather than a documented, named gap.
- Test before writing any flag: could this sentence be defended to the reader even after showing them the full Stage-2 debate on this exact question, win or lose? If the sentence only survives when Stage 2 happens to catch something, don't write it.

**Case-study link (existence-gated — do not force it):**
- A flag becomes a link **only if** a real, genuinely category-matching published case study exists (e.g. *"See how the full version caught a [same category] miss → [case study link]."*).
- If no genuine match exists for a flagged category, say so plainly instead: *"No public case study in this category yet."* Never link to a near-miss or a generically "why upgrade" page to manufacture relevance.
- Render this once per genuine match. If the same category appears more than once in one output, link it each time it genuinely recurs.
- Do not show price or any purchase-pressure copy at the flag itself. The link may lead somewhere that mentions price; the flag text itself never does.

**Placement:** inline, immediately next to the specific claim or branch it corrects — not a footer, not an appendix.

## Output format

1. **Mode declaration** — parallel or sequential, and why
2. **Branches** — all of them (7+), each with pros/cons, and drop reasons (with quotes) for any dropped
3. **Synthesis rationale** — what was pulled from where, and what was left out and why
4. **Golden path** — the final answer for this tier, with soft-spot flags placed inline per the rules above

## Notes for the orchestrating agent

- This tier has no Stage 2. Do not run, simulate, or reference a debate having occurred — the golden path above is the unrevised, single-pass result.
- Soft-spot flags are generated fresh from this specific answer's actual content each run — never templated or reused boilerplate ("this might have edge cases" with no specifics is not a valid flag).
- This skill file has no external dependencies — copying it into `.claude/skills/tot-lite/SKILL.md` (or an equivalent skills directory on another platform) is sufficient to make it available there.
