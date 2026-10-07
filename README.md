# CausalMedia

Code for an anonymous manuscript under review. The study estimates heterogeneous effects of structured-content engagement on attainment in distance higher education, using a causal forest, and tests the estimator against a benchmark with known ground truth.

## Contents

| Folder | Notebook | Purpose |
|---|---|---|
| `01_corpus` | `01_corpus_construction.ipynb` | Loads and verifies the OULAD tables and builds the analytical corpus (five exclusions, 17,529 enrolments) |
| `02_benchmark` | `02_ihdp_benchmark.ipynb` | Runs the benchmark with known ground truth (100 realisations) |
| `03_causal_structure` | `dag.png` | Causal graph used for confounder selection |
| `04_estimation` | `04_estimation.ipynb` | Fits the causal forest and the baseline estimators |
| `04_estimation` | `04b_stability.ipynb` | Stability checks: leaf size, seeds (five for the corpus estimate), calibration |
| `05_evaluation` | `05_explainability.ipynb` | Explainability and heterogeneity analysis |
| `05_evaluation` | `05b_refutation.ipynb` | Refutation tests and sensitivity analysis |
| `05_evaluation` | `05c_figures.ipynb` | Figures |

## Data

The study uses the Open University Learning Analytics Dataset (OULAD; Kuzilek et al., 2017), released under CC-BY 4.0. The data are not redistributed here. Download the seven tables from the official OULAD page and place them in `raw/` at the repository root:

`studentInfo.csv`, `studentRegistration.csv`, `studentAssessment.csv`, `studentVle.csv`, `assessments.csv`, `vle.csv`, `courses.csv`

The release covers 22 module-presentations. The analysis uses nineteen of them. The loader in `01_corpus` checks row counts and prints a checksum prefix for each file.

## Running

1. Install the packages in `requirements.txt` (Python 3.13; the reported runs used 3.13.16 and 3.13.15 on Google Colab, CPU only).
2. Put the OULAD files in `raw/`.
3. Run the notebooks in numeric order, from the repository root or any folder inside it. Each notebook finds the root by looking for `raw/`, and writes derived files there.

Runtimes are long for the stability and refutation notebooks, because they refit the forest many times. The corpus estimate is reported over five seeds (42, 1, 7, 123, 2024). Course estimates are reported over four seeds (42, 1, 7, 123), in `04_estimation.ipynb`.

## Notes

- Course CCC cannot be resolved at its enrolment. No computation repairs this, and extra seeds do not narrow its interval.
- Sensitivity to unmeasured confounding is reported in standard-deviation units of treatment and outcome.

## Licence

MIT. See `LICENSE`.
