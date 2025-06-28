# Product Requirements Document – Maptica

## 1. Overview

**Maptica** is a web-based application designed to assist writers, game developers, and fantasy worldbuilding enthusiasts in creating fictional maps in a visual, intuitive, and collaborative way. Maptica offers a canvas-based drawing tool equipped with symbolic elements such as mountains, trees, rivers, and cities, alongside annotation features, layer management, export options, and real-time collaboration. By implementing a hybrid system of user tiers and credits, Maptica enables users to access premium features flexibly without forcing a subscription. The primary goal of the product is to deliver a fast, seamless map creation experience that is enjoyable for both free and paying users.

The project is engineered to operate entirely on Vercel, utilizing Supabase for backend services and Yjs + y-webrtc for real-time peer-to-peer collaboration. The initial development focus is to build a lightweight, responsive MVP that functions without requiring user login (guest mode), while maintaining scalability for professional use cases.

---

## 2. Goals

- Deliver a fully functional MVP that supports guest-mode map creation, drawing tools, and PNG export with basic resolution and watermark.
- Provide a frictionless map editing experience for casual users, while offering a scalable system for power users and professionals.
- Support collaborative real-time editing using peer-to-peer WebRTC without backend infrastructure cost.
- Implement a hybrid monetization model through subscriptions and credit-based transactions.
- Enable users to upgrade progressively via feature unlocks and premium asset access without mandatory subscription lock-in.
- Operate efficiently within the free tier of Vercel and Supabase during MVP phase, to minimize hosting costs.
- Lay the foundation for a sustainable and user-centric SaaS product that balances creative freedom with fair monetization.

---

## 3. Non-Goals

- Maptica will not aim to provide procedural map generation or AI-generated landscapes in its MVP.
- The platform will not include video export, animation tools, or timeline-based media editing.
- Social media integrations (e.g., Instagram share, community templates) are out of scope for the initial release.
- No support for backend-hosted collaboration servers; all real-time editing will rely on peer-to-peer methods.
- User account management will be minimal, without advanced team/organization roles during MVP.
- Multi-language/i18n support will not be prioritized until post-MVP stages.

---

## 4. Audience

This document is intended for the following stakeholders:

- **Solo developer (project owner)**: To guide design decisions, development priorities, and maintain project clarity.
- **Future collaborators or open-source contributors**: To understand the system's scope, architecture, and vision if the project is opened to the public.
- **Mentors or evaluators**: For academic, professional, or portfolio review of the product planning and execution.
- **Target users (indirectly)**: Represented in user research, to ensure the product aligns with the needs of writers, game developers, and map-making hobbyists.

---

## 5. Existing Solutions and Issues

Several digital map editors and drawing tools exist, but none fully address the unique needs of collaborative worldbuilding for fantasy settings. Tools like **Inkarnate**, **Wonderdraft**, and **Dungeon Scrawl** provide beautiful map creation features but are often desktop-based, lack real-time collaboration, or require upfront payment without free access. On the other hand, tools like **Excalidraw** support freehand collaborative drawing but lack map-specific brushes and context.

Key issues with existing solutions include:
- High learning curves or software installation requirements
- Limited or no real-time collaboration
- Absence of symbolic fantasy brushes (mountains, trees, biomes)
- Export restrictions or mandatory watermarking without context-based options
- No hybrid monetization — users must either subscribe fully or cannot access advanced features

Maptica addresses these gaps by combining web accessibility, peer-to-peer collaboration, fantasy-focused toolsets, and a user-friendly monetization model designed to feel optional and fair.

---

## 6. Assumptions

- Users will primarily access Maptica via modern desktop browsers with sufficient WebGL and canvas rendering support.
- Guest mode users will constitute a significant portion of early adopters.
- Fantasy map creators prefer manual, symbolic drawing over automated/procedural generation.
- Internet access is assumed during collaboration sessions, though offline drawing (via IndexedDB) is expected for solo mode.
- Initial usage will focus on individual worldbuilders and indie game developers rather than enterprise or education sectors.
- Monetization through microtransactions and tier-based subscriptions is acceptable as long as free usage remains valuable.
- Credit-based systems are familiar enough to users due to widespread adoption in other creative tools (e.g., Canva, Figma, Excalidraw).

---

## 7. Constraints

- The platform must operate entirely within the limits of the Vercel free tier during MVP stage, including bandwidth, build minutes, and function execution quotas.
- Supabase usage (auth, storage, database) should remain under the free quota, with hard limits on upload size and storage per user.
- IndexedDB must be leveraged for local storage without external dependencies.
- y-webrtc must be used for real-time collaboration to avoid backend server costs.
- No integration with external payment processors beyond Zendit.
- The system must not depend on native mobile app capabilities or APIs.
- Performance optimizations are required for WebGL/canvas rendering to remain responsive on mid-tier devices.

---

## 8. Key Use Cases

1. **Solo Worldbuilder (Guest Mode)**  
   A user accesses Maptica without logging in, creates a map using symbolic brushes (mountains, rivers), saves progress locally via IndexedDB, and exports a 2K PNG with watermark.

2. **Indie Game Developer (Registered User)**  
   A user logs in, creates multiple maps, uploads custom assets, and organizes map layers for a game prototype. They export maps in 4K resolution without watermark using subscription credits.

3. **Collaborative Campaign Planning**  
   Two users join a shared room via link and co-edit a map in real-time using y-webrtc. One places terrain, the other adds annotations. Edits are reflected live, no backend sync involved.

4. **Asset Collector (Pro User)**  
   A premium user purchases credit bundles to unlock unique asset packs (e.g., Jungle Pack, Castle Icons) and uses them across multiple maps.

5. **Restorer and Exporter**  
   A user restores a previously deleted map using credit and exports both standard and high-resolution versions for print or online publication.

These use cases demonstrate the flexibility of Maptica to serve both free and paying users, casual creators and professionals, while maintaining low operational cost through P2P and local-first technologies.

---

## 9. Research

### 9.1 User Research
User insights were derived from identifying common pain points in fantasy map creation tools and observing usage patterns in visual collaboration apps. Many users seek tools that are fast, don't require installation, and offer symbolic representation without a steep learning curve. Casual worldbuilders prefer freedom and minimal friction, while professionals demand export control and asset flexibility. The guest-mode first approach is designed in response to this need for accessibility.

### 9.2 Technical Research
Multiple existing tools were benchmarked, including Excalidraw (collaboration model), Canva (credit + subscription hybrid), and Inkarnate (map-specific UI). The stack was selected based on performance, scalability, and cost efficiency. IndexedDB was chosen for local persistence to enable offline-first design. Supabase was chosen for its all-in-one backend capability on a free tier. y-webrtc enables scalable real-time collaboration without requiring server hosting. Zendit was selected as the payment provider due to its compatibility with international and Indonesian payments.

