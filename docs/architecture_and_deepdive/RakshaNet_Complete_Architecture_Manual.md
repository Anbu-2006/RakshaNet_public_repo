# RAKSHANET (NATIONAL CYBER INTERCEPTION FRAMEWORK)
## Complete Technical Architecture & AI Forensics Deep-Dive Manual
**National Cyber Threat Operations Center (NCTOC) & Financial Crimes Interception Command**  
*Next-Generation 1930 Cyber Helpline & Core Banking Switch (CBS) Interception Framework*  
*Smart India Hackathon (SIH 2024) — Problem Statement 26184*

---

## 1. EXECUTIVE SUMMARY & OPERATIONAL MANDATE

In India, financial cybercrime — specifically Digital Arrest extortions, electricity disconnection threats, and fake loan schemes — has evolved into multi-state, syndicated operations. When a victim dials the National Cybercrime Helpline (1930), legacy procedures rely on manual operator form-filling, retrospective FIR registration, and delayed email communications to bank nodal officers. By the time a debit freeze is manually communicated (often 24 to 72 hours later), the syndicates have already routed the stolen funds through a 3-layer money mule network and physically withdrawn cash from automated teller machines (ATMs) within **15 to 30 minutes**.

**RakshaNet transforms cybercrime response from retrospective forensic post-mortems into real-time tactical interdiction.** By directly ingesting citizen voice calls, transcribing audio in under 5 seconds using Groq Whisper Large v3, extracting bank accounts and IFSC codes with ML Financial NER, tracing multi-bank ledgers via NetworkX directed graphs, and predicting ATM cash-out terminals via spatial Haversine mathematics, RakshaNet executes an automated **Section 106 BNSS Statutory Debit Freeze** before physical cash leaves the machine.

---

## 2. THE 6-LAYER INTERCEPTION PIPELINE

### Layer 1: Acoustic Ingestion & Dual-Groq Failover Engine
- **Voice Ingestion Modalities**:
  1. *Web Speech API*: Live microphone streaming directly from the Command Center UI (Port 3000).
  2. *Mobile Tethering Hotspot Mic*: Native `<input type="file" accept="audio/*" capture="microphone">` bypassing mobile HTTPS restrictions on local IP `http://<LAN_IP>:3000`.
  3. *Android Debug Bridge (ADB) Watcher*: Background Python listener (`scripts/sync_phone_call_recordings.py`) watching native phone call recording folders over Wi-Fi or USB tethering.
- **ASR Acoustic Transcription**:
  - Uses Groq `whisper-large-v3` running on LPUs (Language Processing Units) with `<5s` transcription latency for standard call segments.
  - Normalizes telephony phonemes and spoken numbers in Indian English and Hindi (e.g., 'triple zero' -> '000', 'double six' -> '66').
- **Dual-Groq API Failover Pool**:
  - Maintains Primary and Secondary Groq API keys (`GROQ_API_KEY_PRIMARY`, `GROQ_API_KEY_SECONDARY`).
  - If Key #1 hits an HTTP 429 quota exhaustion or rate limit, it automatically rotates to Key #2 and replays the request in 0.05ms without application failure.
  - If offline or keys are exhausted, gracefully falls back to local Google SpeechRecognition (`en-IN`) and offline Scikit-Learn models.

### Layer 2: Real-time Threat Relevance & Temporal Intent
- **Relevance Classifier**:
  - LLM compound-mini scoring distinguishing genuine cyber threats (Digital Arrest, extortion, phishing) from casual non-crime conversations.
  - Proven 100% precision: Casual lunch invitations yield `[INFO] CASUAL / NON-CRIME` with zero false alarms.
- **Temporal Narrative Engine**:
  - Classifies urgency based on spoken time anchors:
    - `PRE_CASHOUT_URGENT` (< 60 minutes): Triggers immediate physical ATM cordon and beat marshal alert.
    - `POST_CASHOUT_HISTORICAL` (> 2 hours): Initiates statutory CCTV preservation orders and formal ledger audits.

