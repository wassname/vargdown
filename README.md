# vargdown - Verified Argument Maps Skill

Goal: make it **hard** to the LLM to hallucinate, and **easy** for you to check.

- 1st pass: automatic verification with code
- 2nd pass: approximate verification by another agent (sub agent)
- 3rd pass: human, assisted by good UI

To use, just give you LLM the skill: https://raw.githubusercontent.com/wassname/vargdown/refs/heads/main/SKILL.md or install with [openskills](https://github.com/numman-ali/openskills)

## Example

```argdown
===
model:
    mode: strict
===

[Umbrella]: I should bring an umbrella today.
  + <Forecast Says Rain>
  - <Clear Sky Now>

<Forecast Says Rain>

(1) [Forecast]: The weather app says 70% chance of rain this afternoon. #assumption
   [weatherzone](https://www.weatherzone.com.au/wa/perth/perth)(evidence/202060601_weatherzone_perth.md#L53-L53)
   > Perth for Tuesday. Cloudy, **70% chance of afternoon showers**. Winds SE 20 to 30 km/h turning S/SW in the early afternoon then tending S/SE 15 to 20 km/h in the evening.
    {reason: "data provided by the Bureau of Meteorology (BOM)", credence: 0.95}
----
(2) [Rain Likely]: It will probably rain today.
    {reason: "BOM highly calibrated", inference: 0.70}
  +> [Umbrella]

<Clear Sky Now>

(1) [Blue Sky]: The sky is currently clear and blue. #assumption
    {reason: "looking out the window right now", credence: 0.95}
----
(2) [Might Stay Dry]: It may not rain after all.
    {reason: "current sky tells you almost nothing about 4pm -- weather changes fast", inference: 0.20}
  -> [Umbrella]
```

Output: `[Umbrella]` implied credence ~62% (forecast outweighs the weak con of current clear sky).

**See [SKILL.md](./SKILL.md) for a realistic example with sources and quotes.

## Quick start (LLM use)

Give [SKILL.md](SKILL.md) to your agent.

## Dev

See [AGENTS.md](AGENTS.md) for developing the skill itself (tests, sub-agent loop, adding rules).

## References

- [Argdown syntax](https://argdown.org/syntax/)
