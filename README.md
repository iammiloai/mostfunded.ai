# mostfunded.ai

A leaderboard of the most funded YC companies.

[mostfunded.ai](https://mostfunded.ai)

Write-up, not source code.

## What it is

The YC companies that have raised the most money, ranked, and filterable by batch. That's it.

Funding data goes stale the day you publish it, and keeping it fresh is exactly the kind of job nobody wants every week. So it updates itself. Something runs every day, looks up new rounds from public sources, and updates the list. I check on it when I feel like it.

## The decision that made it work

Every row is tagged with where it came from. Rows written automatically are marked as such. Anything I fix by hand is marked as mine, and the automatic update isn't allowed to touch it.

Without that, every correction I made got quietly wiped the next morning and I stopped trusting the whole thing inside a week.

## What didn't work

**Believing the numbers.** Early runs cheerfully reported rounds that were rumoured, counted twice, or belonged to a different company with a similar name. The fix wasn't a better prompt, it was requiring a source and failing loudly when there isn't one.

**No way to override it.** See above. Version one had nothing but the automatic updates. The first error I fixed disappeared overnight.

**Moving off a no-code host halfway through.** Getting the site out was fine. Getting the data out without anything quietly changing shape was the actual project.

**"Total raised" means different things.** Depending on the source it mixes rounds, valuations, debt and secondaries. A good chunk of building a leaderboard is deciding what the number is allowed to be.

## What I learned

Something that updates itself turns a one off blog post into a page that keeps earning links. Same effort, completely different shelf life.

If a person and a machine are both going to write to the same data, decide up front who wins. Otherwise the answer is "whoever ran last", which isn't an answer.

---

Built by [Milo](https://milo.gg)
