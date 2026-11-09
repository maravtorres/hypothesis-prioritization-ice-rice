# Hypothesis Prioritization with ICE and RICE — and an A/B Test Decision

Prioritizing product hypotheses with the ICE and RICE frameworks, then running an A/B test analysis to decide whether to ship a change.

TripleTen Data Analyst program project — Mara Torres Blanco.

## What this project does

1. **Scores product hypotheses with ICE** (Impact, Confidence, Effort) and **RICE** (Reach, Impact, Confidence, Effort) and compares the two rankings.
2. **Analyzes an A/B test** (groups A and B) on conversion and average order size, first on raw data and then after removing outliers.
3. **Reaches a decision** on whether to stop the test and ship the change.

## Tools

- Python
- Pandas
- Matplotlib
- SciPy (statistical tests)

## Key findings

### ICE vs. RICE prioritization

- The top ICE hypothesis is **"Launch a promotion" (ICE 16.2)** — high impact and confidence with moderate effort. The lowest is **"Change the background color" (ICE 1.0)**.
- **RICE changes the ranking significantly** because it adds Reach:
  - "Launch a promotion" falls from **#1 to #5** — high impact and confidence, but very low Reach (1), so it affects very few users.
  - "Add subscription form" rises from **#3 to #1** — the highest Reach (10), so it reaches the most users.
  - "Add product recommendation blocks" rises from **#5 to #2** thanks to a Reach of 8, which offsets its relatively low Impact.
- Conclusion: ICE can overestimate hypotheses with big impact that reach few users. RICE is more complete because it considers how many people benefit, not just how good the idea is.

### A/B test: raw data

- Group B conversion is **15.98% higher** than group A (0.029 vs. 0.025), but the difference is **not statistically significant (p = 0.588 > 0.05)** — it could be chance.
- Average order size also shows **no significant difference (p = 0.862)**.
- Group B accumulated more revenue, with a sharp jump around August 20, probably caused by one or a few very high-value orders (outliers) that distort the results.

### A/B test: filtered data (outliers removed)

- **9 outlier orders removed**, leaving 1,007 clean orders.
- Conversion is still not significant (**p = 0.580**), and order size is not significant either (**p = 0.934**). The order-size difference seen in raw data disappears after filtering, confirming it was caused by those few high-value orders.

### Decision

**Stop the test — do not ship the change tested in group B.** Neither conversion nor order size shows a statistically significant difference, with raw or filtered data, and continuing would consume resources with no guarantee of a different result.

## Data

- `hypotheses_us.csv` — product hypotheses with ICE/RICE scores.
- `orders_us.csv` — orders for the A/B test analysis.
- `visits_us.csv` — visits for the A/B test analysis.

**The datasets are not included in this repository** — they were provided on the TripleTen learning platform. The notebook will not run without them; the code and outputs are preserved as delivered.

## Files

- `hypothesis_prioritization_ice_rice.ipynb` — the analysis notebook (34 cells).
- `README.md` — this file.

## How to run

Open `hypothesis_prioritization_ice_rice.ipynb` in Jupyter Notebook or JupyterLab and run the cells top to bottom. It expects `hypotheses_us.csv`, `orders_us.csv` and `visits_us.csv` in the same folder (not included — see Data above).
