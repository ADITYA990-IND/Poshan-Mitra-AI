# Poshan Mitra Ai (पोषण मित्र AI)

> **Child Nutrition & Early At-Risk Malnutrition (SAM/MAM) Detection for Anganwadi Workers** — Unifying fragmented attendance, ration (THR), anthropometry, and household signals into **one clear follow-up action** in **Hindi (हिन्दी)**, **Bhojpuri (शुद्ध भोजपुरी)**, and **English**.

---

## Why Poshan Mitra Ai?

### The Challenge
Anganwadi workers (दीदी) often miss early warning signs when a child slides toward **Moderate Acute Malnutrition (MAM)** or **Severe Acute Malnutrition (SAM)** because critical signals sit in separate, disconnected registers:
1. **Center Attendance** (consecutive absences or low monthly presence)
2. **Take-Home Ration (THR) Uptake** (missed or partial rations)
3. **Health & Growth Measurements** (Weight drop/stagnation, Height, MUAC tape mm, missed immunization)
4. **Illness & Household Context** (diarrhea, fever, loss of appetite, food shortage, seasonal migration, mother unwell, missed IFA)

### The Solution
**Poshan Mitra Ai** pulls all 4 scattered signals into a single smartphone- and laptop-friendly workspace, scores emerging risk automatically, visualizes growth history over time, and gives the worker **one clear, practical next action**—with AI-powered mother counseling scripts, offline-resilient Firestore sync, and downloadable PDF reports.

---

## Key Features

### 1. Unified 4-Signal Risk Engine & Clear Action
- Combines **Attendance**, **Ration/THR**, **Weight/Height/MUAC**, and **Illness/Household** flags into real-time risk classification (**High Risk / SAM**, **Rising Watch / MAM**, **Healthy / Normal**).
- Highlights **One Clear Follow-Up Action** with urgency level, voice read-aloud (`Web Speech API`), and one-tap **Mark Action Done** logging into the child's follow-up history.
- Includes **Quick Risk Check** (`त्वरित जांच`) for rapid ad-hoc screening during field visits.

### 2. Nutritional Growth Trend Charts
- Interactive **Recharts** (`ComposedChart`) inside every child's workspace plotting **Weight (kg)** and **Height (cm)** across months.
- Metric view switcher (**Both**, **Weight Only**, **Height Only**) with net weight/height delta indicators and one-tap measurement logging.

### 3. Multilingual Support: Hindi, Pure Bhojpuri & English
- Instant language switcher supporting:
  - **हिन्दी (Hindi)**
  - **भोजपुरी (Pure Bhojpuri — शुद्ध भोजपुरी)**
  - **English**
- Covers UI labels, risk assessment messages, AI counseling responses, voice read-aloud, and exported PDF reports.

### 4. AI Counseling & Assistant Chat (Server-Side Gemini)
- **Mother Counseling Generator (`/api/analyze-child`)**: Generates concise, locally grounded nutrition advice (moong dal khichdi, sattu, seasonal greens, peanut/jaggery, ORS + Zinc) tailored to the child's combined signals.
- **Poshan Assistant Chat (`/api/chat`)**: Multi-turn conversational assistant for Anganwadi workers with child-context awareness and fast-response mode toggle.
- **Nutrition Guide**: Built-in reference guide for local nutrient-dense foods, SAM/MAM thresholds, and hygiene/ORS practices.

### 5. Offline-Resilient Sync & Cloud Persistence (Firebase)
- Backed by **Firebase Authentication (Google Sign-In)** and **Cloud Firestore** with real-time snapshot listeners (`includeMetadataChanges`).
- **Live Sync Status Indicator** in the top bar (**Synced**, **Syncing**, **Queued**, **Offline**) so workers in low-connectivity areas know whether edits are safely stored locally and awaiting upload or synced to Firestore.

### 6. Downloadable PDF Nutrition Reports
- Export **Individual Child Nutrition Reports** or a **Center-Wide Summary Report** as clean PDFs (`jspdf` + `html2canvas-pro`), automatically stamped with the worker's profile and Anganwadi center details.

### 7. Worker Profile & Privacy-First Community Feedback
- **Editable Worker Profile**: Manage display name, center code, profile photo (with client-side compression), mobile number, email, gender, and address. Private PII fields are isolated in `/users/{userId}/private/profile`.
- **Shared Community Feedback**: Workers can rate the app (**1–5 stars**) and submit written feedback visible across all signed-in accounts—strictly storing **display name only** (zero email, mobile number, or address stored or exposed).

### 8. Responsive Across Mobile, Tablet & Desktop
- Touch-first ergonomics (`44px+` minimum hit targets), mobile bottom tab navigation (`BottomNav`), desktop/laptop workspace toolbar, and automatic portrait/landscape adaptation.

---

## Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 19, TypeScript, Vite 8, Tailwind CSS v4, Lucide Icons, Motion |
| **Data Visualization** | Recharts (`ComposedChart`, `ResponsiveContainer`) |
| **Backend Server** | Node.js, Express (`server.ts` with Vite dev middleware & static prod serving) |
| **AI Integration** | `@google/genai` (server-side Gemini API proxy routes) |
| **Database & Auth** | Firebase Authentication (Google Sign-In), Cloud Firestore |
| **PDF Export** | `jspdf`, `html2canvas-pro` |

---

## Project Structure

