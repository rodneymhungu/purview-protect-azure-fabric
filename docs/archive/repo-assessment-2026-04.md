# Repo Assessment & Completion Plan
## `purview-protect-azure-fabric` — End-to-End Review
**Reviewed:** April 14, 2026  
**Repo:** https://github.com/rodneymhungu/purview-protect-azure-fabric  
**Reviewed by:** Claude (Cowork mode)

---

## 1. Repository Structure (Actual Layout)

The repo has a nested structure — all content lives inside a subdirectory of the same name:

```
purview-protect-azure-fabric/          ← repo root
├── purview-protect-azure-fabric/      ← main content folder (nested)
│   ├── docs/
│   │   ├── images/                    ← 17 screenshots already uploaded
│   │   ├── getting-started-for-non-experts.md
│   │   ├── Prerequisites.md
│   │   ├── classification-engines.md
│   │   └── apply-purview-labels.md
│   ├── dummy-files/
│   │   └── dummy_data_azure_blob_storage.zip
│   └── use_cases/
│       ├── azure_blob_storage_test.md
│       └── azure_sql_database_test.md
├── LICENSE
└── README.md
```

> **Note:** The `scripts/` folder referenced in the README does **not yet exist** in the repo.

---

## 2. What Is Complete and Production-Ready ✅

### README.md
**Status: Complete.** Professional, well-structured, and honest about what's in progress. The three-paragraph framing ("product-oriented docs vs. role-collaborative reality") is distinctive and sets the repo apart. Minimal typo cleanup needed ("consultatants", "functioanlity") but not blocking.

### docs/getting-started-for-non-experts.md
**Status: Complete.** One of the strongest files in the repo. Covers:
- Why governance matters (backed by three real market stats from Gartner/ISMG)
- Clear, jargon-light explanations of Fabric and Purview
- Coverage of insider risk, DLP, responsible AI activation, and compliance simplification

This file would genuinely help a compliance lead or a VP-level stakeholder understand the "why" before touching a single Azure resource. No gaps.

### docs/Prerequisites.md
**Status: Complete.** Thorough and practical. Covers all four foundational requirements (Entra ID tenant, Azure subscription, M365 E5 license, Fabric trial), spells out exact roles needed per product area (Purview/Azure/Fabric), calls out the modern portal URL vs. legacy, and lists the four most common pitfalls that block first-time setups. A practitioner could follow this alone and avoid the most common configuration mistakes.

### docs/classification-engines.md
**Status: Complete — arguably the best file in the repo.** The two-engine comparison (Data Map vs. Sensitive Information Types) is a genuinely useful piece of writing that Microsoft's own documentation never presents this clearly. Key strengths:
- Summary table with use-case-to-engine mapping and direct docs links
- Full feature comparison table
- Two concrete worked examples (IaaS/PaaS vs. SaaS scenarios with BSNs and IBANs)
- Clear articulation of the critical nuance: Data Map labels are *metadata for governance*, not encryption

This file alone would justify the repo's existence for a data engineer stepping into the compliance space for the first time.

### docs/images/ (17 screenshots)
**Status: All 17 screenshots uploaded.** This is actually significant — taking, annotating, and uploading real portal screenshots is the hardest part of technical docs. The full set is present. The files are:

| # | Filename | Purpose |
|---|----------|---------|
| 1 | `microsoft-purview-portal.png` | Step 1(a) — Portal homepage |
| 2 | `Data Security Section of Purview Portal.png` | Step 1(a) — Data Security card |
| 3 | `Create a label information protection.png` | Step 1(b) — Create label entry |
| 4 | `edit label.png` | Step 1(b) — Edit label context menu |
| 5 | `provide basic details of label.png` | Step 1(c) — Basic metadata form |
| 6 | `define the scope for this label - files & other data assets.png` | Step 1(d) — Scope selection |
| 7 | `control who has access to these files.png` | Step 1(e) — Access control settings |
| 8 | `assign the permissions immedialy when labelling the assets and items.png` | Step 1(e) — Permission assignment |
| 9 | `Define protection settings for groups and sites...png` | Step 1(f) — Groups & sites |
| 10 | `external user access.png` | Step 1(f) — External user config |
| 11 | `external sharing and conditional access setting.png` | Step 1(g) — Conditional access |
| 12 | `reviewing your settings.png` | Step 1(h) — Final review screen |
| 13 | `blob_storage.png` | Blob storage container layout |
| 14 | `debt_collection_letter.png` | Sample debt collection letter |
| 15 | `labelling-process-diagram.png` | Overview diagram for apply-purview-labels.md |
| 16 | `loan_confirmation_letter.png` | Sample loan confirmation letter |
| 17 | `purview-enterprise-account.png` | Enterprise account upgrade (Prerequisites) |

