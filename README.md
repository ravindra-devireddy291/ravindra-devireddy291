# Hi, I'm Ravindra Devireddy

**Senior Frontend Engineer** | React, Next.js, TypeScript | Bengaluru, India (remote-friendly)

I have about 5 years 10 months of experience building production web applications. At work I build bilingual English/Arabic (RTL) products. In my own time I build full systems end to end: a web app, an API behind it, and the research tooling that feeds it.

**Available in 15 days** for remote, hybrid or 12-month-plus contract roles.

[Portfolio](https://portfolio.ravindra-devireddy.com/) | [LinkedIn](https://www.linkedin.com/in/ravindra-devireddy/) | ravindra.devireddy1995@gmail.com

> **About the code:** my repositories are private. This page exists so you can see what each one does without opening it. I am happy to give a live screen-share walkthrough of any codebase, or to share read-only access for a hiring process.

---

## My projects at a glance

| Project | What it is (in one line) | Main tech |
|---|---|---|
| **Edge Desk (web and Android app)** | A trading-desk interface for paper trading Indian index options | Next.js, TypeScript, Capacitor |
| **Edge Desk API** | The backend service that powers the desk | Python, FastAPI, WebSockets |
| **Edge Lab (BANKNIFTY)** | A research lab that tests trading rules on five years of market data | Python, YAML configs |
| **Edge Lab (NIFTY)** | A sister lab for the NIFTY index with stricter promotion rules | Python, YAML configs |
| **Iron Log** | A gym app that adjusts your training to how recovered you are | Next.js, Redux, Firebase, Capacitor |
| **Developer portfolio and CMS** | My portfolio site with a private, owner-only content editor | Next.js 16, Firebase, NextAuth |

All trading projects are **paper trading only**. No real money is traded and none of this is investment advice.

---

## 1. Edge Desk: web and Android app

**In plain words:** a screen a trader would use to watch the market, see signals from a trading engine, and track a practice (paper) portfolio. The design rule is "the engine signals, you place the trade." It does not trade for you.

**What I built**
- A web app for the NIFTY and BANKNIFTY index options desk, with an Android app built from the same code using Capacitor.
- A **backend-for-frontend (BFF)** layer in Next.js. The browser never talks to the trading API directly. Every request goes through my server, which holds the secrets.
- Login with **signed session cookies**, limited to an allow-listed admin account, with password hashing support (scrypt).
- Clear failure handling: the app keeps working and says so when the backend is slow or down.

**Why it matters (engineering points)**
- **Security by design:** API keys are server-only and never exposed to the browser.
- **Honest UI:** it shows last-known data with an "as of" time and never invents prices.
- **Operations:** environment-based configuration, a deploy checklist, a production deployment, and an automated test suite (`npm test`).

**Stack:** Next.js (App Router), TypeScript, Tailwind CSS, Capacitor (Android), Vercel.

---

## 2. Edge Desk API (Python)

**In plain words:** the service behind the desk screen. It collects market and account data from a broker, applies the desk's rules and sends clean, predictable responses to the app.

**What I built**
- A **FastAPI** service with REST endpoints (`/api/v1/desk/*`) that all return the same response shape (`ok`, `server_time`, `data`), plus a **WebSocket** feed for live health updates.
- Three run modes: **mock**, **paper** and **live**. Live trading is switched off by default and cannot be enabled by accident.
- Only my own web app's server can call it (API-key authentication). Browsers are blocked.
- **Automatic broker-token renewal** every 15 minutes so the desk stays connected without manual steps.
- Scripted deployment and restart tooling for a Linux server, with TLS through nginx.
- Written API contracts and a scenario matrix for every mode, so the frontend and backend agree before code is written.

**Why it matters:** this is the part that shows I think about contracts, safety defaults, auth boundaries and operations, not only screens.

**Stack:** Python, FastAPI, WebSockets, nginx.

---

## 3. Edge Lab: BANKNIFTY research (Python)

**In plain words:** a workshop for testing trading ideas on historical data before any idea gets near a desk. It answers "would this rule have worked, after realistic costs?"

**What I built**
- A **rules-only** system. It uses no machine learning, so every decision can be explained.
- A **backtesting engine** with documented assumptions for fills and costs (spreads, brokerage, charges), so results are not flattering.
- Five years of options data (2021 to 2026) stored in a compact, query-friendly format.
- **Config-driven strategies:** each strategy version is a YAML file. Position size, risk limits and capital rules sit in config, not in code.
- A **pre-entry gate** that checks every trade idea against risk rules before it is allowed.
- A **shadow mode** that runs the strategy daily alongside the market without trading, with end-of-day summaries and reports.
- A written capital-allocation policy: the premium at risk is a fixed percentage of equity, so the logic scales with account size.

**Why it matters:** it shows disciplined, testable, reproducible engineering, and the habit of measuring before trusting.

**Stack:** Python, Parquet, YAML.

---

## 4. Edge Lab: NIFTY research (Python)

**In plain words:** the NIFTY version of the lab above, kept completely separate on purpose, with its own capital, results and rules.

**What I built**
- The same engine and reporting structure, adapted to a different market, with a separate data lake and configs.
- **A promotion process:** ideas live on a `research` branch. They move to the stable `main` branch only after out-of-sample testing and sign-off.
- **Gates and runbooks:** the paper stack must clear a set number of filled sessions before it is trusted.
- Two active strategy slots only, so results stay easy to read.
- An honest-results rule written into the project: a result from one market is not assumed to hold in another.

**Why it matters:** this shows the engineering process: versioning, validation, documentation and not fooling myself with the data.

**Stack:** Python, YAML configs, Parquet.

---

## 5. Iron Log: readiness-based gym coach

**In plain words:** most gym apps are logbooks. Iron Log is a coach. It asks how you slept and how stressed you are, then adjusts how much training it recommends.

**What I built**
- A **readiness score** from sleep and stress, which tightens or relaxes your volume limits for the day.
- A **body heatmap** with 21 muscle regions. Colours go from yellow to orange to red as fatigue builds during a session.
- **Progressive overload targets** from your own history (for example "Target: 185 lbs x 8").
- AI-generated session suggestions, saved workout templates, body-metric tracking and insights.
- **Silent cloud sync** with Firebase, so nothing needs a manual save.
- Web and Android (Capacitor) builds, with English and other locale routes.

**Engineering idea:** *derived state.* Raw inputs (sets, sleep, weight) are stored as plain data and every insight is computed from them by pure functions. The screen can never disagree with the data.

**Stack:** Next.js, TypeScript, Redux Toolkit, Firebase, Stripe, Capacitor.

---

## 6. Developer portfolio and content system

**In plain words:** my portfolio website at [portfolio.ravindra-devireddy.com](https://portfolio.ravindra-devireddy.com/), with a private admin area where I edit all of its content without redeploying.

**What I built**
- A public site: hero, experience timeline, project case studies, engineering principles, an animated tech-stack marquee, a skills chart and a downloadable PDF resume.
- An owner-only **CMS** with an accessible, focus-trapped edit modal, toast notifications and a command palette (Cmd/Ctrl + K) for quick navigation.
- **Firebase** as the database (no custom backend server), with **NextAuth v5** login. Admin routes are protected twice: by middleware and by the layout.
- **Redux Toolkit** with separate slices for each content area.
- Written high-level and low-level design documents and architecture diagrams.

**Stack:** Next.js 16 (App Router), TypeScript, Firebase, Redux Toolkit, NextAuth, Recharts, Vercel.

---

## Professional experience (in company repositories)

| Company | Role | Highlights |
|---|---|---|
| **Andersen Lab** (2026 to now) | React Developer | Sole frontend developer on an admin and verification platform with role-based portals. Building a bilingual English/Arabic (RTL) app with UAE Pass sign-in. |
| **Verizon Data Services** (2023 to 2025) | Engineer II, Software Development | Built a workflow that replaced 3 legacy flows: **60% fewer navigation steps, 40% fewer redundant API calls, 90%+ unit test coverage.** |
| **Excelsoft Technologies** (2020 to 2022) | Software Engineer | Redux and React UIs with 100% Figma fidelity. Single-SPA micro-frontend migration. |

Company code is confidential, so none of it is on this profile.

## Skills

**Frontend:** React, Next.js, TypeScript, JavaScript (ES6+), Redux Toolkit, TanStack Query, Tailwind CSS, Storybook, accessibility, performance optimisation, micro-frontends
**Testing:** Jest, React Testing Library, Playwright
**Backend and data (own projects):** Python, FastAPI, REST, WebSockets, Firebase
**Mobile:** Capacitor (Android)
**Practices:** CI/CD, design documents (HLD/LLD), config-driven design, secure auth patterns

## Education

MBA (Business Analytics), Manipal Academy of Higher Education, 2026. B.Tech (Civil Engineering), 2017.

---

*The trading projects are for learning and research only. They use paper (simulated) money, and nothing here is investment advice.*
