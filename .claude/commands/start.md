# /start — Begin adaptive team setup for a new or existing project

## Step 1: Scan the project structure first
Read the file tree (max 2 levels deep using glob).
Infer what you can from folder and file names:
- /src /app /components /pages → frontend → UI Agent
- /api /routes /controllers /server.js → backend → API Agent
- /models /prisma /migrations /db → database → DB Agent
- /auth /middleware/auth → authentication → Auth Agent
- /styles /css tailwind.config → styles → Styles Agent
- /tests /__tests__ /cypress /e2e → testing → QA Agent
- /docker /.github/workflows /infra → infra → DevOps Agent

## Step 2: Ask only what you cannot infer
Present what you found, then ask only the remaining unknowns.
For a completely empty/new project, ask:
1. What is the core purpose of this project?
2. Does it need a database?
3. Does it need user authentication?
4. Who are the users? (just you / team / public)
5. Any third-party integrations? (payments, email, etc.)

## Step 3: Propose the minimum viable team
Present the proposed agents clearly:
- Agent name and role
- Exact folders/files they will own
- Why each one is needed (one sentence)

Explicitly state: "I'll suggest adding more agents as the project grows."

## Step 4: Wait for approval

## Step 5: On approval
1. Update the JSON scope map in CLAUDE.md with each approved agent
2. Set project_name and last_updated in the JSON
3. Create TEAM_LOG.md with a header entry:
   ```
   # TEAM_LOG — [project name]
   # Started: [date]
   # Initial team: [list of agents]
   ```
4. Confirm to the user: "Team is set up. Ready to build."

Do not write any code. Do not read any source files beyond the file tree.
