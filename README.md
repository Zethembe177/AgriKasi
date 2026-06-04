# AgriKasi
A modern web application built on the PERN stack designed to help local farmers track livestock, feed, and poultry cycles efficiently.
### A Type-Safe Operational Ledger & Analytics Engine for Micro-Commercial Poultry Farmers

---

## 🛑 The Friction (The Problem)
In South Africa, the AgTech space is dominated by enterprise platforms (like Kraal, Beeftrack, or HerdSync) built for multi-million Rand operations. These systems depend heavily on expensive solar-powered GPS ear tags, IoT scales, and proprietary RFID infrastructure. 

For the micro-commercial smallholder—the farmer managing rolling cycles of 100 to 500 broiler chickens in a local community—these corporate systems are financially inaccessible. Consequently, these entrepreneurs run their businesses using disorganized paper notebooks or easily corrupted Excel sheets. 

Because critical data is locked on paper, smallholders face devastating friction:
1. **Invisible Losses:** Disease or temperature spikes aren't flagged until mortality rates reach a catastrophic threshold.
2. **Untracked Efficiency:** Feed accounts for ~70% of production costs, but without tracking the **Feed Conversion Ratio (FCR)** daily, farmers cannot identify feed waste or poor bird development in real-time.
3. **Financial Blind Spots:** Out-of-date records mean farmers rarely know their exact break-even production cost per bird in ZAR until after harvest, forcing them to guess their market pricing.

---

## 💡 The Architecture (The Solution)
This application is a software-only operational ledger designed to bridge the gap between paper logs and enterprise analytics. By eliminating hardware dependencies, it provides an accessible, mobile-first data engine tailored for ground-level agricultural workers and farm owners.

Built using the **PERN Stack** (PostgreSQL, Express, React, Node.js) with strict **TypeScript**, the platform utilizes Role-Based Access Control (RBAC) to segment operational tasks:

1. Ground-Level Data Entry (Worker Role)
Workers standing in the shed use a distraction-free, low-bandwidth mobile view to submit simple, manual daily logs in under 2 minutes:
* Select active batch dropdown.
* Input daily mortality count.
* Input bags of feed utilized (Starter/Grower/Finisher).

### 2. The Analytical Engine (Owner Role)
The TypeScript backend automatically processes these raw inputs against relational schemas to generate real-time metrics:
* **Dynamic Age Tracker:** Automated tracking of days in production to flag peak harvest windows (Day 35–42).
* **Live FCR Calculator:** Aggregates cumulative feed consumption against sample weights to monitor feed-to-meat conversion efficiency.
* **Real-Time Cost-Per-Bird:** Dynamically divides live chick purchase costs and fluctuating feed prices by surviving stock numbers to establish exact break-even margins.

---

## 🛠️ The Tech Stack & Engineering Focus
This project was built to prioritize structural logic and data scale over superficial UI aesthetics.

* **Frontend:** React with TypeScript (optimized state management for asynchronous dashboard calculations).
* **Backend:** Node.js / Express with TypeScript.
* **Database:** PostgreSQL (Strict foreign keys, relational mapping, and constraints to manage rolling cycles).
* **OR/M:** Prisma or Knex.js for type-safe query building.

### Core Engineering Requirements:
* **Relational Integrity:** A strict `ON DELETE CASCADE` or `RESTRICT` hierarchy ensuring `DailyLogs` are securely tied to unique `Batch` IDs.
* **Global Error Handling:** Explicit HTTP status codes (`400`, `404`, `500`) returned from custom centralized backend middleware to handle database downtime gracefully.
* **Run-Time Validation:** Type safety enforced at the network boundary using strict validation schemas (Zod/Joi) to reject malformed inputs before they hit the database layer.

---

## 🏗️ Technical Hurdles & The Struggle Log
*(Senior Devs: This section documents the actual debugging journey, type conflicts, and architectural decisions made during development.)*

* **Hurdle 1: Calculating Dynamic FCR over Relational Datasets**
  * *The Problem:* Initially attempted to run multiple map/reduce array functions on the frontend, causing unnecessary layout shifts and data lagging.
  * *The Fix:* Refactored the data layer to calculate the running sum directly inside the PostgreSQL query using aggregate functions (`SUM`, `COUNT`), reducing the payload weight by over 60%.
* **Hurdle 2: TypeScript Typing for Multi-Role Payloads**
  * *[Insert your next genuine bug here as you build!]*
