# RegiShield: Diabetic Regimen Safety & Sick-Day Care Continuity Bridge

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Track](https://img.shields.io/badge/Track-Diabetes%20•%20Patient%20Education%20%26%20Digital%20Engagement-green)](#hackathon-track)
[![Compliance](https://img.shields.io/badge/Standards-HL7%20FHIR%20%7C%20ABDM%20Aligned-orange)](#data-standards--privacy)

> **RegiShield** is an omnichannel patient engagement and care-coordination bridge engineered to eliminate the communication vacuum in Type 2 Diabetes management during acute intercurrent events (the "Sick-Day" gap).

---

## 📌 Executive Summary

Outpatient chronic diabetes care predominantly operates on static 3- to 6-month consultation cycles. While patients maintain stable oral regimens at home, acute life events—such as acute gastroenteritis, intercurrent infections, or newly co-prescribed steroid and anti-tubercular courses—frequently collide with ongoing therapies. 

In low-resource and semi-urban settings, patients often lack access to continuous digital tools, and blood glucose meters can provide misleadingly normal readings during conditions like **Euglycemic Diabetic Ketoacidosis (EDKA)**. Consequently, patients delay seeking timely advice while solo general practitioners remain unaware of acute deteriorations until emergency hospitalizations occur.

**RegiShield** bridges this divide by delivering an accessible, zero-barrier communication channel (via regional WhatsApp and automated IVR voice check-ins) that surfaces pre-configured, clinician-approved sick-day lifestyle reminders to patients and dispatches structured event timelines directly to the primary doctor.

---

## 🎯 Hackathon Scope & Regulatory Guardrail Compliance

To maintain strict adherence to healthcare software safety guidelines:

- **What RegiShield DOES:**
  - Facilitates bilingual and vernacular patient-reported symptom logging (Tamil, Hindi, English).
  - Delivers pre-configured, doctor-approved lifestyle checklists and educational sick-day self-care prompts.
  - Automatically notifies the primary doctor with structured clinical timelines and event logs.
  - Formats patient records into HL7 FHIR-compliant schema for electronic health record (EHR) continuity.

- **What RegiShield DOES NOT do (Strict Scope Boundaries):**
  - ❌ **No autonomous medical diagnosis**
  - ❌ **No automated medication titration or dosage alterations**
  - ❌ **No autonomous clinical decision-making or therapy recommendations**
  - ❌ **No autonomous interpretation of medical diagnostics**

*All treatment reviews and therapy adjustments remain strictly under the direct oversight of the licensed treating physician.*

---

## 🔬 Scientific & Clinical Evidence Base

RegiShield is designed around peer-reviewed consensus and landmark clinical pharmacology:

1. **Euglycemic DKA & SGLT-2 Inhibitor Risks:**  
   *Chow, E., Clement, S., Garg, R. (2023).* "Euglycemic diabetic ketoacidosis in the era of SGLT-2 inhibitors." *BMJ Open Diabetes Research & Care*, 11:e003666.  
   *Key Insight:* Glucosuria persists despite severe hypovolemia and metabolic acidosis, causing capillary blood glucose to remain deceptively $< 200\text{ mg/dL}$. Timely sick-day hydration prompts and doctor consultation are critical.

2. **Glucocorticoid-Induced Hyperglycemic Dynamics:**  
   *Shah, P., Kalra, S., et al. (2022).* "Management of Glucocorticoid-Induced Hyperglycemia." *Diabetes, Metabolic Syndrome and Obesity: Targets and Therapy*, 15:1577–1588.  
   *Key Insight:* Morning oral steroids produce delayed postprandial glucose excursions peaking 4 to 6 hours post-dose (late afternoon/evening), rendering standard morning fasting tests uninformative.

3. **TB–Diabetes Pharmacokinetic Interactions:**  
   *van Crevel, R., et al. (2018).* "Clinical management of combined tuberculosis and diabetes." *International Journal of Tuberculosis and Lung Disease*, 22(12):1404–1410.  
   *Key Insight:* Rifampicin enzyme induction substantially alters sulfonylurea bio-efficacy, requiring structured communication between TB treatment programs and primary diabetes caregivers.

---

## 📐 Conceptual System Architecture

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        PATIENT ACCESS SURFACES                         │
│   • 2G / Basic Feature Phone: Interactive Voice Response (IVR Calls)   │
│   • WhatsApp Business Platform: Regional Text & Audio Check-ins       │
│   • Progressive Web App (PWA): Low-bandwidth offline-first portal      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Webhook Payloads
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                   INGESTION & DATA MAPPING LAYER                       │
│   • Vernacular Speech-to-Text Parsing (Indic-Wav2Vec / Whisper)        │
│   • Symptom Entity Normalization (e.g., Vomiting, Poor Oral Intake)     │
│   • HL7 FHIR Profile Serialization (MedicationStatement, Observation)  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Structured FHIR Objects
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                 REGISHIELD EVENT ORCHESTRATION CORE                    │
│   • Identifies Event Trigger (Acute Illness / Intercurrent Rx)         │
│   • Retrieves Pre-Configured Physician Sick-Day Protocols             │
│   • Zero runtime LLM hallucination for safety instructions             │
└──────────────────┬──────────────────────────────────┬──────────────────┘
                   │                                  │
      Patient Nudge│                                  │Doctor Alert
                   ▼                                  ▼
┌──────────────────────────────────────┐  ┌──────────────────────────────┐
│     PATIENT-FACING NOTIFICATIONS     │  │    CLINICIAN TRIAGE PORTAL   │
│ • "Standard sick-day hydration tips" │  │ • Structured Event Digest    │
│ • "Reminder to check urine ketones"  │  │ • Patient Timeline Log       │
│ • "Doctor consultation recommended"  │  │ • 1-Click Callback Trigger   │
└──────────────────────────────────────┘  └──────────────────────────────┘
