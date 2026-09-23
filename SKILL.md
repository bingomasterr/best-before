---
name: best-before
description: Adds a short "Best Before" stamp to any answer that contains facts which can go out of date, such as prices, tax rates and thresholds, laws and regulations, software versions, API behaviour, security advisories, product availability, who holds a role, deadlines, fees, or official guidance. The stamp says when the answer was true, where it came from, what could make it wrong, and when to recheck. Use this skill whenever an answer includes anything that could change after today, even if the user did not ask about freshness, and especially when the answer is likely to be copied into a document, runbook, plan, or decision. Do not stamp timeless answers.
---

# Best Before

Answers rarely fail on the day they are given. They fail months later, after someone pasted them into a doc or a decision and nothing told them the facts had moved on. This skill adds one short stamp so the reader always knows how fresh an answer is and where to check it.

## When to stamp

Stamp an answer when it contains at least one fact that could realistically change within the next few years and the reader might act on it. Examples: a price, a tax threshold, a legal rule, a software version or default setting, a CVE mitigation, an eligibility rule, who runs a company, a deadline.

Do not stamp:

- Timeless material: maths, definitions, settled history, how a concept works.
- Creative writing, opinions, brainstorming, or code the user wrote themselves.
- Casual chat and quick one-line answers where a stamp would be longer than the answer, unless the fact is one people act on (money, law, health, security).

If most of the answer is timeless and one line is time-sensitive, stamp only that line's fact. When unsure, ask: "Would it matter if this were a year out of date?" If yes, stamp it.

## The stamp format

Place the stamp at the very end of the answer, separated by a blank line. Keep it to three lines:

```
True as of: [date], from [source name, updated date]
Could change if: [the single most likely thing to make this wrong]
Recheck: [when], at [link]
```

## Sources

The source is what makes the stamp usable. Without it, the reader knows the answer might be stale but not where to check.

1. **Live data (search or fetch):** name the source and link it. Prefer the primary source, such as the government site, the vendor's official docs, the regulator, or the official changelog. A blog or news summary is a fallback, not the default, because the primary page is the one that changes first.
2. **Use the source's own date, not just the search date.** A page fetched today may not have been updated for two years. If the page shows a "last updated" or publication date, use it. If it shows none, say "page undated".
3. **One source in the stamp.** The main answer can cite as many sources as it needs. The stamp points to the single best place to recheck.
4. **Training data only:** say so plainly, for example "True as of: training data, not checked live". Give no link. Never add a plausible-looking link or source to make an unchecked answer look verified. If search tools are available and the fact matters, search instead of stamping from training data.
5. **User-supplied data:** if the fact came from a file or message the user provided, say "from your [document name]" with its date if known.

## Choosing "Could change if"

Name one concrete trigger, not a vague warning. Good: "the thresholds are revised at the next Budget", "a new major version of the library ships", "the vendor changes its pricing page". Bad: "things may change", "always check the latest information".

## Choosing the recheck point

Use a known event when there is one, because it is more accurate than a guessed interval. For example, a UK tax figure should be rechecked after the next Budget or at the start of the next tax year (6 April). A library default should be rechecked at the next major release.

When there is no known event, use these rough default intervals. They are starting points for judgement, not rules:

| Type of fact | Default recheck |
|---|---|
| Live prices, exchange rates, stock levels, scores, weather | Same day |
| Retail prices, deals, availability, waiting times | 2 to 4 weeks |
| Security advisories, CVE guidance, actively exploited issues | 1 to 2 weeks |
| Software versions, API behaviour, SaaS features and plans, AI model names | 1 to 3 months |
| Who holds a role (CEO, minister, office holder) | 3 to 6 months, or after the next election or announcement |
| Fees, benefits, eligibility rules, company policies | 6 months, or next scheduled review |
| Tax rates and thresholds | Next Budget or next tax year |
| Laws and regulations | 12 months, or when new legislation takes effect |
| Clinical or official health guidance | 12 months, or when the guideline body publishes an update |

If the answer contains several time-sensitive facts, use the shortest recheck point among them.

## Reminders

If the app has a reminders or calendar tool and the answer is something the user is clearly going to rely on (a filing deadline, a renewal, a threshold in a financial plan), offer once, in one short line, to set a reminder for the recheck date. Do not offer for every stamp.

## Examples

**Example 1: live source**

User asks for the current UK VAT registration threshold.

Answer gives the figure, then:

```
True as of: 23 Sep 2026, from GOV.UK VAT registration guidance (updated [page date])
Could change if: the threshold is changed at the next Budget
Recheck: after the next Budget, at [GOV.UK link]
```

**Example 2: training data only**

User asks which Python version a library supports and no search tool is available.

```
True as of: training data, not checked live
Could change if: the library ships a new release that drops or adds versions
Recheck: now, on the library's PyPI page or changelog
```

**Example 3: no stamp**

User asks how public key cryptography works. The explanation is timeless, so no stamp.

## Writing the stamp

Keep it plain and short. No hedging paragraphs, no disclaimers about AI, no bold warnings. The stamp should read like a label on a jar: small, factual, easy to skip when you do not need it and easy to find when you do.
