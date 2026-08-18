# AarogyaRescue Workflow

## 1. Normal Setup

```text
User
  |
  v
Registration
  |
  v
Medical Profile
  |
  +--> Blood Group
  +--> Allergies
  +--> Medications
  +--> Insurance
  +--> Doctor Details
  +--> Address
  +--> Emergency Contacts
  |
  v
SOS Dashboard
```

## 2. Emergency Trigger

AarogyaRescue supports two trigger paths:

```text
                 +------------------+
                 | Emergency Event  |
                 +---------+--------+
                           |
                +----------+----------+
                |                     |
                v                     v
          Manual SOS             Crash Detection
          Button                Accelerometer
                |                     |
                +----------+----------+
                           |
                           v
                    Emergency Trigger
```

The demonstrated interface uses a three-second hold for the manual SOS button to help prevent accidental activation.

## 3. Location Acquisition

```text
Emergency Trigger
       |
       v
Get GPS Coordinates
       |
       v
Latitude + Longitude
       |
       +--> Map display
       |
       +--> Hospital search
       |
       +--> Family alert
       |
       +--> Hospital alert
```

The presentation describes browser geolocation and OpenStreetMap/Nominatim for location handling.

## 4. Nearest Hospital Selection

The backend uses a Haversine-distance approach to compare the user's coordinates with registered hospitals.

```text
User GPS
   |
   v
Hospital Registry
   |
   v
Calculate Distance
   |
   v
Sort / Select Nearest Suitable Hospital
```

Conceptually:

```text
Distance(user, hospital_1)
Distance(user, hospital_2)
Distance(user, hospital_3)
...
             |
             v
      Nearest Hospital
```

## 5. Emergency Communication

After the emergency is triggered:

```text
                     Emergency Event
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
     Voice Call          SMS Alert      Medical Data
      (Twilio)           (Twilio)          Share
          |                |                |
          v                v                v
 Ambulance/Hospital   Family/Contacts    Hospital
```

## 6. Blood Bank Notification

```text
Patient Medical Profile
        |
        v
Blood Group
        |
        v
Hospital / Blood Bank
        |
        v
Prepare Required Blood Group
```

This is part of the project's demonstrated emergency-response concept.

## 7. Live Tracking

```text
Browser Geolocation
        |
        v
Current Coordinates
        |
        v
Leaflet Map
        |
        +--> Hospital
        +--> Family
        +--> Emergency Event
```

## 8. Alert Status

The interface provides a status panel for emergency actions:

```text
Call placed        ✓
SMS sent           ✓
Hospital notified  ✓
Blood bank alerted ✓
```

## 9. Hospital Admin Workflow

```text
Hospital Admin
      |
      v
Hospital Registry
      |
      +--> Hospital Name
      +--> Latitude / Longitude
      +--> Blood Bank Flag
      +--> Ambulance Direct Line
      |
      v
Accident Event Log
```

## 10. End-to-End Workflow

```text
ACCIDENT
   |
   v
ACCIDENT DETECTED / SOS
   |
   v
GPS ACQUIRED
   |
   v
NEAREST HOSPITAL FOUND
   |
   +-----------------------------+
   |             |               |
   v             v               v
Voice Call      SMS         Medical Profile
   |             |               |
   v             v               v
Hospital      Family       Hospital
   |             |
   +------+------+ 
          |
          v
   Blood Bank Alert
          |
          v
   Help Dispatched
```

## Failure Handling

A production implementation should define fallback behavior for:

- GPS unavailable
- Internet unavailable
- Twilio call failure
- SMS failure
- Hospital registry unavailable
- Duplicate emergency triggers
- False crash detection
- Missing medical profile
- Device/browser permission denial

Emergency communication should fail safely and provide a clear status to the user whenever possible.
