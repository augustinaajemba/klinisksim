# 🏥 KliniskSim

> AI-powered case-based clinical training simulator for Norwegian nursing students

![Version](https://img.shields.io/badge/Version-0.9%20MVP-blue)
![Status](https://img.shields.io/badge/Status-Active%20Development-green)
![Stack](https://img.shields.io/badge/Stack-React%20%7C%20Supabase%20%7C%20Anthropic-0B3D91)
![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-red)
![Language](https://img.shields.io/badge/Language-Norsk%20Bokmål-lightgrey)

---

## 📋 Table of Contents
- [About](#about)
- [Problem Statement](#problem-statement)
- [Features](#features)
- [Clinical Arenas](#clinical-arenas)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [ISO Relevance](#iso-relevance)
- [Known Issues / Roadmap](#known-issues--roadmap)
- [Disclaimer](#disclaimer)
- [Built By](#built-by)
- [License](#license)

---

## About

KliniskSim is a mobile-optimised, AI-driven training application for nursing students and healthcare professionals in Norway. The app simulates realistic clinical cases across five healthcare arenas, testing users on clinical assessment, medical decision-making, ethical reasoning, and Norwegian health law — including Pasientrettighetsloven §4A and Helsepersonelloven §4.

Cases are generated in real time using the Anthropic API (claude-sonnet-4-6) via a secure Supabase Edge Function, ensuring an unlimited supply of unique, clinically accurate scenarios. A curated bank of seed-data cases is always available offline.

> *"Bridging the gap between clinical systems and care."*

---

## Problem Statement

Nursing students in Norway lack access to structured, digital practice tools that combine:

- Realistic clinical scenarios from the Norwegian healthcare system
- Immediate, evidence-based feedback
- Integrated health law and ethics (not just biomedicine)
- Mobile accessibility during clinical placements

Existing solutions — textbooks, simulation centres — are static, expensive, or unavailable between teaching sessions. KliniskSim fills this gap with an always-available, gamified learning experience.

---

## Features

### Core
- 🏥 **5 clinical arenas** — Legevakt, Hjemmesykepleie, Sykehjem, KAD, Demensskjermet avdeling
- 🎮 **Gamified case flow** — progress bar, immediate answer feedback, scoring
- ✅ **4-choice questions** — colour-coded correct/incorrect with instant reveal
- 📖 **Clinical begrunnelser** — evidence-based explanations with Norwegian law references
- 📊 **Results summary** — score, per-step review, expandable accordion

### AI Generation
- ✨ **Unlimited case generation** via Anthropic API (server-side, secure)
- 🔄 **Background preloading** — next case generates while current case is in progress
- 💾 **Case caching** — generated cases saved to Supabase, reused instantly
- ⚡ **Fallback to seed-data** if API unavailable

### Access & Auth
- 🔐 **Supabase Auth** — email/password registration and login
- 🛡️ **Auth-guard** on all protected routes
- 👤 **Role-based profiles** — Sykepleierstudent, Sykepleier, Faglærer, Annet
- 📈 **Personal statistics** — cases completed, average score

---

## Clinical Arenas

| Arena | Clinical Focus | Legal/Ethical Focus |
|---|---|---|
| Legevakt | Acute assessment, ACS, anaphylaxis | Pasientrettigheter §3-2 |
| Hjemmesykepleie | Chronic disease, KOLS, autonomy | Samtykke §4-1, refusal of care |
| Sykehjem | Geriatrics, delirium, UVI, nutrition | Tvang §4A, documentation |
| KAD | Heart failure, hypoglycaemia, communication | Medvirkning §3-1 |
| Demensskjermet | Dementia, sundowning, falls | Tvungen helsehjelp §4A |

**Question categories per case:**
- 🩺 Klinikk — clinical observation and assessment
- 💊 Medisin — pharmacology and medical management
- ⚖️ Etikk — ethical reasoning and patient dignity
- 📜 Lovverk — Norwegian health law application

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React + Tailwind CSS |
| Database + Auth | Supabase (PostgreSQL + Auth) |
| AI Case Generation | Anthropic API — claude-sonnet-4-6 |
| Edge Functions | Supabase Edge Functions (Deno) |
| Deployment | Lovable + Vercel |
| Icons | Lucide React |

---

## Architecture

```
┌─────────────────────────────────────┐
│         React Frontend              │
│   (Tailwind, Lucide, React Router)  │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│            Supabase                 │
│  ┌──────────┐  ┌─────────────────┐  │
│  │   Auth   │  │    Database     │  │
│  │          │  │ profiles        │  │
│  └──────────┘  │ cases           │  │
│                │ resultater      │  │
│  ┌──────────┐  │ genereringer    │  │
│  │  Edge    │  │ error_logs      │  │
│  │ Function │  └─────────────────┘  │
│  │generate- │                       │
│  │  case    │                       │
│  └────┬─────┘                       │
└───────┼─────────────────────────────┘
        │
┌───────▼──────────┐
│  Anthropic API   │
│ claude-sonnet-4-6│
└──────────────────┘
```

---

## ISO Relevance

This project is developed with awareness of relevant standards for health-IT and medical software. Documentation follows ISO 13485:2016 design control requirements.

| Standard | Clause | Implementation |
|---|---|---|
| ISO 13485:2016 | 7.3 — Design & Development | This PRD serves as the design input document |
| ISO 13485:2016 | 4.2 — Document Control | Version-controlled via GitHub, case data in Supabase |
| ISO 13485:2016 | 8.2 — Monitoring | Error logging table, KPI tracking via resultater-table |
| ISO 27001:2022 | A.9 — Access Control | Auth-guard on all routes, role-based profiles |
| ISO 27001:2022 | A.8 — Asset Management | Server-side API keys, Supabase Secrets only |
| ISO 27001:2022 | A.14 — Secure Development | No API keys in frontend, secure Edge Function pattern |

> **Note:** KliniskSim stores no real patient data. All scenarios are fictional and generated for educational purposes only. This app is not classified as a medical device under MDR 2017/745.

---

## Known Issues / Roadmap

### Known Issues
| Issue | Status |
|---|---|
| Edge Function timeout on rapid consecutive generation | Known — seed-data fallback in place |
| Acronym inline explanation (ABCDE, SEPSIS etc.) | Fix in progress |
| Deeper clinical reasoning in AI begrunnelser | Fix in progress |

### Roadmap

#### v1.0 — Current MVP
- [x] 5 arenas with seed-data cases (3 per arena)
- [x] AI case generation via Anthropic API
- [x] Supabase Auth + user profiles
- [x] Background preloading for zero wait time
- [x] Results summary with per-step review
- [x] Daily generation limit (5/user/day)

#### v1.1 — Planned
- [ ] Pharmacology training module
- [ ] Deeper clinical reasoning in begrunnelser
- [ ] Acronym auto-explanation
- [ ] Teacher role with student overview

#### v2.0 — Future
- [ ] LMS integration (Canvas/Blackboard)
- [ ] Completion certificates per arena
- [ ] Analytics dashboard for nursing schools
- [ ] Freemium model with institutional licensing

---

## ⚠️ Disclaimer

KliniskSim is an **educational training tool** designed for nursing students and healthcare professionals in Norway.

- All patient scenarios are **entirely fictional** and AI-generated
- **No real patient data** is stored or processed at any point
- This app **does not constitute medical advice**
- Clinical decisions must always be made by qualified healthcare professionals
- Case content is for **learning purposes only** and does not replace formal clinical education or official Norwegian clinical guidelines
- The app is currently in **MVP (v0.9) status** and under active development

---

## 👩‍⚕️ Built By

**Augustina Ajemba**
Registered Nurse | Nurse Practitioner | Health-IT

Sykepleier with a master's in advanced clinical nursing and a bachelor's in IT and digitalization in progress. Building digital tools that bridge clinical judgment and healthcare systems.

[🌐 Portfolio](https://augustinaajemba.github.io) · [💼 LinkedIn](https://linkedin.com/in/augustina-ajemba) · [🐙 GitHub](https://github.com/augustinaajemba)

> *This project is part of a health-IT portfolio demonstrating clinical reasoning, product thinking, and regulatory awareness — built using AI-assisted development tools (Claude and Lovable).*

---

## License

```
Copyright (c) 2026 Augustina Ajemba
All rights reserved.

This repository is made available for portfolio viewing 
purposes only. No part of this codebase, documentation, 
or clinical content may be copied, modified, distributed, 
sold, or used commercially without explicit written 
permission from the copyright holder.

The full codebase including AI prompts, Edge Functions, 
and clinical case content is maintained in a private 
repository.

Contact: linkedin.com/in/augustina-ajemba
```
