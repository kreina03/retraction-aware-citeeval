# Retraction-Aware Citation Evaluation

Testing whether fine-grained citation-quality metrics (CiteEval-Auto) are blind to
citations of *retracted* biomedical papers, and proposing a retraction-aware extension.
Extends CiteEval (Xu et al., 2025). Code and data for the seminar paper 'Retraction-Aware Citation Evaluation' (Augmentation Methods for Language Models, Summer 2026)

## Data
- **Retraction Watch** (via Crossref/GitLab), accessed 2026-09-03 (retraction ground truth).
- **PubMed** (via NCBI E-utilities) — abstract text for cited passages.
All public, evaluation-only, no patient data.

## Key finding
CiteEval-Auto gives a mean rating of **4.99 / 5** (99% rated the maximum) on 253 citations to retracted biomedical papers, 
and NLI/AIS rates **100%** as "supported". Both correctly floor irrelevant controls. 
Standard citation metrics are blind to retraction and reward the citations that should never be made.

## Structure
- 'data/raw/' — untouched source files (not committed)
- 'data/interim/' — processed intermediate data (e.g. tier1_pool.csv)
- 'data/final/' — frozen benchmark
- 'notebooks/' — pipeline, one per phase
- 'src/' — reusable functions

## Pipeline
1. 'notebooks/data_prep.ipynb' builds Tier-1 retracted-paper pool (14,984 papers) 
2. 'notebooks/build_pairs.ipynb' benchmark construction
   - claim extraction (GPT-4o-mini) -> PubMed retrieval -> NLI entailment gate (DeBERTa-SciFact)
   - **frozen benchmark of 253 retracted-paper claims** ('data/final/benchmark_pairs.csv')
3. 'notebooks/blindspot_evaluation.ipynb' scores citations to retracted
   papers with CiteEval-Auto + NLI/AIS
   - also contains a breakdown of the papers by their retraction reason and scores citations to retracted papers with both CiteEval-Auto and NLI/AIS
4. 'notebooks/retraction_aware_fix.ipynb' creates the missing retracted paper label and gives the 'delete-retracted' action
