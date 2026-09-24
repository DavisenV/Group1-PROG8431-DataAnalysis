# Group 1: Predictive Maintenance Data Analysis (PROG8431)

This is Group 1's collaborative project for PROG8431. We explore the **AI4I 2020 Predictive Maintenance Dataset** to understand *when* and *why* a milling machine fails, using descriptive statistics and visualizations in a single Jupyter notebook.

The notebook [`main.ipynb`](main.ipynb) is both our analysis and the guide for our 5-minute presentation.

## Key findings

- **Failures are rare.** Only 339 of 10,000 runs (3.4%) end in a failure.
- **Torque is the strongest warning sign.** Failed runs have a median torque of 53.7 Nm, against 39.9 Nm for healthy runs.
- **Failures happen at the extremes of the operating range.** Most occur with a slow spindle under heavy load; a smaller group occurs at very high speed and low load.
- **Most failures have one identifiable cause.** Heat dissipation is the most common (115 runs), and only 21 failed runs combine two of the three main failure modes.
- **Low-quality (L) products fail most often**: 3.9%, compared with 2.1% for high-quality (H) products.

## The dataset

`data/predictive_maintenance.csv` is the [AI4I 2020 Predictive Maintenance Dataset](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset) from the UCI Machine Learning Repository. It is synthetic, but modelled on a real milling machine.

It has 10,000 rows (one per machine run), 12 columns and no missing values.

| Column | Meaning | Unit / values |
|---|---|---|
| `Type` | Product quality grade | `L` low (60%), `M` medium (30%), `H` high (10%) |
| `Air temperature [K]` | Temperature around the machine | kelvin |
| `Process temperature [K]` | Temperature of the cutting process | kelvin |
| `Rotational speed [rpm]` | Spindle speed | revolutions per minute |
| `Torque [Nm]` | Turning force on the spindle | newton-metres |
| `Tool wear [min]` | Time the current tool has been in use | minutes |
| `Machine failure` | Did this run fail? | `0` = no, `1` = yes |
| `TWF`, `HDF`, `PWF`, `OSF`, `RNF` | Failure mode: tool wear, heat dissipation, power, overstrain, random | `0` / `1` flags |

> **Note on column names:** the CSV headers have no units (e.g. `Air temperature`). The `MaintenanceDataset` loader adds the units when it reads the file, so **always load the data through `MaintenanceDataset`** rather than `pd.read_csv`. That way every section uses the same column names.

## Getting started

**You need:** Python **3.12 or newer** (the pinned `contourpy` and `numpy` versions do not install on 3.11), and VS Code with the Python and Jupyter extensions.

```bash
git clone https://github.com/DavisenV/Group1-PROG8431-DataAnalysis.git
cd Group1-PROG8431-DataAnalysis

python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Then open `main.ipynb` in VS Code:

1. Select the `.venv` interpreter as the kernel.
2. Click **Run All**.

The whole notebook should finish in under a minute with no errors.

### Libraries

| Library | Used for |
|---|---|
| pandas | Loading the CSV and calculating statistics |
| matplotlib | Scatter plot, histogram and box plots |
| matplotlib-venn | Venn diagram of failure modes |
| ipykernel | Running the notebook in VS Code |

## Notebook guide

The sections appear in this order in `main.ipynb`:

| Section | Assignment item | Owner | What it covers |
|---|---|---|---|
| Failure mode counts | Challenge 1 | Group | How many runs had each failure mode. This supports our essay in `docs/`. |
| Dataset overview | Challenge 3 | Person A | A one-minute explanation of every column. |
| `MaintenanceDataset` class | Challenge 4 | Person A | Loads the CSV once and provides the sensor columns and healthy/failed subsets. |
| Use case summary | Challenge 5 | Person B | The 50-word summary. |
| Central tendency and spread (`DescriptiveStats`) | Challenges 5 and 6 | Person B | Mean, median, mode, variance, standard deviation, quartiles and IQR. |
| Visualization and numerical summary (`MaintenanceVisualizer`) | Challenge 7 | Person C | Scatter plot, histogram, box plots, Venn diagram, a numerical summary, and failure rate by product type. |

## Repository layout

```
main.ipynb                        the analysis and presentation notebook
data/predictive_maintenance.csv   the dataset (10,000 rows)
docs/Group1 - Description.docx    Challenge 1 essay: field of inquiry
requirements.txt                  pinned library versions
```

## Team

| Role | Member | Sections |
|---|---|---|
| Person A | Davisen V. ([@DavisenV](https://github.com/DavisenV)) | Dataset overview, `MaintenanceDataset` class |
| Person B | Carlos Gutierrez | Use case summary, central tendency and spread |
| Person C | Nnamdi Ikengah ([@Namypark](https://github.com/Namypark)) | Visualization and numerical summary |

Every member must be able to explain and modify every section, not only their own.

## How we work

GitHub is our central hub for the project.

- **One branch per task.** For example: `challenge-7-visualization`.
- **Pull requests into `main`.** Another member reviews the pull request before it is merged.
- **Run All before merging.** The notebook must run top to bottom without errors on your machine first.
- **Descriptive commit messages** that say what changed and why.

### Coding standards

- Follow PEP 8 naming: `snake_case` for variables and methods, `PascalCase` for classes, `UPPER_CASE` for constants.
- Each section keeps its logic in a class and reuses the single `maintenance_dataset` object instead of reading the CSV again.
- Every chart or table is followed by a Markdown cell that explains what it shows and why it matters.

## Before the presentation

Every member should do this on their **own laptop**:

1. `git pull` the latest `main`.
2. Run `pip install -r requirements.txt`.
3. **Run All** in `main.ipynb`.
4. Check that the laptop connects to the classroom projector.
