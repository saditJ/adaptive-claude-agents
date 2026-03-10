# /rollback $ARGUMENTS — Identify and revert recent agent changes

Arguments: optional — agent name, file name, or number of tasks to roll back.
Examples:
  /rollback                        ← show last 5 changes, pick what to revert
  /rollback ui-agent               ← show last 5 changes by ui-agent
  /rollback 3                      ← show last 3 changes across all agents
  /rollback src/components/Graph   ← show all changes to that file

## Step 1: Read TEAM_LOG.md
Filter entries based on the arguments provided.
If no arguments: show the last 5 entries.

## Step 2: Present what can be rolled back
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECENT CHANGES — available to rollback
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[1] 2026-03-07 | ui-agent    | /src/components/Graph.jsx — resized chart
[2] 2026-03-07 | api-agent   | /api/routes/users.js     — fixed DELETE 500
[3] 2026-03-06 | db-agent    | /migrations/add_roles    — added roles table
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Which change(s) do you want to roll back? (Enter numbers, e.g. "1" or "1,3")
Or type "none" to cancel.
```

## Step 3: Wait for user selection

## Step 4: For each selected change
1. Read the current state of the file
2. Present what the rollback would do:
```
Rolling back [1]: /src/components/Graph.jsx
Agent: ui-agent | Date: 2026-03-07
Action taken: resized chart dimensions

I will revert this file to its state before this change.
Note: This uses git — run `git diff` to preview before confirming.

Suggested git command:
  git log --oneline -- src/components/Graph.jsx
  git checkout [commit-hash] -- src/components/Graph.jsx

Shall I read the file and attempt to revert the specific change,
or would you prefer to use git directly?
```

## Step 5: On approval to revert
1. Read the file
2. Attempt to identify and revert the specific change described in the log
3. If the change is too complex to revert safely, say so and provide the git command instead
4. Log in TEAM_LOG.md:
   LEAD | [file] — ROLLBACK of [agent] change from [date]

## Important
Always prefer git for rollbacks when available.
Never attempt to revert a migration or schema change without explicit user confirmation.
Never rollback auth or security changes silently — always flag the implications.
