# /add-agent $ARGUMENTS — Add a new specialist agent to the team

Arguments: describe the agent you want.
Examples:
  /add-agent payments agent for /src/payments and /api/billing
  /add-agent email agent for /src/emails and /services/mailer.js
  /add-agent websocket agent for /src/realtime and /server/ws.js

## Step 1: Parse the arguments
Extract:
- Desired role/name
- File paths mentioned
- Domain (what kind of work does this agent do)

## Step 2: Check for conflicts
Read JSON scope map from CLAUDE.md.
Check if any proposed file paths overlap with existing agents.
If overlap exists:
```
I found a conflict:
[proposed file] is currently owned by [existing agent].

Options:
1. Reassign that path to the new agent
2. Keep it with [existing agent] and adjust the new agent's scope
3. Split the file's responsibilities

How would you like to handle this?
```
Wait for resolution before proceeding.

## Step 3: Confirm scope with user
```
New agent proposal:

Name: [agent-name]
Role: [what it does]
Owns: [file paths]
Does not touch: [other agents' domains]

Confirm?
```

## Step 4: On approval
1. Copy _template.md structure
2. Fill in all placeholders with real values
3. Save as .claude/agents/[agent-name].md
4. Update JSON scope map in CLAUDE.md — add new agent entry
5. Update last_updated timestamp
6. Log: LEAD | CLAUDE.md — added [agent-name] owning [paths]
7. Confirm to user: "Agent added. Use /status to see updated team."
