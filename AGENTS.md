# Dev Workflow

How to develop and test changes to vargdown (the SKILL.md format, verify.mjs verifier, etc.).

## Principles

**Automate first, delegate second, human last.** If something can be machine-checked, put it in the verifier -- don't ask agents or humans to eyeball it. The verifier handles: credence ranges, reason-before-credence ordering, inference vs credence on conclusions, top-level credence, PCS math, graph structure, quote presence, evidence headers. The sub-agent handles judgment calls the machine can't: is this credence calibrated or motivated? Are these arguments truly independent? Is this inference leap justified? The human handles cruxes -- the rest should already be resolved.

**Show what you mean, do what you say.** Every example in SKILL.md is extracted and verified by the test suite. If a rule says "do X", the examples must do X. If an example does Y, either the rule is wrong or the example is. Self-consistency is tested automatically -- the SKILL.md argdown block must pass the verifier.

**Sub-agents are testers, not helpers.** The worker sub-agent is a naive user who stress-tests whether SKILL.md is followable. The reviewer sub-agent is adversarial -- it finds problems. The main agent consolidates. If the sub-agent was confused, that's a bug in the docs, not in the sub-agent.

## Setup

```bash
git clone https://github.com/wassname/vargdown
cd vargdown
npm install

# smoke test
npx @argdown/cli json examples/linear_probs.argdown examples
npx vargdown examples/linear_probs.json examples/linear_probs_verified.html
```

## Cycle

```
make change -> npm test -> test with sub-agent -> review output -> address feedback -> commit
```

### 1. Make a change

Key files:
- `SKILL.md` -- format rules and principles (LLM-facing)
- `review_prompt.md` -- adversarial reviewer instructions (sub-agent-facing)
- `verify.mjs` -- orchestrator: loads JSON, calls ASP compiler, runs clingo-wasm, checks evidence, renders HTML
- `compile_asp.mjs` -- compiles argdown JSON into ASP facts (integer basis points, collision-checked atom IDs)
- `rules.lp` -- declarative verification rules (ranges, entailment, contrary, cycles, isolation)
- `test.mjs` -- test runner

When deciding where a check belongs:
- Can a regex/ASP rule catch it? -> `rules.lp` + `violationToMessage` in `verify.mjs`
- Does it need reading comprehension? -> `review_prompt.md` (sub-agent)
- Does it need domain expertise or value judgment? -> human (surfaced in HTML output)

### 2. Run unit tests

```bash
npm test
```

This runs `test.mjs` (Node.js built-in `node:test`). It covers:

1. **SKILL.md example** -- extracts the first argdown block from SKILL.md, parses and verifies it. Ensures the spec's own example stays valid.
2. **test_patterns/** -- one test per `.argdown` file. Each exercises a specific feature (undercut, contradiction, multi-step PCS, etc.).
3. **examples/** -- end-to-end examples produced by sub-agents or humans.

To add a new test pattern: create `test_patterns/<name>.argdown` with supporting evidence files (symlink `test_patterns/evidence -> ../evidence`). Picked up automatically.

All tests must pass before committing.

### 3. Test with a sub-agent

Spawn a sub-agent as a naive user of the skill:

```
You are testing the vargdown skill. Do NOT contact the user directly.

1. Read SKILL.md for the format rules.
2. Download sources into examples/evidence/*.md (with Source/Title/Fetched-via/Fetch-status headers as shown in SKILL.md).
3. Write an argument map to examples/test_output.argdown following SKILL.md.
   The thesis should be: [your thesis here].
4. Run: npx @argdown/cli json examples/test_output.argdown examples
5. Run: npx vargdown examples/test_output.json --verify-only
6. Fix any errors the verifier reports. Re-run until clean.
7. Run: npx vargdown examples/test_output.json examples/test_output_verified.html
8. Exit interview -- report back:
   - Was SKILL.md clear enough to follow without guessing?
   - What parts were confusing or ambiguous?
   - Were the verifier error messages helpful? Which ones weren't?
   - Do the examples in SKILL.md follow its own rules? Any inconsistencies?
   - Did you end up breaking any rules? Which ones and why?
   - What would you improve?
   - Paste the final .argdown content.
```

### 4. Review

If the sub-agent was confused by something, that's a signal SKILL.md needs clarifying. If the verifier missed something it could have caught, fix verify.mjs. Don't ask humans to check things the verifier can check.

### 5. Commit

```bash
npm test
git add -A && git commit
```

## Test sources

Put markdown files in `test_sources/<topic>/` with raw content for the sub-agent to argue about. Each topic folder should contain:
- Source files (`.md`) with exact quotes, URLs, and study details
- A `TASK.md` with thesis, source list, and step-by-step instructions

### Current test topics

| Topic | Folder | Thesis |
|---|---|---|
| Creatine & cognition | `test_sources/creatine_cognition/` | Does creatine supplementation improve cognitive performance? |

### Adding a new test topic

1. Create `test_sources/<topic>/` with source `.md` files (exact quotes + URLs)
2. Write `test_sources/<topic>/TASK.md` following the creatine example
3. Run the test, review, iterate
