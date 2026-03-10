# /status — Show current team health and project coverage

## Step 1: Read everything needed
1. Read JSON scope map from CLAUDE.md
2. Read last 30 lines of TEAM_LOG.md
3. Read file tree (max 2 levels)

## Step 2: Present a clear status report

Format:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PROJECT: [name]  |  LAST UPDATED: [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ACTIVE TEAM ([n] agents)
─────────────────────────
[agent-name]   → [owned paths]
[agent-name]   → [owned paths]
...

SHARED FILES (managed by Lead)
─────────────────────────────
[list shared files]

RECENT ACTIVITY (last 10 tasks)
────────────────────────────────
[last 10 TEAM_LOG entries]

COVERAGE GAPS
─────────────
[any folders not owned by any agent — or "None detected"]

OVERLAP RISKS  
─────────────
[any files claimable by 2+ agents — or "None detected"]

SUGGESTIONS
───────────
[any recommended actions — or "Team looks healthy"]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

This is read-only. No changes are made by this command.
