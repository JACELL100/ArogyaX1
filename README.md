# ArogyaX — AI-Powered Oncology Management Platform

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-6.0-092E20?style=for-the-badge&logo=django&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-Llama%203.3%2070B-FF6C37?style=for-the-badge)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-00FFFF?style=for-the-badge)
![Ethereum](https://img.shields.io/badge/Ethereum-Sepolia-627EEA?style=for-the-badge&logo=ethereum&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)

**A comprehensive, full-stack cancer care platform integrating AI diagnostics, blockchain verification, real-time video consultations, and patient gamification — built for the Indian healthcare ecosystem.**

</div>

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture Overview](#architecture-overview)
- [Technology Stack](#technology-stack)
- [Django Apps](#django-apps)
  - [Authentication](#authentication-app)
  - [Cancer Detection](#cancer-detection-app)
  - [Clinical Decision Support](#clinical-decision-support-app)
  - [Patient Portal](#patient-portal-app)
  - [Medical Chatbot](#medical-chatbot-app)
  - [Medicine Identifier](#medicine-identifier-app)
  - [Insurance SIP](#insurance-sip-app)
  - [Blockchain](#blockchain-app)
- [AI & ML Components](#ai--ml-components)
- [Blockchain Integration](#blockchain-integration)
- [Database Models](#database-models)
- [API Endpoints](#api-endpoints)
- [External Integrations](#external-integrations)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Environment Variables](#environment-variables)
- [Smart Contracts](#smart-contracts)
- [User Roles](#user-roles)
- [Security](#security)
- [Utilities & Scripts](#utilities--scripts)

---

## Overview

**ArogyaX** is a production-grade oncology management platform built with Django. It unifies the complete cancer care journey — from AI-powered medical image analysis and treatment planning, to secure doctor-patient consultations, blockchain-verified prescriptions, real-time video calling, gamified patient engagement, and government insurance guidance.

The platform serves two primary user roles — **Patients** and **Doctors** — and is designed for the Indian healthcare market (IST timezone, Indian government schemes, Razorpay payments).

### What makes ArogyaX unique:

- **AI Diagnostics at Scale**: YOLOv8 tumor detection + Groq LLM (Llama 3.3 70B) for histopathology, genomics, and treatment plan generation — all in one pipeline.
- **Blockchain-Verified Trust**: Every prescription and QR code scan is logged on the Ethereum Sepolia testnet via three purpose-built smart contracts.
- **Evidence-Traced Recommendations**: Every AI treatment recommendation is linked to clinical trials, guidelines, and case studies through an evidence traceability engine.
- **Full Consultation Loop**: Patients schedule appointments, join WebRTC/Agora video calls, receive blockchain-verified prescriptions, and log symptoms — all within the platform.
- **Explainable AI (XAI)**: Doctors see ranked contributing factors with influence percentages for every AI recommendation, alongside multi-modal confidence scores.

---

## Key Features

### For Patients
- Secure registration and login via **Supabase OAuth** (Google, etc.)
- Personal health dashboard with treatment plan overview
- **Symptom Logging**: Track 15+ oncology-specific symptoms (fatigue, pain, nausea, hair loss, emotional symptoms) with severity ratings
- **AI Medical Chatbot**: Context-aware chat powered by Groq LLM, pre-loaded with the patient's treatment history
- **Medicine Identifier**: Photograph a medicine package → AI identifies drug name, uses, side effects, contraindications, and interactions
- **Video Consultations**: Request appointments, join calls with doctors via WebRTC or Agora RTC
- **Blockchain-Verified Prescriptions**: Download PDFs with SHA-256 hash anchored on Ethereum
- **Patient QR Code**: Encrypted, expirable QR for secure doctor access to medical records
- **Telegram Notifications**: Receive alerts, reminders, and updates directly in Telegram
- **Gamification**: Earn badges and points for consistent symptom logging and treatment adherence
- **Insurance & Schemes**: Browse government health schemes and private insurance policies; check eligibility and apply online
- **Offline Sync**: PWA-style data sync for low-connectivity scenarios

### For Doctors
- Role-gated dashboard with their patient list
- **Cancer Image Upload & Analysis**: Submit X-Ray, CT, MRI, biopsy, or ultrasound images for AI analysis (YOLOv8 + OpenCV)
- **Treatment Plan Generator**: AI-generated personalized plans with primary/adjuvant/targeted therapies, 5-year survival predictions, QoL scores, and clinical trial recommendations
- **Clinical Decision Support**: AI confidence scores (traffic-light: High/Moderate/Low), uncertainty breakdowns, missing data source flags, and conflicting modality alerts
- **Explainable AI (XAI)**: Ranked factors and influence percentages driving each treatment recommendation
- **Tumor Board Sessions**: Multi-doctor collaborative case reviews with full audit logs
- **Toxicity Predictions**: Chemotherapy toxicity risk assessments per patient
- **Symptom Monitoring Alerts**: Configure thresholds; get notified when a patient's symptoms exceed them
- **Histopathology & Genomics Analysis**: Upload pathology PDFs and genomic data for AI parsing and integration into treatment plans
- **Evidence Search**: Query a clinical evidence database (trials, guidelines, case studies) supporting each recommendation
- **Prescription Issuance**: Generate and blockchain-anchor prescription PDFs with QR verification codes
- **KYC Verification**: Submit license documents for platform verification

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                        ArogyaX Platform                      │
│                      (Django 6.0 Monolith)                   │
├──────────────┬──────────────┬──────────────┬─────────────────┤
│ authentication│cancer_detect.│ clinical_ds  │ patient_portal  │
│  (Auth/QR)   │ (AI/ML/Image)│(Doctor AI)   │(Patient Hub)    │
├──────────────┴──────────────┴──────────────┴─────────────────┤
│ medical_chatbot │ medicine_identifier │ Insurance_SIP         │
│  (LLM Chat)     │ (OCR + Groq)       │ (Schemes/Payment)     │
├─────────────────┴─────────────────────┴───────────────────────┤
│                      blockchain app                            │
│        (Web3.py → Ethereum Sepolia via Alchemy RPC)           │
└───────────────────────────────────────────────────────────────┘
         │                │              │              │
    Supabase          Groq API       Telegram       Agora RTC
   (Auth + DB)     (Llama 3.3 70B)  (Notifications) (Video)
         │                │
   PostgreSQL         YOLOv8n.pt
   (Production)      (Tumor Detection)
```

---

## Technology Stack

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Python | 3.10+ | Core language |
| Django | 6.0 | Web framework |
| Django REST Framework | 3.14 | REST APIs |
| psycopg2-binary | latest | PostgreSQL adapter |
| python-dotenv | latest | Environment variable management |
| Supabase-py | latest | Auth + Storage client |
| PyJWT | latest | JWT handling |

### AI / Machine Learning
| Technology | Version | Purpose |
|---|---|---|
| Groq SDK | 0.15 | LLM API client (Llama 3.3 70B Versatile) |
| Ultralytics (YOLOv8) | latest | Tumor detection in medical images |
| OpenCV (contrib) | 4.13 | Image pre-processing, contour detection |
| EasyOCR | 1.7.2 | Text extraction from medicine packaging |
| Pytesseract | 0.3.13 | OCR fallback for text extraction |
| PyTorch + Torchvision | latest | Deep learning inference backend |
| scikit-learn | latest | Traditional ML pipelines |
| NumPy / pandas | latest | Data processing |
| matplotlib | latest | Chart and visualization generation |
| HuggingFace Hub | latest | ML model downloads |
| modelscope | latest | Alternative model repository |

### Blockchain
| Technology | Purpose |
|---|---|
| Web3.py | Ethereum node interaction |
| eth-account | Transaction signing |
| eth-keys / eth-abi | Key management, ABI encoding |
| py-solc-x | Solidity contract compilation |
| pycryptodome | Cryptographic primitives (SHA-256, etc.) |

### Document Processing
| Technology | Purpose |
|---|---|
| pdf2image | Convert prescription/report PDFs to images |
| PyPDF2 | PDF reading and metadata extraction |
| pypdfium2 | High-fidelity PDF rendering |
| python-docx | Generate Word document reports |
| ReportLab / WeasyPrint | PDF generation for prescriptions |

### External Services
| Service | Purpose |
|---|---|
| Supabase | Auth provider (Google OAuth), PostgreSQL, file storage |
| Alchemy | Ethereum Sepolia RPC node provider |
| Groq | LLM inference (Llama 3.3 70B) |
| Telegram Bot API | Patient notifications and alerts |
| Razorpay | Insurance premium payment processing |
| Agora RTC | Production-grade video consultation |
| Gmail SMTP | Email notifications |

### Frontend
- Django Template Engine
- WebRTC (browser-native, with Django signaling backend for offer/answer/ICE)
- Agora RTC Web SDK (fallback/primary video)
- Tailwind CSS / Bootstrap (template-level)

---

## Django Apps

### Authentication App

**Location**: `authentication/`

The authentication app handles the complete identity and access management layer, supporting dual-role access for patients and doctors.

#### Responsibilities
- Custom `User` model (`AbstractUser`) with UUID primary key and `user_type` field (`patient` / `doctor`)
- Supabase OAuth integration — Google Sign-In redirects through Supabase, which returns a token; Django's `/auth/callback/` endpoint exchanges it, creates a local user session, and logs them in
- Separate login entry points for patients and doctors; cross-role login is blocked at the view layer
- Patient and Doctor profiles with rich metadata
- Doctor KYC (Know Your Customer) — license document submission and verification workflow
- Medical record uploads by patients (PDF / image)
- **Patient QR Code System**: encrypted, time-limited QR codes that doctors scan to access a patient's records; each scan is logged on-chain (see Blockchain)
- **Voice/Text Assistant**: Groq-powered navigation assistant that maps natural language input ("go to my prescriptions") to platform URLs, supporting both patients and doctors
- **Nearby Clinics API**: geolocation-based clinic discovery using doctor profile coordinates

#### Key Models
| Model | Description |
|---|---|
| `User` | UUID PK, `user_type`, `supabase_user_id`, `profile_picture`, `phone_number` |
| `PatientProfile` | DOB, gender, blood group, address, emergency contact, medical history, allergies, `telegram_chat_id` |
| `DoctorProfile` | Specialty, license number, hospital, consultation fee, lat/lng coordinates |
| `DoctorKYC` | License document (file), verification status, notes |
| `MedicalRecord` | Patient-uploaded files; record type (lab report, scan, prescription, other) |
| `PatientQRCode` | Encrypted token, expiry datetime, status, generated QR image |
| `QRCodeScanLog` | Scan timestamp, scanning doctor, IP address, user agent, `blockchain_tx_hash` |

#### Key Views / Endpoints
| Endpoint | Description |
|---|---|
| `GET/POST /auth/register/patient/` | Patient registration |
| `GET/POST /auth/register/doctor/` | Doctor registration |
| `GET /auth/login/patient/` | Patient login page |
| `GET /auth/login/doctor/` | Doctor login page |
| `POST /auth/callback/` | Supabase OAuth token exchange and session setup |
| `GET /auth/dashboard/patient/` | Patient dashboard |
| `GET /auth/dashboard/doctor/` | Doctor dashboard |
| `POST /api/voice-assistant/` | Voice/text navigation assistant |
| `GET /api/nearby-clinics/` | Geolocation clinic search |
| `GET /auth/qr/dashboard/` | Patient QR code management |
| `GET /auth/qr/scan/<token>/` | Doctor scans patient QR code |

---

### Cancer Detection App

**Location**: `cancer_detection/`

The core diagnostic engine. Accepts medical images and reports, performs multi-modal AI analysis, and generates comprehensive, evidence-backed treatment plans.

#### Responsibilities
- Upload and analyze medical images (X-Ray, CT scan, MRI, tumor biopsy, ultrasound)
- Run **YOLOv8n** object detection to identify and localize tumors
- Run **OpenCV** pipelines for CUDA-accelerated image pre-processing, contour analysis, size estimation
- Parse histopathology PDF reports via OCR → extract stage, grade, surgical margins, biomarkers
- Process genomic/molecular data → identify mutations (BRCA1, EGFR, HER2, PIK3CA, etc.)
- Generate **PersonalizedTreatmentPlan** via Groq LLM — includes primary therapy, adjuvant therapy, targeted therapy, immunotherapy, surgery recommendations, clinical trial matches, contraindications, 5-year survival prediction, and QoL scores
- **Evidence Traceability Engine**: every recommendation is linked to clinical trials, published guidelines, and case studies with XAI explanations and feedback logging
- Treatment pathway visualization
- Outcome prediction (ML model)

#### Key Models
| Model | Key Fields |
|---|---|
| `CancerImageAnalysis` | Image file, `tumor_detected` (bool), `tumor_type`, `cancer_stage`, `tumor_size_cm`, `tumor_location`, `confidence_score`, `genetic_profile`, `image_type` |
| `PersonalizedTreatmentPlan` | Cancer type, stage, `primary_treatment`, `adjuvant_treatment`, `targeted_therapy`, `immunotherapy`, `surgery_recommendation`, `clinical_trials`, `five_year_survival`, `contraindications`, linked to `CancerImageAnalysis` |
| `HistopathologyReport` | PDF file, extracted OCR text, `cancer_stage`, `grade`, `surgical_margins`, `biomarkers` |
| `GenomicProfile` | Patient reference, mutations JSON, biomarkers JSON, analysis results |
| `TreatmentOutcome` | Patient response, milestone tracking |
| Evidence models | Clinical trial links, guideline references, case study citations, XAI factor rankings |

#### Key Views / Endpoints
| Endpoint | Description |
|---|---|
| `GET /cancer-detection/` | Doctor analysis dashboard |
| `POST /cancer-detection/upload/` | Upload and trigger AI analysis |
| `GET /cancer-detection/analyses/<id>/` | View analysis detail |
| `POST /cancer-detection/analyses/<id>/treatment-plan/` | Generate Groq treatment plan |
| `GET /cancer-detection/treatment-plan/<id>/` | View treatment plan |
| `GET /cancer-detection/visualize-pathway/<id>/` | Treatment pathway visualization |
| `GET /cancer-detection/api/evidence/explain/<plan_id>/` | XAI explanation for a recommendation |
| `GET /cancer-detection/api/evidence/search/` | Search the evidence database |
| `POST /cancer-detection/api/evidence/ingest-studies/` | Ingest external clinical studies |
| `GET /cancer-detection/histopathology/` | Histopathology hub |
| `POST /cancer-detection/histopathology/upload/` | Upload pathology PDF |
| `GET /cancer-detection/genomics/` | Genomics hub |
| `POST /cancer-detection/genomics/upload/` | Upload genomic data |

---

### Clinical Decision Support App

**Location**: `clinical_decision_support/`

Doctor-only. Provides explainability, confidence scoring, multi-doctor case review, and toxicity prediction as a layer on top of the cancer detection AI results.

#### Responsibilities
- Compute and display **AI Confidence Metadata** for each treatment recommendation (overall confidence, data quality score, model certainty, evidence strength)
- Categorize confidence into traffic-light levels: **High** (≥80%), **Moderate** (50–79%), **Low** (<50%)
- Surface **uncertainty reasons** and missing data sources (e.g., "no genomic data", "limited histopathology")
- Flag conflicting outputs between imaging modalities
- Generate **XAI Explanations**: ranked list of contributing factors with percentage influence on the recommendation
- Manage **Tumor Board Sessions**: collaborative multi-doctor case reviews with member roles, discussion logging, and a full audit trail
- Run **Toxicity Predictions**: chemotherapy regimen risk assessment
- Allow doctors to configure **Symptom Monitoring Thresholds** per patient

#### Key Models
| Model | Key Fields |
|---|---|
| `AIConfidenceMetadata` | `treatment_plan_fk`, `overall_confidence`, `data_quality_score`, `model_certainty`, `evidence_strength`, `confidence_level` (High/Moderate/Low), `uncertainty_reasons`, `missing_data_sources`, `conflicting_modalities` |
| `XAIExplanation` | `treatment_plan_fk`, `contributing_factors` (JSON: factor name + influence %), `recommendation_rationale` |
| `TumorBoardSession` | `cancer_analysis_fk`, `lead_oncologist`, `status`, `notes`, `scheduled_date` |
| `TumorBoardMember` | Session FK, doctor FK, `role` (oncologist, radiologist, pathologist, etc.) |
| `TumorBoardAuditLog` | Session FK, action, doctor, timestamp |
| `ToxicityPrediction` | Patient FK, `drug_regimen`, `overall_risk` (High/Medium/Low), individual organ risk scores |
| `DoctorSymptomMonitor` | Doctor FK, patient FK, symptom field, threshold severity |

#### Access Control
All views in this app are protected by a `@doctor_required` decorator that verifies `user.user_type == 'doctor'` before granting access.

---

### Patient Portal App

**Location**: `patient_portal/`

The complete patient-facing hub for the treatment journey — from symptom tracking and consultations to prescriptions and gamification.

#### Responsibilities

**Health & Symptom Tracking**
- `PatientSymptomLog`: log 15+ oncology symptoms (fatigue, pain, nausea, vomiting, hair loss, appetite loss, fever, shortness of breath, emotional symptoms) with severity 1–5
- Doctor can review and respond to logged symptoms
- `PatientAlert`: automated alerts sent when symptom severity exceeds configured thresholds; read/unread tracking

**Treatment Center**
- View AI-generated treatment plans in patient-friendly language (plain-language summaries generated by Groq)
- `PatientTreatmentExplanation`: explains _why_ a specific treatment was recommended in accessible terms
- `PatientSideEffectInfo`: side effect details per treatment, generated with patient education in mind

**Consultation System**
- `DoctorAvailability`: doctors configure available slots (weekday, start/end time, slot duration)
- `ConsultationRequest`: patient requests a consultation (initial evaluation, follow-up, second opinion, treatment review)
- `Consultation`: confirmed session with scheduled time, call status, notes
- Download blockchain-verified consultation token PDFs

**Video Calling**
- Django signaling backend for peer-to-peer WebRTC (offer / answer / ICE endpoint pairs)
- Agora RTC token generation endpoint (`/portal/call/<id>/agora-token/`) for production-grade video
- `VideoCallSession` model for call history and recording metadata

**Prescription Management**
- Doctors issue prescriptions with `PrescriptionMedicine` entries (drug, dosage, frequency, duration)
- PDF is generated, SHA-256 hash computed, and hash stored on-chain via `PrescriptionVerifier` contract
- Embedded QR code on the PDF links to the verification endpoint
- Patients or pharmacists can upload the PDF at `/portal/prescription/<id>/verify/` to confirm authenticity on-chain

**Notifications**
- `PatientNotificationPreference`: patient controls email, Telegram, and in-app notification channels
- `TelegramBotService`: HTTP-based Telegram Bot API wrapper; sends treatment alerts, appointment reminders, prescription notifications

**Gamification**
- `UserProgress`: cumulative points and level
- `Badge`: predefined achievement types (e.g., "Consistent Logger", "7-Day Streak", "Treatment Completer")
- `UserBadge`: awarded badges with timestamp
- `HealthChallenge`: configurable challenges (e.g., "Log symptoms daily for 7 days")
- `ChallengeParticipation`: patient enrollment and completion tracking
- `ActivityFeed`: chronological feed of patient health activities and achievements

**Offline Sync**
- PWA-style endpoints in `offline_sync_views.py` for syncing symptom logs and alerts when connectivity is restored

#### Key Signals
`patient_portal/signals.py` contains Django post-save signals that automatically:
- Create alerts when a symptom log exceeds severity thresholds
- Trigger Telegram notifications on critical events
- Award gamification badges on milestones

---

### Medical Chatbot App

**Location**: `medical_chatbot/`

A context-aware medical conversational AI for patients, powered by Groq's Llama 3.3 70B.

#### Responsibilities
- Maintain per-patient chat session history (`ChatSession` → multiple `ChatMessage` records)
- Inject patient-specific medical context (current treatment plans, diagnoses, medical history) into the LLM system prompt before each query
- Auto-generate conversation titles from the first message
- Support up to 20 recent sessions in the sidebar
- Restrict access to authenticated patients only

#### Key Models
| Model | Key Fields |
|---|---|
| `ChatSession` | Patient FK, `title`, `is_active`, `created_at` |
| `ChatMessage` | Session FK, `role` (user/assistant/system), `content`, `timestamp` |
| `UserMedicalContext` | Patient FK, `context_json` (cached treatment plans + history), `updated_at` |

#### Key Endpoints
| Endpoint | Description |
|---|---|
| `GET /chatbot/` | Chat interface with session sidebar |
| `POST /chatbot/send/` | Send message → injects medical context → Groq API → return response |
| `POST /chatbot/new-session/` | Create new session |
| `GET /chatbot/session/<id>/` | Load a previous session |

---

### Medicine Identifier App

**Location**: `medicine_identifier/`

Allows patients to identify an unknown medicine by photographing its packaging.

#### Pipeline
1. Patient uploads an image of a medicine package
2. **OpenCV** pre-processes the image (grayscale, thresholding, deskew)
3. **EasyOCR** extracts text from the image
4. **Tesseract** runs as OCR fallback if EasyOCR confidence is low
5. Extracted text (+ optional filename hint) is sent to **Groq LLM**
6. Groq returns structured identification: medicine name, generic name, brand, manufacturer, dosage form, indications, side effects, warnings, contraindications, drug interactions
7. Result is stored in `MedicineIdentification` and cached in `MedicineDatabase`

#### Key Models
| Model | Key Fields |
|---|---|
| `MedicineIdentification` | Patient FK, `image`, `ocr_text`, `identified_name`, `generic_name`, `manufacturer`, `uses`, `side_effects`, `warnings`, `interactions`, `confidence` |
| `MedicineDatabase` | `medicine_name`, `generic_name`, `full_details` (JSON cache), `last_updated` |

#### Key Endpoints
| Endpoint | Description |
|---|---|
| `GET /medicine/` | Medicine identifier home |
| `POST /medicine/upload/` | Upload image, run full pipeline, return results |
| `GET /medicine/history/` | Patient's past identifications |
| `GET /medicine/<id>/` | Detail view of a single identification |

---

### Insurance SIP App

**Location**: `Insurance_SIP/`

Helps patients discover, check eligibility for, and apply to government health schemes and private insurance policies — with Razorpay payment integration for purchasing insurance premiums.

#### Key Models
| Model | Key Fields |
|---|---|
| `GovernmentScheme` | Name, `scheme_type` (health/life/accident/pension/education/agriculture), description, coverage, benefits, application steps, documents required |
| `InsurancePolicy` | Provider, `policy_type`, `premium_amount`, `coverage_amount`, `min/max_age`, features, `is_active` |
| `Eligibility` | Linked scheme/policy, `min/max_age`, `income_limit`, `eligible_states`, `gender` |
| `Application` | Patient FK, scheme/policy FK, `status` (draft/submitted/under_review/approved/rejected), `razorpay_payment_id`, documents |

#### Key Features
- **Eligibility Checker**: input age, income, state, gender → filter matching schemes and policies
- **Application Tracker**: dashboard showing submission status and next steps
- **Razorpay Integration**: collect insurance premium payments; store payment ID against application

---

### Blockchain App

**Location**: `blockchain/`

Provides a clean Python abstraction over three Ethereum smart contracts deployed on the Sepolia testnet, used for immutable audit logging across the platform.

#### Smart Contracts

| Contract | File | Purpose |
|---|---|---|
| `MedicalAccessLogger` | `contract_abi.json` + `deployment_info.json` | Logs every patient QR code scan with patient ID, doctor ID, and timestamp on-chain |
| `PrescriptionVerifier` | `contract_abi.json` + `deployment_info.json` | Stores SHA-256 hashes of prescription PDFs; exposes a verify function callable by anyone |
| `ConsultationTokenVerifier` | `consultation_token_abi.json` + `consultation_token_deployment_info.json` | Issues and verifies blockchain-backed consultation tokens |

#### `BlockchainService` Class
Located in `blockchain/blockchain_service.py`, this class:
- Connects to the Sepolia testnet via **Alchemy RPC URL** (Web3.py HTTPProvider)
- Signs transactions using the platform's **private key** (stored in env vars — never in code)
- Broadcasts signed transactions and returns the TX hash for storage in Django models
- Queries on-chain events (e.g., find all scans for a patient, verify a hash)
- Exposes `check_balance()` for monitoring the signing wallet's ETH balance
- Provides `is_connected()` health check; `blockchain/status_updater.py` polls this for the admin dashboard

All three contract ABIs and deployment addresses are loaded from JSON files at startup.

---

## AI & ML Components

```
Medical Image (X-Ray/CT/MRI)
        │
        ▼
  OpenCV Pre-processing
  (grayscale, CLAHE, resize,
   CUDA-accelerated if available)
        │
        ▼
   YOLOv8n Detection          ──► Tumor bounding boxes, class, confidence
        │
        ▼
   OpenCV Contour Analysis    ──► Tumor size (cm), location, shape metrics
        │
        ▼
   Groq LLM (Llama 3.3 70B)  ──► Structured analysis report
        │
   ┌────┴────┐
   │         │
Histopath  Genomic
 PDF OCR    Data
   │         │
   ▼         ▼
Groq LLM analysis + integration
        │
        ▼
PersonalizedTreatmentPlan generation (Groq)
  - Primary/adjuvant/targeted/immunotherapy
  - Surgery recommendation
  - Clinical trial matching
  - 5-year survival prediction
  - QoL scores
  - Contraindications
        │
        ▼
Evidence Retrieval Engine
  - Clinical trial citations
  - Guideline references
  - Case study links
        │
        ▼
AI Confidence Scoring (clinical_decision_support)
  - Overall: data quality × model certainty × evidence strength
  - Traffic-light: High / Moderate / Low
  - Uncertainty reasons + missing data source flags
        │
        ▼
XAI Explanation
  - Ranked contributing factors
  - Influence percentages
  - Rationale narrative
```

### Groq LLM Usage Summary

| Use Case | Prompt Content | Output |
|---|---|---|
| Cancer image report | Image analysis results, patient demographics | Structured medical report |
| Histopathology analysis | OCR-extracted pathology text | Stage, grade, biomarker summary |
| Genomics analysis | Mutation/biomarker JSON | Clinical significance, therapy targets |
| Treatment plan generation | Full patient profile + all analyses | Structured JSON treatment plan |
| Plain-language explanation | Treatment plan JSON | Patient-friendly summary |
| Medical chatbot | Patient context + conversation history | Conversational medical answer |
| Medicine identification | OCR text from packaging | Structured medicine details |
| Voice assistant | User utterance + page list | URL redirect target |

---

## Blockchain Integration

### Flow: Prescription Verification

```
Doctor creates prescription
        │
        ▼
PDF generated (ReportLab/WeasyPrint)
with embedded QR code
        │
        ▼
SHA-256 hash of PDF bytes computed
        │
        ▼
BlockchainService.store_prescription_hash(hash, patient_id, doctor_id)
  → signs tx with platform private key
  → broadcasts to Sepolia via Alchemy RPC
  → returns tx_hash
        │
        ▼
tx_hash stored in Prescription.blockchain_tx_hash
hash stored in Prescription.pdf_hash
        │
Verification (patient/pharmacist):
        │
        ▼
Upload PDF → recompute SHA-256
  → BlockchainService.verify_prescription_hash(hash)
  → call PrescriptionVerifier.verify() on-chain
  → return True/False + tx details
```

### Flow: QR Code Access Logging

```
Patient generates QR (encrypted token, 24hr expiry)
        │
Doctor scans QR
        │
        ▼
/auth/qr/scan/<token>/ validates token,
decrypts patient ID
        │
        ▼
BlockchainService.log_access(patient_id, doctor_id, timestamp)
  → MedicalAccessLogger contract
  → tx_hash returned
        │
        ▼
QRCodeScanLog created with tx_hash
Patient notified via Telegram
```

---

## Database Models

### Complete Model Reference

| Model | App | Key Fields |
|---|---|---|
| `User` | authentication | UUID PK, `user_type` (patient/doctor), `supabase_user_id`, `profile_picture`, `phone_number` |
| `PatientProfile` | authentication | `dob`, `gender`, `blood_group`, `address`, `emergency_contact`, `medical_history`, `allergies`, `telegram_chat_id` |
| `DoctorProfile` | authentication | `specialty`, `license_number`, `hospital`, `consultation_fee`, `latitude`, `longitude` |
| `DoctorKYC` | authentication | `license_document`, `verification_status`, `reviewed_by`, `notes` |
| `MedicalRecord` | authentication | `file`, `record_type`, `description`, patient FK |
| `PatientQRCode` | authentication | `encrypted_token`, `expires_at`, `status`, `qr_image` |
| `QRCodeScanLog` | authentication | `scan_timestamp`, `scanning_doctor` FK, `ip_address`, `user_agent`, `blockchain_tx_hash` |
| `CancerImageAnalysis` | cancer_detection | `image`, `image_type`, `tumor_detected`, `tumor_type`, `cancer_stage`, `tumor_size_cm`, `tumor_location`, `confidence_score`, `genetic_profile`, `analysis_report` |
| `PersonalizedTreatmentPlan` | cancer_detection | `cancer_type`, `stage`, `primary_treatment`, `adjuvant_treatment`, `targeted_therapy`, `immunotherapy`, `surgery_recommendation`, `clinical_trials`, `five_year_survival_rate`, `quality_of_life_score`, `contraindications` |
| `HistopathologyReport` | cancer_detection | `pdf_file`, `ocr_text`, `cancer_type`, `stage`, `grade`, `surgical_margins`, `biomarkers` |
| `GenomicProfile` | cancer_detection | `mutations` (JSON), `biomarkers` (JSON), `analysis_summary` |
| `TreatmentOutcome` | cancer_detection | `response_status`, `milestones`, `follow_up_date` |
| `AIConfidenceMetadata` | clinical_decision_support | `overall_confidence`, `data_quality_score`, `model_certainty`, `evidence_strength`, `confidence_level`, `uncertainty_reasons`, `missing_data_sources`, `conflicting_modalities` |
| `XAIExplanation` | clinical_decision_support | `contributing_factors` (JSON), `recommendation_rationale` |
| `TumorBoardSession` | clinical_decision_support | `cancer_analysis_fk`, `lead_oncologist`, `status`, `notes`, `scheduled_date` |
| `TumorBoardMember` | clinical_decision_support | `session_fk`, `doctor_fk`, `role` |
| `TumorBoardAuditLog` | clinical_decision_support | `session_fk`, `action`, `doctor_fk`, `timestamp` |
| `ToxicityPrediction` | clinical_decision_support | `drug_regimen`, `overall_risk`, organ-specific risk scores |
| `DoctorSymptomMonitor` | clinical_decision_support | `doctor_fk`, `patient_fk`, `symptom_field`, `threshold_severity` |
| `PatientSymptomLog` | patient_portal | 15+ symptom fields (fatigue, pain, nausea, etc.), `overall_severity`, `doctor_reviewed` |
| `PatientAlert` | patient_portal | `alert_type`, `message`, `is_read`, `created_at` |
| `PatientTreatmentExplanation` | patient_portal | `treatment_plan_fk`, `plain_language_summary`, `why_this_treatment` |
| `PatientSideEffectInfo` | patient_portal | `treatment_plan_fk`, `side_effect_name`, `description`, `management_tips` |
| `DoctorAvailability` | patient_portal | `doctor_fk`, `weekday`, `start_time`, `end_time`, `slot_duration_minutes` |
| `ConsultationRequest` | patient_portal | `patient_fk`, `doctor_fk`, `request_type`, `status`, `preferred_date` |
| `Consultation` | patient_portal | `request_fk`, `scheduled_datetime`, `call_status`, `meeting_notes` |
| `VideoCallSession` | patient_portal | `consultation_fk`, `call_type` (WebRTC/Agora), `duration`, `recording_url` |
| `Prescription` | patient_portal | `consultation_fk`, `diagnosis`, `notes`, `pdf_file`, `pdf_hash`, `blockchain_tx_hash`, `qr_code` |
| `PrescriptionMedicine` | patient_portal | `prescription_fk`, `medicine_name`, `generic_name`, `dosage`, `frequency`, `duration`, `instructions` |
| `Badge` | patient_portal | `name`, `description`, `icon`, `badge_type`, `points_required` |
| `UserBadge` | patient_portal | `user_fk`, `badge_fk`, `awarded_at` |
| `UserProgress` | patient_portal | `user_fk`, `total_points`, `current_level`, `streak_days` |
| `HealthChallenge` | patient_portal | `title`, `description`, `challenge_type`, `target_value`, `reward_points` |
| `ChallengeParticipation` | patient_portal | `user_fk`, `challenge_fk`, `progress`, `completed`, `completed_at` |
| `ActivityFeed` | patient_portal | `user_fk`, `activity_type`, `description`, `timestamp` |
| `PatientNotificationPreference` | patient_portal | `user_fk`, `email_enabled`, `telegram_enabled`, `in_app_enabled` |
| `ChatSession` | medical_chatbot | `patient_fk`, `title`, `is_active`, `created_at` |
| `ChatMessage` | medical_chatbot | `session_fk`, `role` (user/assistant/system), `content`, `timestamp` |
| `UserMedicalContext` | medical_chatbot | `patient_fk`, `context_json`, `updated_at` |
| `MedicineIdentification` | medicine_identifier | `patient_fk`, `image`, `ocr_text`, `identified_name`, `generic_name`, `uses`, `side_effects`, `warnings`, `interactions` |
| `MedicineDatabase` | medicine_identifier | `medicine_name`, `generic_name`, `full_details` (JSON), `last_updated` |
| `GovernmentScheme` | Insurance_SIP | `name`, `scheme_type`, `description`, `coverage`, `benefits`, `application_steps` |
| `InsurancePolicy` | Insurance_SIP | `provider`, `policy_type`, `premium_amount`, `coverage_amount`, `min_age`, `max_age` |
| `Eligibility` | Insurance_SIP | `min_age`, `max_age`, `income_limit`, `eligible_states`, `gender` |
| `Application` | Insurance_SIP | `patient_fk`, `status`, `razorpay_payment_id`, `submitted_at` |

---

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/callback/` | Supabase OAuth token exchange |
| GET | `/api/nearby-clinics/` | Geolocation-based clinic discovery |
| POST | `/api/voice-assistant/` | Voice/text navigation |
| GET | `/auth/qr/scan/<token>/` | Doctor scans patient QR (logs to blockchain) |
| GET | `/blockchain/refresh-status/` | Blockchain connection health check |

### Cancer Detection
| Method | Endpoint | Description |
|---|---|---|
| POST | `/cancer-detection/upload/` | Upload image → AI analysis |
| POST | `/cancer-detection/analyses/<id>/treatment-plan/` | Generate treatment plan |
| GET | `/cancer-detection/api/evidence/explain/<plan_id>/` | XAI explanation |
| GET | `/cancer-detection/api/evidence/search/` | Evidence database search |
| POST | `/cancer-detection/api/evidence/ingest-studies/` | Ingest external studies |

### Patient Portal
| Method | Endpoint | Description |
|---|---|---|
| GET | `/portal/api/alerts/count/` | Unread alert count |
| GET | `/portal/api/symptoms/trend/` | Symptom trend chart data |
| POST | `/portal/call/<id>/offer/` | WebRTC offer signaling |
| POST | `/portal/call/<id>/answer/` | WebRTC answer signaling |
| POST | `/portal/call/<id>/ice/` | ICE candidate exchange |
| GET | `/portal/call/<id>/agora-token/` | Agora RTC token generation |
| POST | `/portal/prescription/<id>/verify/` | Verify prescription on-chain |

### Medical Chatbot
| Method | Endpoint | Description |
|---|---|---|
| POST | `/chatbot/send/` | Send chat message |
| POST | `/chatbot/new-session/` | Create new session |

### Medicine Identifier
| Method | Endpoint | Description |
|---|---|---|
| POST | `/medicine/upload/` | Upload medicine image → identification |

### Insurance
| Method | Endpoint | Description |
|---|---|---|
| GET | `/insurance/check-eligibility/` | Eligibility check form |
| GET | `/insurance/payment/<id>/` | Razorpay payment page |

---

## External Integrations

### Supabase
- **Auth**: All OAuth flows go through Supabase (Google Sign-In, magic links). The JS client on the frontend captures the token fragment after redirect, then POSTs to `/auth/callback/` where Django creates or retrieves the local user and establishes a session.
- **Database**: Supabase PostgreSQL is the production database. SQLite is used in development when `USE_LOCAL_DB=true`.
- **Storage**: `SupabaseStorage` is a custom Django storage backend (`authentication/supabase_storage.py`) configured for media file uploads to a specified bucket.

### Telegram Bot
Patients link their Telegram account by sharing their `telegram_chat_id` in their profile. `TelegramBotService` (`patient_portal/telegram_service.py`) sends HTTP requests to `https://api.telegram.org/bot<token>/sendMessage` for:
- Symptom severity alerts
- New consultation confirmations
- Prescription issuance notices
- QR code scan notifications

Setup scripts:
- `setup_telegram_webhook.py` — registers the bot's webhook URL with Telegram
- `link_telegram_manual.py` — helper to manually link a Telegram account for testing

### Agora RTC
Token generation uses the Agora token builder (`agora_token_builder` package) with `AGORA_APP_ID` and `AGORA_APP_CERTIFICATE`. Tokens are short-lived and generated per call session at `/portal/call/<id>/agora-token/`.

### Razorpay
Insurance premium payments use the Razorpay Python SDK. Order is created server-side with the policy premium amount; the frontend Razorpay.js handles the checkout flow; the callback verifies the `razorpay_signature` with HMAC-SHA256 before marking the application as paid.

---

## Project Structure

```
ArogyaX/
├── manage.py
├── requirements.txt
├── yolov8n.pt                          # YOLOv8 nano weights (tumor detection)
├── fix_prescription_hashes.py          # Utility: rebuild blockchain hashes
├── setup_telegram_webhook.py           # Telegram webhook registration
├── link_telegram_manual.py             # Manual Telegram account linking
├── setup_jason_telegram.py             # Telegram setup helper
├── test_telegram_notification.py       # Notification test script
│
├── cancer_treatment_system/            # Django project config
│   ├── settings.py
│   ├── urls.py                         # Root URL configuration
│   ├── wsgi.py
│   └── asgi.py
│
├── authentication/                     # User auth, profiles, QR, voice assistant
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── forms.py
│   ├── qr_utils.py                     # QR code generation + encryption
│   ├── qr_views.py                     # QR dashboard + scan endpoint
│   ├── voice_assistant.py              # Groq-powered navigation assistant
│   ├── supabase_client.py              # Supabase client factory
│   ├── supabase_storage.py             # Custom Django storage backend
│   ├── context_processors.py           # Injects Supabase config into templates
│   ├── management/                     # Django management commands
│   ├── migrations/
│   └── templates/authentication/
│
├── cancer_detection/                   # Core AI diagnostics + treatment planning
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── ml_analyzer.py                  # YOLOv8 + OpenCV image analysis
│   ├── groq_analyzer.py                # Groq histopathology/genomics analysis
│   ├── groq_treatment_planner.py       # Groq treatment plan generation
│   ├── histopathology_analyzer.py      # PDF OCR + parsing pipeline
│   ├── genomics_analyzer.py            # Genomic data processing
│   ├── opencv_analyzer.py              # OpenCV image pre-processing
│   ├── outcome_predictor.py            # ML outcome prediction model
│   ├── evidence_ingester.py            # Ingest external clinical studies
│   ├── evidence_retriever.py           # Evidence search and ranking
│   ├── evidence_integration.py         # Evidence ↔ treatment plan linking
│   ├── evidence_models.py              # Evidence database models
│   ├── evidence_views.py               # Evidence API views
│   ├── evidence_web_views.py           # Evidence web views
│   ├── rule_based_references.py        # Oncology rule-based knowledge base
│   ├── treatment_planner.py            # Treatment plan orchestrator
│   ├── management/                     # Django management commands
│   ├── migrations/
│   └── templates/cancer_detection/
│
├── clinical_decision_support/          # Doctor-only: XAI, confidence, tumor board
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── ai_services.py                  # Confidence scoring + XAI generation
│   ├── toxicity_service.py             # Chemo toxicity prediction
│   ├── migrations/
│   └── templates/clinical_decision_support/
│
├── patient_portal/                     # Patient hub: symptoms, consultations, Rx
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── call_views.py                   # WebRTC + Agora signaling
│   ├── prescription_pdf.py             # PDF generation
│   ├── prescription_verification.py    # Blockchain hash verification
│   ├── consultation_token_pdf.py       # Consultation token PDF
│   ├── telegram_service.py             # Telegram Bot HTTP wrapper
│   ├── gamification_service.py         # Badge awarding engine
│   ├── offline_sync_views.py           # Offline/PWA sync endpoints
│   ├── signals.py                      # Django signals for alerts + badges
│   ├── migrations/
│   └── templates/patient_portal/
│
├── medical_chatbot/                    # Groq LLM chatbot with patient context
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── chatbot_service.py              # Groq API wrapper + context injection
│   ├── context_builder.py              # Builds patient medical context
│   ├── migrations/
│   └── templates/medical_chatbot/
│
├── medicine_identifier/                # Medicine identification via OCR + Groq
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── image_analyzer.py              # OpenCV + EasyOCR + Tesseract pipeline
│   ├── groq_medicine_service.py       # Groq identification
│   ├── migrations/
│   └── templates/medicine_identifier/
│
├── Insurance_SIP/                      # Government schemes + insurance
│   ├── Insurance_SIP/                  # Inner app package
│   └── migrations/
│
├── blockchain/                         # Ethereum smart contract integration
│   ├── blockchain_service.py           # Web3.py wrapper (BlockchainService class)
│   ├── status_updater.py              # Background blockchain health polling
│   ├── contract_abi.json              # MedicalAccessLogger ABI
│   ├── deployment_info.json           # MedicalAccessLogger address
│   ├── medical_access_logger_abi.json # Alternative ABI file
│   ├── consultation_token_abi.json    # ConsultationTokenVerifier ABI
│   ├── consultation_token_deployment_info.json
│   ├── contracts/                     # Solidity source files
│   └── scripts/                       # Deployment scripts
│
├── media/
│   └── cancer_images/                 # Uploaded medical images
│
├── templates/                         # Global base templates
│   ├── base.html
│   ├── base_call.html
│   └── partials/
│
└── utils/                             # Shared utilities
    └── geocoding.py                   # Lat/lng lookup for nearby clinics
```

---

## Installation & Setup

### Prerequisites

- Python 3.10+
- pip
- PostgreSQL (or use SQLite for development)
- Tesseract OCR installed on the system ([download](https://github.com/UB-Mannheim/tesseract/wiki))
- Git

### Step 1: Clone and Create Virtual Environment

```bash
git clone <repository-url>
cd ArogyaX
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

> **Note**: PyTorch installation may require a separate command depending on your CUDA version. Visit [pytorch.org](https://pytorch.org) for the correct command. The YOLOv8 model will use CUDA automatically if available, otherwise falls back to CPU.

### Step 3: Configure Environment Variables

Copy the template below into a `.env` file in the project root and fill in all values:

```env
# See Environment Variables section below for full reference
SECRET_KEY=your-django-secret-key
USE_LOCAL_DB=true
GROQ_API_KEY=your-groq-api-key
# ... (see full list below)
```

### Step 4: Database Setup

```bash
# Development (SQLite)
USE_LOCAL_DB=true python manage.py migrate

# Production (Supabase PostgreSQL)
python manage.py migrate
```

### Step 5: Create Superuser

```bash
python manage.py createsuperuser
```

### Step 6: Collect Static Files (production)

```bash
python manage.py collectstatic
```

### Step 7: Run Development Server

```bash
python manage.py runserver
```

Visit `http://localhost:8000` to access the platform.

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# ─── Django Core ─────────────────────────────────────────────
SECRET_KEY=your-very-long-random-django-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# ─── Database ────────────────────────────────────────────────
# Set to 'true' to use SQLite locally, 'false' for Supabase PostgreSQL
USE_LOCAL_DB=true
DB_HOST=db.your-project.supabase.co
DB_NAME=postgres
DB_USER=postgres
DB_PASSWORD=your-db-password
DB_PORT=5432

# ─── Supabase (Auth + Storage) ───────────────────────────────
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-supabase-anon-key
SUPABASE_SERVICE_KEY=your-supabase-service-role-key
SUPABASE_STORAGE_BUCKET=media
SITE_URL=http://localhost:8000

# ─── AI / LLM ────────────────────────────────────────────────
GROQ_API_KEY=gsk_your-groq-api-key

# ─── Blockchain (Ethereum Sepolia) ───────────────────────────
ALCHEMY_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/your-api-key
BLOCKCHAIN_PRIVATE_KEY=0xyour-private-key-hex
BLOCKCHAIN_CONTRACT_ADDRESS=0xMedicalAccessLoggerAddress
PRESCRIPTION_CONTRACT_ADDRESS=0xPrescriptionVerifierAddress
CONSULTATION_TOKEN_CONTRACT_ADDRESS=0xConsultationTokenVerifierAddress
BLOCKCHAIN_ENABLED=True

# ─── Notifications ───────────────────────────────────────────
TELEGRAM_BOT_TOKEN=1234567890:your-telegram-bot-token
WEB_APP_URL=http://localhost:8000

# ─── Email (Gmail SMTP) ──────────────────────────────────────
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-gmail-app-password

# ─── Payments ────────────────────────────────────────────────
RAZORPAY_KEY_ID=rzp_test_your-key-id
RAZORPAY_KEY_SECRET=your-razorpay-key-secret

# ─── Video Calling ───────────────────────────────────────────
AGORA_APP_ID=your-agora-app-id
AGORA_APP_CERTIFICATE=your-agora-app-certificate
```

> **Security**: Never commit `.env` to version control. Always store `BLOCKCHAIN_PRIVATE_KEY` and `SUPABASE_SERVICE_KEY` in a secrets manager in production.

---

## Smart Contracts

The three Solidity contracts live in `blockchain/contracts/` and are deployed to the Ethereum Sepolia testnet.

### Deployment

```bash
# Install py-solc-x and compile contracts
cd blockchain
python scripts/deploy.py
```

Deployment writes the contract address and ABI to the corresponding JSON files (`deployment_info.json`, `consultation_token_deployment_info.json`). These addresses must then be set in your `.env` file.

### Verifying a Prescription On-Chain

Anyone (patient, pharmacist, regulator) can verify a prescription without trusting the platform:

1. Download the prescription PDF from the patient portal
2. Navigate to `/portal/prescription/<id>/verify/` or upload the PDF directly
3. The platform computes SHA-256 of the uploaded PDF and calls `PrescriptionVerifier.verify(hash)` on Sepolia
4. A green/red result is returned with the confirmation transaction details

---

## User Roles

### Patient
- Registers with email or Google (via Supabase)
- Completes `PatientProfile` (DOB, blood group, emergency contact, etc.)
- Accesses: Health Hub, Treatment Center, Chatbot, Medicine Identifier, Consultations, Prescriptions, Insurance, Gamification
- Cannot access: Cancer Detection analysis, Clinical Decision Support, Tumor Board, AI Confidence Dashboard

### Doctor
- Registers with email or Google; submits KYC documents
- Completes `DoctorProfile` (specialty, hospital, fee, coordinates)
- Accesses: Cancer Detection, Clinical Decision Support, Tumor Board, Patient list, Prescription issuance
- Cannot access: Patient symptom logs (unless monitoring), Insurance application flow

### Admin
- Full Django admin access
- Manages `DoctorKYC` verification, user oversight, scheme/policy management
- Blockchain status monitoring via admin dashboard

---

## Security

- **Authentication**: Supabase OAuth (PKCE flow); Django session backend; CSRF protection on all POST endpoints
- **Role Enforcement**: Custom `@patient_required` and `@doctor_required` decorators applied to all role-sensitive views; cross-role access returns `403 Forbidden`
- **Blockchain Keys**: Private key loaded exclusively from environment variable; never hardcoded or logged
- **QR Token Encryption**: Patient QR tokens are encrypted with Fernet symmetric encryption before being embedded in QR codes; expiry is enforced server-side
- **Prescription Hashes**: SHA-256 computed server-side from the raw PDF bytes; stored on-chain for tamper-evidence
- **Razorpay Signatures**: Webhook/callback signature verified with HMAC-SHA256 before processing any payment
- **Input Validation**: Uploaded files (images, PDFs) are validated for MIME type and size before being processed by AI pipelines
- **SQL Injection**: Django ORM parameterized queries used exclusively; no raw SQL string interpolation
- **XSS**: Django template auto-escaping enabled; `{% autoescape on %}` in all templates

---

## Utilities & Scripts

| Script / Module | Purpose |
|---|---|
| `fix_prescription_hashes.py` | Re-compute and re-anchor blockchain hashes for existing prescriptions (run after migration) |
| `setup_telegram_webhook.py` | Register the bot's webhook URL with the Telegram Bot API |
| `link_telegram_manual.py` | Manually link a Telegram `chat_id` to a patient account for testing |
| `test_telegram_notification.py` | Send a test Telegram message to verify bot configuration |
| `authentication/qr_utils.py` | Fernet encryption/decryption for QR tokens; QR image generation with `qrcode` library |
| `authentication/supabase_storage.py` | Custom `Storage` class for Django to use Supabase buckets for `MEDIA_ROOT` |
| `authentication/context_processors.py` | Injects `SUPABASE_URL` and `SUPABASE_KEY` into every template context (required by Supabase JS client) |
| `patient_portal/gamification_service.py` | Evaluates badge award conditions and creates `UserBadge` records |
| `patient_portal/signals.py` | `post_save` on `PatientSymptomLog` → create alerts, trigger Telegram, award badges |
| `cancer_detection/rule_based_references.py` | Curated oncology knowledge base: NCCN guideline references, standard-of-care rules by cancer type and stage |
| `cancer_detection/evidence_ingester.py` | Fetches and ingests studies from external clinical trial sources into the evidence database |
| `blockchain/status_updater.py` | Background thread that polls `BlockchainService.is_connected()` and updates a status flag readable by the admin dashboard |
| `utils/geocoding.py` | Converts address strings to lat/lng coordinates using a geocoding service; used for populating `DoctorProfile` coordinates |

---

## Stats at a Glance

| Metric | Value |
|---|---|
| Django Apps | 9 |
| Database Models | 35+ |
| Ethereum Smart Contracts | 3 (Sepolia testnet) |
| LLM Use Cases | 7 (treatment, histopath, genomics, chatbot, medicine, voice, XAI narrative) |
| AI/ML Pipelines | YOLOv8, OpenCV (CUDA), EasyOCR, Tesseract, scikit-learn |
| External Service Integrations | 7 (Supabase, Alchemy, Groq, Telegram, Razorpay, Agora, Gmail) |
| Target Market | India (IST, Indian government schemes, Razorpay INR payments) |
| Database (dev) | SQLite |
| Database (prod) | Supabase PostgreSQL with SSL |

---

<div align="center">
Built for better cancer care outcomes.
</div>