### dummy-files/dummy_data_azure_blob_storage.zip
**Status: Present.** The sample `.docx` files (loan confirmation and debt collection letters with embedded IBAN/BSN/passport data) are packaged and available. Referenced correctly in `azure_blob_storage_test.md`.

---

## 3. What Is Partially Complete ⚠️

### docs/apply-purview-labels.md
**Status: Text 100% complete — images NOT embedded.**

This is the most critical gap, and the easiest to fix. The file has a fully written 5-step walkthrough (Create Label → Register Asset → Scan → Classifications Found → Labels Applied), including a Step 4.5 for auto-labeling policies. All 12 screenshot references exist as text placeholders:

```
📸 Screenshot: Microsoft Purview homepage → Information Protection section
📸 Screenshot: Data Security section with Information Protection card
...
```

All 12 corresponding images (numbered 1–12 in the images folder) **already exist** and are uploaded. The `labelling-process-diagram.png` for the intro section also exists. Nothing needs to be recreated — this is purely a markdown embedding task.

**What's needed:** Replace each `📸 Screenshot: [description]` placeholder with proper markdown image syntax:
```markdown
![description](../docs/images/filename.png)
```

**Time estimate: 30–45 minutes.**

### use_cases/azure_blob_storage_test.md
**Status: Setup narrative complete — test reproduction section missing.**

The file has excellent context: the fictional bank scenario, file types (loan confirmations and debt collection letters), sensitive data types present (IBAN, BSN, passport, full name, address), the analytics rationale, and the privacy/compliance rationale. It also has three image placeholders for `loan_confirmation_letter.png`, `debt_collection_letter.png`, and `blob_storage.png` — all of which exist in the images folder.

The file ends with a single placeholder line:
> *"Under construction 20-08-2025 - labelling and protecting data in blob storage test reproduction"*

**What's missing:** The actual test reproduction — a step-by-step account of running the Purview scan on the blob container, seeing the BSN/IBAN classifications appear, setting up the auto-labeling policy, re-scanning, and confirming labels are applied. This would look like a numbered walkthrough with screenshots of the actual results.

**Time estimate: 2–4 hours** (requires either having previously run the test and saved results, or re-running it).

---

## 4. What Is Unstarted ❌

### use_cases/azure_sql_database_test.md
**Status: Empty placeholder (1 line).**

Contains only:
> *"Under construction 20-08-2025 - labelling and protecting data in azure sql database test reproduction"*

No setup narrative, no scenario context, no structure. Needs to be built from scratch, likely following the same pattern as the blob storage use case (scenario → sample data → why it matters → test reproduction).

**What's needed:** 
- A business scenario (different from blob — e.g., a database with customer records or transaction history)
- Sample SQL schema or table structure showing what sensitive data types are present
- Test reproduction showing scan → classification → label application in Azure SQL
- Screenshots of the Data Map scan results against a SQL source

**Time estimate: 3–6 hours** (depending on whether you have an Azure SQL demo environment ready).

### scripts/ folder
**Status: Does not exist yet.** README says "coming soon — after gaining initial feedback."

**What's needed:** Scope definition first. Could include:
- PowerShell/CLI commands to register and scan data sources
- Python or REST API calls to query Purview classification results
- Automation for creating sensitivity labels programmatically

**Time estimate: 8–20 hours** depending on scope. Low priority until feedback validates demand.

### Microsoft Fabric integration docs
**Status: Mentioned in README as future work ("Fabric-focused data security demos") but no files, no outline, no placeholder.**

This is the most strategically valuable and technically demanding piece of the repo. The README promises:
> "Fabric-focused data security demos"

Potential coverage:
- How sensitivity labels applied to Azure assets propagate into Fabric (OneLake, Lakehouses)
- How to query label metadata in Fabric Notebooks or using Semantic Models
- DLP policy behavior when labeled data is used in Power BI reports
- Fabric workspace security tied to Purview governance

**Time estimate: 12–20 hours.** Requires Fabric capacity (trial or paid) and hands-on testing.

---

## 5. Is Completion Worthwhile? Assessment

**Yes — strongly.** Here's why:

