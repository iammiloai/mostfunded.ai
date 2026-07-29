# mostfunded 📊

**A live leaderboard of the most funded Y Combinator companies — maintained by an agent, not by me.**

[mostfunded.ai](https://mostfunded.ai)

> Showcase repo — the concept, the pipeline shape, and the teardown. Source is private.

---

## The idea

Funding data goes stale the day you publish it. A leaderboard is only interesting if it's *current*, and keeping it current is exactly the kind of work nobody wants to do every week.

So the site doesn't have an editorial team. It has a scheduled agent that researches fresh funding rounds from public sources every day and updates the dataset. I look at it when I feel like it.

## How the pipeline works

```
  scheduled agent
  researches public funding sources daily
          │
          ▼
  updates the tracked dataset
          │
          ▼
  deploy → on boot, sync into the database
          │
          ▼
  leaderboard, ranked by total raised, filterable by batch
```

The design decision that makes it survivable: **every row is tagged with its origin.** Agent-written rows are marked `auto`. Anything I add or correct by hand is marked `manual` — and the sync is forbidden from touching those.

Without that, every human correction gets silently reverted on the next run and you stop trusting the whole thing within a week. With it, the agent and I can both write to the same table forever.

## What flopped

**Trusting the agent's numbers unconditionally.** Early runs happily reported rounds that were rumoured, double-counted, or from the wrong company with a similar name. The fix wasn't a better prompt — it was requiring a source and making anything unsourced fail loudly instead of landing quietly.

**No manual override.** See above. Version one had the agent as the only writer. First time I spotted an error I fixed it, and it vanished the next morning. That's the bug that produced the `auto`/`manual` split.

**Ejecting from a no-code host mid-flight.** This started life on a hosted builder and got moved onto real infrastructure. Getting the app out was fine; getting the *data* out with nothing silently reshaped was the actual project.

**Ranking on a number that means different things.** "Total raised" quietly mixes rounds, valuations, debt, and secondaries depending on the source. Half the work in a leaderboard is deciding what the number is allowed to be.

## What I learned

**Scheduled agents are underrated content infrastructure.** A daily agent turns a one-off blog post into a living page that earns links forever. Same effort, completely different half-life.

**Design for two writers from day one.** Any agent-maintained dataset will eventually need a human to correct it. If you don't decide up front who wins, the answer is "whoever ran last," and that's not an answer.

**Make the agent's work auditable.** Origin tags, sources, and a visible last-updated date. Autonomy without a paper trail isn't autonomy, it's just a system you can't debug.

---

Built by [Milo](https://hey.milo.gg)
