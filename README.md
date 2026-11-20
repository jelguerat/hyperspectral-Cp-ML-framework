# Hyperspectral Cp machine-learning framework

This repository provides a reproducible R workflow for predicting the source-defined Cp trait from hyperspectral reflectance data. It includes the project scripts, fitted model objects, metadata, cross-validation predictions, model-comparison summaries, and external-validation results.

## Existing results are ready to inspect

**You do not need to rerun the analysis to use the results included in this repository.** The supplied `.rds` model objects, metadata, cross-validation predictions, summary tables, and Dataset 26 external-validation results are already included.

The portability update changed file paths in the R scripts to project-relative paths. It did not refit the models, regenerate the reported results, or intentionally change the modelling procedures.

## Repository contents

- `Code/` — six R scripts for preprocessing, nested cross-validation, model fitting, and external validation.
- `Models/` — existing fitted PLSR, RF, MBL, and SVR model objects and associated metadata.
- `Results/` — existing cross-validation predictions, model-comparison summaries, dataset-screening information, and Dataset 26 external-validation results.
- `hyperspectral-Cp-ML-framework.Rproj` — RStudio project file.
- `README_PORTABLE_PATHS.md` — instructions for reproducing the workflow from the source data.

## Source dataset

The hyperspectral data used in this study are available from the public **[GreenHyperSpectra dataset on Hugging Face](https://huggingface.co/datasets/Avatarr05/GreenHyperSpectra)**.

The dataset repository provides a labeled configuration (`labeled/all.csv`) containing sample identifiers, dataset identifiers, spectral reflectance bands, and trait measurements. The study workflow uses selected source datasets from this collection, including Dataset 13 for model development and Dataset 26 for external validation.

The GreenHyperSpectra dataset is distributed under **CC BY-NC 4.0**. Please consult the dataset card for the applicable terms, attribution requirements, and recommended citation before downloading, using, or redistributing the data. The data are not duplicated in this GitHub repository.

**Data citation:**  
Cherif, E., Feilhauer, H., Berger, K., et al. (2023). From spectra to plant functional traits: Transferable multi-trait models from heterogeneous and sparse data. *Remote Sensing of Environment*, 292, 113580.

Cherif, E., Ouaknine, A., Brown, L. A., et al. (2025). GreenHyperSpectra: A multi-source hyperspectral dataset for global vegetation trait prediction. arXiv:2507.06806.

## Open the project and inspect the supplied results

1. Download or clone this repository.
2. Open `hyperspectral-Cp-ML-framework.Rproj` in RStudio.
3. Inspect the existing model objects and results in `Models/` and `Results/`.

No source-data download or model rerun is needed to inspect the outputs already supplied.

## Reproducing the workflow

To rerun the workflow, first obtain the relevant source data from the [GreenHyperSpectra dataset](https://huggingface.co/datasets/Avatarr05/GreenHyperSpectra). The scripts were originally configured to read a local input file named `Spectral_library_06-Oct-2026.csv`.

For a reproduction run:

1. Download the relevant labeled source data and prepare the input CSV in the same structure expected by the scripts.
2. Create a local `data/raw/` directory in the project root and place the prepared file there as `Spectral_library_06-Oct-2026.csv`.
3. Open the RStudio project and install `here` if needed:

   ```r
   install.packages("here")
   ```

4. Run the scripts in the order described in `README_PORTABLE_PATHS.md`.

The `data/` directory is intentionally not included in this repository because the source data are available from the external dataset repository and the local input file is only needed when rerunning the workflow. The existing fitted models and results are already provided.

**Important:** The public source dataset and the locally prepared input file should not automatically be assumed to be byte-for-byte identical. Check the dataset version, selected source datasets, columns, and preprocessing/input format before attempting a full reproduction.

## Notes on the portable scripts

- Machine-specific `F:/...` and `D:/...` paths were replaced with project-relative paths using `here::here()`.
- The modelling procedures, model settings, cross-validation design, preprocessing choices, target definitions, and validation thresholds were not intentionally changed.
- The preprocessing script still changes the working directory to its dated output folder so its relative diagnostic outputs are saved alongside the preprocessing workspace.
- Model scripts save new model objects under `Models/` and new summary outputs under `Results/Model_Summaries/`.
- The model scripts select the most recently modified preprocessing subfolder. If multiple preprocessing runs exist, verify that the newest folder is the intended one before running the model scripts.

## License and citation

The code in this repository is distributed under the MIT License, as specified in `LICENSE`. This license does **not** change the license or terms applying to the third-party GreenHyperSpectra dataset.

If you use this repository, please cite it using the information in `CITATION.cff`. If you use the GreenHyperSpectra data, also cite the dataset and its associated publications as requested by the dataset authors.
