# FORKED! Thanks, @amaezey!
## grill-hard

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill for stress-testing plans and designs.

### What it does

Asks you one question at a time about your plan, starting with the most foundational decisions. Each question uses the `AskUserQuestion` tool with a recommended answer and alternatives. You resolve one thing, then get the next. At the end you get a summary of every decision made.

Without the skill, Claude tends to ask long lists of questions, gets ahead of itself, and buries key decisions.

### Origin and attribution

Forked from [Matt Pocock's grill-me skill](https://github.com/mattpocock/skills), which is great and worth using as-is. This version tweaks it for my preferences: less meta-framing, more thoughtful questions grounded in the codebase, and a stricter interview style. I ran it through four rounds of structured evaluation (baseline comparisons, LLM-graded assertions, human review) to get there. The main changes:

- **AskUserQuestion as mandatory tool:** questions go through the structured tool rather than as text, which enforces one-at-a-time and the options format naturally
- **Explained reasoning over prohibitions:** "don't list future questions" failed repeatedly; explaining *why* (focused attention > comprehensive preview) made it stick across all test cases
- **Decision-tree strategy:** foundational decisions first, dependencies resolved in order, rather than ad-hoc questioning
- **"I don't know" handling:** uncertainty gets concrete options and a "park it" escape hatch, not a dead end
- **Codebase awareness:** looks things up instead of asking you questions it could answer itself


### Install

Copy `SKILL.md` to your Claude Code skills directory:

```
mkdir -p ~/.claude/skills/grill-hard
cp SKILL.md ~/.claude/skills/grill-hard/skill.md
```

Or clone and symlink:

```
git clone https://github.com/amaezey/grill-hard.git
mkdir -p ~/.claude/skills/grill-hard
ln -s "$(pwd)/grill-hard/SKILL.md" ~/.claude/skills/grill-hard/skill.md
```

### Usage

Just tell Claude to grill you:

- "grill me on this migration plan"
- "poke holes in this architecture"
- "what am I missing in this design"
- "tear this apart before I ship it"

### Licence

MIT
