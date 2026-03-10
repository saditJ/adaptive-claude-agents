# adaptive-claude-agents

> A dynamic, approval-gated multi-agent framework for Claude Code that grows with your project.

Most agent templates are static — you define your team upfront and it never changes.
This framework is different. It starts lean, scans your project intelligently, evolves as you build, and always asks before expanding.

---

## What Makes This Different

| Other Frameworks | adaptive-claude-agents |
|-----------------|----------------------|
| Fixed team defined upfront | Starts lean, grows dynamically |
| You decide team size | Lead scans project + interviews you |
| Agents read whatever they want | Each agent owns specific files only |
| No conflict detection | Shared files always go through Lead |
| No session memory | TEAM_LOG.md persists full activity history |
| Static config | JSON scope map updates automatically |
| No approval gates | Every change requires your sign-off |
| No undo | /rollback reads TEAM_LOG and reverts |
| No preview | /dry-run shows plan before executing |
| Single-project only | Full monorepo support |

---

## How It Works

**1. Start with an idea (or an existing project)**
Run `/start` — the Lead scans your project structure first, detects monorepos, infers what it can, then asks only what it can't figure out on its own.

**2. Lead proposes a minimal team**
Only the agents actually needed. A simple app gets 2 agents. A SaaS platform gets 5. No over-engineering from day one.

**3. You approve — nothing happens without your sign-off**
The JSON scope map is updated. The team is live. Work begins.

**4. Each agent owns its files**
UI Agent reads components. API Agent reads routes. DevOps Agent handles CI/CD. They never cross domains without reason.

**5. Project grows — Lead notices and suggests expansions**
New `/payments` folder appeared? Lead proposes a Payments Agent. One agent handling too much? Lead suggests splitting. Always approval-gated.

**6. Everything is logged — and reversible**
Every task logged in `TEAM_LOG.md`. Use `/rollback` to undo. Use `/dry-run` to preview before executing. Full control at every step.

---

## Quick Start

```bash
# Add to any project
git clone https://github.com/YOUR_USERNAME/adaptive-claude-agents .ada-tmp
cp -r .ada-tmp/.claude ./
cp .ada-tmp/CLAUDE.md ./
cp .ada-tmp/TEAM_LOG.md ./
rm -rf .ada-tmp

# Start Claude Code
claude

# Run setup — Lead scans your project and proposes the right team
/start
```

---

## Commands (v2)

| Command | What it does |
|---------|-------------|
| `/start` | Scans project → detects monorepo → proposes minimal team → approval-gated |
| `/status` | Full team overview: agents, coverage, gaps, recent activity |
| `/expand` | Detects growth → suggests new agents → approval-gated |
| `/add-agent [desc]` | Add a specific agent with defined file ownership |
| `/remove-agent [name]` | Safely retire an agent, reassign its files |
| `/rollback [optional]` | Identify and revert recent changes using TEAM_LOG |
| `/dry-run [task]` | Preview routing + approach before executing anything |
| `/log` | View full TEAM_LOG activity history with stats |

---

## Pre-Built Agents

| Agent | Triggered by | Owns |
|-------|-------------|------|
| `ui-agent` | Components, pages, visual bugs, graphs | `/src/components`, `/src/pages` |
| `api-agent` | Routes, endpoints, 500 errors | `/api`, `/routes`, `/controllers` |
| `db-agent` | Schema, migrations, SQL errors | `/models`, `/migrations`, `/prisma` |
| `auth-agent` | Login, sessions, JWT, roles | `/auth`, `/middleware/auth` |
| `styles-agent` | CSS, Tailwind, layout, spacing | `/styles`, `tailwind.config` |
| `qa-agent` | Tests, coverage, specs | `/tests`, `/__tests__`, `/e2e` |
| `devops-agent` | Docker, CI/CD, builds, deploy | `/.github/workflows`, `/infra` |

Need a custom agent? Use `/add-agent` or copy `_template.md` — it now includes conditional sections for API, DB, security, and infra rules.

---

## Shared Files Protocol

Some files belong to no single agent. Lead coordinates all edits:

```
package.json · tsconfig.json · .env · .gitignore
docker-compose.yml · Dockerfile · turbo.json · README.md
```

When any agent needs to touch these, it proposes the change to Lead. Lead checks for conflicts, then applies it. Always logged.

---

## Session Memory — TEAM_LOG.md

