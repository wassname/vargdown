# Merge plan: skill-adversarial-review -> ASP

Branch: https://github.com/wassname/vargdown/compare/main...skill-adversarial-review

## What to take (in priority order)

### 1. Principle 1b2: Independent verifiability (high value, no conflict)
> Each claim is independently verifiable at its level. Observations: checkable by reading only the quote + source. Assumptions: assessable on their stated reason alone. Inferences: evaluable given only the stated premises and reason.

This is a new principle that slots between 1b and 1c. Pure addition, no conflicts.

### 2. Tighter credence semantics on Rule 1 (high value, minor rewrite)
Branch sharpens `{credence: X}` from "trust in source" to "how much you trust the source's own finding is accurately reported and methodologically sound." Relevance-to-thesis goes in the inference step. This is a meaningful semantic distinction that prevents conflating source quality with argument relevance.

### 3. Three-layer verification table (medium value, replaces prose)
Replaces the one-line verification section with a table: machine / sub-agent / human, each with what they check. We already have the principle in AGENTS.md ("automate first, delegate second, human last") -- this makes it concrete in SKILL.md.

### 4. More skeptical calibration in examples (medium value, requires re-verification)
The branch drops several credences in the SKILL.md example:
- Nesbit observation: 0.70 -> 0.55 (abstract-only access)
- Mapping Helps Thinking inference: 0.75 -> 0.40 (domain transfer concerns)
- Forced Sourcing Helps inference: 0.85 -> 0.60 (LLMs can hallucinate evidence files too)

These are more honest numbers. Must re-run tests after applying.

### 5. Scalable oversight framing (low priority, nice context)
Connects vargdown to debate/iterated amplification literature (Irving et al. 2018, Christiano et al. 2018) with honest caveats about where vargdown falls short. Good for the README or an appendix, not critical for the skill itself.

## What NOT to take (already done differently on ASP)

- **Adversarial workflow structure**: the branch restructures Usage into worker/reviewer/consolidator roles. We've already done this differently: SKILL.md step 3 + review_prompt.md. The branch version is more prescriptive; ours is more flexible (capability modes). Reconcile by checking if the branch's rubric adds anything review_prompt.md doesn't cover.

- **Ensemble mode rewrite**: the branch makes ensemble mode procedural (spawn n=3 workers, judge scores on 4 axes). This is ambitious but untested. Defer.

- **Cluster-X documentation**: the branch says clustered arguments are "just flagged for human review." We went further with Rule 7 (must merge). Keep our version.

## Merge procedure

1. Cherry-pick principle 1b2 into SKILL.md Principles section
2. Update Rule 1 credence semantics (manual edit, small)
3. Add three-layer verification table to SKILL.md Verification section
4. Apply calibration updates to SKILL.md example + pattern_0_main.argdown
5. Run `npm test`, fix any breakage
6. Optionally add scalable oversight section to README.md
