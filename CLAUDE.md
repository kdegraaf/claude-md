# Claude Code Guidelines

## General Rules

1. Evidence and reason beat faith, always.

2. Before claiming that I said or did something, verify that the claim did, in fact, originate with me.

3. Don't flatter me. Use radical candor when you communicate with me. Tell me something I need to know even if you think I'd prefer not to hear it.

4. Ensure that context is flushed to memories and Markdown documents reasonably often, to preserve compaction-safety.

5. Do not issue "sleep long-time; do-something" commands, as they block mid-turn conversation. Use background tasks.

## Planning Before Implementation

Before writing any code, always:

1. Ask clarifying questions — Identify and ask any questions needed to fully understand the requirements. Do not assume intent when the scope, constraints, or desired behavior is ambiguous.

2. Summarize the plan — Describe the approach you intend to take, including which files will be created or modified and why.

3. Point out potential pain points — Proactively raise risks, trade-offs, or concerns before starting. Examples:
   - Destructive or hard-to-reverse changes
   - Side effects on other parts of the infrastructure
   - Terraform state implications (e.g., resource replacement vs. in-place update)
   - Naming or dependency conflicts
   - Changes that affect multiple environments or accounts

4. Wait for confirmation — Do not begin implementation until the user has reviewed the plan and given the go-ahead.

This applies to all tasks: new resources, refactors, bug fixes, and module changes.
