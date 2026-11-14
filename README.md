<div align="center">

# 🍼 Poshan Mitra AI (पोषण मित्र AI)
### *AI-Powered Child Nutrition & Early At-Risk Malnutrition (SAM/MAM) Detection for Anganwadi Workers*

[![React 19](https://img.shields.io/badge/React-19-blue?style=for-the-badge&logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-Vite-blue?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS v4](https://img.shields.io/badge/Tailwind_CSS-v4-38B2AC?style=for-the-badge&logo=tailwind-css)](https://tailwindcss.com/)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_%26_Firestore-FFCA28?style=for-the-badge&logo=firebase)](https://firebase.google.com/)
[![Gemini AI](https://img.shields.io/badge/Google_Gemini-API-8E75B2?style=for-the-badge&logo=google)](https://ai.google.dev/)

*Unifying fragmented attendance, ration (THR), anthropometry, and household signals into one clear, actionable follow-up step in **Hindi (हिन्दी)**, **Pure Bhojpuri (शुद्ध भोजपुरी)**, and **English**.*

</div>

---

## 🌟 The Challenge & The Solution

### 🛑 The Problem
Anganwadi workers (**दीदी**) often struggle to catch children sliding toward Moderate Acute Malnutrition (MAM) or Severe Acute Malnutrition (SAM) early because critical operational signals sit in separate, disconnected registers:
1. **Center Attendance:** Consecutive absences or low monthly presence.
2. **Take-Home Ration (THR):** Missed or partial rations.
3. **Health & Growth:** Weight drop/stagnation, height, MUAC tape mm, missed immunizations.
4. **Illness & Household Context:** Diarrhea, fever, loss of appetite, seasonal migration, or household food shortages.

### ✨ The Solution (`Poshan Mitra AI`)
A unified smart workspace built for basic smartphones and tablets that pulls all 4 scattered signals together, scores emerging risk automatically using Google Gemini AI, visualizes growth trends over time, and hands the worker **one clear, practical next action** with offline resilience.

---

## 🚀 Key Features

<table>
  <tr>
    <td width="50%">
      <h3>🎯 1. Unified 4-Signal Risk Engine</h3>
      <p>Automated risk classification (<b>High Risk / SAM</b>, <b>Rising Watch / MAM</b>, <b>Healthy / Normal</b>). Provides one clear follow-up action with Web Speech API voice read-aloud and quick ad-hoc field screening.</p>
    </td>
    <td width="50%">
      <h3>📈 2. Growth Trend Charts</h3>
      <p>Interactive Recharts (ComposedChart) tracking Weight (kg) and Height (cm) across months with net delta indicators and one-tap measurement loggers.</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>🗣️ 3. Trilingual Support</h3>
      <p>Native language switcher covering UI labels, risk assessments, AI counseling responses, voice read-aloud, and PDF exports for:</p>
      <ul>
        <li>🇮🇳 <b>हिन्दी</b> (Hindi)</li>
        <li>🌾 <b>भोजपुरी</b> (Pure Bhojpuri — शुद्ध भोजपुरी)</li>
        <li>🇬🇧 <b>English</b></li>
      </ul>
    </td>
    <td width="50%">
      <h3>🤖 4. Gemini AI Counseling & Assistant</h3>
      <p>Server-side Gemini integration generating localized dietary advice (moong dal khichdi, sattu, local greens, ORS + Zinc) and multi-turn conversational chat for Anganwadi workers.</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>☁️ 5. Offline-Resilient Sync</h3>
      <p>Powered by Firebase Auth & Cloud Firestore with real-time listeners and a live sync status indicator (<b>Synced</b>, <b>Syncing</b>, <b>Queued</b>, <b>Offline</b>) for low-connectivity rural zones.</p>
    </td>
    <td width="50%">
      <h3>📄 6. PDF Report Generator</h3>
      <p>Export individual child nutrition reports or center-wide summaries as clean PDFs stamped with worker profiles and Anganwadi center credentials via <code>jspdf</code> & <code>html2canvas</code>.</p>
    </td>
  </tr>
</table>

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 19, TypeScript, Vite 8, Tailwind CSS v4, Lucide Icons, Motion |
| **Data Visualization** | Recharts (`ComposedChart`, `ResponsiveContainer`) |
| **Backend Server** | Node.js, Express (`server.ts` with Vite dev middleware & static prod serving) |
| **AI Integration** | `@google/genai` (Server-side Gemini API proxy routes) |
| **Database & Auth** | Firebase Authentication (Google Sign-In), Cloud Firestore |
| **Export Utilities** | `jspdf`, `html2canvas-pro` |

---

## 📁 Project Architecture

```text
poshan-mitra-ai/
├── server.ts                        # Express server + Gemini API endpoints + Vite middleware
├── index.html                       # HTML entry point & Devanagari/Latin font setup
├── metadata.json                    # App metadata & capabilities
├── firebase-blueprint.json          # Firestore schema blueprint (IR)
├── firebase-applet-config.json      # Firebase project & Firestore database config
├── firestore.rules                  # Hardened Firestore security rules
├── package.json                     # Dependencies & scripts
├── .env.example                     # Environment variable template
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
    │   └── initialChildren.ts       # Initial sample records for onboarding
    └── components/
        ├── LoginPage.tsx            # Google Sign-In screen
        ├── TopBar.tsx               # Header navigation & offline/Firestore sync indicator
        ├── BottomNav.tsx            # Mobile bottom tab navigation
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
