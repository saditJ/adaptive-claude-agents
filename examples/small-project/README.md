# Example: Small Project (2 Agents)

**Project:** Simple todo app with a React frontend and a Node.js API

---

## After running /start, the Lead proposed:

```
Based on your answers, here's the team I recommend:

Agent 1 — UI Agent: owns /src/components, /src/pages
Agent 2 — API Agent: owns /api, /routes, /server.js

This is intentionally lean. The project is small enough that a DB Agent
isn't needed yet — the API agent can handle simple file-based or in-memory
storage. I'll suggest adding one if you introduce a real database.

Shall I proceed?
```

---

## AGENT SCOPE MAP (in CLAUDE.md after approval)

```
UI Agent    → /src/components, /src/pages
API Agent   → /api, /routes, /server.js
```

---

## Example Task Routing

**Task:** "Change the button color on the todo form"
→ Lead reads task → "button = UI" → delegates to UI Agent with `/src/components/TodoForm.jsx`
→ No file tree reading needed

**Task:** "The DELETE /api/todos/:id endpoint returns 500"
→ Lead reads error → "DELETE /api/todos = API Agent" → delegates with `/api/routes/todos.js`
→ No full project reading needed

---

## When It Grows

User later says: "I want to add a PostgreSQL database and user accounts"

Lead responds:
```
This requires two new agents:

ADD DB Agent: owns /models, /migrations, /db
ADD Auth Agent: owns /auth, /middleware/auth.js

Approve to expand the team? (2 agents → 4 agents)
```
