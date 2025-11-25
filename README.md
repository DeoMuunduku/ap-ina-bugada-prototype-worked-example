# AP-InA Worked Example (BugAda / Bugzilla–Jira incidents)

This repository provides a small, reproducible **worked example** that instantiates the **AP-InA** minimal criteria
(**R–A–U–H–T–P–O–I/N**) in an incident-dashboard setting, using BugAda-style Bugzilla/Jira tickets as incident cards.

It is designed to show **how AP-InA can be integrated into an Information System (IS)** and which **audit artefacts**
are produced (allowlists, traces, provenance logs, audit tables, and outcome metrics).

## Related paper
**Towards Traceable Meaning in Information Systems** (Deo Munduku, Elsa Negre).  
Accepted at **ICIM 2026**, University of Oxford, Oxford, UK (Mar 27–29, 2026).  
*To appear in the conference proceedings.*  
(We will update the final bibliographic reference once official metadata is available.)

## What the pipeline does (high level)
We treat each bug report as an **incident card** described only by **early / available-at-creation** fields (**anti-leakage**).
Then we:

1. **Prepare clean incident cards** + QC reports + anti-leakage allowlist  
2. Generate **silver labels** (deterministic rules) to operationalize candidate meanings **H**  
3. Create **DEV / HOLDOUT-H** splits (deterministic seed)  
4. Calibrate a **gating threshold (τ)** to target an abstention rate (e.g., 20%), run the gate, and generate:
   - `eligibility_audit.csv`
   - per-incident **trace logs** (`traces/`)
   - per-incident **provenance logs** (`prov/`)
   - figures (decision distribution, p_top histograms, latency, sweep curves)
5. Evaluate gate behaviour against **GOLD labels** (coverage & abstention metrics)

## Repository content
### Code
Current scripts (recommended names / mapping):
- `src/step1_prepare_cards_clean.py`  (prepare cards + QC + datacard + allowlist)
- `src/step2_generate_silver_labels.py` (silver labels)
- `src/step3_make_splits_dev_holdoutH.py` (DEV/H split)
- `src/step4_calibrate_tau_and_run_protocol.py` (τ sweep + protocol run + traces/prov)
- `src/step5_eval_gate_vs_gold.py` (gate vs gold evaluation)

> Note: these scripts were initially developed in a single Colab notebook and exported here.

### Sample artefacts (lightweight)
We include a small `artefacts_sample/` folder with:
- `DATACARD.md`, `dataset_stats.json`, `feature_allowlist.txt`
- a few key figures used for the paper
- a small sample of `traces/` and `prov/` (10–20 incidents)
- `eligibility_audit.csv` (DEV and/or HOLDOUT-H)

### Full artefacts (optional)
Full generated outputs may be large. For convenience, we provide them as **Release assets** (ZIP), not tracked in git.

## How to run (typical)
Python 3.10+ recommended.

```bash
pip install -r requirements.txt
python src/step1_prepare_cards_clean.py
python src/step2_generate_silver_labels.py
python src/step3_make_splits_dev_holdoutH.py
python src/step4_calibrate_tau_and_run_protocol.py
python src/step5_eval_gate_vs_gold.py
