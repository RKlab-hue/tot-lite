---
name: "tot-lite"
description: "Free lite tier of /tot. Tree of Thought only (complexity-adaptive branch count → evaluate → synthesize → golden path), with a fact-checking/citation discipline for load-bearing claims — the adversarial 'Robots Fight' debate stage is not included in this tier. Use for architecture decisions, hard debugging, irreversible calls, security-sensitive design, or research synthesis where a single-pass exploration is enough. For a result pressure-tested by 2-7 adversarial personas (expanding with contrarian perspectives on fast convergence) across 3+ rubric-weighted rounds before finalizing, see /tot (full version)."
---

# ToT Lite

This is the free lite tier of `/tot`. It runs **Stage 1 (Tree of Thought) only, at full quality** — the same branch count, evaluation, and synthesis as the full version. Nothing in Stage 1 is degraded, shortened, or simplified for this tier.

It does **not** run Stage 2 ("Robots Fight" — an adversarial 3-persona, 3-round debate that pressure-tests the golden path and revises it before finalizing). That stage exists only in the full paid version of `/tot`.

Scope: reserve this for prompts where being wrong or sloppy is expensive — architecture/design decisions, hard bugs, irreversible or high-blast-radius calls, security-sensitive design, research synthesis. Do not invoke for routine requests; the multi-branch fan-out is not worth the cost otherwise.

## Execution mode — check this first

This skill runs differently depending on what the current environment actually supports. Determine which mode applies before starting:

- **Parallel mode** (Agent/subagent tool with background execution is available — e.g. Claude Code, Cowork): every branch is a real, independent subagent call, batched so they run concurrently. Preferred whenever available.
- **Sequential mode** (no subagent tool, or a single-session environment like claude.ai): simulate independence deliberately — generate each branch in its own clearly-delimited pass, explicitly discarding/ignoring earlier passes' content while writing the next one. Say so plainly in the output ("running in sequential mode — branches are simulated independently, not truly concurrent") rather than implying subagents ran when they didn't.

## Fact-checking & citations

Treat this like evidence in a debate or court proceeding: a claim earns trust by being checkable, not by being stated confidently. This applies to branches and the golden path alike.

- A claim is **load-bearing and externally verifiable** if it asserts a fact about the world outside this reasoning process (a law, a technical spec, a historical event, a statistic, what a tool/library actually does) — as opposed to a judgment call or tradeoff assessment, which cannot be "cited" and shouldn't pretend to be.
- If a search/fetch tool is available in this environment: use it to find a real source for load-bearing claims that materially affect the conclusion, and cite it.
- If no such tool is available, or a claim can't be verified even with one: state it as **"unverified — no citation available"** plainly next to it, rather than presenting it with unearned confidence.
- Never fabricate a citation or a source. An honest "unverified" beats an invented-sounding reference every time.

## Tree of Thought

### 1. Branch generation
Before generating branches, judge the problem's actual scope: how many genuinely distinct core mechanisms/approaches does this specific problem support? Produce that many branches — **complexity-adaptive, not a fixed count** (a narrow problem might genuinely support only 4-5; a genuinely open-ended one may support 10+). Never pad with near-duplicates to hit a number, and never force a narrow problem down to fewer branches than it actually supports. State the branch count and a one-line justification before generating them. Each branch is a self-contained solution/approach built around one genuinely different core idea or mechanism. In parallel mode, spawn one subagent per branch with only the original prompt. In sequential mode, generate each branch in its own pass per the independence discipline above.

Before finalizing the branch set, sanity-check spread: if two branches are really the same mechanism with different names, replace one of them with a genuinely different approach. If this drops the count below the stated justification, generate one more genuinely distinct branch rather than silently shipping fewer than announced.

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
- Test before writing any flag: is this a specific, checkable statement of what's untested — not a hedge, not a hint of doubt, not something dressed up to look more alarming than "I didn't check this"? If the sentence implies more than "this specific thing wasn't verified," rewrite it or drop it.

Flags apply to the golden path only — Stage 1's branches (in the Branches output section) are not flagged individually; a branch-level concern gets folded into a golden-path-level flag if it survives synthesis.

**Case-study link (existence-gated — do not force it):**
- A flag becomes a link **only if** a real, genuinely category-matching published case study exists (e.g. *"See how the full version caught a [same category] miss → [case study link]."*).
- The published case-study library lives at `https://github.com/RKlab-hue/tot-lite#<category-slug>` (e.g. `#unstated-assumption`, `#claims-overreach`, `#edge-case-blindness`, `#proportionality-mismatch`, `#internal-inconsistency`, `#stakeholder-incentive-blindness`, `#evidence-gap`) — link directly to the matching anchor, not the repo root. If this URL is ever unreachable or the case-study library is moved, do not render any case-study link — fall back to "No public case study in this category yet" for every flag, since a broken link is worse than no link.
- If no genuine match exists for a flagged category, say so plainly instead: *"No public case study in this category yet."* Never link to a near-miss or a generically "why upgrade" page to manufacture relevance.
- Render this once per genuine match. If the same category appears more than once in one output, link it each time it genuinely recurs.
- Do not show price or any purchase-pressure copy at the flag itself. The link may lead somewhere that mentions price; the flag text itself never does.

**Placement:** inline, immediately next to the specific claim or branch it corrects — not a footer, not an appendix.

## Output format

1. **Mode declaration** — parallel or sequential, and why
2. **Branches** — all of them, with the stated count/justification from step 1, each with pros/cons, and drop reasons (with quotes) for any dropped
3. **Synthesis rationale** — what was pulled from where, and what was left out and why
4. **Golden path** — the final answer for this tier, with load-bearing claims marked per the Fact-checking & citations section
5. **Soft-spot flags** — mandatory, not optional. Placed inline within the golden path (per the Soft-spot disclosure rules above), not appended separately or omitted. A response missing this section is incomplete even if items 1-4 are otherwise present.

## Notes for the orchestrating agent

- This tier has no Stage 2. Do not run, simulate, or reference a debate having occurred — the golden path above is the unrevised, single-pass result.
- Soft-spot flags are generated fresh from this specific answer's actual content each run — never templated or reused boilerplate ("this might have edge cases" with no specifics is not a valid flag).
- Branch count is complexity-adaptive now — don't default back to a fixed number out of habit; actually judge each run's problem scope.
- Apply the Fact-checking & citations discipline to branches too, not just the golden path.
- This skill file has no external dependencies — copying it into `.claude/skills/tot-lite/SKILL.md` (or an equivalent skills directory on another platform) is sufficient to make it available there.
