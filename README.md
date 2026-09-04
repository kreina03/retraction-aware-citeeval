# Retraction-Aware Citation Evaluation

Testing whether fine-grained citation-quality metrics (CiteEval-Auto) are blind to
citations of *retracted* biomedical papers, and proposing a retraction-aware extension.
Extends CiteEval (Xu et al., 2025).

## Data
- **Retraction Watch** (via Crossref/GitLab), accessed 2026-09-03 (retraction ground truth).
- **PubMed** (via NCBI E-utilities) — abstract text for cited passages.
All public, evaluation-only, no patient data.

## Structure
- 'data/raw/' — untouched source files (not committed)
- 'data/interim/' — processed intermediate data (e.g. tier1_pool.csv)
- 'data/final/' — frozen benchmark
- 'notebooks/' — pipeline, one per phase
- 'src/' — reusable functions

## Pipeline
1. 'notebooks/data_prep.ipynb' builds Tier-1 retracted-paper pool (14,984 papers) 
2. Step 2 — matched-pair construction (in progress)
