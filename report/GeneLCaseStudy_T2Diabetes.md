[GeneLens_CaseStudy_T2Diabetes_Final.md](https://github.com/user-attachments/files/28789232/GeneLens_CaseStudy_T2Diabetes_Final.md)
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

This case study extends those wet-lab findings computationally. Using **GeneLens**, I applied a full RNA-seq differential expression and pathway enrichment pipeline to a human diabetic liver dataset to ask: **do the same antioxidant genes I measured biochemically in my thesis appear dysregulated at the transcriptomic and pathway level in Type 2 diabetes?**

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
| Upregulated in T2DM | ~22 |
| Downregulated in T2DM | ~26 |
| Not significant | ~178 |

### 4.2 Key Upregulated Genes

| Gene | Function | log2FC |
|------|----------|--------|
| CYP2E1 | ROS-generating cytochrome P450 | +2.35 |
| G6PC | Gluconeogenesis — glucose-6-phosphatase | +2.07 |
| COL1A1 | Liver fibrosis marker | +2.17 |
| IL6 | Pro-inflammatory cytokine | +2.04 |
| NOX4 | NADPH oxidase — ROS production | +1.96 |
| PCK1 | Gluconeogenesis — PEPCK | +1.93 |
| TNF | Pro-inflammatory cytokine | +1.93 |
| TGFB1 | Fibrogenic signalling | +1.72 |

### 4.3 Key Downregulated Genes

| Gene | Function | log2FC | Thesis connection |
|------|----------|--------|-------------------|
| GPX1 | Glutathione peroxidase | −2.00 | ✅ Measured in thesis |
| SOD2 | Superoxide dismutase | −1.84 | ✅ Measured in thesis |
| GCLC | GSH synthesis — rate-limiting enzyme | −1.89 | ✅ GSH pathway |
| GSR | Glutathione reductase | −1.74 | ✅ Measured in thesis |
| CAT | Catalase | −1.64 | ✅ Measured in thesis |
| GCLM | GSH synthesis modifier subunit | −1.60 | ✅ GSH pathway |
| NQO1 | Antioxidant — quinone oxidoreductase | −1.51 | ✅ Antioxidant defence |
| SIRT1 | Metabolic and antioxidant regulator | −1.74 | — |
| PPARA | Fatty acid oxidation master regulator | −1.74 | — |
| INSR | Insulin receptor | −1.51 | — |

---

## 5. GO Enrichment Analysis

### Downregulated Gene Set

| GO Term | Biological Process | Genes | p-adj |
|---------|-------------------|-------|-------|
| GO:0006749 | **Glutathione metabolic process** | SOD2, GPX1, GSR, GCLC, GCLM | 0.0001 |
| GO:0042744 | Hydrogen peroxide catabolic process | CAT, GPX1, PRDX3 | 0.0003 |
| GO:0019430 | Removal of superoxide radicals | SOD2, PRDX3, TXN2 | 0.0005 |
| GO:0045454 | **Cell redox homeostasis** | TXN2, TXNRD2, GSR, PRDX3 | 0.0008 |
| GO:0006119 | Oxidative phosphorylation | TFAM, SIRT3, SDHA | 0.0012 |
| GO:0006006 | Glucose metabolic process | GCK, PYGL, HK1, INSR | 0.0015 |
| GO:0006635 | Fatty acid beta-oxidation | PPARA, ACOX1, HADHA, CPT1A | 0.0024 |

### Upregulated Gene Set

| GO Term | Biological Process | Genes | p-adj |
|---------|-------------------|-------|-------|
| GO:0006094 | **Gluconeogenesis** | G6PC, PCK1, FBP1, PPARGC1A | 0.0001 |
| GO:0006954 | **Inflammatory response** | TNF, IL6, IL1B, CCL2 | 0.0002 |
| GO:0072593 | **ROS metabolic process** | CYP2E1, NOX4, PTGS2 | 0.0009 |
| GO:0030199 | Collagen fibril organisation | COL1A1, TGFB1, ACTA2 | 0.0014 |
| GO:0006986 | Response to unfolded protein — ER stress | DDIT3, ATF3, HSPA5 | 0.0023 |

### GO Interpretation

The GO enrichment results reveal the molecular mechanism behind my thesis findings. The three most significantly enriched downregulated GO terms cover glutathione metabolism, hydrogen peroxide catabolism, and superoxide removal — the three primary antioxidant defence systems I measured biochemically. Simultaneously, the upregulated ROS metabolic process term (CYP2E1, NOX4, PTGS2) shows active generation of reactive oxygen species. The T2DM liver is producing more ROS while losing the capacity to neutralise it — a double hit on redox homeostasis that my thesis observed at the enzyme activity level.

---

## 6. KEGG Pathway Enrichment

| KEGG ID | Pathway | Key Genes | p-adj | Direction |
|---------|---------|-----------|-------|-----------|
| hsa04932 | **Non-alcoholic fatty liver disease** | TNF, IL6, INSR, IRS1, FASN | 0.0001 | UP+DOWN |
| hsa04930 | **Type II diabetes mellitus** | INSR, IRS1, IRS2, AKT2, GCK | 0.0002 | DOWN |
| hsa00480 | **Glutathione metabolism** | GPX1, GSR, GCLC, GCLM | 0.0003 | DOWN |
| hsa04920 | Adipocytokine signaling | PPARA, SIRT1, AMPK, IRS1 | 0.0005 | DOWN |
| hsa04910 | **Insulin signaling pathway** | INSR, IRS1, IRS2, AKT2, MTOR | 0.0006 | DOWN |
| hsa04151 | PI3K-Akt signaling | INSR, AKT2, MTOR, PIK3CA | 0.0009 | DOWN |
| hsa04010 | MAPK signaling | TNF, IL1B, TGFB1, DDIT3 | 0.0012 | UP |
| hsa04668 | TNF signaling pathway | TNF, IL6, IL1B, CCL2 | 0.0019 | UP |
| hsa04350 | TGF-beta signaling | TGFB1, SMAD3, COL1A1, ACTA2 | 0.0028 | UP |
| hsa03320 | PPAR signaling pathway | PPARA, FASN, ACOX1, CPT1A | 0.0038 | DOWN |

### KEGG Interpretation

Five interconnected mechanisms emerge:

**1. Core T2DM pathway disrupted (hsa04930)** — INSR, IRS1, IRS2, AKT2 all downregulated, confirming genuine T2DM biology at the pathway level.

**2. Glutathione metabolism comprehensively suppressed (hsa00480)** — GPX1, GSR, GCLC, GCLM all downregulated within this pathway. This is the direct molecular explanation for the reduced GSH levels my thesis measured: the pathway responsible for glutathione synthesis and recycling is transcriptionally silenced in T2DM liver.

**3. Fatty liver progression (hsa04932)** — Most significantly enriched pathway overall, connecting T2DM to NAFLD progression through lipid accumulation and inflammatory activation.

**4. PPAR signalling suppressed (hsa03320)** — PPARA downregulation means reduced fatty acid oxidation. When fat cannot be oxidised it accumulates, driving steatosis.

**5. Three inflammatory pathways activated** — TNF, MAPK, and TGF-beta pathways enriched among upregulated genes, confirming chronic hepatic inflammation as a central T2DM feature.

---

## 7. The Full Wet Lab → Computational Bridge

| Thesis Measurement | Gene Expression | GO Term | KEGG Pathway |
|-------------------|-----------------|---------|--------------|
| SOD activity ↓ | SOD2 ↓ (−1.84) | GO:0019430 Superoxide removal | hsa00480 Glutathione metabolism |
| CAT activity ↓ | CAT ↓ (−1.64) | GO:0042744 H₂O₂ catabolism | hsa00480 Glutathione metabolism |
| GPx activity ↓ | GPX1 ↓ (−2.00) | GO:0006749 Glutathione process | hsa00480 Glutathione metabolism |
| GSH levels ↓ | GCLC, GCLM ↓ | GO:0006749 Glutathione process | hsa00480 Glutathione metabolism |
| MDA levels ↑ | CYP2E1, NOX4 ↑ | GO:0072593 ROS metabolic process | hsa04932 NAFLD |

Each row traces a single biochemical observation from bench measurement → gene expression → GO biological process → KEGG disease pathway. This four-level chain is the core contribution of this case study.

---

## 8. ML Classification Results

| Metric | Value |
|--------|-------|
| Cross-Validation AUC | ~0.98 |
| Top discriminating features | SOD2, CYP2E1, G6PC, GPX1, GCLC |
| Classifier | Random Forest (200 trees, 5-fold CV) |

Antioxidant gene expression alone achieves near-perfect classification of T2DM vs. normal liver samples — confirming SOD2, GPX1, and GSH pathway genes as robust transcriptomic biomarkers of diabetic liver injury.

---

## 9. Conclusion

This case study establishes three results:

**1.** GeneLens correctly identifies established T2DM biology from raw count data — gluconeogenic upregulation, antioxidant suppression, inflammatory activation, and fibrotic progression.

**2.** Thesis wet-lab findings are computationally validated. Reduced SOD, CAT, GPx, and GSH activity corresponds to transcriptional downregulation of SOD2, CAT, GPX1, GCLC, and GCLM — confirmed at the GO term and KEGG pathway level.

**3.** The full chain from bench to pathway is traceable. Each enzyme measured in the thesis maps to a gene, a GO term, and a KEGG pathway — demonstrating that wet-lab biochemistry and computational transcriptomics are complementary disciplines.

This bridge is the research direction I intend to pursue in graduate school.

---

## 10. Reproducibility

- **Live app:** [YOUR-STREAMLIT-URL.streamlit.app](https://YOUR-STREAMLIT-URL.streamlit.app)
- **Tool:** [github.com/ESTIE-CREATOR/genelens](https://github.com/ESTIE-CREATOR/genelens)
- **Dataset:** [`data/Diabetic_Liver_RNA-seq.csv`](data/Diabetic_Liver_RNA-seq.csv)
- **Parameters:** padj < 0.05, FC ≥ 1.5, 200 RF trees, 5-fold CV

---

## 11. References

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
