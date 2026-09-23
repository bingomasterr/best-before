# Best Before

**AI answers go stale silently. Best Before adds a three-line stamp to any answer that can date: the source, what could change it, and when to check again.**

A skill for Claude that works like a use-by date on food. When an answer contains something that can go out of date, Claude adds a small label at the end. When the answer is timeless, it adds nothing.

## The problem

Most wrong answers aren't wrong on the day you get them. They go wrong later.

You ask about a tax threshold, a library's default setting, or a security fix. The answer is correct. You paste it into a doc, a runbook, or a spreadsheet. Six months later the threshold changes, the library ships a new version, the advisory gets updated, and nothing tells you. The answer is still sitting there looking just as confident as the day you copied it.

Best Before doesn't make answers more accurate. It makes their shelf life visible.

## What it looks like

Ask Claude for the current UK VAT registration threshold and the answer ends with:

```
True as of: 23 Sep 2026, from GOV.UK VAT registration guidance (updated [page date])
Could change if: the threshold is changed at the next Budget
Recheck: after the next Budget, at [GOV.UK link]
```

If the answer came from Claude's training data rather than a live source, it says so plainly:

```
True as of: training data, not checked live
Could change if: the library ships a new release that drops or adds versions
Recheck: now, on the library's PyPI page or changelog
```

Ask how public key cryptography works and you get no stamp at all, because that answer won't expire.

## How it decides

**When to stamp.** Anything the reader might act on that could realistically change: prices, tax rates, laws, software versions, API behaviour, security advisories, who holds a role, fees, deadlines, official guidance.

**When to stay quiet.** Maths, definitions, settled history, creative writing, opinions, and quick chat where a stamp would be longer than the answer.

**Sources.** The stamp always says where the fact came from.

- It prefers the primary source (the government site, vendor docs, the official changelog) over a blog summarising it, because the primary page is the one that changes first.
- It uses the source's own "last updated" date, not just the date it searched. A page fetched today might not have been touched in two years.
- It names one source in the stamp, the best place to recheck. The main answer can cite as many as it needs.
- If there's no live source, it says "training data, not checked live" and gives no link. It never invents a source to look more trustworthy.

**Recheck timing.** It uses a known event when there is one, like the next Budget or the next major release. Otherwise it falls back to rough defaults by fact type:

| Type of fact | Default recheck |
|---|---|
| Live prices, exchange rates, scores, weather | Same day |
| Retail prices, deals, availability | 2 to 4 weeks |
| Security advisories, CVE guidance | 1 to 2 weeks |
| Software versions, APIs, SaaS plans, AI model names | 1 to 3 months |
| Who holds a role | 3 to 6 months, or after the next election or announcement |
| Fees, benefits, eligibility rules | 6 months, or next scheduled review |
| Tax rates and thresholds | Next Budget or next tax year |
| Laws and regulations | 12 months, or when new legislation takes effect |
| Clinical or official health guidance | 12 months, or when the guideline body updates |

These intervals are judgement-based starting points, not research findings. Better-evidenced numbers are very welcome (see Contributing).

**Reminders.** If Claude has access to a reminders or calendar tool and you're clearly going to rely on the answer, it offers once to set a reminder for the recheck date.

## Install

### Claude Code

For all your projects:

```bash
mkdir -p ~/.claude/skills/best-before
cp SKILL.md ~/.claude/skills/best-before/
```

For one project only:

```bash
mkdir -p .claude/skills/best-before
cp SKILL.md .claude/skills/best-before/
```

Start a new session and it loads automatically.

### Claude.ai and Claude Desktop

Claude.ai takes skills as a zip file, not a bare `SKILL.md`. Custom skills need a Pro, Max, Team, or Enterprise plan with code execution turned on.

1. Create a folder called `best-before` and put `SKILL.md` inside it.
2. Zip the folder, so the zip contains `best-before/SKILL.md`. The folder name must match the skill's name.
3. In Claude.ai, open Settings, find Skills, and upload the zip.

### Other agents

The skill uses the standard Agent Skills format (a folder with a `SKILL.md`), so it should work with other tools that support that format. It has only been tested with Claude.

## Try it

Once installed, ask something time-sensitive:

- "What's the latest Node.js LTS version?"
- "What's the UK personal allowance this tax year?"
- "Is there a fix for [recent CVE]?"

Then ask something timeless, like "explain how DNS works", and check that no stamp appears.

## Repo structure

```
best-before/
├── SKILL.md      The skill itself
└── README.md     This file
```

## Contributing

Issues and pull requests are welcome, especially:

- **Better recheck intervals** backed by a source (for example, how often a vendor actually changes its pricing, or how often a guidance body revises its advice).
- **Over-stamping or under-stamping.** If it stamps something that doesn't need it, or misses something that does, open an issue with the question you asked and what you got.
- **New fact types** that don't fit the current table.

Please keep the stamp short. The whole point is a label you can skip when you don't need it and find when you do.

## Status

Early version. The core rules are stable, but the default intervals will change as people test it on real questions.

## License

MIT
