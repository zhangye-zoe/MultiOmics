# Intraclass Correlation Coefficient (ICC)

This module provides a simple and reproducible implementation of the **Intraclass Correlation Coefficient (ICC)** using Python.  
ICC is widely used to quantify **reliability**, **agreement**, and **measurement consistency** across raters, modalities, instruments, or repeated measurements.

---

## 📌 What is ICC?

The **Intraclass Correlation Coefficient (ICC)** measures how strongly units in the same group resemble each other.  
It answers questions such as:

- *How consistent are multiple raters evaluating the same samples?*  
- *Do different modalities (e.g., RNA vs ATAC) give consistent outputs for the same biological entity?*  
- *Is repeated measurement stable across time or instruments?*

Mathematically, ICC decomposes variance into:

- **Between-target variance** (signal)
- **Within-target variance** (noise)

and evaluates the proportion of total variance attributable to true differences among targets.

Higher ICC ⇒ higher consistency.  
Values typically interpreted as:

| ICC Range | Interpretation |
|-----------|----------------|
| < 0.5     | Poor reliability |
| 0.5–0.75  | Moderate reliability |
| 0.75–0.9  | Good reliability |
| > 0.9     | Excellent reliability |

---

## 📘 ICC Models

Pingouin supports several models based on the classical Shrout & Fleiss (1979) framework:

- **ICC1** → One-way random effects  
- **ICC2** → Two-way random effects, absolute agreement  
- **ICC3** → Two-way mixed effects, consistency  

The most commonly used for multi-rater reliability is **ICC(2,1)**.

This README uses `pingouin.intraclass_corr()` for computation.

---

## 📦 Dependencies

Install `pingouin`:

```bash
pip install pingouin
```

Make sure SciPy is updated (≥1.9):

```bash
pip install --upgrade scipy
```

---

## 🧪 Example: Computing ICC in Python

Below is a reproducible example adapted from Statology (https://www.statology.org/intraclass-correlation-coefficient-python/).

This data represents **6 exams**, each rated by **4 judges (A–D)**.

```python
import pandas as pd
import pingouin as pg

# Create DataFrame
df = pd.DataFrame({
    'exam':   [1,2,3,4,5,6, 1,2,3,4,5,6, 1,2,3,4,5,6, 1,2,3,4,5,6],
    'judge':  ['A']*6 + ['B']*6 + ['C']*6 + ['D']*6,
    'rating': [1,1,3,6,6,7, 2,3,8,4,5,5, 0,4,1,5,5,6, 1,2,3,3,6,4]
})

print(df.head())

# Compute ICC
icc = pg.intraclass_corr(data=df, targets='exam', raters='judge', ratings='rating')

# Display ICC table
icc.set_index('Type')
```

---

## 📊 Example Output

The output is a table containing:

- ICC1, ICC2, ICC3
- Confidence intervals
- F-statistics
- p-values
- Degrees of freedom

Example:

```
             ICC      F   df1  df2   pval    CI95%
Type                                             
ICC1   0.285739  2.594     5    18  0.053  [..., ...]
ICC2   0.284231  2.577     5    15  0.063  [..., ...]
ICC3   0.336781  2.594     5    15  0.053  [..., ...]
```

---

## 🧭 When to Use ICC?

Use ICC when you want to measure **agreement or reliability** across:

- Raters / annotators  
- Biological modalities (RNA vs ATAC vs protein)  
- Experimental replicates  
- Sensors or instruments  
- Timepoints  
- Cross-batch validation  

ICC is extremely common in:

- Bioinformatics  
- Computational pathology  
- Multi-omics integration  
- Psychology & clinical scoring  
- Reliability engineering

---

## 🔗 Reference

Original tutorial reference:  
**Statology — Intraclass Correlation in Python**  
https://www.statology.org/intraclass-correlation-coefficient-python/

Mathematical background:  
Shrout & Fleiss (1979). *Intraclass correlations: Uses in assessing rater reliability.*

---

## 💬 Contact & Contributions

Contributions, suggestions, and discussions are welcome.  
Feel free to open an issue or pull request.

---