**Audience value:** The repo targets a genuine gap. Most practitioners trying to implement Purview in Azure either come from a security background (and struggle with the Azure side) or from a data engineering background (and struggle with the compliance side). This repo bridges that gap at a level of clarity that Microsoft's own docs don't reach.

**Quality signal:** The content that exists is notably good — not boilerplate. The classification-engines.md file in particular is the kind of writing that gets shared on LinkedIn and referenced in internal onboarding docs. That quality level means the repo has credibility worth protecting.

**Completion leverage:** The most visible gap (missing screenshots in apply-purview-labels.md) is also the easiest to fix. A visitor landing on that file today sees walls of `📸 Screenshot:` text placeholders, which undercuts the quality signal of the other files. Fixing this first dramatically improves the first impression.

**ROI summary:**
- 45 minutes of work on image embedding = the repo's centerpiece guide becomes fully usable
- 3–4 hours on blob storage test reproduction = the use case section becomes demonstrable
- 8–12 hours on SQL use case + Fabric docs = the repo reaches "reference resource" status

---

## 6. Completion Priority Roadmap

### Phase 1 — Quick Wins (Est. 1–2 hours total)
**Goal: Make the repo look complete to a first-time visitor**

**Task 1.1 — Embed screenshots in apply-purview-labels.md** *(~45 min)*  
Replace all 12 `📸 Screenshot:` placeholders with actual `![alt](../docs/images/filename.png)` embeds. Also embed the `labelling-process-diagram.png` in the intro section.

Mapping (placeholder → image file):
```
📸 Portal homepage          → 1. microsoft-purview-portal.png
📸 Data Security card       → 2. Data Security Section of Purview Portal.png
📸 Create label entry       → 3. Create a label information protection.png
📸 Edit label menu          → 4. edit label.png
📸 Basic metadata form      → 5. provide basic details of label.png
📸 Scope selection          → 6. define the scope for this label - files & other data assets.png
📸 Access control settings  → 7. control who has access to these files.png
📸 Assigning permissions    → 8. assign the permissions immedialy when labelling the assets and items.png
📸 Groups & sites           → 9. Define protection settings for groups and sites...png
📸 External user access     → 10. external user access.png
📸 Conditional access       → 11. external sharing and conditional access setting.png
📸 Final review screen      → 12. reviewing your settings.png
```

**Task 1.2 — Embed images in azure_blob_storage_test.md** *(~15 min)*  
Replace the three image placeholders with embeds of `loan_confirmation_letter.png`, `debt_collection_letter.png`, and `blob_storage.png`.

**Task 1.3 — Fix README typos** *(~5 min)*  
Correct "consultatants" → "consultants" and "functioanlity" → "functionality".

**Task 1.4 — Consider embedding purview-enterprise-account.png in Prerequisites.md** *(~10 min)*  
This image exists and the Prerequisites file would benefit from a visual anchor near the "upgrade to Enterprise" section.

---

### Phase 2 — Medium Effort (Est. 3–6 hours)
**Goal: Make use cases demonstrable and testable**

**Task 2.1 — Complete blob storage test reproduction** *(2–4 hours)*  
Write the step-by-step test walkthrough section at the bottom of `azure_blob_storage_test.md`. This should show:
- Uploading the sample files to a blob container
- Running a Purview scan and seeing IBAN/BSN/passport number classifications appear
- Creating the auto-labeling policy
- Re-scanning and confirming label application
- (Optionally) Viewing the labeled asset in Fabric

Add relevant screenshots of the actual portal results. If you ran this test when building the repo, the screenshots may already exist locally.

**Task 2.2 — Build azure_sql_database_test.md from scratch** *(3–6 hours)*  
Recommended approach: mirror the blob storage use case structure:
- Choose a business scenario (e.g., a financial services company with a customer database)
- Create or reference sample SQL data containing IBANs, BSNs, or credit card numbers
- Document the scan → classification → label pipeline end-to-end
- Add a dummy SQL schema file to `dummy-files/` for credibility

---

### Phase 3 — Major Effort (Est. 12–20 hours)
**Goal: Deliver on the core promise of Fabric integration**

**Task 3.1 — Create Fabric integration documentation**  
This is the most strategically important piece and the one most absent from existing Microsoft documentation. Recommended file: `docs/fabric-integration.md`

Suggested sections:
- How sensitivity labels applied via Data Map flow into Fabric OneLake
- Querying label metadata in a Fabric Notebook (Python/Spark)
- DLP behavior when labeled blobs are ingested into a Lakehouse
- Power BI report labeling inheritance from labeled datasets
- Setting up workspace-level governance tied to Purview Unified Catalog

