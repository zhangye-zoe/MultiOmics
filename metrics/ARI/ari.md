# Adjusted Rand Index (ARI)

The **Adjusted Rand Index (ARI)** is a widely used external clustering evaluation metric that measures the agreement between two clustering assignments. In multi-omics research, ARI is especially useful for assessing **how consistent the clustering structure is across different modalities**, such as RNA and ATAC.

ARI adjusts the classical Rand Index by accounting for chance alignment, making the score more robust and interpretable.

---

## 📘 What ARI Measures

ARI quantifies the similarity between two clustering results by comparing all pairs of samples:

- **ARI = 1.0** → Perfect clustering agreement  
- **ARI = 0.0** → Agreement equals random chance  
- **ARI < 0** → Worse than random (rare in practice)

In multi-omics analysis (e.g., RNA vs ATAC):

- A **high ARI** indicates that both modalities capture similar biological structure  
- A **low ARI** suggests modality-specific variation or poor integration  
- ARI can be used to **benchmark multi-omics integration models** (e.g., MultiVI, MOFA+, MultiGATE)

---

## 📦 Installation

```bash
pip install scikit-learn numpy pandas
```

---

## 🧪 Minimal Example: Compute ARI in Python

```python
from sklearn.metrics import adjusted_rand_score

rna_clusters  = [0, 1, 1, 2, 2, 0, 1, 2]
atac_clusters = [1, 1, 1, 2, 2, 0, 0, 2]

ari = adjusted_rand_score(rna_clusters, atac_clusters)
print("Adjusted Rand Index (ARI) =", ari)
```

---

## 🧬 ARI for RNA–ATAC Clustering Consistency

If you have clustering results from two different modalities:

```python
import pandas as pd
from sklearn.metrics import adjusted_rand_score

# Load clustering labels for RNA and ATAC
rna_df  = pd.read_csv("rna_clusters.csv")     # columns: cell_id, cluster
atac_df = pd.read_csv("atac_clusters.csv")    # columns: cell_id, cluster

# Align cells by ID
df = pd.merge(rna_df, atac_df, on="cell_id", suffixes=("_rna", "_atac"))

# Compute ARI
ari = adjusted_rand_score(df["cluster_rna"], df["cluster_atac"])
print("RNA–ATAC ARI =", ari)
```

This evaluates how similarly RNA and ATAC cluster the same cells.

---

## 🧬 ARI using Scanpy AnnData Objects

If the clustering labels are stored in `.obs` (e.g., Leiden/Louvain):

```python
import scanpy as sc
from sklearn.metrics import adjusted_rand_score

rna  = sc.read_h5ad("rna_processed.h5ad")
atac = sc.read_h5ad("atac_processed.h5ad")

ari = adjusted_rand_score(rna.obs["leiden"], atac.obs["leiden"])
print("ARI =", ari)
```

---

## 📊 Practical Applications

ARI is commonly used in multi-omics workflows for:

- Evaluating **RNA vs ATAC** clustering consistency  
- Assessing multi-omics integration quality (before/after integration)  
- Benchmarking different integration algorithms (e.g., MultiVI, MOFA+, MultiGATE)  
- Checking whether different assays capture similar biological structure  
- Comparing clustering stability across batches or preprocessing methods  

ARI pairs naturally with:

- **ICC (Intraclass Correlation Coefficient)**  
- **NMI (Normalized Mutual Information)**  
- **Silhouette score / Davies–Bouldin score**

---

## 🔗 Reference

**Scikit-learn documentation**  
https://scikit-learn.org/stable/modules/generated/sklearn.metrics.adjusted_rand_score.html

---

## 🤝 Contributing

Contributions, suggestions, and discussions are welcome.  
Feel free to open an issue or submit a pull request.

---

