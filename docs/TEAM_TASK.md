# Smart Tourism MVP — Team Task Plan

## Hackathon Constraint
Total available time: approximately 4 hours remaining.

Therefore:
**Do not work on everything. Build the demo path first.**

## Team Strategy

### Agent/Developer 1 — Backend Core
Priority:
1. FastAPI setup
2. Auth
3. Trip CRUD
4. Preferences
5. Itinerary endpoints
6. Recommendation service

Deliverable:
Working API + seed/demo data.

### Agent/Developer 2 — Frontend Core
Priority:
1. React setup
2. Login/onboarding
3. Trip planner
4. Trip dashboard
5. Itinerary timeline

Deliverable:
Complete main user flow.

### Agent/Developer 3 — Maps + Discovery
Priority:
1. Map integration
2. Place search
3. Restaurants
4. Attractions
5. Events
6. Route display

Deliverable:
Map + useful destination data.

### Agent/Developer 4 — AI + Integration + Polish
Priority:
1. AI assistant
2. Recommendation explanation
3. Re-optimization demo
4. API integration fixes
5. UI polish
6. Deployment/demo support

If only 1–2 people are available, combine these roles in this order:
Backend Core → Frontend Core → Maps → AI/Polish.

## Critical Rule
Every agent must commit to the same API contract.

Do not allow agents to invent different:
- endpoint names
- field names
- ID formats
- response shapes

## Git Branches

```text
main
dev
feature/backend
feature/frontend
feature/maps
feature/ai
```

Merge only tested work.

## P0 Acceptance Criteria

### Backend
- User can authenticate
- User can create trip
- User can save preferences
- Trip itinerary can be generated
- Itinerary can be updated

### Frontend
- User can enter trip information
- User can generate trip
- User can view timeline
- User can view map
- User can modify itinerary

### Intelligence
- Recommendations reflect preferences
- Budget is visible
- Travel time is visible
- Re-optimization works for at least one simulated disruption

## What Agents Must NOT Do
- Do not redesign architecture mid-build.
- Do not add microservices.
- Do not add Kubernetes.
- Do not build payment processing.
- Do not build native mobile app.
- Do not train a complex ML model.
- Do not replace the database.
- Do not spend more than 20 minutes polishing one component.
- Do not generate huge amounts of code without running it.

## Definition of Done
A task is done only when:
1. Code exists.
2. It runs.
3. API/UI path is tested.
4. It integrates with the rest of the application.
5. The agent reports exactly what changed.
