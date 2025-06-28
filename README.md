# Maptica

**Maptica** is a web-based collaborative fantasy map editor built for writers, indie game developers, and worldbuilding hobbyists. It offers an intuitive canvas with fantasy-themed brushes, offline-first editing, export controls, and a hybrid monetization system combining subscriptions and credits.

---

## Features

- Canvas-based editor powered by Konva
- Fantasy brushes: mountains, forests, rivers, and cities
- Offline-first map creation with IndexedDB
- Guest mode: start drawing without login
- Export to PNG (2K/4K/8K, watermark based on tier)
- Save and sync maps with Supabase (for logged-in users)
- Real-time collaboration via y-webrtc (Pro users only)
- Credit-based system with monthly allocations and asset store
- Custom asset upload for premium users

---

## Tech Stack

- **Frontend:** SvelteKit + TypeScript + TailwindCSS + shadcn-svelte
- **Canvas Engine:** Konva
- **State & Storage:** IndexedDB, Supabase
- **Realtime:** Yjs + y-webrtc
- **Auth & Backend:** Supabase
- **Payments:** Zendit (supports international + Indonesia)
- **Deployment:** Vercel

---

## Project Structure

```sh
src/
├── lib/               # Utilities and shared logic
├── components/        # UI components
├── features/          # Core modules (canvas, credits, auth, collab)
├── routes/            # Application routes (SvelteKit)
└── hooks/             # Lifecycle bindings and event handlers
```

---

## Development Setup

Clone the repository and install dependencies using your preferred package manager:

```bash
# Using npm
git clone https://github.com/KaisAbiyyi/maptica.git
cd maptica
npm install
npm run dev

# Using pnpm
pnpm install
pnpm dev

# Using bun
bun install
bun dev
```

Create a `.env` file with your Supabase and Zendit credentials.

---

## Roadmap Highlights

- MVP with guest mode, drawing tools, 2K export
- Monthly credit refresh for free users
- Pro users unlock high-res export, collaboration, and asset store
- Public map gallery and team roles in post-MVP

See full roadmap in `ROADMAP.md`

---

## License & Usage

- Free users are limited to personal use.
- Cartographer tier: non-commercial use + extra credits.
- Worldsmith tier: full commercial use license + unlimited assets.

See `LICENSE.md` and `TERMS.md` for more.

---

## Contributing

Contributions welcome after MVP release. Codebase is modular and follows SOLID principles.

---

## Credits & Inspiration

- Inspired by Excalidraw (collaboration model), Inkarnate (UX), and Canva (monetization).
- Powered by open source and modern web standards.

---

## Contact

For feedback, reach out at: [business.kaisabiyi@gmail.com](mailto\:business.kaisabiyi@gmail.com)

