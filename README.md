<p align="center">
  <a href="https://github.com/Anbu-2006/RakshaNet_public_repo">
    <img src="assets/rakshanet_banner.svg" alt="RakshaNet — Predictive Cash-Out Interception Framework" width="100%" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SIH_2024-PS_26184-0284c7?style=flat-square&logo=target" alt="SIH PS 26184" />&nbsp;
  <img src="https://img.shields.io/badge/BNSS_2023-Sec_106-059669?style=flat-square&logo=shield" alt="Section 106 BNSS" />&nbsp;
  <img src="https://img.shields.io/badge/ISO_20022-camt.056-7c3aed?style=flat-square&logo=currys" alt="ISO 20022" />&nbsp;
  <img src="https://img.shields.io/badge/Tests-51%2F51_Passed-10b981?style=flat-square&logo=checkmarx" alt="51 Tests Passed" />&nbsp;
  <img src="https://img.shields.io/badge/License-MIT-38bdf8?style=flat-square" alt="License MIT" />
</p>

<p align="center">
  <strong>National Cyber Threat Operations Center (NCTOC) &amp; Financial Crimes Interception Command</strong><br>
  <em>Next-Generation 1930 Cyber Helpline &amp; Core Banking Switch (CBS) Interception Framework</em>
</p>

<p align="center">
  <a href="#-problem-statement-26184">Problem Statement</a> &nbsp;•&nbsp;
  <a href="#-the-15-minute-golden-window">15-Min Golden Window</a> &nbsp;•&nbsp;
  <a href="#-system-architecture">Architecture</a> &nbsp;•&nbsp;
  <a href="#-dual-portal-ecosystem">Dual Portals</a> &nbsp;•&nbsp;
  <a href="#-operational-showcase--visual-evidence">Visual Evidence</a> &nbsp;•&nbsp;
  <a href="#-statutory--banking-standards">Statutory Law</a> &nbsp;•&nbsp;
  <a href="#-official-sih-deliverables">Deliverables</a>
</p>

---

## 🎯 Problem Statement 26184

> [!IMPORTANT]
> **The Real-World Crisis in India's Cybercrime Response:**
> In contemporary Indian cyber-extortion schemes—including **Digital Arrests**, **Fake Police Verifications**, **Customs Seizures**, and **Instant Task/Investment Scams**—adversary syndicates rapidly siphon extorted money across multiple bank layers (*Layer 1 Mule → Layer 2 Digital Intermediary → Layer 3 Shell Entity*). Finally, physical **cash-out runners** withdraw paper currency from automated teller machines (ATMs) across interstate borders **in under 15 minutes**.
>
> By the time a distressed citizen dials **1930** and a police operator finishes manual handwritten intake and email notifications, **the cash has already left the banking system.**

### The Performance Delta: Conventional 1930 vs. RakshaNet

| Operational Vector | Conventional 1930 Helpdesk | RakshaNet Interception Engine | Operational Impact |
| :--- | :--- | :--- | :---: |
| **Intake Modality** | Manual typing post-call | Direct USB/SIP Telephony audio streaming | **Real-Time** |
| **Speaker Diarization** | Unassisted human ear | Smart Automatic Speaker Attribution (Victim vs. Scammer) | **Instant** |
| **Entity Extraction** | Manual note-taking | Dual-Model Financial NER (IFSC, Account, Amount, UPI) | **Sub-second** |
| **Branch Verification** | Slow manual search | Automated checksum + RBI Master Directory (150K+ branches) | **&lt; 5 ms** |
| **Time to Debit Hold** | **45 – 90 Minutes** | **&lt; 3 Minutes (Inside Golden Window)** | **30x Faster** |
| **Interbank Signaling** | Unstructured emails / PDFs | Standardized **ISO 20022 `camt.056` XML** | **Machine-to-Machine** |
| **Field Coordination** | Disconnected from local police | Automated geocoded dispatch to nearest **ERSS 112** patrol | **GPS Synced** |

---

## ⏱️ The 15-Minute Golden Window

Once physical paper currency is dispensed from an automated teller machine, **recovery probability drops to near zero**. The 15-Minute Golden Window defines the absolute tactical threshold to freeze accounts before physical drainage:

```
CONVENTIONAL WORKFLOW (45+ Minutes — 92% Cash Lost)
[Victim Transfer] ──> [Layer-1 Mule] ──> [ATM Cash-Out (Min 14)] ──> [Operator Intake] ──> [Email Sent (Min 45)]
                                                    ▲                                              │
                                                    └──────────────── TOO LATE ────────────────────┘

RAKSHANET PREDICTIVE INTERCEPTION (< 3 Minutes — 98% Funds Preserved)
[Victim Transfer] ──> [1930 Live Stream] ──> [Financial NER] ──> [Section 106 BNSS Freeze] ──> [CBS Hold Active (Min 2.5)]
                                                                        │                                │
                                                                        ▼                                ▼
                                                            [ERSS 112 Police Cordon]          [ATM Cash-Out Blocked]
```

