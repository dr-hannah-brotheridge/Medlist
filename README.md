# MedList PWA: Lightweight Medication Compliance Engine

A clinical, user-centric Progressive Web App (PWA) designed to simplify medication tracking, prevent compliance errors, and provide seamless data collation for patient-doctor check-ups. 

I am an Applied AI Systems Architect, so I prioritise rapid prototyping and robust data guardrails over manual syntax typing. I architected the relational database schema in Supabase PostgreSQL, implemented Row-Level Security (RLS) to protect clinical data privacy, and used FlutterFlow as an agile compiler for the frontend canvas. For specialised backend behaviours like our automated PDF compilation—I built and deployed targeted TypeScript Edge Functions via the Supabase CLI.

## 🛠️ Core Functional Architecture

### 1. Progressive Web App Infrastructure
Built as a highly accessible frontend application designed to operate seamlessly across mobile devices and desktops.
* **Offline First Capability:** Caches critical medication schedules locally on the device using Service Workers, ensuring patients can log compliance data even without an active internet connection.
* **Zero-Install Deployment:** Installs directly from a web browser onto a smartphone home screen, bypassing app store friction for elderly or non-tech-savvy users.

### 2. Clinical Data Structure & Tracking
Designed around human-factors engineering to minimize cognitive load during active medical treatments:
* **Structured Dosing Windows:** Logs entries under strict timestamp anchors, mapping compliance accuracy over time.
* **Medication Information Collation:** Organizes active prescriptions into clear, readable formats ready to be exported directly during a clinical consultation.

## 🗄️ Backend Data Architecture (Supabase PostgreSQL)

The relational database layer is managed via Supabase, enforcing strict integrity constraints for medical logging data.

### 1. Database Schema Layout

#### `users` Table
* `id` (uuid, primary key) -> Links directly to Supabase Auth.
* `clinical_identifier` (text) -> Anonymous hash used to segment patient metadata safely.

#### `medications` Table
* `id` (bigint, primary key)
* `user_id` (uuid, foreign key -> users.id) -> Ensures strict data isolation.
* `medication_name` (text) -> Standardized string.
* `dosage_instruction` (text) -> (e.g., "Take 1 tablet in the morning").
* `created_at` (timestamp)

### 2. Row Level Security (RLS) Policies
To maintain clinical privacy boundaries, **Row Level Security (RLS)** is explicitly enabled on all tables. Users are cryptographically barred from querying or modifying rows that do not match their verified `auth.uid()` token payload.

### 3. Serverless Edge Infrastructure
* **Automated Document Compilation:** Deployed an isolated **TypeScript Edge Function** via the Supabase CLI. This service interceptively fetches user-specific relational rows to dynamically compile, structure, and deliver audit-ready compliance history report PDFs directly to the client interface.

## 🚀 Next Phases of Development
- **API Orchestration Layer:** Integrating the NZULM or MedSafe medication list as an automatically updating API.
- **Automated Summarisation:** Implementing a structured pipeline to export compliance history directly into standard GP consultation templates.
