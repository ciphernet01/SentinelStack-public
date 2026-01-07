# Public Google Integration Starter

A minimal, public-safe starter that demonstrates **Google tech integration only**:

- **Firebase Auth (client)**: Google sign-in
- **Firebase Admin (server)**: verify ID tokens
- **Genkit + Gemini**: a simple `summarize` example

This repo intentionally contains **no proprietary scanning/engine logic**.

## 1) Setup

### Prereqs
- Node.js 18+

### Install
```bash
npm install
```

### Configure env
Copy:
```bash
cp .env.example .env
```
Fill in values:
- `NEXT_PUBLIC_FIREBASE_*` from Firebase Console → Project settings → Web app
- `FIREBASE_*` from a Firebase service account (server-side)
- `GEMINI_API_KEY` from Google AI Studio

Notes (matches the MVP approach):
- The client tries `initializeApp()` with no args first (Firebase App Hosting can inject config in production).
- In local dev, it falls back to explicit `NEXT_PUBLIC_FIREBASE_*` env vars.

> Important: Never commit `.env` or service account JSON.

## 2) Run
```bash
npm run dev
```
Open `http://localhost:3000`.

## 3) What to try
- Click **Sign in with Google**
- Enter any text and press **Summarize with Gemini**

The UI sends a Firebase ID token to `/api/ai/summarize`.
The server verifies the token using Firebase Admin, then calls Genkit/Gemini.

### API
- `POST /api/ai/summarize`
	- Headers: `Authorization: Bearer <firebase_id_token>`
	- Body: `{ "text": "..." }`
	- Response: `{ "summary": "..." }`

## Safety Notes
- This starter is designed to be safe for public GitHub.
- It uses placeholders and generic flows; add your private logic in a separate private repo.
