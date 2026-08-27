# Matching an account to the right company profile

The single highest-cost error in this work. Every other mistake is visible in the output; this
one produces a complete, well-written, entirely wrong brief about a company your prospect has
never heard of.

## Why scoring alone fails

The obvious approach is a score: name overlap, headcount plausibility, does a profile exist,
does the location fit. It fails, and it fails confidently.

A real case: an account named *Cannon Packing* resolved to *Cannon Technologies Ltd*, an
electronics manufacturer. That candidate scored well — strong name overlap, plausible size, a
real profile, right country. It shares no domain and no industry with the target. Nothing in
the numbers caught it. Reading the profile's own description caught it in seconds.

**So the meaning check is not optional and cannot be replaced by a threshold.** Read what the
company says it does, and compare it to what you know the account does.

## The four failure modes, all observed

**Acquired-brand artifact.** The name resolves to a profile like `formerly-cannon-hygiene-uk`
— a hygiene services business carrying the brand through an acquisition. The name matches
because it is genuinely the same words. The company is not the same company.

**Same name, different industry.** Packaging resolving to electronics. Common with short or
generic trading names, and the more industrial the sector the more often it happens.

**Holding company, not the operating company.** Right corporate group, wrong entity. This one
is especially dangerous because the brief will not look wrong — it will describe a real,
related business. The people are simply not the people who sell your prospect's product.

**Same name, different country.** A US namesake of a UK company. Location filters help but do
not close it, because plenty of legitimate profiles list a global HQ.

## The confirmation procedure

1. **Domain first.** If the profile states a website and it matches the account's domain, that
   is near-decisive. Prefer this evidence over everything else.
2. **Read the self-description.** The industry, the about text, the specialties. Does this
   read like the business you are targeting? A human reading two sentences catches what a
   score cannot.
3. **Sanity-check the size.** A 12-person operation resolving to a 4,000-person profile is a
   holding company or a namesake.
4. **Check the geography** against where the account actually trades.
5. **When two candidates both survive, take neither.** Ambiguity is a finding. Mark it
   unresolved rather than picking the higher score.

## Generic names: do not resolve automatically

Names built from category words — *3PL*, *Packaging Ltd*, *Logistics Group* — will match a
long list of unrelated companies, all scoring well, none confirmable.

Detect them by asking whether the name is anything more than its industry plus a legal suffix.
If not, route to manual handling. Automated resolution on generic names does not produce a
wrong answer occasionally; it produces one most of the time.

## What to do when it cannot be confirmed

Mark the account as no profile found and move on.

This is the right outcome and it should not feel like failure. An account marked unresolved
costs a reader thirty seconds to check by hand. An account resolved to the wrong company costs
them a brief they believe, copy written from it, and an email that lands on a prospect
describing a business that is not theirs.

**Under-resolving is recoverable. Mis-resolving is not**, because nothing downstream can
detect it.