```text
poshan-mitra-ai/
├── server.ts                        # Express server + Gemini API endpoints + Vite middleware
├── index.html                       # HTML entry point & Devanagari/Latin font setup
├── metadata.json                    # App metadata & capabilities
├── firebase-blueprint.json          # Firestore schema blueprint (IR)
├── firebase-applet-config.json      # Firebase project & Firestore database config
├── firestore.rules                  # Hardened Firestore security rules
├── package.json                     # Dependencies & scripts
├── .env.example                     # Environment variable template (no secrets)
└── src/
    ├── App.tsx                      # Root app state, auth lifecycle, Firestore sync & views
    ├── main.tsx                     # React entrypoint
    ├── index.css                    # Tailwind CSS v4 entry & typography utilities
    ├── types.ts                     # Shared TypeScript interfaces & types
    ├── i18n/
    │   └── translations.ts          # Hindi, Bhojpuri, and English UI dictionary
    ├── lib/
    │   └── firebase.ts              # Firebase initialization & structured error logging
    ├── services/
    │   └── firestoreService.ts      # Firestore CRUD & realtime subscriptions
    ├── utils/
    │   ├── riskEngine.ts            # 4-signal SAM/MAM risk scoring & action generator
    │   └── pdfReport.ts             # Individual & center PDF report generator
    ├── data/
    │   └── initialChildren.ts       # Initial sample records for first-time worker onboarding
    └── components/
        ├── LoginPage.tsx            # Google Sign-In screen
        ├── TopBar.tsx               # Header navigation & offline/Firestore sync indicator
        ├── BottomNav.tsx            # Mobile bottom tab navigation (incl. Profile & Feedback)
        ├── ChildListPanel.tsx       # Searchable & filterable child list
        ├── ChildDetailWorkspace.tsx # 4-signal editor, AI guidance, Recharts & PDF export
        ├── FollowUpQueueView.tsx    # Prioritized daily home-visit / follow-up queue
        ├── QuickRiskCheckView.tsx   # Rapid field MUAC/weight/signal screener
        ├── NutritionGuideView.tsx   # ICDS & local food nutrition reference
        ├── PoshanChatView.tsx       # Multi-turn Gemini nutrition assistant
        ├── ProfileView.tsx          # Editable worker profile & photo upload
        ├── FeedbackView.tsx         # 1–5 star community feedback & privacy-safe feed
        ├── AddChildModal.tsx        # Modal to register a new child
        └── ConfirmDeleteModal.tsx   # In-app confirmation modal for child deletion
```

---

## Firestore Data Model & Privacy Architecture

| Collection / Document Path | Purpose | Access Control (`firestore.rules`) |
| :--- | :--- | :--- |
| `/users/{userId}` | Non-PII worker display profile (`displayName`, `centerCode`, `photoUrl`) | Owner-only read & write |
| `/users/{userId}/private/profile` | Worker PII (`email`, `phone`, `gender`, `address`, `villageWard`, `districtState`, `pincode`) | Strict owner-only read & write |
| `/users/{userId}/children/{childId}` | Child nutrition records, growth history & follow-up logs | Owner-only read, create, update & delete |
| `/feedbacks/{feedbackId}` | Shared community ratings & reviews (`authorName`, `rating`, `comment`, `visibility`) | Signed-in read (`visibility == 'public'`), verified create, owner-only delete, **zero PII allowed** |

---

## API Endpoints (`server.ts`)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/analyze-child` | Evaluates a child's 4 combined signals via Gemini and returns structured JSON (`oneClearAction`, `whyFlagged`, `motherCounselingScript`, `urgencyLabel`) in `hi`, `bho`, or `en`. |
| `POST` | `/api/chat` | Multi-turn conversational nutrition assistant with optional active child context and fast-model toggle. |

---

## Getting Started (Local Development)

### 1. Prerequisites
- **Node.js** `v20+`
- **npm** (or compatible package manager)
- A **Google Gemini API Key** (from Google AI Studio)
- A **Firebase Project** with **Google Authentication** and **Cloud Firestore** enabled

### 2. Clone & Install
```bash
git clone <your-repo-url>
cd poshan-mitra-ai
npm install
```

### 3. Configure Environment Variables
Copy `.env.example` to `.env` (never commit `.env` to GitHub):
```bash
cp .env.example .env
```

Update `.env` with your values:
```env
GEMINI_API_KEY="your_gemini_api_key_here"
APP_URL="http://localhost:3000"
```

### 4. Configure Firebase
Ensure `firebase-applet-config.json` contains your Firebase web configuration (`apiKey`, `authDomain`, `projectId`, `appId`, `firestoreDatabaseId`) and deploy `firestore.rules` to your Firestore database.

> **Security Tip**: Always review and test `firestore.rules` in the Firebase Console or Emulator Suite before sharing your deployment publicly.

### 5. Run Development Server
```bash
npm run dev
```
The app and API server run together on **`http://localhost:3000`**.

### 6. Type-Check & Production Build
```bash
# Run TypeScript check
npm run lint

# Build frontend (dist/) + server bundle (server.js)
npm run build

# Start production server
NODE_ENV=production npm start
```

---

## Contributing & Pushing to GitHub

1. Verify `.env` is ignored (`.gitignore` already excludes `.env*` while keeping `!.env.example`).
2. Confirm no real API keys or personal secrets exist in `.env.example` before committing.
3. Push to your GitHub repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Poshan Mitra Ai"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```
