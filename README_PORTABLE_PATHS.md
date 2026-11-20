# Portable R scripts: folder setup and execution

The six scripts in `Code/` have had machine-specific `F:/...` and `D:/...` paths replaced with project-relative paths. The statistical/model-fitting code and parameter settings were not intentionally changed.

## 1. Open the project

1. Download or clone this repository.
2. Open `hyperspectral-Cp-ML-framework.Rproj` in RStudio.
3. Install `here` if needed:

   ```r
   install.packages("here")
   ```

The scripts use `here::here()` to resolve paths relative to the project root. Run them from the opened RStudio project.

## 2. Obtain and prepare the source data

The source hyperspectral data are available from the [GreenHyperSpectra dataset on Hugging Face](https://huggingface.co/datasets/Avatarr05/GreenHyperSpectra). The labeled configuration includes the spectral and trait data.

The scripts expect a local input file named:

`data/raw/Spectral_library_06-Oct-2026.csv`

The source file downloaded from Hugging Face may require preparation to match the exact structure expected by the scripts. Before running the workflow, verify the dataset version, selected source datasets, required columns, and file structure. Do not assume that simply renaming the downloaded `labeled/all.csv` file is sufficient.

Create the local input directory yourself; it is not tracked in this GitHub repository:

```text
hyperspectral-Cp-ML-framework/
├── hyperspectral-Cp-ML-framework.Rproj
├── Code/
├── data/
│   └── raw/
│       └── Spectral_library_06-Oct-2026.csv
├── Models/
└── Results/
```

The preprocessing script creates a dated workspace folder under `data/processed/` when it runs. You do not need to create or upload empty data folders in advance.

## 3. Run order

Run the scripts in this order:

1. `Code/01_preprocessing.R`
2. `Code/02_PLSR_nested_CV.R`
3. `Code/03_RF_nested_CV.R`
4. `Code/04_MBL_nested_CV.R`
5. `Code/05_SVR_nested_CV.R`
6. `Code/06_Validation.R` (after the four model scripts have generated their model and metadata files)

Run each script from RStudio using **Source**. Do not run the model scripts before preprocessing has generated the required `.RData` workspace.

## 4. Important notes

- The raw spectral data are not bundled with this repository; obtain them from the public GreenHyperSpectra dataset and prepare the expected local input file.
- The GreenHyperSpectra dataset is licensed under CC BY-NC 4.0. Consult its dataset card for terms and attribution before using or redistributing the data.
- The preprocessing script still changes the R working directory to its dated output folder so its existing relative diagnostic-output writes are saved alongside the preprocessing workspace. This does not affect the project-relative input/output locations used by the other scripts.
- The scripts select the most recently modified preprocessing subfolder. If you have multiple preprocessing runs, verify that the newest folder is the intended one before running the models.
- Keep the expected input filename unchanged, or update `INPUT_CSV`/`Input_CSV` consistently in the scripts.
- No modelling parameters, cross-validation settings, preprocessing choices, target definitions, or validation thresholds were deliberately altered in this path-portability update.
