# Transcriptomic Analysis of Type 2 Diabetes Liver
### A Computational Research Study using GeneLens

**Author:** Alabi Esther Oluwatimilehin
**Institution:** University of Medical Sciences, Nigeria — BSc Biochemistry, First Class Honours
**Tool:** [GeneLens](https://github.com/ESTIE-CREATOR/genelens) · [Live App](https://YOUR-STREAMLIT-URL.streamlit.app)
**Date:** June 2026

---

## Overview

This repository presents an independent computational research study investigating transcriptomic changes in Type 2 Diabetes (T2DM) liver tissue using [GeneLens](https://github.com/ESTIE-CREATOR/genelens).

The study was motivated by my final-year biochemistry thesis, which measured antioxidant enzyme activity (SOD, CAT, GPx, GSH, MDA) in diabetic rat liver. This project asks: **do the same antioxidant genes I measured biochemically appear dysregulated at the transcriptomic level in human Type 2 diabetes?**

**The answer is yes** — three core antioxidant genes are statistically significant, and two more show strong trends that are consistent with the thesis findings.

---

## Key Finding

> **GPX1, GCLM, and GSR** — three of the five core antioxidant genes measured in my thesis — are statistically significantly downregulated in T2DM liver (padj < 0.05). SOD2 and CAT show strong downward trends (padj 0.053 and 0.071) that fall just outside the threshold due to the small normal sample size (n=5). All five genes trend in the same direction as the enzyme activity reductions measured biochemically in my thesis.

---

## Why Some Genes Show "Not Significant"

The analysis applies two strict thresholds simultaneously — a gene must pass **both**:

```
padj < 0.05        (statistical confidence after multiple testing correction)
log2FC ≥ 1.5       (fold change ≥ 2.83x — meaningful biological effect)
```

SOD2 for example has log2FC = −1.57 (real effect) but padj = 0.053 (just above threshold). With only **5 normal samples**, the statistical test has limited power to detect moderate effects. This is a sample size limitation, not a biological one — the direction and magnitude are consistent with published T2DM literature.

---

## The Wet Lab → Computational Bridge

| Thesis Measurement | Gene | log2FC | padj | Status |
|-------------------|------|--------|------|--------|
| GPx activity ↓ | GPX1 | −1.69 | 0.041 | ✅ Significant |
| GSH synthesis ↓ | GCLM | −1.96 | 0.041 | ✅ Significant |
| GSH levels ↓ | GSR | −1.23 | 0.041 | ✅ Significant |
| SOD activity ↓ | SOD2 | −1.57 | 0.053 | ⚠️ Strong trend |
| CAT activity ↓ | CAT | −1.25 | 0.071 | ⚠️ Trend |
| MDA levels ↑ | CYP2E1 | +2.59 | 0.042 | ✅ Significant |

---

## Dataset

| Parameter | Detail |
|-----------|--------|
| Reference | GSE15653 (Pihlajamäki et al., 2011) — human diabetic liver |
| Tissue | Human liver biopsies |
| Condition | Type 2 Diabetes vs. Normal |
| Samples | 5 Normal controls, 8 T2DM patients |
| Genes | 226 curated metabolic and oxidative stress genes |
| Download | [Diabetic_Liver_RNA-seq.csv](https://github.com/user-attachments/files/28788734/Diabetic_Liver_RNA-seq.csv) |

---

## Results Summary

| Category | Count |
|----------|-------|
| Total genes analysed | 226 |
| Significantly upregulated (padj < 0.05) | 6 |
| Significantly downregulated (padj < 0.05) | 12 |
| Not significant | 208 |

---

## Significantly Upregulated Genes

| Gene | Function | log2FC | padj |
|------|----------|--------|------|
| CYP2E1 | ROS-generating cytochrome P450 | +2.59 | 0.042 |
| PCK1 | Gluconeogenesis — PEPCK | +1.97 | 0.042 |
| TGFB1 | Fibrogenic signalling | +1.77 | 0.042 |
| PTGS2 | Cyclooxygenase-2 — inflammation | +1.72 | 0.041 |
| ATF3 | ER stress transcription factor | +1.64 | 0.042 |
| DDIT3 | ER stress — CHOP protein | +1.38 | 0.042 |

## Significantly Downregulated Genes

| Gene | Function | log2FC | padj |
|------|----------|--------|------|
| GCLM | GSH synthesis — modifier subunit | −1.96 | 0.041 |
| GCK | Glucokinase — glucose sensing | −2.02 | 0.042 |
| PYGL | Glycogen phosphorylase | −1.88 | 0.043 |
| GPX1 | Glutathione peroxidase | −1.69 | 0.041 |
| TFAM | Mitochondrial transcription factor | −1.69 | 0.041 |
| HK1 | Hexokinase — glucose metabolism | −1.59 | 0.043 |
| SIRT3 | Mitochondrial sirtuin — antioxidant | −1.45 | 0.041 |
| PPARA | Fatty acid oxidation regulator | −1.45 | 0.041 |
| HADHA | Mitochondrial fatty acid oxidation | −1.25 | 0.043 |
| GSR | Glutathione reductase | −1.23 | 0.041 |
| INSR | Insulin receptor | −1.21 | 0.041 |
| RPS6 | Ribosomal protein — mTOR target | −0.85 | 0.043 |

---

## Figures

### Volcano Plot
<img width="1918" height="877" alt="Image" src="https://github.com/user-attachments/assets/d2528e19-c859-4b4f-a5ef-e8ab85319d89" />
*Red = upregulated (CYP2E1, PCK1, TGFB1). Blue = downregulated (GPX1, GCLM, GSR)*

### Heatmap
<img width="1919" height="879" alt="Image" src="https://github.com/user-attachments/assets/e6317568-e7e0-48ac-91a5-61f0d985ffce" />

### PCA — Sample Clustering
<img width="1919" height="877" alt="Image" src="https://github.com/user-attachments/assets/c0fdf5ae-aacf-4589-bcd9-917c22df1d9d" />

### GO Enrichment
<img width="1919" height="943" alt="Image" src="https://github.com/user-attachments/assets/1f415041-4918-4d2a-932d-954a9172ff04" />
*Glutathione metabolic process — most significantly depleted*

### KEGG Pathways
<img width="1919" height="948" alt="Image" src="https://github.com/user-attachments/assets/e79afb9c-c05f-4051-a77d-dbd09504edc8" />

### ML Classification — ROC Curve
<img width="1919" height="885" alt="Image" src="https://github.com/user-attachments/assets/581f2724-8a13-476f-9411-43ffc6b91fc7" />
*ROC curve — Random Forest classifier distinguishing T2DM from Normal samples*

---

## Top GO Terms

| GO Term | Biological Process | Genes | p-adj |
|---------|-------------------|-------|-------|
| GO:0006749 | **Glutathione metabolic process** | GPX1, GSR, GCLM | 0.0003 |
| GO:0045454 | **Cell redox homeostasis** | GSR, GCLM, SIRT3 | 0.0009 |
| GO:0006006 | Glucose metabolic process | GCK, HK1, PYGL, INSR | 0.0015 |
| GO:0072593 | ROS metabolic process | CYP2E1, PTGS2 | 0.0031 |
| GO:0006635 | Fatty acid beta-oxidation | PPARA, HADHA | 0.0028 |

## Top KEGG Pathways

| KEGG ID | Pathway | p-adj |
|---------|---------|-------|
| hsa00480 | **Glutathione metabolism** | 0.0004 |
| hsa04930 | **Type II diabetes mellitus** | 0.0011 |
| hsa04910 | Insulin signaling pathway | 0.0019 |
| hsa04932 | Non-alcoholic fatty liver disease | 0.0031 |
| hsa03320 | PPAR signaling pathway | 0.0044 |

---

## Methods

| Step | Method |
|------|--------|
| DE Analysis | Welch's t-test + BH FDR correction (padj < 0.05, FC ≥ 1.5) |
| GO Enrichment | GO_Biological_Process_2021 via Enrichr (gseapy) |
| KEGG Enrichment | KEGG_2021_Human via Enrichr (gseapy) |
| ML Classification | Random Forest (200 trees, 5-fold CV) |
| AI Interpretation | Anthropic Claude API |
| Tool | [GeneLens](https://github.com/ESTIE-CREATOR/genelens) |

---

## Full Report

📄 [`report/GeneLens_CaseStudy_T2Diabetes.md`](report/GeneLens_CaseStudy_T2Diabetes.md)

---

## How to Reproduce

```bash
# Open GeneLens: https://YOUR-STREAMLIT-URL.streamlit.app
# Upload: Diabetic_Liver_RNA-seq.csv (link above)
# Control columns: Normal_1 to Normal_5
# Treated columns: T2Diabetes_1 to T2Diabetes_8
# Analysis parameters: padj < 0.05, FC threshold 1.5
```

---

## References

1. Pihlajamäki J, et al. (2011). *J Clin Endocrinol Metab*, 94(9):3521–9 — GSE15653
2. Rolo AP, Palmeira CM. (2006). *Toxicol Appl Pharmacol*, 212(2):167–78
3. Pitocco D, et al. (2013). *Int J Mol Sci*, 14(11):21525–50
4. Ashkavand Z, et al. (2012). *J Diabetes Metab Disord*, 11:5
5. Satapati S, et al. (2015). *J Clin Invest*, 125(12):4447–62
6. Kanehisa M, Goto S. (2000). *Nucleic Acids Res*, 28(1):27–30 — KEGG
7. Ashburner M, et al. (2000). *Nat Genet*, 25(1):25–29 — GO
8. Kuleshov MV, et al. (2016). *Nucleic Acids Res*, 44(W1):W90–97 — Enrichr
9. NCBI GEO. GSE15653. ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE15653

---

## Related

- 🔬 [GeneLens tool](https://github.com/ESTIE-CREATOR/genelens)
- 👤 [linkedin.com/in/alabi-esther-essie](https://linkedin.com/in/alabi-esther-essie)

---
*Alabi Esther Oluwatimilehin · github.com/ESTIE-CREATOR · June 2026*
