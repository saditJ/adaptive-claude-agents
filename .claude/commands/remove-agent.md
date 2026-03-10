# /remove-agent $ARGUMENTS — Safely retire an agent from the team

Arguments: the agent name to remove.
Examples:
  /remove-agent styles-agent
  /remove-agent payments-agent

## Step 1: Read current state
1. Read JSON scope map from CLAUDE.md
2. Check if the agent exists — if not, tell the user and stop
3. Read TEAM_LOG.md — how recently was this agent active?

## Step 2: Check for orphaned files
Compare the agent's owned files against the other agents' scope maps.
Find any files that would become unowned after removal.

## Step 3: Present a removal plan
```
Removing: [agent-name]
Currently owns: [list of files/folders]

⚠️  These files will be unowned after removal:
  [file/folder] — currently owned by [agent-name]
  [file/folder] — currently owned by [agent-name]

Options:
A) Reassign all files to [suggested agent] (most logical owner)
B) Reassign files individually:
   [file] → which agent should own this?
C) Leave unowned (Lead will handle tasks for these files directly)

Recent activity: [agent-name] last worked on [date] — [last log entry]

Confirm removal and choose an option?
```

## Step 4: Wait for approval and reassignment decision

## Step 5: On approval
1. Delete .claude/agents/[agent-name].md
2. Update JSON scope map in CLAUDE.md:
   - Remove the agent entry
   - Reassign files per user's choice
   - Update last_updated timestamp
3. Log in TEAM_LOG.md:
   LEAD | CLAUDE.md — removed [agent-name], files reassigned to [agent(s)]
4. Confirm: "Agent removed. Use /status to see updated team."
