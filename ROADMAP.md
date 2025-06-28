# Maptica – Development Roadmap

This roadmap integrates Maptica’s product delivery with a credit-first monetization strategy inspired by Vercel v0, where free users receive limited recurring credits monthly and only paid subscribers can top up or unlock unlimited access. The roadmap prioritizes scalable architecture, tier incentives, and frictionless UX.

---

## Phase 1 – Core MVP (Weeks 1–2)

- Initialize SvelteKit project with Tailwind and shadcn-svelte
- Build canvas editor with Konva + IndexedDB (offline-first)
- Add toolset UI: brush selector, basic stamps (mountain, tree, city)
- Implement PNG export (2K) with default watermark
- Enable guest mode with autosave and local load
- Setup Supabase Auth (email login) and Supabase Storage
- Deploy MVP on Vercel Free Plan

## Phase 2 – Credit System Foundation (Week 3)

- Implement credit system with frontend & Supabase tables
- Allocate 5 credits/month to Free users (non-top-up)
- Restrict credit top-up to subscribers only
- Setup credit consumption rules: export, upload, asset access
- Design visual prompt when user lacks credit (upgrade call-to-action)
- Display credit balance in UI (contextual per action)

## Phase 3 – Tier System and Zendit Integration (Week 4)

- Create subscription tiers: Cartographer (20 credit/month), Worldsmith (50 credit/month)
- Integrate Zendit for tier checkout and credit top-up payment
- Implement license differentiation: Cartographer = personal use, Worldsmith = commercial use
- Assign asset accessibility per tier (Worldsmith gets all, Cartographer selective)
- Enable watermark toggle and high-res export (gated by credit/tier)

## Phase 4 – Asset Economy and Upload (Week 5)

- Launch asset marketplace: free assets, credit-based packs
- Enable custom asset upload (credit-based)
- Introduce bonus events (e.g., login streak = 1 credit)
- Limit asset upload size/frequency per tier

## Phase 5 – Real-Time Collaboration (Week 6)

- Integrate y-webrtc and Yjs for peer-to-peer live collaboration
- Add visual indicators for presence (cursor, live activity)
- Allow shared session via tokenized public URL
- Restrict collaboration to subscribers only

## Phase 6 – UX Polish & Tier-Onboarding (Week 7)

- Build pricing page, feature comparison chart, and upgrade funnel
- Create onboarding tour per tier
- Add account dashboard: billing, usage stats, license type
- Improve mobile/responsive support for viewer/editor
- Add versioning & map history for logged-in users

## Phase 7 – Post-MVP Expansion

- Add team roles & permissions (org support)
- Launch public gallery of maps (optional search & filters)
- Internationalization (i18n support)
- Start community campaign (asset submission, contests)
