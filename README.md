# skills

The Claude Code skills I run on every PR — across AMAR, Funnlr, and three other companies.

Stolen, adapted, and built. All free.

Not vibe coding. Real engineering.

---

## The 5 Skills

A staged workflow, not a flat list. Each skill is a checkpoint between an idea and a merged PR.

| Stage | Skill | What it does | Source |
|-------|-------|--------------|--------|
| 1. Think  | `grill-me`         | Interrogates you relentlessly before you build. Surfaces every unresolved decision — product, technical, edge case, release. | Built here. Adapted from [Matt Pocock](https://github.com/mattpocock/skills). |
| 2. Plan   | Plan Mode          | Built into Claude Code. `Shift+Tab` twice. Reads the codebase, writes a spec to `plans/`, asks before edits. | [Anthropic](https://docs.anthropic.com/en/docs/claude-code) |
| 3. Build  | (Claude does this) | Once the plan is approved, Claude executes it. | — |
| 4. Refine | `simplify`         | Refactors what Claude just shipped. Strips guards you don't need, collapses verbosity, runs tests. | [pr-review-toolkit](https://github.com/anthropics/pr-review-toolkit) |
| 5. Review | `code-review`      | Staff-level review on your own PR before a human ever sees it. | [pr-review-toolkit](https://github.com/anthropics/pr-review-toolkit) |
| 6. Ship   | `vercel-security`  | Snyk-audited security skill. Catches hardcoded secrets, missing input validation, CVE-laden deps. Ship-gate before merge. | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) |

The numbering is a workflow, not a ranking — `grill-me` runs once per feature, `simplify` and `code-review` run on every PR, `vercel-security` runs before every merge.

---

## Install

### grill-me (built here)

```bash
# clone this repo into your project's .claude/skills/
git clone https://github.com/imaadmalikk/skills.git tmp-skills
mkdir -p .claude/skills
cp -r tmp-skills/skills/grill-me .claude/skills/
rm -rf tmp-skills
```

Or copy `skills/grill-me/SKILL.md` into your project's `.claude/skills/grill-me/SKILL.md` directly.

### Plan Mode

No install. Press `Shift+Tab` twice in Claude Code.

### simplify + code-review

These come bundled in the `pr-review-toolkit` plugin:

```bash
claude plugin add pr-review-toolkit
```

### vercel-security

```bash
npx skills add vercel-labs/agent-skills --skill security-audit -a claude-code
```

---

## How to Actually Use These

This is the loop I run on every meaningful PR:

```
Feature idea
  ↓
/grill-me  →  spec written to plans/[feature]-spec.md
  ↓
Plan Mode (Shift+Tab×2)  →  detailed plan in plans/[feature].md
  ↓
Claude builds it
  ↓
/simplify  →  shrink and clean
  ↓
/code-review  →  catch what I missed
  ↓
/security-audit  →  ship-gate
  ↓
PR opened, merged
```

Idea to merged PR, solo, in roughly 6–10 minutes for a feature of moderate scope. The skills do the deciding. I do the typing.

---

## Why grill-me Specifically

Most Claude Code failures happen *before* Claude writes any code. You give it a vague brief, it writes vague code, you're surprised when it doesn't ship.

`grill-me` flips it. Claude becomes the senior engineer who has seen things break in production, and you become the founder who has to defend every decision before a single line is written. By the time `grill-me` finishes, you have a spec a different engineer could pick up and ship without asking you a single follow-up question.

The original is by [Matt Pocock](https://www.aihero.dev/my-grill-me-skill-has-gone-viral) — credit where it's due. This version adds:

- **Explicit phases** — Intent, Product, Technical, Edge Cases, Release. No skipping.
- **Codebase-first** — explore before asking. Don't waste the user's time on questions a `git grep` would answer.
- **Final spec output** — saves to `plans/[feature]-spec.md` so the answers don't evaporate.
- **Founder-grade edge cases** — timezones, prayer times, rollback plans, comms. The stuff that breaks in week three.

---

## Credits

- [Matt Pocock](https://github.com/mattpocock/skills) — original `grill-me`, the philosophy of "real engineers, not vibe coders"
- [Anthropic](https://github.com/anthropics) — Claude Code, Plan Mode, the `pr-review-toolkit` plugin
- [Vercel Labs](https://github.com/vercel-labs/agent-skills) + [Snyk](https://snyk.io/blog/snyk-vercel-securing-agent-skill-ecosystem/) — the security-audit skill

---

## Video

Walkthrough of the entire workflow on a real Funnlr PR: [YouTube link — coming soon]

---

## Contributing

Issues and PRs welcome. If you've built a skill that fits this workflow, open a PR — I'll credit you in the next video if it ships in my daily rotation.

---

## Licence

MIT. Use, fork, adapt, sell. Just keep the credits intact.
