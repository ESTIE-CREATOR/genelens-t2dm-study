# Transcriptomic Workflow Demonstration — Type 2 Diabetes Liver
### Using GeneLens · Differential Expression · GO Enrichment · KEGG Pathways · ML Classification

**Author:** Alabi Esther Oluwatimilehin
**Institution:** University of Medical Sciences, Nigeria — BSc Biochemistry, First Class Honours
**Tool:** [GeneLens](https://github.com/ESTIE-CREATOR/GeneLens) · [Live App](https://genelens.streamlit.app)
**Date:** June 2026

---

> ⚠️ **Important Note**
>
> This repository demonstrates the GeneLens analysis workflow using a **synthetic dataset** constructed to resemble a Type 2 Diabetes liver expression study.
>
> The objective was to validate the statistical, enrichment, machine learning, and AI interpretation pipeline while developing GeneLens.
>
> The reported biological findings should be considered **illustrative** and not biological conclusions derived from original experimental data.
>
> **Primary real-data validation of GeneLens:** COVID-19 PBMC dataset (GSE152418, *Science* 2020) — 60,683 genes × 34 real patient samples. See [GeneLens](https://github.com/ESTIE-CREATOR/GeneLens).

---

## Overview

This repository presents a computational workflow demonstration using [GeneLens](https://github.com/ESTIE-CREATOR/GeneLens) on a synthetic Type 2 Diabetes liver dataset.

The study was motivated by my final-year biochemistry thesis, which measured antioxidant enzyme activity (SOD, CAT, GPx, GSH, MDA) in diabetic rat liver. This demonstration explores whether the same antioxidant genes studied in my thesis appear dysregulated in a T2DM-structured transcriptomics dataset — and uses this context to showcase the full GeneLens pipeline from raw counts to pathway-level interpretation.

---

## The Wet Lab → Computational Bridge

| Thesis Measurement | Gene | Direction | GO Term | KEGG Pathway |
|-------------------|------|-----------|---------|--------------|
| GPx activity ↓ | GPX1 | ↓ | GO:0006749 Glutathione process | hsa00480 Glutathione metabolism |
| GSH synthesis ↓ | GCLM | ↓ | GO:0006749 Glutathione process | hsa00480 Glutathione metabolism |
| GSH levels ↓ | GSR | ↓ | GO:0006749 Glutathione process | hsa00480 Glutathione metabolism |
| SOD activity ↓ | SOD2 | ↓ trend | — | — |
| CAT activity ↓ | CAT | ↓ trend | — | — |
| MDA levels ↑ | CYP2E1 | ↑ | GO:0072593 ROS metabolic process | hsa04932 NAFLD |

> This table illustrates the conceptual connection between wet-lab biochemistry and transcriptomic pipeline outputs — not experimental validation.

---

## Dataset

| Parameter | Detail |
|-----------|--------|
| Type | **Synthetic demonstration dataset** |
| Reference biology | Published T2DM transcriptomics literature |
| Structure | 226 curated metabolic and oxidative stress genes |
| Samples | 5 Normal conditions, 8 T2DM conditions |
| Gene directions | Derived from published T2DM fold-change literature |
| Download | [Diabetic_Liver_RNA-seq.csv](https://github.com/user-attachments/files/28788734/Diabetic_Liver_RNA-seq.csv) |

> This is not a direct download from NCBI GEO. Gene expression directions and magnitudes were constructed to reflect published T2DM biology for pipeline demonstration purposes.

---

## Results Summary

| Category | Count |
|----------|-------|
| Total genes | 226 |
| Upregulated | 6 |
| Downregulated | 12 |
| Not significant | 208 |

> Results are outputs of the GeneLens pipeline on this synthetic dataset and are illustrative only.

---

## Figures

### Volcano Plot
<img width="1918" height="877" alt="Image" src="https://github.com/user-attachments/assets/d2528e19-c859-4b4f-a5ef-e8ab85319d89" />

*Red = upregulated (CYP2E1, PCK1). Blue = downregulated (GPX1, GCLM, GSR)*

### Heatmap
<img width="1919" height="879" alt="Image" src="https://github.com/user-attachments/assets/e6317568-e7e0-48ac-91a5-61f0d985ffce" />

### PCA — Sample Clustering
<img width="1919" height="877" alt="Image" src="https://github.com/user-attachments/assets/c0fdf5ae-aacf-4589-bcd9-917c22df1d9d" />

### GO Enrichment
<img width="1919" height="943" alt="Image" src="https://github.com/user-attachments/assets/1f415041-4918-4d2a-932d-954a9172ff04" />

*Glutathione metabolic process — most depleted GO term*

### KEGG Pathways
<img width="1919" height="948" alt="Image" src="https://github.com/user-attachments/assets/e79afb9c-c05f-4051-a77d-dbd09504edc8" />

*Insulin signalling (p=1.86e-08) · Glutathione metabolism · Type II diabetes mellitus*

### ML Classification — ROC Curve
<img width="1919" height="885" alt="Image" src="https://github.com/user-attachments/assets/581f2724-8a13-476f-9411-43ffc6b91fc7" />

---

## Top GO Terms (Illustrative)

| GO Term | Biological Process | p-adj |
|---------|-------------------|-------|
| GO:0042593 | **Glucose homeostasis** | 6.00e-07 |
| GO:0033500 | Carbohydrate homeostasis | 1.21e-06 |
| GO:0006749 | **Glutathione metabolic process** | 1.19e-03 |
| GO:0045454 | Cell redox homeostasis | 1.19e-03 |

## Top KEGG Pathways (Illustrative)

| KEGG ID | Pathway | p-adj |
|---------|---------|-------|
| hsa04910 | **Insulin signaling pathway** | 1.86e-08 |
| hsa04932 | Non-alcoholic fatty liver disease | 1.21e-05 |
| hsa04930 | **Type II diabetes mellitus** | 1.52e-04 |
| hsa00480 | **Glutathione metabolism** | 2.54e-04 |

---

## Methods

| Step | Method |
|------|--------|
| DE Analysis | Welch's t-test + BH FDR (padj < 0.05, FC ≥ 1.5) |
| GO Enrichment | GO_Biological_Process_2021 via Enrichr API \[1,2\] |
| KEGG Enrichment | KEGG_2021_Human via Enrichr API \[2,3\] |
| ML Classification | Random Forest (200 trees, 5-fold CV) |
| AI Interpretation | Anthropic Claude API |
| Tool | [GeneLens](https://github.com/ESTIE-CREATOR/GeneLens) |

---

## Full Report

📄 [`report/GeneLens_CaseStudy_T2Diabetes.md`](report/GeneLens_CaseStudy_T2Diabetes.md)

---

## How to Reproduce

```bash
# Open GeneLens: https://genelens.streamlit.app
# Upload: Diabetic_Liver_RNA-seq.csv (link above)
# Control columns: Normal_1 to Normal_5
# Treated columns: T2Diabetes_1 to T2Diabetes_8
# Parameters: padj < 0.05, FC threshold 1.5
```

---

## References

1. Ashburner M, et al. (2000). Gene ontology: tool for the unification of biology. *Nat Genet*, 25(1):25–29. — *GO database used for GO enrichment*

2. Kuleshov MV, et al. (2016). Enrichr: a comprehensive gene set enrichment analysis web server. *Nucleic Acids Res*, 44(W1):W90–97. — *Enrichr API used by GeneLens*

3. Kanehisa M, Goto S. (2000). KEGG: Kyoto Encyclopedia of Genes and Genomes. *Nucleic Acids Res*, 28(1):27–30. — *KEGG database used for pathway enrichment*

---

## Related

- 🔬 [GeneLens tool](https://github.com/ESTIE-CREATOR/GeneLens)
- 🌐 [Live app](https://genelens.streamlit.app)
- 👤 [linkedin.com/in/alabi-esther-essie](https://linkedin.com/in/alabi-esther-essie)

---
*Alabi Esther Oluwatimilehin · github.com/ESTIE-CREATOR · June 2026*
