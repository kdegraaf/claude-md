# claude-md

Rules for Claude Code that I've built up from watching agents go wrong. Two files:

| File | What it is | Share it? |
|---|---|---|
| [`agent-ops.md`](agent-ops.md) | How an agent verifies, acts, and coordinates with other agents. Each rule carries the reason it exists. | Yes. This is the part meant for others. |
| [`personal.md`](personal.md) | How I like to be talked to. | No. It's taste. |

Claude Code combines every `CLAUDE.md` it finds instead of letting one override
another. Your user-scope file, `~/.claude/CLAUDE.md`, loads in every project, and
each repo's own `CLAUDE.md` loads on top of it. So general rules live once, at user
scope, and each repo carries only what's specific to it.

## Install on a machine

1. In any Claude Code session, run `/context`. If something managed already
   appears under **Memory files**, read it first. It loads before your rules and
   can't be excluded, and where the two contradict, Claude may follow either.
2. Clone and install:
   ```
   git clone https://github.com/kdegraaf/claude-md.git ~/code/claude-md && ~/code/claude-md/install.sh
   ```
   `install.sh` concatenates both files into `~/.claude/CLAUDE.md`, or into
   `$CLAUDE_CONFIG_DIR/CLAUDE.md` when that variable is set. It writes a real file
   rather than a symlink, because Cowork skips a symlinked `~/.claude/CLAUDE.md`.
   It shows what it would install and asks first; without a terminal, pass `--yes`.
3. Start a fresh session and check that `/context` lists `~/.claude/CLAUDE.md`.

## Change the rules

1. Edit `personal.md` or `agent-ops.md` in this repo, never the installed copy. A
   new rule goes in `agent-ops.md` unless it's pure taste. Give it a one-line
   *Why*, and leave out hostnames, IPs, employer names, and people's names: this
   repo is public.
2. If you changed `agent-ops.md`, bump the rev in its header comment. Commit and push.
3. On each machine:
   1. `git pull`. If its file list includes `install.sh`, read that change before
      running it: `git diff HEAD@{1} -- install.sh`. A changed installer could skip
      the next step's question.
   2. `./install.sh`. It shows what would change in your installed rules and asks
      before installing. Read it: these rules steer Claude Code on every machine, so a
      bad push reaches all of them.

If the install refuses, something has written to the installed copy since the last
install: asking Claude to "add this to CLAUDE.md", for example, or editing through
`/memory`. Lines marked `-` in the diff it prints exist only in the installed copy.
Move them into the source files here and rerun, or pass `--force` to back up the
installed copy and overwrite it.

## New repos

- Don't copy these rules in. User scope already loads them everywhere.
- A repo's `CLAUDE.md` holds only what can't be looked up elsewhere: unwritten
  conventions, gotchas, and the reasons behind choices. `/init` can draft a first
  version.
- Personal notes about one project go in `CLAUDE.local.md`, added to `.gitignore`.
- In a large repo, a `CLAUDE.md` in a subdirectory loads only when Claude reads
  files in that subdirectory, so the root file can stay small.

## Repos that already contain copied rules

Every version of these rules mentions radical candor, so this finds the copies:

```
grep -rli --include=CLAUDE.md 'radical candor' <your code directory>
```

- **A file that's nothing but copied rules:** delete it. Until you can, list its
  absolute path under `claudeMdExcludes` in `~/.claude/settings.json`. Exclusions
  match exact paths, so moving the repo makes its copy load again. Delete copies
  before moving repos, and drop the exclusions once the copies are gone.
- **Copied rules followed by project content:** delete the copied part and keep
  the project section; excluding the file would drop the project content too.
  Until then, an older copy can contradict the installed rules, and Claude may
  follow either.

## Share `agent-ops.md` with collaborators

Copy it into the repo as `.claude/rules/agent-ops.md`. Claude Code loads every
file in `.claude/rules/` alongside the project's `CLAUDE.md`.

- To update, replace the file wholesale. The rev in its header comment tells you
  which version you have.
- Put the repo's own rules in its `CLAUDE.md`, not in this file. That keeps every
  update a copy instead of a merge.
- If you've also installed these rules at user scope, exclude that path in your
  own `~/.claude/settings.json` so the rules don't load twice.
