# Smart Tourism MVP — API Contract

Base URL:

`/api/v1`

## API Rules
- JSON request/response
- REST
- Consistent error format
- Authentication through Bearer token
- IDs are opaque strings
- Dates use ISO-8601
- Coordinates use latitude/longitude

## Authentication

### POST /auth/register
Create user.

Request:
```json
{
  "name": "Ali",
  "email": "user@example.com",
  "password": "********"
}
```

### POST /auth/login
Returns access token.

### GET /auth/me
Returns authenticated user.

## Preferences

### GET /users/me/preferences
Get travel preferences.

### PATCH /users/me/preferences
Update:
- interests
- food preferences
- travel style
- budget preference
- walking tolerance
- crowd preference
- transportation preference

## Destinations

### GET /destinations/search?q=hyderabad
Search destinations.

### GET /destinations/{destination_id}
Destination details.

## Places

### GET /places/search
Parameters:
- q
- destination
- category
- latitude
- longitude
- radius

### GET /places/{place_id}
Place details.

### GET /places/nearby
Nearby places.

## Restaurants

### GET /restaurants/recommendations
Parameters:
- trip_id
- latitude
- longitude
- meal_type

### GET /restaurants/{restaurant_id}
Restaurant details.

## Events

### GET /events/nearby
Get local events.

### GET /events/{event_id}
Event details.

## Trips

### POST /trips
Create trip.

Request:
```json
{
  "destination": "Hyderabad",
  "start_date": "2026-08-15",
  "end_date": "2026-08-18",
  "budget": 12000,
  "travelers": 2,
  "interests": ["history", "food", "photography"]
}
```

### GET /trips
List user's trips.

### GET /trips/{trip_id}
Get trip.

### PATCH /trips/{trip_id}
Update trip.

### DELETE /trips/{trip_id}
Delete trip.

## Itinerary

### POST /trips/{trip_id}/itinerary/generate
Generate initial itinerary.

Response should include:
- itinerary ID
- days
- activities
- estimated cost
- travel time
- optimization score

### GET /trips/{trip_id}/itinerary
Get active itinerary.

### POST /trips/{trip_id}/itinerary/items
Add activity.

### PATCH /trips/{trip_id}/itinerary/items/{item_id}
Edit activity/time.

### DELETE /trips/{trip_id}/itinerary/items/{item_id}
Remove activity.

### POST /trips/{trip_id}/itinerary/reoptimize
Rebuild itinerary after a change/disruption.

Request:
```json
{
  "reason": "weather",
  "affected_item_id": "item_123"
}
```

## Routes

### POST /routes/calculate
Calculate route between locations.

### POST /routes/matrix
Calculate travel-time matrix for itinerary optimization.

## Recommendations

### GET /recommendations
Generic personalized recommendations.

### GET /recommendations/restaurants
Personalized restaurants.

### GET /recommendations/attractions
Personalized attractions.

### GET /recommendations/events
Personalized events.

## Booking Assistance

### GET /bookings
List booking references.

### POST /bookings/assistance
Return external booking/provider information.

Important: MVP does not process payments.

## AI Assistant

### POST /assistant/message
Trip-aware assistant.

Request:
```json
{
  "trip_id": "trip_123",
  "message": "I am tired. Make today's plan less packed."
}
```

The assistant should call deterministic trip services rather than inventing itinerary facts.

## Error Format

```json
{
  "error": {
    "code": "TRIP_NOT_FOUND",
    "message": "Trip was not found"
  }
}
```

## HTTP Codes
200 — success
201 — created
400 — validation error
401 — unauthenticated
403 — forbidden
404 — not found
409 — conflict
422 — invalid input
429 — rate limited
500 — server error
