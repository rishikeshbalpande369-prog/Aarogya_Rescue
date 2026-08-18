# AarogyaRescue

> **Fast Care. Save Life.**

AarogyaRescue is an emergency response system designed to reduce the delay between a road accident and the arrival of medical help. The project combines crash detection, GPS location, automated communication, medical-profile sharing, and hospital/blood-bank notification into one emergency workflow.

## Project Information

- **Project:** AarogyaRescue
- **Event:** KIRO Buildathon 2026
- **Institution:** RTMSSU Nagpur
- **Build date:** 15 August 2026
- **Demo:** https://arogyarescue-cjpp353.public.builtwithrocket.new/emergency-confirmation-screen

## Problem

The project presentation identifies several emergency-response gaps:

- A victim may be unconscious and unable to call for help.
- Emergency contacts may not know the accident location.
- Hospitals may not have medical information before the patient arrives.
- Blood banks may not be prepared for a required blood group in time.

The presentation frames the problem around the importance of reducing response time during the emergency window.

## Solution

AarogyaRescue creates an automated emergency chain:

1. Accident is detected or the SOS is triggered.
2. GPS location is acquired.
3. The nearest hospital is identified.
4. An ambulance/hospital call and SMS alerts are initiated.
5. The user's medical information is shared.
6. Family/emergency contacts receive the location and emergency information.
7. The hospital and blood bank can prepare before the patient arrives.

## Core Features

### 1. Crash Auto-Detection
The presentation describes accelerometer-based crash detection. A G-force spike above **25 m/s²** is used as the trigger threshold in the demonstrated concept.

### 2. Automated Ambulance Call
Twilio is used for outbound voice communication. The call can communicate emergency information such as patient details, blood group and GPS location.

### 3. Instant SMS Alerts
Emergency contacts receive an SMS containing the accident location, Google Maps link, blood group and relevant patient information.

### 4. Blood Bank Notification
The hospital/blood-bank workflow is designed to notify the required blood group before the patient arrives.

### 5. Real-Time GPS Tracking
Browser geolocation and OpenStreetMap are used to obtain and display the live location.

### 6. Medical Profile Sharing
The medical profile can contain:

- Blood group
- Allergies
- Medications
- Insurance information
- Doctor information
- Address
- Age

The presentation also shows support for up to five emergency contacts.

## Main Screens

### Registration & Medical Profile
Collects personal and medical information required during an emergency.

### SOS Dashboard
Provides:

- Live GPS map
- Large SOS button
- Automatic accelerometer detection
- Three-second hold interaction to reduce accidental triggers

### Alert Status
Shows the status of emergency actions such as:

- Call placed
- SMS sent
- Hospital notified
- Blood bank alerted

### Hospital Admin Registry
Allows hospital-side information such as:

- Hospital latitude/longitude
- Blood-bank availability flag
- Ambulance direct line
- Accident event log

## Technology Stack

The project presentation lists:

- Python 3.14
- Flask 3.0
- SQLAlchemy
- SQLite
- Twilio Voice & SMS API
- OpenStreetMap / Nominatim
- Leaflet.js
- Bootstrap 5
- Vanilla JavaScript

## System Architecture

```text
Mobile / Browser
      |
      | GPS + Accelerometer + SOS
      v
Flask Backend
      |
      +--> Haversine distance / Hospital Finder
      |
      +--> Medical Profile
      |
      +--> Emergency Event
      |
      v
Twilio Voice + SMS
      |
      +--> Ambulance / Hospital
      +--> Family / Emergency Contacts
      |
      v
Hospital / Blood Bank
```

## Project Impact

The presentation identifies these intended benefits:

- Help when a victim is unconscious.
- Reduced ambulance-response delay.
- Earlier hospital preparation.
- Earlier blood-bank preparation.
- Faster family notification with the accident location.
- Minimal user action after an accident.

## Future Scope

The presented roadmap includes:

- AI-based severity scoring using crash photos
- OBD-II vehicle integration
- IoT wearable SOS band with vitals and GPS
- WhatsApp-based automatic family alerts
- Nearby certified first-aider/volunteer network
- Integration with a government 108 ambulance API

## Important Note

This repository should clearly distinguish between **implemented/demo functionality** and **future or planned functionality**. Do not claim that a future integration is already production-ready unless it has actually been implemented and tested.

## Safety & Privacy

AarogyaRescue handles potentially sensitive medical and location information. A production version should use:

- Authentication and authorization
- HTTPS
- Secure environment variables for API credentials
- Encryption for sensitive data
- Minimal data collection
- Access controls for hospital/admin users
- Audit logs
- Clear consent and privacy policies
- Reliable failure handling for emergency communication

## Demo

Open the deployed project:

https://arogyarescue-cjpp353.public.builtwithrocket.new/emergency-confirmation-screen
