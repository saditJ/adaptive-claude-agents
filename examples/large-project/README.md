# Example: Large Project (6 Agents — grew over time)

**Project:** SaaS dashboard with auth, payments, real-time data, and multi-tenant roles

---

## How the Team Grew

### Week 1 — Started with 2 agents
```
UI Agent    → /src/components, /src/pages
API Agent   → /api, /routes
```

### Week 2 — Added DB after introducing Postgres
```
Lead suggested: "You've added /models and /migrations. 
I recommend a DB Agent to own the data layer."

DB Agent    → /models, /migrations, /prisma
```

### Week 3 — Added Auth after introducing login
```
Lead suggested: "Auth logic is growing. The API Agent 
is handling too many concerns. I recommend splitting out an Auth Agent."

Auth Agent  → /auth, /middleware/auth.js, /config/session.js
```

### Week 4 — Added Styles after design system introduced
```
Lead suggested: "You've added a /styles folder and Tailwind config. 
A Styles Agent would keep this separate from component logic."

Styles Agent → /styles, tailwind.config.js, /tokens
```

### Week 5 — Added Payments for Stripe integration
```
User ran /add-agent "payments agent for /src/payments and /api/billing"

Payments Agent → /src/payments, /api/billing, /webhooks/stripe.js
```

---

## Final AGENT SCOPE MAP

```
UI Agent       → /src/components, /src/pages, /src/layouts
API Agent      → /api/routes, /controllers, /middleware (non-auth)
DB Agent       → /models, /migrations, /prisma, /seeds
Auth Agent     → /auth, /middleware/auth.js, /config/session.js
Styles Agent   → /styles, tailwind.config.js, /tokens
Payments Agent → /src/payments, /api/billing, /webhooks/stripe.js
```

---

## Example Complex Task Routing

**Task:** "Users with 'viewer' role can see the billing page but shouldn't be able to cancel"

Lead breaks this into:
1. Auth Agent → update role permissions config to define viewer access
2. UI Agent → conditionally render cancel button based on role
3. API Agent → add role check middleware to the cancel endpoint

Lead coordinates the order: Auth first → API second → UI last
Each agent reads only its own files.
