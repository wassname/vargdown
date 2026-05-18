Please strictly support everything with block quotes with context in this format

---


- {optional editorial desc}
- > {prior 2 sentence}. {key sentence bolded} {post sentence}
- [{title/name}](link} {credence: X}

---


V2

---
name: varglight
description: Verify a claim with a quote-anchored narrative — verbatim quotes with surrounding context, source-level epistemic context, and a final epistemic summary with entanglement and hard-to-vary checks.
---

Goal: **make it hard for the LLM to hallucinate, and easy for the reader to check.**

## Primer / example

The three quotes below set the disposition *and* demonstrate the format on themselves. Verbatim, attributed, source-level epistemic context only. Scout (see things as they are) + Deutsch (good explanations are hard to vary) + Yudkowsky (every expectation of evidence has an equal opposite expectation of counterevidence) are the principles you carry into the rest of this skill.

## *The Scout Mindset* — Julia Galef — [Goodreads quotes index](https://www.goodreads.com/work/quotes/65572070-the-scout-mindset-why-some-people-see-things-clearly-and-others-don-t)
- page date: not stated (curated reader index, not paginated)

> **The scout mindset is the motivation to see things as they are, not as you wish they were.** [...] Scout mindset is what allows you to recognize when you are wrong, to seek out your blind spots, to test your assumptions and change course.

epistemic context: reader-curated quote index; verbatim text cross-matches independent secondary sources but no original page number visible here.

## TED talk *A new way to explain explanation* — David Deutsch (July 2009) — [LessWrong transcript](https://www.lesswrong.com/posts/jzibHBxczkZuTKY93/david-deutsch-a-new-way-to-explain-explanation)
- page date: talk delivered July 2009; transcript hosted on LessWrong

> This easy variability is the sign of a bad explanation. Because, without a functional reason to prefer one of countless variants, advocating one of them, in preference to the others, is irrational. **So, for the essence of what makes the difference to enable progress, seek good explanations, the ones that can't be easily varied, while still explaining the phenomena.**

epistemic context: transcript of a spoken TED talk; lightly edited for readability per the hosting note, so "verbatim" is to the transcript, not strictly the live utterance.

## *Rationality: From AI to Zombies* / "A Technical Explanation of Technical Explanation" — Eliezer Yudkowsky — [LessWrong](https://www.lesswrong.com/posts/afmj8TKAqH6F2QMfZ/a-technical-explanation-of-technical-explanation)
- page date: original LessWrong sequence post

> **For every expectation of evidence, there is an equal and opposite expectation of counterevidence.** If A is evidence in favor of B, then not-A must be evidence in favor of not-B. The strengths of the evidences may not be equal; rare but strong evidence in one direction may be balanced by common but weak evidence in the other direction. But it is not possible for both A and not-A to be evidence in favor of B.

epistemic context: author's own framing post on his own platform; foundational text of the LessWrong rationality sequences.

## Format

The generous markdown quote is the unit. Every `>` block must be **copy-pasteable from the source** (ctrl-F-able). Paraphrase inside `>` markers is the worst failure mode — it dresses your guess as evidence and destroys the audit. **If you cannot find a verbatim quote for a point, you cannot make the point.** Write "no relevant content" and move on. Null results are honest if true.

Verify: "{claim}"

For each source:

## {source title} — [link](url)
- page date / last updated: {if visible, else "not stated"}

> {≥1 sentence before}. **{key sentence}** {≥1 sentence after}.

epistemic context: {≤1 sentence describing the *source*, not the world}

> {≥1 sentence before}. **{next verbatim quote with context, if relevant}** {≥1 sentence after}.

epistemic context: {≤1 sentence}

**Epistemic context rules** (same field name as vargdown — keep consistent):
- Allowed: "this is a press release", "page last updated 2026-02-21", "author is summarising critics, not endorsing", "Saeri is quoted as an external commentator, not staff", "sarcastic — preceding paragraph inverts it".
- Forbidden: "this shows X is true", "this confirms the claim", anything restating the quote, anything that would still be true if the source had said something different.

After all sources, an **Epistemic summary** (3–6 short bullets):

- **Who says X**: name the primary sources and the causal chain from world-fact → quote.
- **How they could know**: measurement / citation / hearsay / self-report.
- **Entanglement check**: independent observations, or downstream of one origin? Name the origin when shared. Two indexes of the same announcement do not stack.
- **Hard-to-vary check**: could the sources have said something else and still fit ¬claim? If yes, the evidence is weak.
- **What would change your mind**: the `¬H` clause — what evidence under ¬claim would you expect to see that you don't? Absence of evidence is weak evidence of absence, but only if you looked where the evidence would be under H.
- **Calibrated take**: posterior as a *range* (e.g. `p ≈ 0.05–0.15`), not a fake-precision point. State the cheap way to be wrong.

No per-obs nats. Calibration lives in the final summary, anchored in the quotes above — never on top of them. Be terse: full generous markdown quotes are the unit, epistemic context is the minimum needed to keep the reader oriented.