**Task 3.2 — Add a Fabric use case to use_cases/**  
A `fabric_lakehouse_test.md` showing an end-to-end scenario: sensitive blob data → Fabric Lakehouse ingestion → label preserved or enforced → Power BI report inherits label.

---

### Phase 4 — Future Work (Post-feedback)
**Task 4.1 — Create scripts/ folder**  
After initial community feedback validates which parts of the repo get most traction, build automation scripts for:
- Registering and scanning data sources via Purview REST API
- Querying classification results programmatically
- Creating sensitivity label policies via PowerShell

---

## 7. Collaboration vs. Solo Recommendation

### Solo work (you can do this alone):
- **Phase 1 (all tasks)** — purely editorial, no new Azure resources needed
- **Phase 2 (blob storage reproduction)** — you've already run this test; it's documentation work
- **Phase 2 (SQL use case)** — needs a demo Azure SQL instance but scope is well-defined

### Strongly consider collaboration for:
- **Phase 3 (Fabric integration)** — This requires:
  - Active Microsoft Fabric capacity (trial or paid)
  - Hands-on experience with OneLake, Lakehouses, and Fabric Notebooks
  - Understanding of how Purview label metadata flows across the Fabric estate
  - A Power BI professional who can validate the reporting/DLP angle

**Recommended: Draft a "call for collaboration" for the Fabric section.** The repo's README already positions it as built for cross-functional teams. A note in the README or a GitHub Discussion thread could attract:
- A Fabric-specialist data engineer who wants to document what they know
- A Power BI pro looking to document the governance angle
- A Microsoft MVP or FastTrack engineer who covers both Purview and Fabric

**Suggested call-for-collaboration framing:**
> "Looking for a Fabric or Power BI practitioner who has hands-on experience with sensitivity label inheritance in OneLake and Fabric Lakehouses. If you've implemented Purview governance in a Fabric environment and want to document it in a role-aware, accessible way — open an issue or reach out via LinkedIn."

---

## 8. On Using Claude.ai Projects for Persistent Context

**Recommendation: Yes — this is an ideal use case.**

The repo spans multiple files, has a consistent terminology layer (Data Map, SITs, sensitivity labels, auto-labeling policies, scan rule sets), and requires context about what's been built vs. what's planned. A Claude.ai Project lets you:

- Upload key files (`apply-purview-labels.md`, `classification-engines.md`, the images folder listing) once, so every new conversation starts with full context
- Maintain a running "completion log" as a project document
- Draft new sections (like the Fabric integration doc) iteratively across multiple sessions without re-explaining the repo structure each time

**Practical setup:**
1. Create a new project called "Purview Repo Completion"
2. Upload: README.md, all four docs files, the image inventory list (above), and this assessment document
3. Add a system prompt: "You are helping me complete a GitHub documentation repo about Microsoft Purview, Azure, and Fabric. Context files are attached. Current priority: Phase 1 image embedding."

Each work session then picks up cleanly from where you left off.

---

## 9. Overall Assessment

| File | Completeness | Effort to Finish | Priority |
|------|-------------|-----------------|----------|
| `README.md` | 98% (minor typos) | 5 min | Phase 1 |
| `getting-started-for-non-experts.md` | 100% ✅ | None | — |
| `Prerequisites.md` | 100% ✅ | None | — |
| `classification-engines.md` | 100% ✅ | None | — |
| `apply-purview-labels.md` | 70% (no images embedded) | 45 min | Phase 1 🔴 |
| `docs/images/` (17 files) | 100% ✅ | None | — |
| `azure_blob_storage_test.md` | 60% (no test reproduction) | 2–4 hrs | Phase 2 |
| `azure_sql_database_test.md` | 2% (placeholder only) | 3–6 hrs | Phase 2 |
| `scripts/` folder | 0% (doesn't exist) | 8–20 hrs | Phase 4 |
| Fabric integration docs | 0% (not started) | 12–20 hrs | Phase 3 (collab) |
| **dummy-files/** | 100% ✅ | None | — |

**Bottom line:** The repo is closer to done than it looks. Three of the four core docs files are production-ready. The single most impactful action — embedding the 17 screenshots that already exist — takes less than an hour and transforms the key walkthrough file from "looks broken" to "looks professional." Phase 1 alone would make this a repo worth sharing publicly.
