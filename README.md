# Academic Paper Recommendation

MSc project repository for building and evaluating an academic paper recommendation system.  
This repo currently focuses on the technical implementation, starting with data collection from arXiv.

## Data Collection (arXiv)

The notebook `arxiv-data-collection.ipynb` collects papers from selected categories (`cs.LG`, `cs.CL`, `cs.AI`, `stat.ML`) using the arXiv API, applies date filtering, deduplicates records, and writes:
- `data/papers.jsonl`
- `data/dataset_metadata.json`

The script handles arXiv pagination limits by switching sort order when needed (descending to ascending) so larger datasets can be collected safely.

## OpenAlex Enrichment

The notebook `openalex_enrich.ipynb` enriches collected papers with OpenAlex metadata using DOI-first matching and title-based fallback.

It writes:
- `data/openalex_enriched.jsonl`
- `data/openalex_enrichment_metadata.json`

API failures are handled gracefully: records that still fail after retries are skipped and marked in the output.

## Reproducibility Note

Re-running the data collection notebook may produce a different dataset over time (new submissions, metadata updates, API ordering effects).  
This means future experiment results can change if the dataset is regenerated.

## Quick Start

```bash
conda env create -f environment.yml
conda activate msc-paper-recommendation
jupyter lab
```