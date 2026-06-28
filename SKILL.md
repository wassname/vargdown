---
name: vargdown
description: Evidence council: save quote-anchored evidence, run independent credence chains, then consolidate.
metadata:
  url: https://github.com/wassname/argument-formats
---

# Vargdown

Use this when one perspective is likely to be the limiter.

Default to `varglight` for single-claim verification. Use `vargdown` when the
question needs multiple plausible arguments, adversarial credence estimates, or
a consolidated view of where the uncertainty really lives.

Do not write Argdown by default. Do not render a graph by default. Do not run
the old verifier unless the user explicitly asks for it.

## Procedure

1. Gather evidence and save it.
2. Run multiple independent credence chains.
3. Consolidate.

## 1. Gather Evidence

Create an evidence pack in the project, usually:

```text
evidence/{slug}/
  sources/
  chains/
  consolidated.md
```

For each source, save a markdown file with:

```markdown
Source: {url}
Title: {title}
Date: {visible date, or "not stated"}
Fetched-via: {tool}
Fetch-status: {verbatim | partial | summary}

> {generous verbatim quote with enough context to audit}

epistemic context: {one sentence about the source, not the world}
```

Quotes should follow `varglight`: generous, attributed, ctrl-F-able, and not
collapsed into summary. If the source is partial, say so plainly.

## 2. Independent Credence Chains

Run 3-5 independent passes over the same evidence pack. Each pass writes one
file in `chains/`.

Each chain must include:

```markdown
# Chain {n}: {stance or model}

## Bottom Line
p ~= {range}

## Argument
{short reasoning chain, with links to saved evidence files}

## Key Assumptions
- {assumption}: p ~= {range}

## Cruxes
- {what would change this chain's answer}

## Cheap Way To Be Wrong
{most likely failure mode}
```

Agents may disagree. That is the point. Do not force consensus during this step.

## 3. Consolidate

Write `consolidated.md` after reading the chains and evidence.

Required sections:

```markdown
# Consolidated View

## Answer
p ~= {range}

## Main Evidence
- {claim}: [source](sources/file.md)

## Agreements
- {what most chains agree on}

## Disagreements
- {where chains differ, and why}

## Double-Counting Check
- {shared sources or shared causal origins}

## Cruxes
- {highest-value observations that would change the answer}

## What I Would Check Next
- {smallest useful next search, experiment, or calculation}
```

## Principles

- Auditability beats formalism. Saved quotes and source notes are the core value.
- Multiple perspectives beat one polished argument when the question is uncertain.
- Preserve disagreement until consolidation.
- Do not count the same source twice just because two chains cite it.
- Use credence ranges, not fake-precision points.
- Keep the artifact readable by humans who will not learn a custom syntax.
- Prefer a short honest chain over a complete-looking map no one will validate.
