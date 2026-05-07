# GoHighLevel API Reference

Auth method: Private Integration Token (PIT)
Header: `Authorization: Bearer $GHL_PIT_TOKEN`
Base URL: `https://services.leadconnectorhq.com`
API version: `2021-07-28` (pass as header: `Version: 2021-07-28`)

Credentials: stored in `.env` as `GHL_PIT_TOKEN` and `GHL_LOCATION_ID`

---

## Common endpoints

### Contacts
- `GET /contacts/?locationId={id}` — list all contacts
- `GET /contacts/{contactId}` — get single contact
- `POST /contacts/` — create contact
- `PUT /contacts/{contactId}` — update contact
- `DELETE /contacts/{contactId}` — delete contact

### Opportunities (pipeline/deals)
- `GET /opportunities/search?location_id={id}` — search opportunities
- `POST /opportunities/` — create opportunity
- `PUT /opportunities/{id}` — update opportunity

### Appointments / Calendar
- `GET /calendars/?locationId={id}` — list calendars
- `GET /calendars/events?locationId={id}&startTime=...&endTime=...` — list events
- `POST /calendars/events/appointments` — create appointment

### Conversations / Messaging
- `GET /conversations/search?locationId={id}` — search conversations
- `POST /conversations/messages` — send message (SMS or email)
- `GET /conversations/{id}/messages` — get messages in a conversation

### Workflows / Automations
- `GET /workflows/?locationId={id}` — list workflows
- Triggering a contact into a workflow is done by adding them to the workflow via contact update + tag

---

## Auth example (curl)

```bash
curl -X GET "https://services.leadconnectorhq.com/contacts/?locationId=$GHL_LOCATION_ID" \
  -H "Authorization: Bearer $GHL_PIT_TOKEN" \
  -H "Version: 2021-07-28" \
  -H "Content-Type: application/json"
```

---

## Notes
- PIT tokens are scoped to a single GHL location. This token covers this client's location only.
- Rate limit: 100 req/10s per location for most endpoints.
- Contacts are the core object — most automations start with creating or updating a contact.
- Tags are the primary trigger mechanism for workflows — add a tag to a contact to enroll them in a sequence.
