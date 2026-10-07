# HealthPassport

Passport for your health. Your medical records in your pocket, readable by any hospital, in any country.

HealthPassport is a decentralized patient wallet concept by Team Helix. This repository holds the project website: a single-page site that explains the idea and includes a working in-browser demo of the core flow.

# The problem

A patient's history stays locked in the country where it was created. Reports arrive as PDFs in a local language, in formats the receiving hospital's systems cannot read, and critical time is lost in an emergency.

# The idea

Encrypted wallet: you hold the keys, and records stay on your device.
Emergency QR: one scan gives a doctor the vital summary.
Schema translator: any PDF becomes the format the ER needs (FHIR, SNOMED CT).
You decide: every share is consent-based, time-limited and logged.
What's in the site
Section	What it covers
Hero	Product pitch and a live phone mock that mirrors your demo wallet
Records don't cross borders	The problem: language barriers, incompatible formats, critical delays
One wallet. Every hospital.	The four core features
Try HealthPassport	The working demo (see below)
A day in the life	Meera's story, with a button that runs her emergency in the demo
Under the hood	Patient wallet, schema translator, hospital side and the trust layer
Privacy by design	On-device encryption, keys, consent expiry, audit trail, emergency mode
What we would build it with	Proposed tech stack
Hard problems, real answers	Risks and how the design handles them
Roadmap	MVP, Pilot and Scale phases
The working demo

# The demo runs entirely in your browser. There is no server and no account.

My wallet: view and remove your records. The hero phone updates to match.
Add report: a four-step flow.
Upload: use the sample Italian lab report, or pick a file.
Encrypt: the file is encrypted with AES-256-GCM using the browser's Web Crypto API. The key is non-extractable and stays on the device.
Translate: the three pipeline steps run and each Italian line maps to an English field with its SNOMED CT code.
Review and save: edit any field next to the original. Saving is disabled until you confirm you checked every field.
Share: choose which records to share and an expiry (5 minutes, 1 hour or 24 hours). A QR code is generated with a live countdown and a Revoke button.
Hospital view: open a share as the receiving hospital would. Only the shared fields appear, with an optional FHIR JSON view. Expired and revoked QR codes are blocked. Emergency access shows only blood group, allergies and medication.
Audit log: every add, remove, share, revoke, hospital view and emergency access is recorded.
Demo limitations
Reading your own uploaded file is simulated. The demo always uses the sample fields, because real OCR and AI extraction need a backend.
The link inside the QR code (healthpassport.helix/v/...) is a placeholder, not a live address. Use Open as hospital to view a share.
Data is stored in your browser's localStorage under the key hp_helix_v1. Use Reset demo in the wallet tab to clear it.
This is a concept demo. It is not a medical product and should not be used for real patient data.
Run it

The whole site is one self-contained file: helix-healthpassport.html. Open it in any modern browser, or host it on any static host.

It loads two things from the internet:

Google Fonts (Inter and JetBrains Mono), with system-font fallbacks
qrcodejs from cdnjs, for QR codes

Without a connection the page still works, but the fonts fall back and the QR code image will not draw (the share token is shown as text instead).

The Helix logo symbol is embedded in the file as a base64 image.

# Tech
Plain HTML, CSS and JavaScript, with no build step
Web Crypto API for encryption
localStorage for demo state
Dark console theme with cyan and violet accents
Roadmap
Phase	Timeline	Focus
MVP	0 to 3 months	Wallet and PDF upload, translate to FHIR, QR viewer for doctors
Pilot	3 to 9 months	Partner with 1 or 2 clinics, add a second country pair, doctor feedback loop
Scale	9 to 18 months	More languages, insurer and embassy tie-ins, direct hospital integration

The proposed production stack is Flutter or React Native for the mobile app, on-device OCR plus an LLM for reading reports, FHIR, SNOMED CT and LOINC for standards, and W3C decentralized IDs with verifiable credentials for identity.

Team

Helix: Astronomical Ventures
