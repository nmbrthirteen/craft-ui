# Copy: the words are part of the interface

Microcopy is UI. A headline with an em dash and a "No X, no Y, just Z" subhead
undoes the polish in the pixels, because that phrasing is the clearest signal that a
model wrote the page and nobody edited it. Hold the words to the same bar as the
layout. This file has two parts: how the message is structured, then the line-level
rules.

## Messaging structure

### Hero anatomy

A hero is three things, in this order, and not much else:

1. **Headline.** The core value, stated specifically. Name the outcome the user gets
   or the concrete thing the product does. "Cron jobs you can actually see" works
   because it's specific; "The future of scheduling" doesn't.
2. **Subhead (optional, 1 to 2 sentences).** Adds the one detail the headline
   couldn't carry. Keep it short. If the left column of your hero is a wall of three
   or four lines of body text, cut it down: one idea above the fold, not a paragraph.
3. **One primary CTA.** An action plus what the user gets. "Mail me issue 15" and
   "Start free" beat "Sign up" and "Learn more" because they name the outcome, not the
   system action. A secondary action can sit beside it, quieter.

### The kicker above the headline

A small label or eyebrow above the H1 (the "PRINTED MONTHLY FROM WHAT YOU SAVED" or
"Runs your jobs from 5 regions" line) has become a templated reflex. Default to
cutting it.

**Why:** most kickers set a mood instead of saying anything, and a mood-kicker over
the title is one of the clearest "generated landing page" tells. Keep one only if it
carries specific information the headline can't, like a real category or a concrete
number, and even then question whether the headline should just carry it.

### Page flow

If the page goes past the hero, each section should make one point and move the reader
forward: who it's for and the problem, the solution and its benefit, how it works,
proof, then a final CTA. One idea per section. Don't repeat the hero three times in
different words.

Persuasion copywriting is its own discipline; for deep work on value propositions and
conversion, that's a separate skill. The rules here are the floor that keeps UI copy
from reading as filler.

## No em dashes or en dashes in UI copy

Don't use — or – in headlines, subheads, body copy, button labels, tooltips, or
empty states. Use a period, a comma, a colon, or split into two sentences.

**Why:** the em dash is the number-one tell of generated text. Readers clock it
instantly now, and one of them in a hero subhead makes the whole product feel
auto-written.

- Bad: "Watch a deploy go green below — then roll it back."
- Good: "Watch a deploy go green below, then roll it back."
- Bad: "Fast, reliable — and built for teams."
- Good: "Fast, reliable, and built for teams." or two sentences.

For numeric ranges in copy, use a plain hyphen ("5-10 minutes"), not an en dash.

## No negation-triad

Never build to a noun through stacked negations: "No X. No Y. Just Z." and all its
siblings ("Not X, not Y, just Z", "Not a tool, not an app, a companion"). Define the
thing directly, or let a concrete detail carry it.

**Why:** it's a rhythm that sounds profound and says little, and it's everywhere in
generated marketing copy. Ban it outright.

- Bad: "No streaks to protect, no badges to chase, just the next twenty-five minutes."
- Good: "One timer, twenty-five minutes, then you're done."

The softer cousin is the **"X, not Y" antithesis**: "Built for one wallet, not a
finance team." It positions by what the product isn't, which lands as a vibe instead
of a claim. Prefer stating what it is: "Built for one wallet" or "Tracks one wallet
in two taps."

## Cut hype clichés

Drop the words that every AI landing page reaches for. They add no information and
signal filler:

- "blazing fast", "lightning fast", "10x", "supercharge", "effortless",
  "seamless", "unleash", "revolutionary", "game-changing", "next-level".
- Empty dares like "before you finish reading this line".

**Why:** specifics beat adjectives. "Cold start under 40ms" is worth more than
"blazing fast" because it's a claim you can check.

## Sentence case, not Title Case

Use sentence case for headings, buttons, labels, and menu items ("Deploy a repo",
"Start a session"). Reserve Title Case for proper nouns and real product names.

**Why:** sentence case reads as human and current; Title Case On Everything reads as
a template.

## Be specific and concrete

Say the real number, the real outcome, the real noun. "1,284,946 deploys this week"
lands; "trusted by thousands" doesn't. Concrete copy also pairs with the typography
rules: any number that updates uses tabular figures (see [typography.md](./typography.md)).

## Quick gut check

- [ ] No em dashes or en dashes anywhere in the copy
- [ ] No "No X, no Y, just Z" negation buildup
- [ ] No hype clichés (blazing fast, seamless, 10x, supercharge)
- [ ] Sentence case on headings, buttons, and labels
- [ ] Claims are specific numbers or outcomes, not adjectives
