# .gitignore Recommendations for adaptive-claude-agents

## The Key Decision: Should TEAM_LOG.md be committed?

### Commit TEAM_LOG.md if:
- You work in a team and want shared activity history
- You want to track what AI agents changed over time for accountability
- You're building in public and want transparency

### Gitignore TEAM_LOG.md if:
- This is a solo project and the log is just for your session context
- You don't want AI activity mixed into your git history
- You prefer clean commits that only contain real code changes

---

## Recommended .gitignore additions

Add one of these blocks to your project's `.gitignore`:

### Option A — Ignore TEAM_LOG (solo / clean history)
```gitignore
# adaptive-claude-agents — session log (personal use, not committed)
TEAM_LOG.md
```

### Option B — Commit TEAM_LOG (team / accountability)
```gitignore
# adaptive-claude-agents — commit everything including activity log
# (no additions needed)
```

### Always ignore (regardless of option)
```gitignore
# adaptive-claude-agents — never commit these
.claude/agents/.session-lock
.claude/.tmp/
```

---

## What Should Always Be Committed

```
✅ CLAUDE.md                    ← The team constitution, always commit
✅ .claude/agents/*.md          ← Agent definitions, always commit
✅ .claude/commands/*.md        ← Commands, always commit
```

## What Should Never Be Committed

```
❌ .env                         ← Never (already in your .gitignore)
❌ .claude/.tmp/                ← Temp files if any are created
```

---

## Quick Setup

To use Option A (ignore TEAM_LOG), run:
```bash
echo "\n# adaptive-claude-agents\nTEAM_LOG.md" >> .gitignore
```

To use Option B (commit TEAM_LOG), no action needed.