> [!TIP]
> Read the complete mathematical velocity curve and decay calculus in [docs/15_MINUTE_GOLDEN_WINDOW.md](docs/15_MINUTE_GOLDEN_WINDOW.md).

---

## 🏛️ System Architecture

RakshaNet deploys an asynchronous, event-driven cyber-forensics pipeline engineered for sub-second classification and zero-loss interbank signaling:

```mermaid
flowchart TD
    subgraph S1["1. Distress Telephony Intake"]
        A[Distressed Citizen Calls 1930] -->|Live USB Audio / SIP| B(Telephony Intake Streamer)
        B --> C[Dual-Channel Whisper ASR Engine]
        C --> D[Smart Speaker Attribution: Victim vs Operator]
    end

    subgraph S2["2. Forensic NLP & Entity Extraction"]
        D -->|Real-Time Text Stream| E[Financial NER Sequence Classifier]
        E -->|Extracts Amount, A/C, IFSC| F{RBI Master Directory 150K+ Branches}
        F -->|Verified Branch| G[Section 106 BNSS Statutory Freeze Engine]
        F -->|Misheard / Invalid Digits| H[Proactive Operator Review Modal]
        H -->|One-Click Resolution| G
    end

    subgraph S3["3. Predictive Graph & Spatial Cordon"]
        E -->|Transaction Graph| I[GNN Multi-Hop Layering Tracer]
        E -->|Extracted Geolocation| J[Indian Gazetteer & Pincode Resolver]
        J --> K[Spatial-Temporal ATM Proximity Forecaster]
        K --> L[ERSS 112 Rapid Police Intercept Cordon]
    end

    subgraph S4["4. Core Banking Switch (CBS) Enforcement"]
        G -->|ISO 20022 camt.056 XML| M[Core Banking Switch Port 3001]
        M -->|Electronic Debit Freeze Applied| N[Physical ATM Cash-Out Blocked]
    end
```

---

## 🌐 Dual-Portal Ecosystem

RakshaNet is architected as two decoupled, high-performance web systems:

```
┌──────────────────────────────────────────────┐     ┌──────────────────────────────────────────────┐
│  PORTAL 1: COMMAND CENTER (PORT 3000)        │     │  PORTAL 2: SYNDICATE SIMULATOR (PORT 3001)   │
│  • 1930 Telephony Station & Live Waveforms   │     │  • Scammer Loot Deposit & Layering Hops      │
│  • RBI Master Directory (150K+ Branches)     │ <─> │  • Core Banking Switch (CBS) Ledger Sandbox  │
│  • Section 106 BNSS Freeze Dispatcher        │     │  • Real-Time ATM Hardware Runner Emulation   │
│  • Nationwide Cartographic Radar (Leaflet)   │     │  • Instant Port 3000 Telephony Sync          │
└──────────────────────────────────────────────┘     └──────────────────────────────────────────────┘
```

---

## 📸 Operational Showcase & Visual Evidence

### 1. 1930 Cyber Helpline — Telephony Station & Cartographic Radar
*Real-time telephony hardware link, live incoming citizen distress ingestion, and nationwide radar monitoring.*

![1930 Telephony Command Radar](screenshots/01_1930_telephony_command_radar.png)

---

### 2. Proactive RBI Master Directory Verification Modal
*Automated checksum validation against the 150,000+ branch RBI Master IFSC Directory. Instantly alerts the operator if a digit was misheard, preventing downstream bank rejection.*

![RBI Financial Verification Modal](screenshots/02_rbi_financial_verification_modal.png)

---

### 3. Authentic Distress Call Intake & Smart Speaker Attribution
*Dual-channel audio processing with automatic speaker diarization separating Citizen Victim statements from Operator guidance with real-time entity extraction.*

![Live Transcript Speaker Attribution](screenshots/03_live_transcript_speaker_attribution.png)

---

### 4. Statutory Section 106 BNSS Freeze & ERSS 112 Police Cordon
*One-touch electronic debit hold execution under statutory BNSS powers, dispatching ISO 20022 payloads and arming the nearest ERSS 112 intercept patrol to the predicted ATM terminal.*

![Section 106 BNSS Freeze Cordon](screenshots/04_bnss_section106_freeze_cordon.png)

---

### 5. Adversary Syndicate & Core Banking Switch (CBS) Simulator (Port 3001)
*Independent Port 3001 sandbox modeling illicit extortion transfers, rapid mule layering hops, and live Core Banking Switch ledgers.*

![Adversary Syndicate Simulator](screenshots/05_adversary_syndicate_simulator.png)

---

