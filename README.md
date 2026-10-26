# Terpedia Fusarium proliferatum D-limonene transcriptomics audit

This forkable project audits the published RNA-seq and acetylation-associated pathway tables for [Zhou et al.'s D-limonene study](https://link.springer.com/article/10.1186/s12864-025-12389-w). The [executed Jupyter notebook](notebooks/terputer-fusarium-proliferatum-dlimonene-supplement.ipynb), [generated white paper](research/fusarium-proliferatum-dlimonene-supplement/generated/white-paper.md), [claim ledger](research/fusarium-proliferatum-dlimonene-supplement/generated/claim-ledger.tsv), [result tables](research/fusarium-proliferatum-dlimonene-supplement/results/), and [receipts](research/fusarium-proliferatum-dlimonene-supplement/generated/generation-receipt.json) are committed.

The publisher's DEG table has 2,375 unique feature rows, including 1,135 up and 1,240 down. The paper reports 1,134 up genes. `rrna13` is the extra up entry outside the `FPRO_` pattern, but four down entries also have `rrna` IDs, so the source does not document a uniform exclusion rule. Only ribosome (`ko03010`) has adjusted p < 0.05 in the supplied H3K9ac-associated KEGG list; no H3K27ac-associated term does. These are checks of author-computed tables, not new raw-read differential expression, direct target evidence, or cross-study replication.

The [publisher workbook](https://static-content.springer.com/esm/art%3A10.1186%2Fs12864-025-12389-w/MediaObjects/12864_2025_12389_MOESM2_ESM.xlsx) is checksum-pinned and kept out of Git. Raw RNA-seq reads are under [PRJNA1234870](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA1234870).

## Reproduce

```sh
python -m pip install -r requirements.txt
python restore-inputs.py research/fusarium-proliferatum-dlimonene-supplement/report-spec.json
python notebook-runner.py notebooks/terputer-fusarium-proliferatum-dlimonene-supplement.ipynb . 120 '["research/fusarium-proliferatum-dlimonene-supplement/results/analysis_summary.json","research/fusarium-proliferatum-dlimonene-supplement/results/published_degs.tsv","research/fusarium-proliferatum-dlimonene-supplement/results/acetylation_pathways.tsv","research/fusarium-proliferatum-dlimonene-supplement/results/sample_qc.tsv"]' '["research/fusarium-proliferatum-dlimonene-supplement/data/12864_2025_12389_MOESM2_ESM.xlsx"]'
node report-generator.mjs research/fusarium-proliferatum-dlimonene-supplement/report-spec.json
```

To attach a fork to your `terpedia-report` workspace, fork this repository into your GitHub account under the same repository name and use `add_research_project_submodule` with slug `fusarium-proliferatum-dlimonene-supplement`. The submodule path is `projects/fusarium-proliferatum-dlimonene-supplement`.
