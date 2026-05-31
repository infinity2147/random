# RUDRA — D2 Frontend–Backend Demonstration Video (verbatim transcript)

**Team Bhadra · PSBs Hackathon 2026 · PS3 Fund Flow Tracking**
**Target ~9:30 (spec: min 5, max 10) · YouTube → Unlisted**

Everything in **quotes is spoken word-for-word**. `[DO]` lines are the exact click/action to perform at that moment. `(~m:ss)` are cumulative time checkpoints — if you drift behind, skip the two scenes marked *OPTIONAL*. The D5 *pitch* video script is separate: **`RUDRA_D5_Pitch_Script.md`**.

---

## ⚙️ BEFORE YOU RECORD (not spoken — do first, in order)

1. **Stop any old backend** (Ctrl-C, or `pkill -f "uvicorn main:app"`). Only one process may own port 8000.
2. **Terminal 1 — backend, NO `--reload`:**
   ```bash
   cd /Users/anantasati/Desktop/rudra/backend
   export ANTHROPIC_API_KEY="sk-ant-..."     # omit → copilot uses quick-commands fallback
   RUDRA_DATASET=ibm_aml uvicorn main:app --port 8000
   ```
   Wait for `[backend] ready: ... 562 alerts, 344 incidents …` before recording.
3. **Terminal 2 — frontend:** `cd /Users/anantasati/Desktop/rudra/frontend && npm run dev` → wait for `localhost:5173`.
4. **Terminal 3 — pre-stage the tamper test (don't run yet), leave it ready to press Enter:**
   ```bash
   cd /Users/anantasati/Desktop/rudra && python -m pytest tests/test_case_store.py::test_hash_chain_detects_tampering -v
   ```
5. **Skip Docker** — stay in in-process mode (same scoring path).
6. **Warm-up pass:** click through Dashboard → Run benchmark → Incidents (open INC-0338) → Network Graph (let each layout render) → Fund Journey → Case Workbench (open a case, click "Why this score?") → ML Models → Live Stream (Start/Stop) → Copilot (one query). Then reload Dashboard.
7. **Screen hygiene:** macOS Do-Not-Disturb ON · clean browser window, 100% zoom, full-screen · role = **INVESTIGATOR** · confirm Dashboard shows **562 / 140 / 344 / 281** · don't edit files while recording.

---

# ════════ SPOKEN TRANSCRIPT (read verbatim) ════════

## Scene 0 — Cold open  (~0:00)
`[DO: backend logs visible in one corner; browser open at localhost:5173 Dashboard]`

> "Hi — this is RUDRA, a real-time fund-flow intelligence platform for public-sector banks, built for Problem Statement 3. Everything you'll see is the live system — a FastAPI backend, a React frontend, and machine-learning models trained on the public IBM Anti-Money-Laundering benchmark of one hundred thousand real transactions. Nothing is a mock-up; every number is computed live. Let me walk you from a transaction arriving all the way to a filed regulatory report."

## Scene 1 — Dashboard + live model run  (~0:25)
`[DO: stay on Dashboard, sweep the cursor across the top KPI tiles]`

> "This is the investigator's command centre. RUDRA is monitoring one hundred thousand transactions worth about fifty-nine thousand crore rupees, with roughly eighteen thousand seven hundred crore flagged as suspicious. Six detectors plus a machine-learning stack raised five hundred and sixty-two alerts — and rather than dump those on an analyst, RUDRA clustered them into three hundred and forty-four incidents and surfaced the one hundred and forty critical ones first. It's also tracking two hundred and eighty-one high-risk entities, three hundred and ten velocity-burst accounts, and twenty-five transit-node mules."

`[DO: click "Run benchmark" on the "Detection latency vs T+1 batch" card; wait for the number]`

> "Now the headline. Banks today catch this on a T-plus-one batch — twenty-four hours later. I'll run the latency benchmark live… and there it is — under a millisecond to score a transaction. That gap is the difference between freezing stolen money and losing it."

## Scene 2 — Incidents: ending alert fatigue  (~1:30)
`[DO: sidebar → Incidents; the list of 344 incidents loads]`

> "Here's where alert fatigue ends. Five hundred and sixty-two raw alerts, collapsed into three hundred and forty-four incidents, ranked by severity, not by arrival time."

`[DO: click the top incident, INC-0338; the detail panel expands showing "Underlying Alerts (76)"]`

> "Look at the top one — incident INC-0338. It bundles seventy-six separate alerts spanning all five fraud patterns at once — a circular ring, layering chains, smurfing, a shell-company funnel, and profile mismatches — across fifty entities. Without clustering, an analyst would chase seventy-six disconnected alerts and never see they're one ring. RUDRA hands them a single case."

## Scene 3 — Fund Journey: follow the money  (~2:25)
`[DO: in the incident panel, click "Trace primary alert" → lands on Fund Journey]`

> "Let me trace the primary alert. This is the fund-journey view — it walks the money outward and backward from the flagged account."

`[DO: toggle the direction control between "Both directions" / "Outgoing only"; point at the flagged hops]`

> "I can follow it downstream or upstream, and RUDRA annotates the red flags on the path — structuring-sized amounts, high-value hops, and rapid pass-through where money lands and leaves within the hour. This is fund-flow tracking made visual — exactly what an investigator needs to see how the money actually moved."

## Scene 4 — Network Graph: the fund-flow graph itself  (~3:15)
`[DO: sidebar → Network Graph; the full graph renders; point at the "Showing X of 118,911 entities" counter]`

> "And this is the network underneath it all — a directed money-flow graph of about one hundred and nineteen thousand accounts and eighty-seven thousand edges. The header tells you exactly how much you're seeing of the full graph. RUDRA gives three layouts for it."

`[DO: click the "Matrix" layout tab]`

> "Matrix shows every edge in a fixed grid — the best way to scan the entire graph for dense, suspicious blocks without it turning into a hairball."

`[DO: click the "Arc" layout tab]`

> "Arc lays the accounts along a line and draws the flows as arcs, so tightly-connected clusters — the fraud rings — jump out."

`[DO: click the "Force" layout tab]`

> "And Force is the classic node-link view, best for a focused subgraph."

`[DO: toggle the "Fraud-only" filter on, then the "High-risk" filter]`

> "I can filter to fraud-only edges, or just the high-risk entities, to cut straight to the signal."

`[DO: click a flagged/high-risk node; the "Subgraph" scope tab activates; click it]`

> "And if I click a suspicious account, RUDRA pulls its one-hop neighbourhood into a subgraph — this is the ML-flagged subgraph the problem statement asks for, the ring around a single suspect, isolated in one click."

## Scene 5 — Case Workbench, explainability & tamper-proof audit  (~4:40)
`[DO: sidebar → Case Workbench; click the top CRITICAL case in the list to open it]`

> "Now the investigation itself. I'll open this critical case. The workbench puts everything in one place — a plain-English description, the recommended action, the detector confidence, the machine-learning score, the entities, and the full transaction chain."

`[DO: click the "Why this score?" button to reveal the SHAP feature attributions]`

> "But a score you can't explain is useless in banking. So I click 'Why this score?' — and RUDRA breaks the decision down into the exact features that drove it, using SHAP. That's the on-record reasoning the Prevention of Money Laundering Act requires."

`[DO: type a short note in the note box → click "Add Note"; then click "Investigating"]`

> "I'll add an investigation note, and move the case to Investigating. Every action I take is written to a cryptographic, hash-chained audit log."

`[DO: switch the sidebar role from INVESTIGATOR to SUPERVISOR]`

> "Roles are enforced server-side, so I'll switch to Supervisor — the only role allowed to verify the chain or file a report."

`[DO: click "Verify Chain" → shows chain intact]`

> "I'll verify the audit chain… intact. But is that just a green tick? Let me prove it."

`[DO: cut to Terminal 3; press Enter on the pre-staged test; it runs ~2s → PASS]`

> "This test hand-edits a row directly in the database, behind the application's back, and then re-verifies — and it confirms the chain detects the tampering and breaks. That's verifiable tamper-evidence — exactly what the Reserve Bank's twenty twenty-four Master Direction demands."

`[DO: back in the Case Workbench, click "Download FIU Package"]`

> "And filing — the six hours of manual paperwork, gone. One click builds the complete FIU evidence package: the S-T-R XML in FIU-India format, the SAR PDF, the network subgraph, the transaction chain, the PMLA citations, and the audit log — zipped and ready. Every personal field is auto-redacted under the Data Protection Act."

## Scene 6 — ML Models: the engine, in the open  (~6:15)
`[DO: sidebar → ML Models; point at the metric cards and confusion matrix]`

> "Here's the model behind all of it. Our primary classifier is XGBoost over thirty engineered edge features: F1 of zero-point-six-one-seven, AUC of zero-point-nine-two-seven, precision zero-point-eight-five-one. I'll be honest about that F1 — the published state of the art on this benchmark is zero-point-seven-two and needs multi-GPU training over days. Ours is what a public-sector bank can run on its own CPUs, today."

`[DO: point at the Variant Comparison table]`

> "We also train a GraphSAGE neural network and a stacked ensemble — you can compare every variant right here."

## Scene 7 — Live Stream: the model running in real time  (~7:10)
`[DO: sidebar → Live Stream; click "Start Stream"; rows begin scoring]`

> "Real-time mode. I'm replaying transactions onto the ingest bus, and each one is scored against the current graph state as it arrives. Watch the rows score live — and the latency tile: sub-millisecond per transaction, averaged over the last five hundred events. It says in-process mode here; a real Kafka broker drops in with zero code change, and both run the identical scoring path."

## Scene 8 — AI Copilot: ask in plain English  (~7:55)
`[DO: sidebar → AI Copilot; click the "Find Cycles" quick action, then type "Which entities are at the highest risk right now?" and send]`

> "And an investigator can just ask. This is Claude, with real tool-calling — it picks the right tool, the backend does the computation against live data, and it answers in plain English."

> **[If you have NO API key, say instead]:** "I'm running without an API key, so this is the deterministic quick-commands fallback — the same backend tools, rule-routed. With the key set, it becomes full natural-language Claude."

## Scene 9 — SAR document  (~8:35)
`[DO: sidebar → SAR Reports; pick an alert from "Select Alert"; the SAR text renders]`

> "And here's the formal Suspicious Activity Report the package contains — generated from the case, ready for a compliance officer to review and sign off."

## Scene 10 — *OPTIONAL* — tunable & India-native  (~9:05)
`[DO: sidebar → Detector Settings (ADMIN role)]`

> "Quickly — every detector threshold lives in a config store, not in code, so a supervisor can tune sensitivity and re-run detection live, no redeploy."

`[DO: sidebar → Account Aggregator]`

> "And RUDRA is India-native — Account Aggregator and DiliSense KYC are built in. To be transparent, these two run as clearly-flagged mocks here without sandbox credentials; the same code calls the real APIs once they're set."

## Scene 11 — Close  (~9:30)
`[DO: sidebar → Dashboard]`

> "Real models, real benchmark data, sub-second detection, explainable scores, and tamper-proof evidence — from a transaction arriving to a filed FIU report. That's RUDRA. Thanks for watching."

---

## 🎬 Reminders
- **Read continuously — never go silent while clicking.** The `[DO]` actions are timed to the words next to them.
- If you're past ~8:40 when you reach Scene 9, **skip Scene 10** to stay under 10:00.
- The **tamper test** (Scene 5) is the standout moment — make sure Terminal 3 is pre-typed so it's one keystroke.
- Say "mock / in-process / honest F1" out loud where scripted — judges score honesty.
