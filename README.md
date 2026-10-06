# claude-md

Rules for Claude Code that I've built up from watching agents go wrong. Two files:

| File | What it is | Share it? |
|---|---|---|
| [`agent-ops.md`](agent-ops.md) | How an agent verifies, acts, and coordinates with other agents. Each rule carries the reason it exists. | Yes. This is the part meant for others. |
| [`personal.md`](personal.md) | How I like to be talked to. | No. It's taste. |

## Use `agent-ops.md` in a repo

Copy it to `.claude/rules/agent-ops.md`. Claude Code loads every file in
`.claude/rules/` alongside the project's `CLAUDE.md`.

- To update, replace the file wholesale. The rev in its header comment tells you
  which version you have.
- Put your repo's own rules in its `CLAUDE.md`, not in this file. That keeps every
  update a copy instead of a merge.

## Install for yourself

Run `./install.sh`. It concatenates both files into `~/.claude/CLAUDE.md`, which
Claude Code loads in every project.

If the installed copy was edited since the last install (say, through `/memory`),
the script refuses and shows the diff. Fold those edits back into the repo and
rerun, or pass `--force` to back up the installed copy and overwrite it.