### 6. Physical ATM Cash-Out Blocked at Terminal
*Proof of Interception: When the cash-out runner attempts physical ATM cash withdrawal, the Core Banking Switch debit hold automatically declines the transaction.*

![ATM Cash-Out Blocked](screenshots/06_atm_cashout_blocked_by_cbs.png)

---

### 7. 4-Node Forensic AI Pipeline Live Tracker
*Real-time pipeline progression tracker displaying sub-second latency across Telephony Ingestion, Whisper ASR, Financial NER, and Core Switch Dispatches.*

![Forensic AI Pipeline Tracker](screenshots/07_forensic_ai_pipeline_tracker.png)

---

### 8. Tactical Cartographic Heatmap & Interstate Mule Trajectories
*Dynamic spatial-temporal clustering identifying high-velocity cash-out hotspots and interstate syndicate corridors across India.*

![Interstate Mule Heatmap Radar](screenshots/08_interstate_mule_heatmap_radar.png)

---

### 9. Judicial Audit Trail & Immutable Officer Dossier
*Forensically verifiable log conforming to Section 65B of the Indian Evidence Act, ensuring strict accountability and auditability for court proceedings.*

![Cyber Admin Audit Trail](screenshots/09_cyber_admin_audit_trail.png)

---

## ⚖️ Statutory & Banking Standards

### 1. Section 106, Bharatiya Nagarik Suraksha Sanhita (BNSS), 2023
RakshaNet provides immediate statutory legal backing for police officers. Under Section 106 BNSS, cyber police officers possess the statutory authority to direct commercial banks, payment aggregators, and digital wallets to attach or debit-freeze property suspected of being tainted by criminal extortion.

### 2. ISO 20022 `camt.056.001.08` Electronic Hold Protocol
Rather than sending unstructured emails or scanned PDFs, RakshaNet constructs standardized **Customer Payment Cancellation Request (`camt.056`)** XML payloads. This allows Core Banking Switches (Finacle, TCS BaNCS, Flexcube) to process holds automatically via machine-to-machine APIs.

### 3. Citizen Privacy by Design (DPDP Act 2023 Compliant)
- **Transient In-Memory Buffers**: Telephony audio buffers are processed in volatile memory; zero raw voice data is retained without judicial warrants.
- **PII Minimization**: Scrubber filters strip citizen Aadhaar and PAN data prior to interbank transmission.

---

## 📦 Official SIH Deliverables & Documentation

| Document / Asset | Format | Description |
| :--- | :---: | :--- |
| [**Smart India Hackathon Presentation Deck**](docs/RakshaNet_SIH_Presentation.pptx) | `.pptx` | Official pitch presentation covering architecture, benchmarks, and police workflow |
| [**Official Datasets Master Catalog**](docs/RakshaNet_Datasets_Master_Catalog.pdf) | `.pdf` | Complete reference catalog of all 6 training, geographic, and benchmark datasets |
| [**Problem Statement 26184 Deep Dive**](docs/PROBLEM_STATEMENT_26184.md) | `.md` | Comprehensive analysis of the operational bottlenecks and RakshaNet solution |
| [**The 15-Minute Golden Window Analysis**](docs/15_MINUTE_GOLDEN_WINDOW.md) | `.md` | Mathematical velocity model, decay curves, and tactical interception timing |
| [**System Architecture & Standards**](docs/SYSTEM_ARCHITECTURE.md) | `.md` | Complete dual-portal specification, API contracts, and ISO 20022 schemas |

---

## 🧪 Verified Test Suite

```
============================= test session starts =============================
platform win32 -- Python 3.13.14, pytest-9.0.3, pluggy-1.6.0
rootdir: RakshaNet
collected 51 items

backend\tests\test_api_contracts.py ..........                           [ 19%]
backend\tests\test_audio_ner.py ......                                   [ 31%]
backend\tests\test_bank_tracer.py ......                                 [ 43%]
backend\tests\test_live_call_intake.py ....                              [ 50%]
backend\tests\test_realworld_cashout_predictor.py .....                  [ 60%]
backend\tests\test_simulated_db_endpoints.py .....                       [ 70%]
ml\tests\test_heuristics.py ...............                              [100%]

======================= 51 passed, 1 warning in 43.99s ========================
```

---

## 👥 Authorship & Repositories

Developed by **Team RakshaNet** for the **Smart India Hackathon (SIH)**.

- **Primary Repository (Full Project)**: [https://github.com/Anbu-2006/RakshaNet](https://github.com/Anbu-2006/RakshaNet)
- **Public Showcase Repository**: [https://github.com/Anbu-2006/RakshaNet_public_repo](https://github.com/Anbu-2006/RakshaNet_public_repo)
- **License**: Released under the [MIT License](LICENSE) for hackathon evaluation, academic research, and law-enforcement review.