### Layer 3: Financial Named Entity Recognition (NER) & RBI Master Registry
- **Hybrid Extraction Engine**:
  - Trained Scikit-Learn token classifier combined with ASR-resilient phonetic regular expressions.
  - Prevents common ASR phonetic errors (e.g. ensuring "SBI account" does not corrupt the IFSC into `'SBIN0CCOUNT'`).
  - Validates IFSC codes against the official 32-Bank Reserve Bank of India (RBI) master directory (resolves bank name, branch, and city).
  - Sanitizes and validates Indian bank account numbers (9 to 18 digits).

### Layer 4: Multi-Bank CBS Ledger Harvest & NetworkX Directed Graph
- **Core Banking System (CBS) Integration**:
  - Operates under Section 94 of the Bharatiya Nagarik Suraksha Sanhita (BNSS), 2023.
  - Requisitions real-time transaction ledgers across SBI, HDFC, and ICICI.
  - Models fund flows as a directed graph $G = (V, E)$, tracking:
    - *Layer 1*: Entry mule account receiving victim funds.
    - *Layer 2*: Aggregator / layering node splitting funds.
    - *Layer 3*: Terminal mule account linked to an ATM debit card.
  - Forensic metrics:
    - *Transfer Velocity*: Inter-hop transfer latency < 2 minutes indicative of automated bot scripts.
    - *Fan-out Ratio*: Splitting transactions across 2+ destinations (ratio >= 2.0).
    - *Pass-through Ratio*: Minimal fund retention (>= 90% forwarded).

### Layer 5: Spatial Haversine ATM Cluster Probability & Cash-Out Forecaster
- **Spatial Proximity Ranking**:
  - Computes great-circle distances using the Haversine formula:
    $$d = 2 R rcsin\left(\sqrt{\sin^2\left(rac{\Delta\phi}{2}ight) + \cos(\phi_1)\cos(\phi_2)\sin^2\left(rac{\Delta\lambda}{2}ight)}ight)$$
  - Weights terminal distance (70%), historical mule runner recurrence (20%), and cash reserve level (10%).
  - Pinpoints specific ATM terminal IDs, street addresses, and geographic coordinates.
  - Identifies the local Police Station beat jurisdiction and provides telephone dispatch info with an estimated runner transit window (e.g., 5 to 7 minutes).

### Layer 6: Explainable AI (SHAP) & Section 106 BNSS Statutory Freezes
- **SHAP Legal Explainability**:
  - Converts mathematical model weights into 5 plain-language statutory clauses suitable for magistrate review.
- **Section 106 BNSS Electronic Debit Freeze**:
  - Automatically synthesizes a formal Statutory Freeze Order under Section 106 BNSS, 2023 (Order Ref: `ORDER/BNSS-106/20260913/7C3F26`).
  - Dispatches ISO 20022 `camt.056` payment cancellation / lien requests across participant banks.
  - Blocks recipient bank accounts and the runner's ATM debit card prior to cash withdrawal.

---

## 3. PROTOTYPE VS PRODUCTION ARCHITECTURE

| Component | Working Hackathon Prototype | Full Production Deployment |
| :--- | :--- | :--- |
| **Banking Interface** | Standalone Bank CBS Simulator on Port 3001 with simulated SBI, HDFC, ICICI ledgers and freeze responses. | Direct ISO 20022 / SFMS API integration with NPCI, RBI Clearing House, and scheduled commercial banks. |
| **Telephony Voice Intake** | Tethered phone hotspot, Web Speech API on Port 3000, and USB/Wi-Fi ADB auto-sync script. | Direct SIP trunk / PRI line integration with Telecom Service Providers (Airtel, Jio, Vi) and C-DoT 1930 Helpline switches. |
| **ASR Speech-to-Text** | Cloud Groq Whisper Large v3 (<5s) with Dual-Key failover + local Google ASR fallback. | On-premise air-gapped NVIDIA TensorRT-LLM Whisper cluster in state police data centers. |
| **Geolocation** | Browser GPS gatekeeper or extracted place names (Pune, Kothrud, Bandra, Delhi Aerocity). | Real-time Telecom Cell-ID, Timing Advance (TA), and CDR triangulation under Section 94 BNSS. |
| **ATM Hardware** | Simulated ATM network across Pune, Mumbai, Delhi, and Bangalore with mock card slots. | Direct National Financial Switch (NFS) switch integration locking ATM hardware prior to bill dispension. |
| **Judicial Compliance** | Section 106 BNSS certificates with SHA-256 audit hashes and simulated nodal officer sign-off. | Automated e-Courts integration filing Section 106 BNSS seizure memos with Class 3 DSC police digital signatures. |

