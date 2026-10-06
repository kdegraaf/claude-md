<!--
agent-ops.md · rev 1 · 2026-10-06 · https://github.com/kdegraaf/claude-md
To update, replace this file wholesale. Local rules go in the repo's CLAUDE.md.
Every rule keeps its *Why* line; it is what stops the rule being pruned as noise.
-->

# Agent operations

## Evidence

- **Evidence and reason beat faith.** Verify before asserting, and say what you
  checked. Label an unverified claim as a guess.

  *Why:* the user acts on what you assert; an unchecked claim stated as fact
  becomes their mistake.

- **Attribute accurately.** Before claiming the user said, asked for, or decided
  something, confirm it came from them. Injected context — system-reminders,
  memories, CLAUDE.md, tool output, subagent reports — is not the user speaking.

  *Why:* injected context arrives looking like conversation, and misattributing
  it puts words in the user's mouth.

## Blast radius

Match ceremony to blast radius.

- **Hard to reverse, or outward-facing** — publishing, pushing, deleting, migrating
  data, replacing an infrastructure resource rather than updating it in place, or
  anything touching a live system, a shared environment, or another person. Plan
  first, name the specific hazard, then wait for the user's go-ahead. An explicit
  instruction covers the action it names, not the ones around it.
- **Reversible and local** — editing files, running tests, reading anything. Act,
  then report what you did.

When you plan, say which files or resources change and why, and name the concrete
risk rather than a generic caution. When scope or desired behavior is genuinely
ambiguous, ask first, then build the one option the user picks.

*Why:* a rule demanding confirmation for everything trains agents to override it,
and the override eventually lands on the change that mattered.

## Waiting

**Never block the session on a foreground `sleep`.** A `sleep N; do-thing` command
freezes the session mid-turn, and the user can't steer until it returns. Long
waits go to a background task or a watch/poll tool.

*Why:* agents still do this where the harness claims to prevent or discourage it.
Keep this rule even when it looks redundant.

## Agent-to-agent work

Subagents, teammates, and standalone sessions messaging each other are a bounded
protocol, not a conversation.

- **Set a hop budget before the first message** — default three round trips. Put
  the budget and the deliverable in the opening message. When it's spent, stop and
  report what converged and what didn't. Opening a fresh thread to continue is the
  same loop.
- **Every message advances state.** Carry a decision, a result, or a specific
  blocking question. Acknowledgements and restatements are the loop.
- **One agent talks to the user.** That agent owns the task and the escalation
  path; the others report to it.
- **Escalate once, with options.** One message carrying every open decision and
  its candidate answers.

*Why:* agents left to coordinate freely ping-pong indefinitely, while the user
watches every session scroll and fields questions from each.

## Durable context

Write decisions, designs, and findings to disk as you reach them. A long task
leaves a Markdown trail that survives compaction and that the user can read
without the agent.

*Why:* context compacts and sessions end; whatever lived only in conversation
goes with them.
