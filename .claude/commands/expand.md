# /expand — Detect growth and suggest team expansion

## Step 1: Read current state
1. Read the JSON scope map from CLAUDE.md
2. Read TEAM_LOG.md — understand what's been built recently
3. Read the file tree (max 2 levels deep)

## Step 2: Find the gaps
Compare the file tree against the current scope map.
Look for:
- Folders/files not covered by any agent
- Agents that own too many unrelated concerns
- New patterns that suggest a new domain emerged
  (e.g. /payments appeared → Payments Agent needed)
  (e.g. /emails appeared → Email Agent needed)
  (e.g. /webhooks appeared → could go to API or needs its own agent)

## Step 3: Check TEAM_LOG.md for overload signals
If one agent has 5+ recent log entries and others have 1-2,
that agent is overloaded and may need splitting.

## Step 4: Present findings
```
Current team: [list agents and their coverage]

I found the following gaps or growth signals:

GAP: [folder/area] is not covered by any agent
→ Recommend: ADD [Agent Name] owning [files]
→ Reason: [one sentence]

OVERLOAD: [agent] is handling too many concerns
→ Recommend: SPLIT into [Agent A] and [Agent B]
→ Agent A owns: [files]
→ Agent B owns: [files]
→ Reason: [one sentence]

No changes needed if the current team covers everything well.
```

## Step 5: Wait for approval

## Step 6: On approval
1. Create new agent file(s) using _template.md as base
2. Update JSON scope map in CLAUDE.md
3. Update last_updated timestamp
4. Log in TEAM_LOG.md: LEAD | CLAUDE.md — team expanded, added [agents]
