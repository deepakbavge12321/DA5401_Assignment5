# DA5401 - Assignment 5: Visualizing Data Veracity Challenges in Multi-Label Classification

**Name:** Bavge Deepak Rajkumar  
**Roll Number:** NA22B031  

---

## Overview

This assignment focuses on identifying and understanding **data veracity issues** (e.g., noisy labels, outliers, and hard-to-learn samples) in a **multi-label classification** problem using **nonlinear manifold learning techniques** — **t-SNE** and **Isomap**.

The dataset used is the **Yeast gene function dataset**, where each sample (gene) can belong to multiple functional categories.

The key learning objectives are:
- To apply **t-SNE and Isomap** for 2D visualization
- To **inspect data quality** visually
- To compare **local vs. global structure preservation**
- To analyze the **curvature of the data manifold**

---

## Dataset Used

- **Source**: Mulan Repository – Yeast Dataset (`yeast.arff` + `yeast.xml`)
- **Shape**: 2417 samples × 117 columns
  - 103 feature columns
  - 14 binary label columns (multi-label setting)
- **Task**: Multi-label classification — each gene may belong to one or more functional classes

---

## Assignment Breakdown

### Part A: Preprocessing and Setup

- Loaded `yeast.arff` and parsed `yeast.xml` to extract feature and label matrices (`X`, `Y`)
- Verified shape: `X` (2417×103), `Y` (2417×14)
- Created simplified label variable `label_viz` with 3 classes:
  - Most frequent single-label: `class1`
  - Most frequent multi-label combination: `Top Multi`
  - All others grouped as `Other`
- Standardized `X` before applying distance-based methods

---

### Part B: t-SNE and Veracity Inspection

- Applied t-SNE on `X_scaled` with multiple perplexities ∈ {5, 10, 20, 30, 40, 50, 75, 100}
- Selected **perplexity = 40** as final value based on visual clarity and cluster separation
- Final t-SNE plot highlighted:
  - **Noisy/Ambiguous Labels**: isolated class1/top-multi points embedded in gray clusters
  - **Outliers**: points at plot extremities
  - **Hard-to-Learn Samples**: central region with heavy class overlap

---

### Part C: Isomap and Manifold Learning

- Applied Isomap for multiple `n_neighbors` ∈ {5, 10, 15, 20}
- Compared Isomap vs t-SNE visually and quantitatively:
  - Trustworthiness, k-NN overlap, and distance correlation metrics
- Observed:
  - **t-SNE**: better local structure preservation (trustworthiness: 0.9298)
  - **Isomap**: weaker local fidelity but insights into global curvature
- Concluded that the data lies on a **moderately curved manifold**, requiring nonlinear classifiers

---

## Results Summary

| Method      | Trustworthiness    | kNN Overlap    | Distance Correlation |
|-------------|--------------------|----------------|----------------------|
| **t-SNE**   | 0.9298             | 0.2474         | 0.4218               |
| **Isomap**  | 0.7269             | 0.0381         | 0.2714 (geodesic)    |

> t-SNE provided a better 2D embedding for inspecting noisy labels and hard samples.  
> Isomap was useful for assessing overall manifold curvature.

---

## How to Run

1. Ensure the following files are in your working directory:
   - `yeast.arff`
   - `yeast` (XML descriptor)
2. Open `maniflod.ipynb` in Jupyter Lab or VS Code
3. Run all cells sequentially from top to bottom

> All visualizations and answers are embedded directly in the notebook.

---

## Key Learnings

- Dimensionality reduction helps **diagnose data quality issues** in multi-label problems
- **t-SNE** excels in visualizing **local label noise and outliers**
- **Isomap** is useful for probing **global manifold curvature**
- Visual inspection combined with structure-aware metrics (trustworthiness, correlation) gives a clearer picture of what a classifier will struggle with

---

## Final Insight

A combination of **t-SNE for local insight** and **Isomap for global structure** is most effective for understanding veracity challenges in real-world multi-label datasets.

---