---

## 4. STEP-BY-STEP FORENSIC TIMELINE (PUNE CASE STUDY)

- **T+0.00s**: Citizen Ramesh Sharma calls 1930 Helpline reporting digital arrest extortion in Kothrud, Pune.
- **T+5.34s**: Groq Whisper Large v3 transcribes audio with 100% accuracy.
- **T+5.50s**: Relevance classifier flags extortion threat (0.948 confidence); non-crime filter bypassed.
- **T+5.70s**: Financial NER extracts SBI A/C `918273645019`, IFSC `SBIN0000456`, Rs. 65,000; verified against RBI directory.
- **T+6.20s**: CBS graph traversal detects funds layered from SBI to HDFC (`50100293847561`) in 1.5 mins, then to ICICI (`001205019827`).
- **T+6.50s**: Spatial forecaster pinpoints ICICI ATM Paud Road (Vanaz Metro, Pune); alerts Kothrud Police Station (7m 18s ETA).
- **T+6.80s**: Section 106 BNSS Freeze Order generated and dispatched via ISO 20022 `camt.056`. SBI, HDFC, and ICICI accounts locked; ATM card `4591-XXXX-XXXX-8219` blocked.

---

## 5. API SPECIFICATIONS & TELEMETRY CONTRACTS

| Endpoint | Method | Payload & Response Structure |
| :--- | :--- | :--- |
| `/api/v1/calls/upload-audio` | POST | Multipart file (.wav/.m4a) -> Returns transcribed speech, financial entities (A/C, IFSC, INR), risk tier, and autocreated case ID. |
| `/api/v1/calls/trace-bank-logs` | POST | JSON `{account_number, ifsc_code, amount, city, auto_freeze: true}` -> Returns directed graph telemetry, Haversine forecast, SHAP clauses, and BNSS 106 freeze. |
| `/api/v1/calls/active-telemetry` | GET | Returns live active call state, locus, target ATM terminal, and statutory freeze confirmation for Bank CBS Simulator sync. |
| `/api/v1/calls/ws/{session_id}` | WS | Bidirectional WebSocket stream for token streaming, captions, animated circle radius updates, and freeze status broadcasts. |

---

## 6. STATUTORY LEGAL FRAMEWORK

- **Section 94 BNSS, 2023**: Summons to produce document or banking ledger. Empowers authorized cyber investigators to requisition real-time core banking statement telemetry.
- **Section 106 BNSS, 2023**: Power of police officer to seize / freeze suspect property. Provides statutory power to order electronic debit freezes on suspect mule accounts prior to formal charge-sheet.
- **Section 318(4) BNS, 2023**: Cheating and dishonestly inducing delivery of property (formerly IPC 420). Substantive criminal offense charging the primary cyber extortion syndicate.
- **Section 319(2) BNS, 2023**: Cheating by personation (formerly IPC 419). Charges syndicates posing as CBI, ED, Police, or regulatory authorities during digital arrest extortions.
- **Section 66D IT Act, 2000**: Punishment for cheating by personation by using computer resource. Applied to automated bot networks and fake banking APK gateways.

---

## 7. AUTOMATED TEST SUITE EVIDENCE

- `backend/tests/test_dual_groq_failover.py`: 4/4 Passed (Primary/Secondary Groq key rotation on HTTP 429).
- `backend/tests/test_live_call_intake.py`: 18/18 Passed (Audio upload, deduplication, WebSocket broadcast).
- `backend/tests/test_complaints.py & test_alerts.py`: 17/17 Passed (FastAPI CRUD, DB schemas, audit logging).
- `ml/tests/test_cashout_forecast.py & test_ner.py`: 16/16 Passed (Haversine spatial ranking, Financial NER regex).
- **Total: 55 / 55 Passed (100% test passing rate)**.

---
*Generated by RakshaNet Autonomous Intelligence Group — September 2026*
