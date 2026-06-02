## Data availability and loading instructions

This repository contains the R Markdown file used for the empirical analysis in my bachelor’s thesis on gender differences in behavioral responses to experimentally manipulated social status. The original data are not my own data. They come from publicly available replication packages accompanying the two studies reanalysed in the thesis.

### Study I: Loss Aversion in Social Image Concerns

The first dataset comes from the replication package for:

> Riener, G., Petrishcheva, V., & Schildberg-Hörisch, H. (2022). Replication data for: “Loss Aversion in Social Image Concerns”.
> DOI: https://doi.org/10.25625/IG6ESP

This replication package accompanies:

> Petrishcheva, V., Riener, G., & Schildberg-Hörisch, H. (2023). *Loss aversion in social image concerns*. Experimental Economics, 26(3), 622–645.

To run the analysis, download the replication package and place the file `ExperimentMain.dta` in the following folder:

```text
data/study1_loss_aversion/ExperimentMain.dta
```

### Study II: Social Status and Prosocial Behavior

The second dataset comes from the replication package for:

> Zheng, J. D., Schram, A., & Song, T. (2023). Replication Data for: “Social Status and Prosocial Behavior”. Harvard Dataverse.
> DOI: https://doi.org/10.7910/DVN/CO8RPY

This replication package accompanies:

> Zheng, J. D., Schram, A., & Song, T. (2023). *Social status and prosocial behavior*. Experimental Economics, 26(5), 1085–1114.

To run the analysis, download the replication package and place the file `Pooled_data_April27.dta` in the following folder:

```text
data/study2_prosocial_behavior/Pooled_data_April27.dta
```

### Required folder structure

After downloading the two public replication datasets, the repository should have the following structure:

```text
repo/
├── EOR_Thesis_code.Rmd
├── data/
│   ├── study1_loss_aversion/
│   │   └── ExperimentMain.dta
│   └── study2_prosocial_behavior/
│       └── Pooled_data_April27.dta
└── README.md
```

The `.Rmd` file loads the data using relative paths, so the analysis should run as long as the files are placed in the folders shown above. No personal or machine-specific file paths are required.

The relevant data-loading section in the `.Rmd` file is:

```r
loss_path <- file.path(
  "data",
  "study1_loss_aversion",
  "ExperimentMain.dta"
)

prosocial_path <- file.path(
  "data",
  "study2_prosocial_behavior",
  "Pooled_data_April27.dta"
)

stopifnot(file.exists(loss_path), file.exists(prosocial_path))

loss_raw <- to_numeric(read_dta(loss_path))
prosocial_raw <- to_numeric(read_dta(prosocial_path))
```

If the code returns an error that one of the files cannot be found, check whether the `.dta` files have exactly the file names shown above and whether they are placed in the correct folders.
