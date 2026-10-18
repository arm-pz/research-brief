# research-brief

An agent skill that answers "what is known about this" with a sourced brief: topic overviews, competitor profiles, industry scans, literature reviews, fact checks, expert syntheses, trend scans, due diligence checklists, readings of published figures, and one-page executive briefs. Each claim carries the source it came from, the date it was read and the tool that produced it, or it is marked `[unverified]`. When the session has no network, the brief opens with `STATUS: INCONCLUSIVE` and delivers the structure of what is assumed instead of a confident report. It prefers an honest gap over a filled one, because a plausible invented citation is the failure this skill exists to prevent.

Install: `npx skills add arm-pz/research-brief --skill research-brief`

Ask it things like:

- "Research the companies selling usage-based billing tooling for mid-market SaaS."
- "Is it actually true that the regulation bans this? Show me the sources either way."
- "Brief me before I meet them tomorrow, what is worth knowing."
- "Everyone says this market is worth billions. What is that number built on?"

## What you get

| Mode | Output |
|---|---|
| Topic overview | Scoped overview with the load-bearing findings in front, contested points separated out |
| Competitive intelligence | Profile per competitor, or one comparison table, with date of scan and a `What we cannot see` section |
| Industry analysis | Sized market picture where each estimate is a row: source, year, what it counts, method weakness |
| Literature review | Knowledge map clustered by conclusion: consensus, disputes, weak evidence, method limits |
| Fact check | Verdict wording for one claim, strongest source for, strongest against, both dated |
| Expert synthesis | Each named position stated at its strongest argument, attributed to a dated artifact |
| Trend scan | Patterns with two dated observations, a mechanism, a counter-case and a falsifier |
| Due diligence | Partner, investment or hire checklist: verified findings, red flags, and `Ask them for` |
| Public-figure interpretation | Published numbers read in their own terms, with definitions compared |
| Executive brief | One page, decision-first, every line inheriting the claim table |

Every mode returns the same spine: status line, summary, findings ranked by importance to your decision, claim table, conflicts, gaps, sources read, and a handoff block when the next step belongs to another skill.

## Not for

Turning findings into a recommendation or a roadmap (use `strategy-memo`), analysing your own dataset or CSV (use `data-readout`), being taught a subject concept by concept (use `topic-primer`), attacking a decision you already made (use `crash-test`), or judging a resume you already hold (use `recruiter-lens`). This skill stops at what is known and where it came from.

## Install

```
npx skills add arm-pz/research-brief --skill research-brief
```

Or copy `skills/research-brief/` into your agent's skills directory (`.claude/skills/`, `.agents/skills/`, `.cursor/skills/` or `.qoder/skills/`). With Claude Code plugins, `.claude-plugin/plugin.json` makes the repo installable as a plugin; add it to your marketplace repo as an entry pointing at `arm-pz/research-brief`.

## Structure

```
research-brief/
├── README.md
├── LICENSE
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── research-brief/
│       ├── SKILL.md                    # intake, modes, output spine, quality bar, handoffs
│       └── references/
│           ├── report-formats.md       # shape per mode
│           ├── verification.md         # claim table, statuses, INCONCLUSIVE posture, conflicts
│           └── due-diligence.md        # partner, investment and hire checklists
└── tests/
    └── test-prompts.md                 # triggering, behaviour and boundary cases
```

Part of the Caffeinity content and strategy suite: eight skills with one owner per verb, so research stops at the finding and the decision, the numbers and the lesson each go to their own skill.
