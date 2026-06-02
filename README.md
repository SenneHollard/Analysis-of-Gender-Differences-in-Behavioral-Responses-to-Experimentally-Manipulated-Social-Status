# Gender Differences in Behavioral Responses to Experimentally Manipulated Social Status

This repository contains the complete replication materials for my bachelor's thesis analyzing gender differences in behavioral responses to experimentally manipulated social status. The analysis reexamines two published experimental studies through a gender-heterogeneity lens using transparent, reproducible R code.

## Quick Start

1. **Clone this repository** and set your working directory to the repo root.
2. **Download the two required datasets** (see instructions below).
3. **Place the datasets** in the `data/` subfolder following the structure shown below.
4. **Open `Thesis_code.Rmd`** in RStudio and click *Knit* to reproduce the full analysis.

## Contents

- **`Thesis_code.Rmd`**: Complete empirical analysis with figures, tables, and diagnostic tests. Outputs PDF and HTML documents with table of contents.
- **`data/`**: Folder for the two publicly available replication datasets (not included in this repo).
- **`output/`**: Generated automatically when you run the analysis; contains CSV tables and PNG figures for inclusion in the thesis.

---

## Data Requirements & Setup

### Study I: Loss Aversion in Social Image Concerns

**Source:**  
Riener, G., Petrishcheva, V., & Schildberg-Hörisch, H. (2022). *Replication data for: "Loss Aversion in Social Image Concerns"*. DOI: [10.25625/IG6ESP](https://doi.org/10.25625/IG6ESP)

**Paper:**  
Petrishcheva, V., Riener, G., & Schildberg-Hörisch, H. (2023). *Loss aversion in social image concerns*. *Experimental Economics*, 26(3), 622–645.

**Setup:**
1. Download the replication package from the DOI link above.
2. Extract `ExperimentMain.dta` and place it at:
   ```
   data/study1_loss_aversion/ExperimentMain.dta
   ```

### Study II: Social Status and Prosocial Behavior

**Source:**  
Zheng, J. D., Schram, A., & Song, T. (2023). *Replication Data for: "Social Status and Prosocial Behavior"*. Harvard Dataverse. DOI: [10.7910/DVN/CO8RPY](https://doi.org/10.7910/DVN/CO8RPY)

**Paper:**  
Zheng, J. D., Schram, A., & Song, T. (2023). *Social status and prosocial behavior*. *Experimental Economics*, 26(5), 1085–1114.

**Setup:**
1. Download the replication package from the DOI link above.
2. Extract `Pooled_data_April27.dta` and place it at:
   ```
   data/study2_prosocial_behavior/Pooled_data_April27.dta
   ```

### Complete Repository Structure

After downloading both datasets, your repository should look like this:

```
repo/
├── Thesis_code.Rmd
├── README.md
├── data/
│   ├── study1_loss_aversion/
│   │   └── ExperimentMain.dta
│   └── study2_prosocial_behavior/
│       └── Pooled_data_April27.dta
└── output/                        (generated when you run the analysis)
    ├── study1_rd_table.csv
    ├── study2_regression_table.csv
    ├── study1_power.csv
    ├── study2_power.csv
    ├── study2_wald_chosen_effort.csv
    ├── wald_paragraphs.tex
    ├── fig_study1_rd_male.png
    ├── fig_study1_rd_female.png
    ├── fig_study1_rd_full.png
    └── fig_study2_chosen_effort.png
```

---

## Analysis Overview

### Study I: Regression-Discontinuity Design

Examines loss aversion in social image concerns around a rank-based reference point using a local Tobit model with session-level cluster bootstrap standard errors (499 replications). The analysis is split by gender and includes a pooled gender-interaction model testing whether the loss/gain discontinuity differs between men and women.

**Key specification (Eq. 3):**
$$\text{DieDiff}^* = \alpha + \tau \cdot \text{Loss} + \beta_1 \text{RankDif} + \beta_2 (\text{Loss} \times \text{RankDif}) + X'\gamma + u$$

**Output:** Three RD plots (male, female, full sample), regression table with/without controls, gender-difference test, and power diagnostics.

### Study II: Status-Treatment Model with Gender Interactions

Extends the original status-treatment model to include gender interactions in the effect of randomly assigned and earned status on effort provision. Uses session-clustered (CR1) linear regression and conducts a formal Wald test of whether gender differences in the high-status effect vary by assignment type.

**Key specification (Eq. 7):**
$$Y = \alpha + \sum_{k} \beta_k \text{Status}_k + \delta \cdot \text{Female} + \sum_{k} \theta_k (\text{Status}_k \times \text{Female}) + Z'\gamma + \varepsilon$$

**Output:** Chosen-effort figure (gender × condition interaction plot), three-outcome regression table, Wald test of the main hypothesis, power diagnostics, and ready-to-paste LaTeX paragraphs.

---

## Reproducibility Features

- **No external dependencies beyond base R + standard packages**: Uses only `haven`, `ggplot2`, `survival`, and `knitr`.
- **Self-contained helpers**: All custom functions (Tobit regression, cluster bootstrap, CR1 covariance, Wald test) are defined from scratch in the Rmd file for full transparency.
- **Reproducible randomness**: Fixed seed (`5315751`, my student number) ensures identical bootstrap results across runs.
- **Relative file paths**: No machine-specific paths required; data loading uses relative paths from the repo root.
- **Automatic output creation**: Tables (CSV) and figures (PNG) are written to `output/` for thesis integration.

---

## Requirements

- **R ≥ 3.5** (tested on R 4.x)
- **RStudio** (recommended for Knitting)
- **R packages** (automatically loaded):
  - `haven` – read Stata `.dta` files
  - `ggplot2` – publication-quality figures
  - `survival` – Tobit regression via `survreg()`
  - `knitr` – Markdown and table formatting

Install missing packages with:
```r
install.packages(c("haven", "ggplot2", "survival", "knitr"))
```

---

## Running the Analysis

1. **Open** `Thesis_code.Rmd` in RStudio.
2. **Verify** the data files are in place (see directory structure above).
3. **Click** the *Knit* button (or press Ctrl+Shift+K / Cmd+Shift+K).
4. **Wait** for the analysis to complete (~1–2 minutes, depending on your machine and bootstrap iterations).
5. **Review** the generated PDF/HTML document and check the `output/` folder for tables and figures.

### Troubleshooting

- **"file not found" error:** Check that `.dta` filenames exactly match those shown above and are in the correct folders.
- **Package installation errors:** Run `install.packages("package_name")` for any missing packages.
- **Out-of-memory during bootstrap:** The cluster bootstrap uses 499 replications; reduce `B_BOOT` in the setup chunk if needed.

---

## Main Results Summary

### Study I
- **Male RD estimate (τ):** Reported in Table 5 (Panel B, with controls).
- **Female RD estimate (τ):** Reported in Table 5 (Panel B, with controls).
- **Gender difference (θ):** Formal Wald-style test of `Loss × Male` in the pooled model; results in Table 6 power diagnostics.

### Study II
- **Status treatment effects:** Table 7 shows separate effects for men and gender-interaction coefficients for women across three outcomes (chosen effort, mean response, proposal received).
- **Hypothesis test (H2b):** Wald test of whether the high-status gender interaction differs between randomly assigned and earned status (reported with χ²(1) statistic and p-value).
- **Power:** Table 8 shows post-estimation power diagnostics for all gender coefficients.

---

## Citation

If you use this replication package, please cite:

```bibtex
@thesis{hollard2026,
  author = {Senne Hollard},
  title = {Analysis of Gender Differences in Behavioral Responses to Experimentally Manipulated Social Status},
  school = {[Your University]},
  year = {2026},
  note = {Replication materials available at \url{https://github.com/SenneHollard/Analysis-of-Gender-Differences-in-Behavioral-Responses-to-Experimentally-Manipulated-Social-Status}}
}
```

---

## License

This replication package is provided as-is for academic and educational purposes. The code itself is free to use and modify. The reanalyzed datasets are publicly available through the original replication packages (see citations above).

---

## Contact

For questions about the analysis or replication materials, please open an issue on this repository or contact the author.

---

## Related Publications

The analysis reexamines data from:

1. Petrishcheva, V., Riener, G., & Schildberg-Hörisch, H. (2023). Loss aversion in social image concerns. *Experimental Economics*, 26(3), 622–645.
2. Zheng, J. D., Schram, A., & Song, T. (2023). Social status and prosocial behavior. *Experimental Economics*, 26(5), 1085–1114.