Every completed task is logged:
```
2026-03-07 | ui-agent     | /src/components/Graph.jsx    — resized chart dimensions
2026-03-07 | api-agent    | /api/routes/users.js         — fixed 500 on DELETE /users/:id
2026-03-07 | LEAD         | package.json                 — added recharts dependency
2026-03-07 | LEAD         | CLAUDE.md — ROLLBACK of ui-agent change from 2026-03-06
```

On session start, Lead reads the last 20 entries to restore context automatically.

Should you commit TEAM_LOG.md? See [docs/gitignore-guide.md](./docs/gitignore-guide.md).

---

## Monorepo Support

The framework auto-detects monorepos (turbo, nx, pnpm workspaces, lerna).
When detected, `/start` asks whether you want:

- **Option A** — One team with prefixed ownership (simpler)
- **Option B** — Separate CLAUDE.md per app (more powerful)

See [docs/monorepo.md](./docs/monorepo.md) for full setup guide.

---

## How Tasks Are Routed

**Clear task (zero file reading):**
```
"Change the graph dimensions"
→ Lead: graph = UI concern → UI Agent + exact file path → done
```

**Screenshot error (signal extraction only):**
```
[screenshot of 500 on /api/users]
→ Lead: extracts "/api/users" → API Agent + route file → done
```

**Ambiguous task (minimal targeted reading):**
```
"The login button doesn't work"
→ Lead: reads file tree only
→ Auth Agent for logic first, UI Agent for button state after
→ Sequenced, no file conflicts
```

**Before a risky task (dry run):**
```
/dry-run refactor the entire auth middleware
→ Lead shows: which agent, which files, risk level: HIGH
→ You decide whether to proceed, adjust, or cancel
```

**Oops, that went wrong:**
```
/rollback
→ Lead shows last 5 changes with agent + file + description
→ You pick what to revert → Lead uses git or direct revert
```

---

## Project Structure

```
your-project/
├── CLAUDE.md                        ← Lead brain + JSON scope map (auto-updated)
├── TEAM_LOG.md                      ← Full activity log (auto-updated)
├── docs/
│   ├── monorepo.md                  ← Monorepo setup guide
│   └── gitignore-guide.md           ← Should you commit TEAM_LOG?
└── .claude/
    ├── agents/
    │   ├── lead.md                  ← Orchestrator
    │   ├── ui-agent.md
    │   ├── api-agent.md
    │   ├── db-agent.md
    │   ├── auth-agent.md
    │   ├── styles-agent.md
    │   ├── qa-agent.md
    │   ├── devops-agent.md
    │   └── _template.md             ← Smart template with conditional sections
    └── commands/
        ├── start.md                 ← /start
        ├── status.md                ← /status
        ├── expand.md                ← /expand
        ├── add-agent.md             ← /add-agent
        ├── remove-agent.md          ← /remove-agent (new)
        ├── rollback.md              ← /rollback (new)
        ├── dry-run.md               ← /dry-run (new)
        └── log.md                   ← /log
```

---

## Examples

- [Small Project — 2 agents that grow to 4](./examples/small-project/README.md)
- [Large Project — 6 agents built over 5 weeks](./examples/large-project/README.md)

---

## Changelog

### v2.0
- `/remove-agent` — safely retire agents and reassign file ownership
- `/rollback` — revert recent changes using TEAM_LOG history
- `/dry-run` — preview routing and approach before executing
- `/log` — full activity history with stats
- Monorepo support — auto-detection, Option A/B setup
- Smart `_template.md` — conditional sections for API, DB, security, infra
- JSON scope map updated to v2 with monorepo fields
- `docs/` folder with gitignore guide and monorepo setup

### v1.0
- Initial release: adaptive team setup, approval gates, session memory, 7 pre-built agents

---

## Philosophy

> You don't hire a 10-person team to build a landing page.
> You start with 2, grow when needed, and always stay in control.

This framework applies that same logic to AI agent teams — with the added benefit that your team remembers everything, never steps on its own toes, asks before it grows, and lets you undo anything it does.

---

## Contributing

PRs welcome for:
- New pre-built agent templates (payments, email, websockets, analytics, etc.)
- Better routing heuristics in CLAUDE.md
- Real-world examples of teams that grew organically
- Monorepo examples (Turborepo, Nx, etc.)

---

## License

MIT
