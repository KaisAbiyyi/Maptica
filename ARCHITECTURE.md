# Maptica – Technical Architecture

This document outlines the high-level architecture of Maptica, a collaborative fantasy map editor optimized for performance, offline-first use, and monetization-aware deployment.

---

## 1. Technology Stack

- **Frontend:** SvelteKit + TypeScript + TailwindCSS + shadcn-svelte
- **Canvas Engine:** Konva (for drawing and brush rendering)
- **Storage (Local):** IndexedDB (via custom wrapper or Dexie.js)
- **Realtime Collaboration:** Yjs + y-webrtc (peer-to-peer)
- **Auth & Cloud Backend:** Supabase (Auth, Database, Storage)
- **Deployment Platform:** Vercel (frontend + edge functions)
- **Payment Gateway:** Zendit (supports international and Indonesia)

---

## 2. Folder Structure Overview (Frontend)

```
src/
├── lib/               # Reusable utilities, context, constants
├── components/        # UI components (BrushSelector, Toolbar, etc.)
├── features/
│   ├── canvas/        # Canvas logic & Konva integration
│   ├── auth/          # Login, user context, Supabase session
│   ├── credits/       # Credit system UI & logic
│   ├── export/        # PNG rendering, watermarking, resolution controls
│   ├── assets/        # Asset library management
│   └── collab/        # y-webrtc setup, cursors, presence handlers
├── routes/            # App routes (home, editor, pricing)
└── hooks/             # Svelte lifecycle and event bindings
```

---

## 3. Data Flow & System Interaction

### Map Editing (Offline & Guest)

- Canvas state stored locally in IndexedDB
- On every draw/change: state autosaved (debounced) locally
- No backend write unless user logs in

### User Authentication

- Supabase handles auth (email/password, optionally OAuth)
- Auth token stored via secure cookie/session
- Logged-in users can sync maps to Supabase DB

### Credit System

- Credits stored in Supabase `user_credits` table
- Free users get 5/month (server cron job)
- Only paid users (tiered) can top up credits via Zendit
- Actions (export, upload, asset use) consume credit via edge API route

### Export

- Local rendering via Konva to `canvas.toBlob()`
- If user tier/credit allows: unlock 4K–8K export
- Watermark toggled based on tier (or forced if free)

### Asset Upload & Usage

- Custom asset upload via Supabase Storage
- Credit deducted based on file size/slot rules
- Tier controls access to marketplace & usage quota

### Real-Time Collaboration

- Yjs document created per map session
- y-webrtc handles peer sync (no backend relay)
- Shared tokenized URL grants session entry
- Presence cursors and awareness managed via Yjs

---

## 4. Edge API Endpoints (on Vercel)

- `/api/credit/consume` → Validate and deduct credits
- `/api/credit/monthly-refresh` → Run monthly credit refresh (cron)
- `/api/pay/zendit-hook` → Handle Zendit payment success
- `/api/map/share-token` → Generate share link for collaboration

---

## 5. Security & Limits

- Uploads scanned for MIME/type and size (limit by tier)
- Supabase RLS enabled: only owner can read/write maps
- Guest maps never reach backend
- Map history/versioning stored only for logged-in users

---

## 6. Scalability & CI/CD

- App runs fully on Vercel Free Plan in MVP (100GB/month bandwidth)
- Supabase scales independently (start with free tier)
- CI/CD via GitHub → Vercel auto deploy on push to `main`
- Credit & subscription logic separated in Supabase functions

---

## 7. Future Considerations

- Migrate to serverless backend (e.g., Edge Functions) if collaboration load increases
- Use Supabase Realtime for sync if P2P fails gracefully
- Implement CDN-backed asset distribution for paid packs
- Add Sentry/Monitoring in production tier

