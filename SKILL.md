---
name: grill-me
description: Interview the user relentlessly about a plan or design until reaching shared understanding. Use when user wants to stress-test a plan, challenge a design, or says things like "grill me", "poke holes in this", "what am I missing", "tear this apart", or "challenge this".
---

Interview me relentlessly about this plan until we reach a shared understanding. Your job is to walk down each branch of the decision tree, resolving dependencies between decisions one by one.

## How to interview

**Start with the most foundational decision** — the one that constrains the most downstream choices. Infrastructure before features. Purpose before structure. "Where does this run?" before "how does it handle errors?"

**Ask exactly one question per turn using the AskUserQuestion tool.** This is mandatory — don't put your question in the text response. Use AskUserQuestion so the user gets a clean UI with selectable options. Structure it like this:

- Your recommended answer goes as the first option with "(Recommended)" in the label
- Include 2-3 alternative approaches as other options
- The user can always select "Other" to go a different direction
- Use the `description` field on each option to explain tradeoffs

Before calling AskUserQuestion, briefly explain (in your text response) why this decision matters and what it constrains downstream. Keep this context short — a few sentences, not a report. Then call the tool. Nothing after it.

**Do not list, number, or preview remaining questions — not before the tool call, not after it.** No "topics I'll cover next," no "gaps I'm tracking," no roadmap. The whole point of one-at-a-time is that the user focuses on THIS question without seeing what's coming. Listing future questions lets them skip ahead mentally instead of thinking deeply about the current one. One sentence to signal the next topic is fine: "Once we resolve this, I'll move to X."

## When the user says "I don't know" or picks "Other" with uncertainty

That's valuable signal, not a dead end. Flag it as an open risk, propose 2-3 concrete options with tradeoffs via AskUserQuestion, and recommend one. Include a "Park it — come back later" option so they can defer and revisit after other decisions give more context.

## Tracking progress

Keep a running mental tally of resolved decisions. When a branch is resolved, briefly acknowledge the decision and move to the next branch. When all major branches are resolved, present a summary of every decision made — this is the output the user walks away with.

## Using the codebase

If a question can be answered by exploring the codebase, explore it yourself instead of asking. Don't make the user answer questions you can look up.
