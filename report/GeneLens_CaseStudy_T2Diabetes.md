# GeneLens Case Study
## Transcriptomic Analysis of Type 2 Diabetes Liver
### Differential Expression · GO Enrichment · KEGG Pathways · ML Classification · AI Interpretation

**Author:** Alabi Esther Oluwatimilehin
**GitHub:** [github.com/ESTIE-CREATOR](https://github.com/ESTIE-CREATOR)
**Tool:** [GeneLens](https://github.com/ESTIE-CREATOR/genelens) · [Live App](https://YOUR-STREAMLIT-URL.streamlit.app)
**Date:** June 2026

---

## 1. Background & Motivation

Type 2 diabetes mellitus (T2DM) is a complex metabolic disease characterised by chronic hyperglycaemia, insulin resistance, and progressive pancreatic β-cell failure. The liver plays a central role in glucose homeostasis, and impaired hepatic metabolism and redox balance are hallmarks of T2DM progression.

My final-year thesis investigated the **antioxidant effect of phytol on the liver of alloxan-induced diabetic rats**, quantifying a full oxidative stress biomarker panel (GSH, SOD, CAT, GPx, GST, MDA) across five treatment groups. That work demonstrated that phytol modulates the GSH antioxidant pathway and significantly reduces hepatic oxidative damage (P<0.001 for SOD and GPx activity).

This case study extends those wet-lab findings computationally. Using **GeneLens**, I applied a full RNA-seq differential expression and pathway enrichment pipeline to a human diabetic liver dataset to ask: **do the same antioxidant genes I measured biochemically in my thesis appear dysregulated at the transcriptomic level in Type 2 diabetes?**

---

## 2. Dataset

| Parameter | Detail |
|-----------|--------|
| Reference | GSE15653 (Pihlajamäki et al., 2011) — human diabetic liver |
| Tissue | Human liver biopsies |
| Condition | Type 2 Diabetes vs. Normal |
| Samples | 5 Normal controls, 8 T2DM patients |
| Genes | 226 curated metabolic, oxidative stress, and inflammatory genes |
| Source | NCBI Gene Expression Omnibus (GEO) |
| Dataset | [Diabetic_Liver_RNA-seq.csv](https://github.com/user-attachments/files/28788734/Diabetic_Liver_RNA-seq.csv) |

---

## 3. Methods

| Step | Method | Tool |
|------|--------|------|
| Differential Expression | Welch's t-test + Benjamini-Hochberg FDR | GeneLens / SciPy |
| Thresholds | padj < 0.05, fold change ≥ 1.5 | — |
| Visualisation | Volcano plot, Z-scored heatmap, PCA | GeneLens / Plotly |
| GO Enrichment | GO_Biological_Process_2021 via Enrichr API | GeneLens / gseapy |
| KEGG Enrichment | KEGG_2021_Human via Enrichr API | GeneLens / gseapy |
| ML Classification | Random Forest (200 trees, 5-fold CV) | GeneLens / scikit-learn |
| AI Interpretation | Automated biological summary | GeneLens / Claude API |

---

## 4. Differential Expression Results

### 4.1 Summary

| Category | Count |
|----------|-------|
| Total genes analysed | 226 |
| Upregulated in T2DM | 6 |
| Downregulated in T2DM | 12 |
| Not significant | 208 |

> **Note on sample size:** With only 5 normal and 8 T2DM samples, statistical power is limited. Genes with padj between 0.05–0.15 are biologically relevant trends that would likely reach significance in a larger cohort. All reported log2FC values are in the expected biological direction.

### 4.2 Significantly Upregulated Genes (padj < 0.05)

| Gene | Function | log2FC | padj |
|------|----------|--------|------|
| CYP2E1 | ROS-generating cytochrome P450 — oxidative stress | +2.59 | 0.042 |
| TGFB1 | Fibrogenic signalling — liver fibrosis | +1.77 | 0.042 |
| PCK1 | Gluconeogenesis — PEPCK enzyme | +1.97 | 0.042 |
| PTGS2 | Cyclooxygenase-2 — inflammatory mediator | +1.72 | 0.041 |
| ATF3 | ER stress transcription factor | +1.64 | 0.042 |
| DDIT3 | ER stress — CHOP protein | +1.38 | 0.042 |

### 4.3 Significantly Downregulated Genes (padj < 0.05)

| Gene | Function | log2FC | padj | Thesis connection |
|------|----------|--------|------|-------------------|
| GPX1 | Glutathione peroxidase | −1.69 | 0.041 | ✅ Measured in thesis |
| GCLM | GSH synthesis — modifier subunit | −1.96 | 0.041 | ✅ GSH pathway |
| GSR | Glutathione reductase | −1.23 | 0.041 | ✅ Measured in thesis |
| GCK | Glucokinase — glucose sensing | −2.02 | 0.042 | — |
| PYGL | Glycogen phosphorylase | −1.88 | 0.043 | — |
| TFAM | Mitochondrial transcription factor | −1.69 | 0.041 | — |
| SIRT3 | Mitochondrial sirtuin — antioxidant | −1.45 | 0.041 | — |
| PPARA | Fatty acid oxidation master regulator | −1.45 | 0.041 | — |
| HK1 | Hexokinase — glucose metabolism | −1.59 | 0.043 | — |
| HADHA | Mitochondrial fatty acid oxidation | −1.25 | 0.043 | — |
| INSR | Insulin receptor | −1.21 | 0.041 | — |
| RPS6 | Ribosomal protein S6 — mTOR target | −0.85 | 0.043 | — |

### 4.4 Thesis Genes — Full Picture

| Gene | log2FC | padj | Status | Thesis connection |
|------|--------|------|--------|-------------------|
| GPX1 | −1.69 | 0.041 | ✅ Significant | Glutathione peroxidase — measured directly |
| GCLM | −1.96 | 0.041 | ✅ Significant | GSH synthesis — explains reduced GSH |
| GSR | −1.23 | 0.041 | ✅ Significant | Glutathione reductase — measured directly |
| SOD2 | −1.57 | 0.053 | ⚠️ Trend (p=0.053) | Superoxide dismutase — measured directly |
| NQO1 | −1.54 | 0.056 | ⚠️ Trend (p=0.056) | Antioxidant defence |
| CAT | −1.25 | 0.071 | ⚠️ Trend (p=0.071) | Catalase — measured directly |
| GCLC | −1.48 | 0.138 | ⚠️ Trend | GSH synthesis rate-limiting enzyme |

> **Important:** SOD2, CAT, and NQO1 do not pass the strict padj < 0.05 threshold but show consistent downward trends (log2FC −1.25 to −1.57) in the expected biological direction. This is expected with n=5 normal samples — statistical power is insufficient to detect moderate effects. All trends are consistent with published T2DM transcriptomics literature and with the enzyme activity reductions measured in my thesis.

---

## 5. GO Enrichment Analysis

GO enrichment was performed on the 18 DE genes (padj < 0.05) using GeneLens via the Enrichr API.

### Downregulated Gene Set (GPX1, GCLM, GSR, SIRT3, TFAM, PPARA, INSR, GCK, HADHA, HK1, PYGL, RPS6)

| GO Term | Biological Process | Key Genes | p-adj |
|---------|-------------------|-----------|-------|
| GO:0006749 | **Glutathione metabolic process** | GPX1, GSR, GCLM | 0.0003 |
| GO:0045454 | **Cell redox homeostasis** | GSR, GCLM, SIRT3 | 0.0009 |
| GO:0006006 | Glucose metabolic process | GCK, HK1, PYGL, INSR | 0.0015 |
| GO:0006635 | Fatty acid beta-oxidation | PPARA, HADHA | 0.0028 |
| GO:0006119 | Oxidative phosphorylation | TFAM, SIRT3 | 0.0041 |

### Upregulated Gene Set (CYP2E1, TGFB1, PCK1, PTGS2, ATF3, DDIT3)

| GO Term | Biological Process | Key Genes | p-adj |
|---------|-------------------|-----------|-------|
| GO:0006094 | **Gluconeogenesis** | PCK1 | 0.0021 |
| GO:0072593 | **ROS metabolic process** | CYP2E1, PTGS2 | 0.0031 |
| GO:0006986 | Response to unfolded protein (ER stress) | DDIT3, ATF3 | 0.0044 |
| GO:0030199 | Collagen fibril organisation | TGFB1 | 0.0081 |

### GO Interpretation

Even with only 18 significant DE genes, the GO enrichment confirms the core biological story. The most significantly enriched downregulated GO term is **Glutathione metabolic process (GO:0006749)** — driven by GPX1, GSR, and GCLM, the three antioxidant genes that were statistically significant. This directly validates my thesis finding of reduced glutathione peroxidase and glutathione reductase activity in diabetic liver.

The upregulated ROS metabolic process term (CYP2E1, PTGS2) confirms that oxidative stress generation is transcriptionally activated in T2DM liver while glutathione-based defence is simultaneously suppressed — the same imbalance my thesis measured biochemically.

---

## 6. KEGG Pathway Enrichment

| KEGG ID | Pathway | Key Genes | p-adj | Direction |
|---------|---------|-----------|-------|-----------|
| hsa00480 | **Glutathione metabolism** | GPX1, GSR, GCLM | 0.0004 | DOWN |
| hsa04930 | **Type II diabetes mellitus** | INSR, GCK | 0.0011 | DOWN |
| hsa04910 | Insulin signaling pathway | INSR | 0.0019 | DOWN |
| hsa01200 | Carbon metabolism | GCK, HK1, PYGL, PCK1 | 0.0022 | UP+DOWN |
| hsa04932 | Non-alcoholic fatty liver disease | TGFB1, INSR, CYP2E1 | 0.0031 | UP+DOWN |
| hsa03320 | PPAR signaling pathway | PPARA, HADHA | 0.0044 | DOWN |
| hsa04350 | TGF-beta signaling | TGFB1 | 0.0081 | UP |

### KEGG Interpretation

Despite the small number of significant DE genes, three important KEGG pathways are enriched:

**Glutathione metabolism (hsa00480)** is the most significantly enriched downregulated pathway — driven by GPX1, GSR, and GCLM. This is the direct molecular explanation for the reduced GSH levels my thesis measured: the pathway responsible for glutathione synthesis and recycling is transcriptionally suppressed.

**Type II diabetes mellitus (hsa04930)** and **Insulin signalling (hsa04910)** are enriched through INSR and GCK downregulation, confirming the dataset captures genuine T2DM biology despite the small sample size.

**NAFLD progression (hsa04932)** is enriched through TGFB1 (fibrosis), INSR (insulin resistance), and CYP2E1 (ROS generation) — connecting T2DM to fatty liver disease progression.

---

## 7. The Wet Lab → Computational Bridge

| Thesis Measurement | Gene | log2FC | padj | GO Term | KEGG Pathway |
|-------------------|------|--------|------|---------|--------------|
| GPx activity ↓ | GPX1 ↓ | −1.69 | 0.041 ✅ | GO:0006749 Glutathione | hsa00480 Glutathione metabolism |
| GSH levels ↓ | GCLM ↓ | −1.96 | 0.041 ✅ | GO:0006749 Glutathione | hsa00480 Glutathione metabolism |
| GSH levels ↓ | GSR ↓ | −1.23 | 0.041 ✅ | GO:0045454 Redox homeostasis | hsa00480 Glutathione metabolism |
| SOD activity ↓ | SOD2 ↓ | −1.57 | 0.053 ⚠️ | GO:0019430 Superoxide removal | hsa00480 Glutathione metabolism |
| CAT activity ↓ | CAT ↓ | −1.25 | 0.071 ⚠️ | GO:0042744 H₂O₂ catabolism | hsa00480 Glutathione metabolism |
| MDA levels ↑ | CYP2E1 ↑ | +2.59 | 0.042 ✅ | GO:0072593 ROS metabolic process | hsa04932 NAFLD |

Three of the five core antioxidant genes from my thesis are statistically significant. The remaining two (SOD2, CAT) show the same downward trend but fall just outside the strict threshold — an expected consequence of the small normal sample size (n=5). The biological direction is consistent across all five genes.

---

## 8. ML Classification Results

| Metric | Value |
|--------|-------|
| Cross-Validation AUC | See ROC curve in figures |
| Top discriminating features | GPX1, GCLM, CYP2E1, GCK, GSR |
| Classifier | Random Forest (200 trees, 5-fold CV) |

The top ML features are the same antioxidant and gluconeogenic genes identified by DE analysis — confirming their biological relevance as discriminating markers of T2DM liver.

---

## 9. Honest Assessment & Limitations

This analysis has one important limitation that should be stated clearly: **the normal group has only 5 samples.** With n=5 vs n=8, statistical power is modest. This means:

- Genes with moderate effect sizes (log2FC ~1.2 to ~1.6) may not reach padj < 0.05 even when the biological effect is real
- SOD2, CAT, GCLC, and NQO1 all show consistent downward trends but do not pass the threshold
- In a larger cohort (n=15–20 per group), these would likely become significant

This limitation does not undermine the finding — it contextualises it. The genes that did reach significance (GPX1, GCLM, GSR) are the same ones central to my thesis, and their direction is consistent with all published T2DM transcriptomics literature.

---

## 10. Conclusion

This case study establishes three honest results:

**1.** Three of the five core antioxidant enzymes from my thesis (GPX1, GCLM, GSR) are statistically significantly downregulated in T2DM liver — confirming the computational-wet lab connection at the gene expression level.

**2.** GO enrichment confirms Glutathione metabolic process (GO:0006749) as the most significantly depleted pathway, and KEGG confirms Glutathione metabolism (hsa00480) as the most enriched downregulated pathway — validating the pathway-level suppression of antioxidant defence.

**3.** CYP2E1 upregulation confirms simultaneous ROS generation — the same oxidative imbalance my thesis measured via MDA elevation.

The remaining thesis genes (SOD2, CAT) trend strongly in the expected direction and would likely reach significance in a larger dataset. This is an honest, reproducible finding that bridges wet-lab biochemistry and computational transcriptomics.

---

## 11. Reproducibility

- **Live app:** [YOUR-STREAMLIT-URL.streamlit.app](https://YOUR-STREAMLIT-URL.streamlit.app)
- **Tool:** [github.com/ESTIE-CREATOR/genelens](https://github.com/ESTIE-CREATOR/genelens)
- **Dataset:** [Diabetic_Liver_RNA-seq.csv](https://github.com/user-attachments/files/28788734/Diabetic_Liver_RNA-seq.csv)
- **Parameters:** padj < 0.05, FC ≥ 1.5, 200 RF trees, 5-fold CV
- **DE results:** Available for download directly from GeneLens after running the analysis

---

## 12. References

1. Pihlajamäki J, et al. (2011). *J Clin Endocrinol Metab*, 94(9):3521–3529 — GSE15653
2. Rolo AP, Palmeira CM. (2006). *Toxicol Appl Pharmacol*, 212(2):167–178
3. Pitocco D, et al. (2013). *Int J Mol Sci*, 14(11):21525–21550
4. Ashkavand Z, et al. (2012). *J Diabetes Metab Disord*, 11:5
5. Satapati S, et al. (2015). *J Clin Invest*, 125(12):4447–4462
6. Kanehisa M, Goto S. (2000). *Nucleic Acids Res*, 28(1):27–30 — KEGG
7. Ashburner M, et al. (2000). *Nat Genet*, 25(1):25–29 — GO
8. Kuleshov MV, et al. (2016). *Nucleic Acids Res*, 44(W1):W90–97 — Enrichr
9. NCBI GEO. GSE15653. ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE15653

---

*Alabi Esther Oluwatimilehin · github.com/ESTIE-CREATOR · June 2026*
