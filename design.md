# AarogyaRescue Design

## 1. Design Goal

The primary design principle is **zero-friction emergency interaction**.

During an emergency, the interface should minimize:

- Number of taps
- Reading required
- Form completion
- Navigation between screens
- Decisions required from the victim

The main action should be immediately visible and understandable.

## 2. Design Principles

### Emergency First
The SOS action must be visually dominant on the emergency dashboard.

### Simple Information Hierarchy
Critical information should appear before secondary information.

### Clear Status
Users should immediately understand whether the call, SMS, hospital notification and blood-bank notification succeeded.

### Location Visibility
The current location should be easy to identify on the map.

### Error Transparency
If an emergency action fails, the interface should show the failure clearly instead of silently pretending that it succeeded.

### Accessibility
The interface should support:

- Large touch targets
- Strong contrast
- Readable typography
- Clear labels
- Keyboard accessibility where applicable
- Screen-reader-friendly controls

## 3. Main Screen Structure

### Registration / Medical Profile

```text
+--------------------------------+
|        AarogyaRescue           |
|      Medical Profile           |
+--------------------------------+
| Blood Group                    |
| Age                            |
| Address                        |
| Allergies                      |
| Medications                    |
| Insurance                      |
| Doctor Information             |
|                                |
| Emergency Contacts             |
| Contact 1                      |
| Contact 2                      |
| ...                            |
|                                |
|        Save Profile            |
+--------------------------------+
```

The presentation lists blood group, age, address, allergies, medications, insurance, doctor information and up to five emergency contacts.

## 4. SOS Dashboard

```text
+--------------------------------+
| AarogyaRescue       GPS: ON    |
+--------------------------------+
|                                |
|          LIVE MAP              |
|                                |
|                                |
+--------------------------------+
|                                |
|          [   SOS   ]           |
|                                |
|   Hold for 3 seconds           |
|                                |
| Auto crash detection: ACTIVE   |
+--------------------------------+
```

The SOS control should remain the primary visual focus.

## 5. Alert Status Screen

```text
+--------------------------------+
|      Emergency Status          |
+--------------------------------+
| Call placed             ✓      |
| SMS sent                ✓      |
| Hospital notified       ✓      |
| Blood bank alerted      ✓      |
+--------------------------------+
| Current Location               |
| [Map / Location Details]       |
+--------------------------------+
```

Use explicit states such as:

- Pending
- Processing
- Successful
- Failed
- Retrying

Do not show a success state until the backend confirms the action.

## 6. Hospital Admin Screen

```text
+--------------------------------+
| Hospital Registry              |
+--------------------------------+
| Hospital Name                  |
| Latitude                       |
| Longitude                      |
| Blood Bank Available           |
| Ambulance Direct Line          |
|                                |
|          Save Hospital         |
+--------------------------------+
| Accident Event Log             |
| Date | Location | Status       |
+--------------------------------+
```

## 7. Color and Visual Language

The emergency interface should use a strong emergency visual hierarchy.

Recommended semantic roles:

- Emergency/SOS: red semantic role
- Success: green semantic role
- Warning/pending: amber semantic role
- Neutral information: standard interface color

Avoid relying on color alone. Pair colors with icons, labels or text.

## 8. Typography

Use a clean sans-serif typeface with:

- Large heading sizes
- High readability for emergency messages
- Medium/large button text
- Consistent spacing
- Short labels

## 9. Responsive Design

The application should work across:

- Mobile phones
- Tablets
- Desktop browsers

The emergency dashboard should be designed mobile-first because the core interaction involves GPS and a phone/device.

## 10. Component Structure

Suggested reusable components:

```text
App
├── Navigation
├── Registration
│   └── MedicalProfileForm
├── SOSDashboard
│   ├── LiveMap
│   ├── SOSButton
│   └── CrashDetectionStatus
├── EmergencyStatus
│   ├── CallStatus
│   ├── SMSStatus
│   ├── HospitalStatus
│   └── BloodBankStatus
└── HospitalAdmin
    ├── HospitalForm
    └── AccidentEventLog
```

## 11. Design Validation

Before deployment, test:

- SOS visibility
- Three-second hold behavior
- GPS permission flow
- GPS failure state
- Call/SMS status accuracy
- Medical-profile data visibility
- Mobile responsiveness
- Accessibility
- Duplicate-trigger prevention
