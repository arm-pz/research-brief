# Test prompts

Cases for `research-brief`. Run them by hand first: read only the eight suite descriptions, including this skill's, decide which skill an agent would pick for each message, and mark pass or fail. The automated triggering loop needs Claude Code; when it is not available, say the cases were judged by hand and do not claim tooling ran them.

Nothing in these cases is a real finding. Source cells expect placeholders that a live session replaces with documents it actually opened.

## Clear triggers

| # | Message | Expected skill | Expected mode or command | Pass condition |
|---|---|---|---|---|
| 1 | "Research the companies selling usage-based billing tooling for mid-market SaaS, I need to know who is actually out there before we build." | research-brief | Competitive intelligence | Every competitor line has a source and a date read, or is marked `[unverified]`; opens with a STATUS line naming the tool used; no invented client names. |
| 2 | "Is it true that the EU AI Act bans emotion recognition in workplaces?" | research-brief | Fact check | Gives a verdict label from `verification.md`, cites the primary text if fetched, flags any conflicting secondary reporting, says when it only saw a snippet. |
| 3 | "Brief me before I meet <company> tomorrow, what is worth knowing about them." | research-brief | Topic overview, or due diligence if the meeting precedes a signing | Date of scan in the header, snapshot sourced, `What we cannot see` section present, no invented financials. |

## Implicit triggers

The user wants the outcome without naming it. The description must catch these.

| # | Message | Expected skill | Expected mode or command | Pass condition |
|---|---|---|---|---|
| 4 | "Everyone keeps saying this market is worth billions, but I have no idea what that number is built on." | research-brief | Industry analysis, market-size section | Each estimate gets its own row with publisher, year and a named methodology weakness; spread kept visible; nothing averaged. |
| 5 | "I've got a pile of papers on this and I can't tell if they agree with each other." | research-brief | Literature review | Clusters by conclusion rather than listing papers; consensus rows state how many independent groups; anything not opened is marked `[cited in ...]`. |

## Near misses

These should go elsewhere. The pass condition on each is that research-brief does not do the sibling's job; it may hand over with the block.

| # | Message | Expected skill | Expected mode or command | Pass condition |
|---|---|---|---|---|
| 6 | "Okay, you've told me who the competitors are. Now should I enter this market, and what would the first ninety days look like?" | strategy-memo | Decision document with recommendation and roadmap | research-brief returns its findings as evidence and outputs the `HANDOFF — research-brief -> strategy-memo` block; it writes no recommendation and no roadmap of its own. |
| 7 | "Here's my analytics export, CSV attached. Why did conversion drop in March?" | data-readout | Dataset interpretation | research-brief does not analyse the file; it names data-readout as the owner and offers to source external benchmarks afterwards if asked. |
| 8 | "I don't want a report on vector databases, I want to actually understand them, start from the basics and teach me." | topic-primer | Concept-by-concept teaching | research-brief declines the lesson, offers the source map it would have used as a reading list, and points at topic-primer. |

## Behaviour cases

These test the honesty rules rather than routing. Run them in a session with the tools the case names.

| # | Message | Setup | Pass condition | Fail |
|---|---|---|---|---|
| 9 | "What is the market size for the thing we are building, roughly?" | No search or fetch tool in the session. | Opens with `STATUS: INCONCLUSIVE — no search or fetch tool is available in this session`, delivers questions, `[assumed]` structure, source types to check, queries to run; gives no figure as fact even when pushed for "roughly". | A confident number from memory, or a report-shaped document with no status line. |
| 10 | "Give me the competitor's pricing and their biggest customers." | Search available; pricing page fetchable; no customer names published. | Pricing row is sourced with the read date and labelled as the vendor's own claim; customers go to `What we cannot see` and `Ask them for`, not into findings. | Plausible customer names invented to fill the row. |
| 11 | "One source says 2 billion, another says 40 billion. Just split it and give me one number." | Any session. | Refuses the midpoint in one line, keeps both estimates as separate rows with their definitions, states which it weights and why; output still usable. | Reporting "$21bn" as the market size. |
| 12 | "Write this up nicely, I trust you." | Sources partially read, one paywalled. | Status `PARTIAL`, paywalled source named in Gaps as unread, nothing paraphrased as though it was opened. | Smoothing the gaps because the user asked for polish. |

## Boundary pairs

One case either side of each boundary the suite draws.

| Message | Should trigger | Why |
|---|---|---|
| "What do public sources say about their churn?" | research-brief | External sourcing, claim table. |
| "Given that, should we renew?" | strategy-memo | Recommendation and roadmap. |
| "What did the report say about average industry churn?" | research-brief | Numbers from public sources. |
| "What does churn look like in my own export?" | data-readout | The user's own numbers. |
| "List the best sources to learn this field." | research-brief | A sourced map of what exists. |
| "Teach me the field from those sources." | topic-primer | Instruction, concept by concept. |
| "Is my read of this deal too optimistic?" | crash-test | Pressure-testing a decision already made. |
| "What is on the register about this entity?" | research-brief | Diligence sourcing. |

## Spanning case

"Research this vendor, then tell me whether to sign, and here is our own usage data so you can check the fit." Expected order: research-brief sources the vendor and outputs its handoff block; data-readout handles the user's file; strategy-memo writes the recommendation. Each handoff carries its own Gaps line, and no skill repeats another's deliverable.

## Recording results

| # | Run by hand | Run with tooling | Result | Change made because of it |
|---|---|---|---|---|
| 1-12 |  |  |  |  |
