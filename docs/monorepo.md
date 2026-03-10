# Monorepo Support

If your project is a monorepo (multiple apps in one repo), the adaptive agent framework
supports sub-project scoping out of the box. Here's how to configure it.

---

## What Is a Monorepo?

A monorepo has multiple independent apps or packages sharing one git repository:

```
my-project/
├── apps/
│   ├── frontend/          ← React app
│   ├── backend/           ← Node API
│   └── mobile/            ← React Native
├── packages/
│   ├── shared-types/      ← Shared TypeScript types
│   └── ui-components/     ← Shared component library
└── package.json           ← Root workspace config
```

---

## How to Set Up for a Monorepo

### Option A: One team, sub-project prefixes (small monorepos)
Add sub-project prefix to file ownership in the JSON scope map:

```json
{
  "project_name": "my-monorepo",
  "monorepo": true,
  "apps": ["frontend", "backend", "mobile"],
  "agents": [
    {
      "name": "frontend-ui-agent",
      "owns": ["apps/frontend/src/components", "apps/frontend/src/pages"]
    },
    {
      "name": "backend-api-agent",
      "owns": ["apps/backend/api", "apps/backend/routes"]
    },
    {
      "name": "shared-agent",
      "owns": ["packages/shared-types", "packages/ui-components"]
    }
  ],
  "shared_files": [
    "package.json",
    "turbo.json",
    "pnpm-workspace.yaml",
    ".env",
    "tsconfig.base.json"
  ]
}
```

### Option B: CLAUDE.md per sub-project (large monorepos)
For large monorepos, place a separate CLAUDE.md in each app:

```
my-project/
├── CLAUDE.md              ← Root lead: routes to correct sub-project
├── apps/
│   ├── frontend/
│   │   └── CLAUDE.md      ← Frontend team lead
│   ├── backend/
│   │   └── CLAUDE.md      ← Backend team lead
```

The root CLAUDE.md acts as a **meta-lead** that routes tasks to the correct sub-project lead.

---

## Additional Shared Files for Monorepos

Add these to your shared_files list depending on your toolchain:

```json
"shared_files": [
  "turbo.json",
  "pnpm-workspace.yaml",
  "nx.json",
  "lerna.json",
  "tsconfig.base.json",
  ".npmrc",
  "vitest.workspace.ts"
]
```

---

## Routing in a Monorepo

When a task comes in, the Lead checks:
1. Which app does this affect? (frontend / backend / shared / all)
2. Which agent within that app owns the relevant files?
3. Does this change affect shared packages? → Shared Agent + coordinate with consuming agents

### Example
```
Task: "Fix the Button component spacing"
→ Exists in packages/ui-components → Shared Agent
→ But it affects apps/frontend display → Lead notifies Frontend UI Agent to verify after

Task: "The /api/orders endpoint returns wrong data"
→ apps/backend/routes/orders.js → Backend API Agent
→ No cross-app impact
```

---

## /start for Monorepos

When `/start` detects a monorepo structure (turbo.json, pnpm-workspace.yaml, nx.json, or
multiple package.json files in subdirectories), it will ask:

```
I detected a monorepo structure with these apps: [list]

How would you like to set up the team?
A) One team with prefixed ownership (simpler, good for small monorepos)
B) Separate CLAUDE.md per app (more powerful, good for large monorepos)
```
