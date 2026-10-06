# claude-md

Source for the user-scope `~/.claude/CLAUDE.md`. This file covers only how to
maintain the repo; the rules themselves live in `personal.md` and `agent-ops.md`.

- `personal.md` holds taste, in first person. `agent-ops.md` holds transferable
  rules, in third person, and is the file shared with colleagues. A new rule goes
  in `agent-ops.md` unless it is purely preference.
- Every `agent-ops.md` rule keeps a one-line *Why*, written in general terms. The
  repo is public: no hostnames, IPs, employer names, or people's names.
- Bump the rev in `agent-ops.md`'s header comment on every content change.
- `install.sh` builds `~/.claude/CLAUDE.md`. Edit the sources here, never the
  installed copy.
