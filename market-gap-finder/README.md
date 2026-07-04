# Market Gap Finder

A simple, prompt-driven workflow for finding small, overlooked, profitable niches that big companies ignore — and validating them cheaply before you invest real time or money.

This repo isn't software. It's a set of prompts organized so **Claude Code** can run the whole discover → filter → validate workflow for you and save the results to files. You don't need to write any code.

## What it does

Three stages:

1. **Discover** — scans across all sectors for niches too small, unglamorous, or fragmented for large companies to bother with, but still profitable.
2. **Filter** — narrows results to only what fits *your* situation (budget, time, skills, location, hard constraints).
3. **Validate** — takes your top 3 picks and builds a cheap, fast plan to prove real demand exists before you commit.

## How to use it with Claude Code

1. Open Claude Code in this folder.
2. Say: **"Read CLAUDE.md and run the discovery stage."**
3. Fill in the 3 blanks it asks for (budget, hours/week, income goal).
4. Review the ranked results it saves to `results/`.
5. Pick your top 3, then say: **"Run the validation stage on these three: [names]."**

That's it. Claude Code does the research, ranking, and writing. You make the decisions.

## Files

- `CLAUDE.md` — instructions Claude Code reads to run the workflow.
- `prompts/01-discover.md` — the discovery prompt.
- `prompts/02-filters.md` — your personal filters (already pre-filled).
- `prompts/03-validate.md` — the validation prompt.
- `results/` — where outputs get saved.

## Important honest note

No AI can literally scan every live market in real time. It works from what it already knows plus web access. Treat every result as a smart, structured **shortlist to validate** — not a guaranteed money map. The validation stage exists precisely because paper ideas are cheap and real demand is the only thing that counts.
