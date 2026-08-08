# Smart Tourism MVP — Architecture

## Architecture Decision
Use a **modular monolith** for the hackathon.

Do NOT create microservices. With limited hackathon time, microservices add deployment, networking, debugging and integration overhead without improving the demo.

## High-Level Architecture

```text
React + TypeScript Frontend
          |
          v
      FastAPI API
          |
   +------+------+------------------+
   |             |                  |
 Auth          Trips          Intelligence
   |             |                  |
   |             |       +----------+----------+
   |             |       |          |          |
   |             | Recommendation Itinerary Optimization
   |             |
   +-------------+--------------------------+
                         |
                         v
                    MongoDB
                         |
                      Redis
                         |
              External API Adapters
             /          |          \
          Places       Routes      Events
```

## Frontend Modules
- Auth
- Onboarding
- Home
- Trip Planner
- Itinerary
- Map
- Restaurants
- Attractions
- Events
- Booking Assistance
- Profile

## Backend Modules
- auth
- users
- trips
- places
- restaurants
- attractions
- events
- itinerary
- recommendations
- optimization
- bookings
- notifications
- integrations

## Intelligence Pipeline

```text
User Requirements
      ↓
Candidate Places
      ↓
Filter Hard Constraints
      ↓
Score Candidates
      ↓
Build Daily Schedule
      ↓
Calculate Routes
      ↓
Validate Budget/Time
      ↓
Generate Itinerary
      ↓
Explain Recommendations
```

## Recommendation Score
Use a transparent weighted score rather than an opaque AI-only decision.

Example conceptual score:

preference_match
+ rating
+ proximity
+ budget_fit
+ category_diversity
+ availability

Hard constraints must eliminate invalid candidates before scoring.

## Dynamic Re-optimization

```text
Current Itinerary
      ↓
Detect disruption
      ↓
Remove invalid activity
      ↓
Find nearby alternatives
      ↓
Apply user preferences
      ↓
Validate time + route + budget
      ↓
Generate replacement plan
      ↓
User approves
      ↓
Create new itinerary version
```

## External Integration Rule
All external APIs must be accessed through adapters.

```text
Application
   ↓
Provider Interface
   ↓
Google/Other Provider
```

Never spread provider-specific API calls throughout business logic.

## Data Ownership
MongoDB = source of truth
Redis = cache/temporary state
External APIs = external reference data

## Security
- JWT authentication
- Password hashing
- Environment variables for secrets
- Input validation
- CORS restricted to frontend origin
- Rate limiting on expensive endpoints
- Never expose API keys to frontend unless the provider explicitly requires browser-side keys
