# /dry-run $ARGUMENTS — Preview how a task would be handled before executing

Arguments: the task you want to preview.
Examples:
  /dry-run fix the login button not submitting
  /dry-run add a dark mode toggle
  /dry-run the graph on the dashboard shows wrong data

## Purpose
Shows exactly what the Lead would do for a given task — which agent, which files,
what approach — without actually doing anything. Useful for:
- Learning how the framework routes tasks
- Verifying routing before a risky change
- Onboarding new contributors to the project

## Step 1: Read JSON scope map from CLAUDE.md
## Step 2: Read file tree (max 2 levels)
## Step 3: Analyze the task exactly as you would for real routing

## Step 4: Present the full plan
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DRY RUN — no changes will be made
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Task: "[the task]"

Routing decision:
→ Agent: [agent-name]
→ Reason: [why this agent]
→ Files it would read: [specific files]
→ Files it would likely edit: [specific files]

Approach:
[brief description of what the agent would actually do]

Shared files involved: [yes/no — which ones]
Cross-agent coordination needed: [yes/no — which agents, in what order]
Risk level: [low / medium / high — and why]

Confidence in routing: [high / medium / low]
[If low: explain what's ambiguous and what additional info would help]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Run this task for real? (yes / adjust / cancel)
```

## Step 5: On user response
- "yes" → execute the task as planned
- "adjust" → ask what to change about the plan
- "cancel" → stop, no changes made, no log entry
