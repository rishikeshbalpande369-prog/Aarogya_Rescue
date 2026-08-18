# Kiro Instructions — AarogyaRescue

## Project Mission

Build and maintain **AarogyaRescue**, an emergency response system whose goal is to reduce the time between an accident and medical assistance.

The core experience is:

```text
Accident / SOS
→ GPS acquisition
→ Nearest hospital
→ Emergency call + SMS
→ Medical profile sharing
→ Family notification
→ Blood-bank notification
→ Help dispatched
```

## Product Priorities

Always prioritize:

1. Emergency reliability
2. Clear user feedback
3. Fast interaction
4. Accurate location handling
5. Secure medical information
6. Mobile usability
7. Maintainable code

## Functional Requirements

### SOS

Implement both:

- Manual SOS
- Automatic crash detection

The demo concept uses a three-second hold for the manual SOS button.

### Crash Detection

Use device accelerometer data where supported.

The project presentation specifies a trigger concept based on a G-force/acceleration spike above **25 m/s²**.

Avoid treating a single sensor reading as unquestionable proof of an accident in a production implementation. Use debouncing, confirmation logic or additional signals where appropriate.

### GPS

Acquire the user's current location after an emergency trigger.

The location should be usable for:

- Map display
- Hospital selection
- Emergency SMS
- Hospital communication
- Family notification

### Hospital Finder

Use the registered hospital latitude/longitude values.

Calculate approximate distance between the user and candidate hospitals using the Haversine method and identify the nearest suitable hospital.

### Communication

Use Twilio Voice and SMS where configured.

Never hard-code:

- Twilio credentials
- API tokens
- Secret keys
- Production phone numbers that should remain private

Use environment variables.

### Medical Profile

Support the project's demonstrated profile fields:

- Blood group
- Age
- Address
- Allergies
- Medications
- Insurance
- Doctor information
- Emergency contacts

The presentation specifies support for up to five emergency contacts.

### Hospital Registry

Allow authorized hospital/admin users to manage:

- Hospital name
- Latitude
- Longitude
- Blood-bank availability
- Ambulance direct line
- Accident event records

## Technology Direction

The presentation specifies this stack:

- Python 3.14
- Flask 3.0
- SQLAlchemy
- SQLite
- Twilio Voice & SMS API
- OpenStreetMap / Nominatim
- Leaflet.js
- Bootstrap 5
- Vanilla JavaScript

Preserve the existing stack unless there is a strong technical reason to change it.

## Backend Principles

Use clear separation between:

```text
Routes
Services
Models
External API integrations
Utilities
Templates / frontend assets
Configuration
```

Recommended conceptual structure:

```text
app/
├── routes/
├── services/
│   ├── emergency_service
│   ├── hospital_service
│   ├── location_service
│   └── notification_service
├── models/
├── templates/
├── static/
└── config/
```

Adapt this structure to the actual source tree rather than creating duplicate architecture unnecessarily.

## Database Principles

Use SQLAlchemy models for persistent entities.

Potential entities:

- User
- MedicalProfile
- EmergencyContact
- Hospital
- EmergencyEvent
- NotificationEvent

Store only information necessary for the application.

## API and External Services

Wrap Twilio and geocoding functionality in services instead of calling external APIs directly from every route.

For example:

```text
Route
  ↓
Emergency Service
  ↓
Notification Service
  ↓
Twilio
```

This makes testing and error handling easier.

## Security Rules

Never commit secrets to GitHub.

Use:

```text
.env
```

for local secrets and provide:

```text
.env.example
```

with placeholder variable names.

Add `.env` to `.gitignore`.

Medical information and location data should be treated as sensitive.

## Emergency Reliability Rules

Never show:

```text
"Call placed ✓"
```

unless the backend has confirmed that the call request was successfully accepted.

Use explicit states:

```text
PENDING
PROCESSING
SUCCESS
FAILED
RETRYING
```

Prevent duplicate emergency events where possible.

Log emergency actions with timestamps and status.

## UX Rules

The SOS action must be immediately visible.

Keep emergency screens simple.

Use large controls.

Avoid unnecessary animations during an emergency.

Always provide readable status messages.

Never hide a failure behind a generic success message.

## Development Rules

Before changing code:

1. Inspect the existing project structure.
2. Reuse existing components and services.
3. Avoid duplicate implementations.
4. Keep changes focused.
5. Test the affected workflow.
6. Check mobile responsiveness.
7. Check error states.

## Testing Priorities

Test at minimum:

- Manual SOS
- Three-second hold
- Crash-detection trigger logic
- GPS permission granted
- GPS permission denied
- No GPS signal
- Hospital selection
- Twilio success
- Twilio failure
- SMS success
- SMS failure
- Missing medical profile
- Duplicate trigger
- Mobile layout

## Future Features

Treat these as roadmap items unless they have been implemented and tested:

- AI severity scoring
- OBD-II integration
- IoT SOS wearable
- WhatsApp automatic dispatch
- Volunteer first-aider network
- Government 108 API integration

Do not describe roadmap items as currently available functionality.

## Documentation Rules

Keep the following files updated when architecture changes:

- `README.md`
- `project.md`
- `workflow.md`
- `design.md`
- `kiro-instruction.md`

The documentation should always distinguish:

```text
Implemented
Demo / Prototype
Planned / Future
```

## Definition of Done

A feature is complete only when:

- The UI works
- The backend works
- Errors are handled
- Sensitive values are not hard-coded
- The feature works on a mobile viewport
- Relevant tests pass
- Documentation reflects the actual implementation
