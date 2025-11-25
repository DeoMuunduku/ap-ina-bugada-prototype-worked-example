AP-InA Worked Example (BugAda / Bugzilla–Jira incidents)

This repository provides a reproducible worked example instantiating the
AP-InA minimal audit criteria (R–A–U–H–T–P–O–I/N) on a dataset inspired by BugAda
(Bugzilla/Jira incident reports).

The example demonstrates how AP-InA can be integrated into an Information System (IS)
and which audit artefacts are produced: allowlists, versioned resources, traces,
provenance logs, and eligibility/audit tables.
📄 Related paper

Towards Traceable Meaning in Information Systems
Déo Munduku, Elsa Negre
Accepted at ICIM 2026, University of Oxford (March 27–29, 2026).
To appear in Springer CCIS.

We will update this repository with the final camera-ready version and metadata once available.
1. 📚 Literature Review Reproducibility Package

This section contains all artefacts promised in the article.

1.1 PRISMA Flow Diagram

The PRISMA diagram used in the paper is available here:

<img width="1571" height="1580" alt="prisma 2 drawio" src="https://github.com/user-attachments/assets/775e85a0-1810-4843-8bc4-0f32488c6bbc" />



2. 🧪 AP-InA Worked Example (BugAda)

This example shows how AP-InA operates on incident cards.

⸻

2.1 📦 Repository Structure
.
├── src/
│   ├── step1_prepare_cards_clean.py
│   ├── step2_generate_silver_labels.py
│   ├── step3_make_splits_dev_holdoutH.py
│   ├── step4_calibrate_tau_and_run_protocol.py
│   └── step5_eval_gate_vs_gold.py
│
├── artefacts_sample/ final_bugada_H_tau045
│   ├── DATACARD.md
│   ├── dataset_stats.json
│   ├── feature_allowlist.txt
│   ├── eligibility_audit.csv
│   ├── traces_sample/         ← 10-20 trace examples
│   └── prov_sample/           ← 10-20 provenance examples
│
├── releases/
│   └── final_bugada_H_tau045.zip   ← (Full traces / full prov / resources)
│
└── README.md

Example of AP-InA Trace (T)

This is one of the JSON files inside
final_bugada_H_tau045/traces/:
{
   "episode_id": "BUG-10954",
   "ts": "1999-07-30T22:55:51Z",
   "input": {
      "title": "[BUGS] Settings UI RESOLVED",
      "component": "Settings UI",
      "severity": "medium",
      "desc_len": 46,
      "has_keyword_crash": false,
      "security_flag": false,
      ...
   },
   "context": {
      "team": "ops-L1",
      "recent_incidents_1h": 0,
      "policy": "policy@tau=0.45",
      "policy_decl": "T=0.2; tau=0.45; delta=0.15"
   },
   "branch_scores": {
      "m": { "release_regression": 0.0, "infra_instability": 0.0, ... },
      "c": { "release_regression": 0.0, "infra_instability": 0.0, ... }
   }
}
