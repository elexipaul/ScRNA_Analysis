# **scRNA-seq Analysis of GSE183276**

## **Overview**

This analysis was performed on the single-cell RNA-seq dataset **GSE183276**, which includes kidney samples from four clinical conditions: **AKI, DKD, HCKD, and Healthy**. The aim of the analysis was to assess data quality, compare the uncorrected and Harmony-corrected embeddings, evaluate sample and condition mixing, and review whether the current workflow is suitable for downstream biological interpretation.

Overall, the analysis shows that the dataset can be integrated successfully using Harmony, and the corrected UMAP gives a much cleaner representation of shared cell populations across disease groups. However, the dataset also shows a major quality-control concern: only a small fraction of the original cells remain after filtering. Because of this, the current results should be treated as an **early-stage quality and integration analysis**, not yet as a final biological disease comparison.


## **Dataset Summary**

The dataset contains **49 samples** across four conditions. Before quality control, there were **109,741 cells**. After filtering, only **5,405 cells** remained, corresponding to an overall retention of about **4.9%**.

It suggests that either the original dataset contained many low-quality droplets/cells, or the filtering thresholds may have been too strict.

The post-QC cell distribution was also uneven across conditions:

|               |             |                    |                       |
| :-----------: | :---------: | :----------------: | :-------------------: |
| **Condition** | **Samples** | **Cells after QC** | **Approx. retention** |
|      AKI      |      12     |        2,266       |          6.3%         |
|      DKD      |      14     |        2,066       |          4.8%         |
|      HCKD     |      3      |         619        |          6.7%         |
|    Healthy    |      20     |         454        |          2.1%         |

\


The QC plots show variation in **nCount\_RNA**, **nFeature\_RNA**, mitochondrial percentage, and ribosomal percentage across samples.

The density scatter plot of `log1p(nCount_RNA)` versus `log1p(nFeature_RNA)` shows the expected positive relationship: cells with more RNA counts generally have more detected genes. This suggests that the basic structure of the single-cell data is biologically reasonable. Some outlier cells are still visible, and these should be checked for possible doublets, stressed cells, or low-quality profiles. 


## **Dimensionality Reduction and PCA**

The PCA elbow plot shows a steep drop in variation across the early principal components, followed by a gradual plateau. This suggests that the first **25–35 PCs** likely capture most of the meaningful biological and technical structure in the dataset.


## **Uncorrected UMAP Interpretation**

The uncorrected UMAP shows clear separation between groups of cells

In the uncorrected plots, cells from different conditions and samples do not mix as well. This means that if clustering were performed directly on the uncorrected representation, some clusters might reflect technical variation rather than true cell identity or disease biology. 


## **Harmony Integration Interpretation**

The Harmony-corrected UMAP shows a clear improvement over the uncorrected embedding. After correction, cells from AKI, DKD, HCKD, and Healthy are more evenly mixed within shared UMAP regions.

The CellTypist cell-type proportion plot, the four conditions show different cellular compositions after QC and Harmony integration. These patterns should be interpreted cautiously because the final dataset is imbalanced, especially with **Healthy having only 454 cells** after QC.


# **AKI condition**

The AKI group is mainly composed of tubular epithelial populations.

The most abundant cell types in AKI are approximately:

|               |                        |
| :-----------: | :--------------------: |
| **Cell type** | **Approx. proportion** |
|      aTAL     |          15.3%         |
|       PC      |          14.0%         |
|      aPT      |          11.9%         |
|     C-TAL     |          11.5%         |
|       PT      |          9.9%          |
|    B cells    |          9.6%          |
|     EC-PTC    |          8.3%          |

AKI shows a strong representation of **tubular epithelial cells**, especially **TAL-related cells**, **proximal tubule cells**, and **principal cells**. This fits well with kidney injury biology because AKI commonly affects tubular compartments, particularly proximal tubules and thick ascending limb regions.

The presence of a relatively high **aPT population** suggests an injured or adaptive proximal tubular state. Adaptive proximal tubule cells are often associated with stress response, regeneration, or incomplete repair after injury.

The relatively high proportion of **B cells** in AKI may indicate immune involvement or inflammation. However, this should be confirmed using immune marker genes and sample-level statistics before making a strong conclusion.


# **DKD condition**

The DKD group also contains many tubular epithelial populations, but its distribution is slightly different from AKI

The most abundant cell types in DKD are approximately: 

|               |                        |
| :-----------: | :--------------------: |
| **Cell type** | **Approx. proportion** |
|      aTAL     |          19.0%         |
|       PC      |          14.8%         |
|     EC-PTC    |          10.4%         |
|      aPT      |          10.0%         |
|     C-TAL     |          7.7%          |
|       PT      |          7.7%          |
|      DCT      |          4.5%          |
|     EC-DVR    |          4.3%          |


# **HCKD condition**

The HCKD group has a more unusual composition compared with AKI and DKD.

The most abundant cell types in HCKD are approximately:

|                            |                        |
| :------------------------: | :--------------------: |
|        **Cell type**       | **Approx. proportion** |
|          CDC-IC-A          |          14.4%         |
|             PC             |          13.7%         |
| BATL / TAL-like population |          12.6%         |
|            aTAL            |          10.3%         |
|            MTAL            |          9.0%          |
|           EC-DVR           |          7.8%          |
|             DCT            |          6.1%          |
|           EC-PTC           |          6.1%          |

HCKD appears enriched for **distal nephron and collecting duct-associated populations**, including **principal cells**, **intercalated cells**, **DCT**, and TAL-related populations.

The high proportion of **CDC-IC-A** is notable. Intercalated cells are involved in acid-base regulation and collecting duct function. Their enrichment may suggest altered collecting duct representation or disease-associated remodeling in the HCKD samples.

HCKD also shows a relatively high proportion of **MTAL/TAL-related cells** and **EC-DVR**, suggesting representation of medullary tubular and vascular structures.


# **Healthy condition**

The Healthy group shows a different pattern from the disease groups,

|               |                        |
| :-----------: | :--------------------: |
| **Cell type** | **Approx. proportion** |
|     EC-PTC    |          20.9%         |
|     EC-GC     |          16.5%         |
|       PT      |          9.3%          |
|   Podocytes   |          9.0%          |
|     VSMC/P    |          7.3%          |
|     C-TAL     |          7.9%          |
|      CNT      |          6.2%          |
|      DCT      |          5.1%          |

Healthy samples are enriched for **endothelial populations**, especially **EC-PTC** and **EC-GC**, as well as **podocytes** and vascular-associated cells such as **VSMC/P**.

This suggests that the Healthy group contains more glomerular and vascular-associated cell types compared with the disease groups. The relatively higher podocyte proportion is biologically meaningful because podocytes are expected in normal kidney tissue and may be lost or under-represented in damaged kidney samples.

|               |                                      |                                                            |
| :-----------: | :----------------------------------: | :--------------------------------------------------------: |
| **Condition** |       **Main cellular pattern**      |                     **Interpretation**                     |
|      AKI      |   aTAL, PC, aPT, C-TAL, PT, B cells  | Tubular injury/adaptation with possible immune involvement |
|      DKD      |       aTAL, PC, EC-PTC, aPT, PT      |          Chronic tubular and vascular involvement          |
|      HCKD     | CDC-IC-A, PC, TAL-like, MTAL, EC-DVR |   Distal nephron / collecting duct / medullary enrichment  |
|    Healthy    | EC-PTC, EC-GC, podocytes, VSMC/P, PT |  More glomerular, endothelial, and vascular representation |
