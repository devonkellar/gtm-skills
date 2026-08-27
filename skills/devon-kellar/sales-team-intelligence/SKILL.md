---
name: sales-team-intelligence
title: Sales team intelligence
description: |
  Use this skill when you have a list of target accounts and need to know how each
  one actually sells before you write to them — "research these accounts", "how do
  these companies sell", "what's their sales motion", "prep me for this call list",
  "build account briefs", "who's on their sales team". Produces one intelligence
  brief per account, built by reading the public professional profiles of every
  member of that account's sales team: motion tags with the verbatim quote that
  proves each one, team shape, recent hires, positioning language, and concrete
  outbound hooks. The unit of output is the account, not the contact, and an
  account with no findable sales team is still a row, because that absence is
  itself a signal about how they sell.
category: Research
tags: [Sales, Demand Gen]
contributors: []
---

# Sales team intelligence

Runs before outbound: you have a target list, and writing to it blind means guessing at how
each company sells. Produces one brief per account, assembled by reading the public profiles
of that account's sales team and nothing else.

The failure mode this skill exists to prevent: **a brief that reads well and is quietly
wrong.** Two things produce it. First, researching the wrong company — same-name matches,
acquired-brand artifacts, and holding companies resolve to a plausible profile that survives
every check except reading it. Second, tagging a sales motion from one person's stray
sentence about a job they left in 2019. Both produce confident, fluent, useless output.
Everything below exists to stop them.

## Confirm you have the right company before reading anyone

Resolving an account to its company profile is where this work goes wrong, and it goes wrong
invisibly — you get *a* company, just not theirs.

Never accept a match on name similarity alone. Confirm it by reading what the profile says
about itself: the industry, the description, the specialties, the location. Then check that
against what you already know about the account (its domain above all).

**Deterministic scoring is not enough.** A wrong company can score highly on name overlap,
headcount plausibility, and having a profile at all, while sharing no domain and operating in
a different industry. Measured failure modes, all seen in real runs:

- **Acquired-brand artifact** — the name resolves to a `formerly-<brand>` profile belonging to
  a different business entirely
- **Same name, different industry** — a packaging company resolving to an electronics
  manufacturer
- **Holding company, not the operating company** — right group, wrong entity, wrong people
- **Same name, different country**

If you cannot confirm the match by reading it, mark the account `no_profile_found` and move
on. A wrong company is far worse than a missing one: the missing one is visible.

Generic company names ("3PL", "Packaging Ltd") will match anything. Do not attempt automated
resolution on them — flag them for manual handling.

## Read the sales team, current roles first

Pull the people the account employs in sales-shaped roles. For each, you need their current
title, current-role description, headline, and summary — plus start dates where available.

Treat the function label with suspicion. **These systems tag people by their self-reported
function, not by whether they carry a quota.** A "Sales Operations Analyst" is tagged sales.
A customer success director who used to sell might be too. So team size means "people who look
sales-shaped here", never "people with a number".

Save what you pull before analysing it. Re-reading costs nothing; re-fetching costs money and
some of it will have changed.

## Tag the sales motion, and make every tag carry its proof

This is the field outbound writers care about most: *how does this team actually sell?* Tag
from the eight motions in `references/motion-taxonomy.md` — outbound prospecting, email-led,
phone-led, field, partner/channel, account-based, inbound, and post-sale expansion.

Mark each as **primary** (what they are built around, usually one or two) or **secondary** (real
but not central, often none). **Cap at three tags total.** A team with more than three becomes
scannable noise; if more than three clear the bar, keep the three with the strongest evidence
and drop the rest.

There is no "trace" tier. A motion that cannot clear the bar does not appear.

**The evidence bar — every rule here exists because breaking it muddied real output:**

1. **Threshold.** Tag a motion only if two or more team members show the signal, OR one shows
   it in their *current-role* description unhedged, OR the team is one person and their current
   role states it plainly.
2. **A quote or it did not happen.** Every tag carries a verbatim quote from a named person's
   current-role text. No quote, no tag.
3. **Current roles only.** Previous-role text is research context, never motion evidence.
4. **Hedges disqualify.** If the quote wraps the motion in "also", "sometimes", "in past
   roles", "previously", "before that", "used to" — drop it.
5. **Empty is a valid answer.** If nothing clears the bar, the motion fields stay empty.
   "Unknown" is not a tag. Thin teams honestly produce empty motion fields.

Write each tag as: motion, strength, person's name, and the quote. The quote is what defends
the tag when someone challenges it.

## Count recent hires conservatively

Recent sales hires signal a team being built, which is a reason to reach out now. But start
dates are unreliable: many profiles omit the month, some omit the date entirely.

Accept a year-only date as recent **only if the year is the current one**. Under-counting is
honest; treating "joined sometime in 2023" as a recent hire inflates the signal and the reader
cannot tell.

## Keep every account, including the empty ones

Every input account gets an output row. No filtering.

**An account with no findable sales team is not a bad-fit account.** Small and private B2B
firms often have no publicly visible sales staff because a founder or MD does the selling.
That is a finding about how they sell, and for some offers it is the *best* finding. Keep the
row, leave the fields empty, and let the reader judge.

Use a tight, closed set of status values: found, no profile found, no sales team, error. Resist
inventing variants — "no sales team in region" is a parameter of your query, not a status.

## Write the brief so a reader can act in one screen

Per account: status, team size and shape, the motion tags with their quotes, recent hires,
positioning language in the team's own words, and two or three concrete outbound hooks that
follow from the evidence.

Deliver the whole set once, at the end, in a single write. Streaming partial results into a
shared destination as you go is the most common source of confusion about whether a run
finished.

## What good looks like

- The expert's first move on any promising profile match is to read the description and
  specialties, not to accept the name. Name-matching is how you confidently research a
  company that is not your prospect — and it is invisible in the output, because the brief
  looks perfectly good.
- The mediocre version tags four or five motions per account off single stray sentences,
  reports "unknown" for anything thin, and quietly drops the accounts where nothing was
  found. It reads comprehensive and cannot be trusted anywhere, because the reader has no way
  to tell which rows are real.
- A good brief passes three checks: every motion tag carries a named person and a verbatim
  current-role quote; every input account appears in the output including the empty ones; and
  a filled field is always real, so the reader can trust that empty means empty rather than
  lazy.
- Empty output on a thin team is the skill working. The credibility of every filled field
  depends on the empty ones being honestly empty.

## Rules

- MUST confirm a company match by reading the profile's own description, industry and
  specialties against the known account — never accept name similarity or a numeric score
  alone.
- MUST back every motion tag with a verbatim quote from a named person's current-role text.
  No quote, no tag.
- MUST ignore previous-role text as motion evidence, and MUST drop any quote hedged with
  "also", "sometimes", "previously", "in past roles", "used to".
- MUST cap motion tags at three per account, and MUST leave motion fields empty when nothing
  clears the evidence bar.
- MUST return one row per input account, including accounts with no findable team.
- NEVER invent a value for an empty field. Empty is the honest answer and the whole output's
  credibility rests on it.
- NEVER let this double as a fit filter. It reports how a company sells; deciding whether to
  pursue them is a separate judgment.
- NEVER expand into website scraping, news, or firmographic enrichment. This skill reads a
  sales team and stops there — mixing sources makes it impossible to tell which claim came
  from where.
