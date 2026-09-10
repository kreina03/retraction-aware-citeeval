# Retraction-Aware Citation Evaluation

Testing whether fine-grained citation-quality metrics (CiteEval-Auto) are blind to
citations of *retracted* biomedical papers, and proposing a retraction-aware extension.
Extends CiteEval (Xu et al., 2025).

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
2. 'notebooks/build_pairs.ipynb' matched-pair benchmark construction
   - claim extraction (GPT-4o-mini) -> PubMed control retrieval -> NLI entailment gate (DeBERTa-SciFact)
   - **frozen benchmark of 253 matched retracted/valid pairs** ('data/final/benchmark_pairs.csv')
3. 'notebooks/blindspot_evaluation.ipynb' scores citations to retracted
   papers with CiteEval-Auto + NLI/AIS
   - also contains a breakdown of the papers by their retraction reason and scores citations to retracted papers with both CiteEval-Auto and NLI/AIS
4. IN PROGRESS: retraction-aware extension lookup + proposing the 'deleted-retracted' action







3. 'notebooks/blindspot_evaluation.ipynb' scores citations to retracted
   papers with CiteEval-Auto + NLI/AIS; irrelevant-passage negative control; breakdown
   by retraction reason
4. The fix (in progress) — retraction-aware extension: lookup + `delete-retracted` action
