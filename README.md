# F3Sbr Dark Matter: LHC Recasting and Exclusion Limits

**Research internship — Laboratoire de Physique Théorique et Hautes Énergies (LPTHE), Paris | June–July 2026**

**Project team:** Victor Alessandro Sales Lopez, Sidi-Mansour Malagouen, and Laëtitia Renard  
**Supervisors:** Benjamin Fuks and Silvia Manconi

**[Read the full internship report (PDF)](LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf)**

## Project overview

This project investigates collider constraints on the **F3Sbr simplified dark matter model**, in which a dark matter candidate interacts with Standard Model particles through a mediator in the *t*-channel. The aim was to reinterpret public LHC searches in terms of the model parameters, notably the dark matter mass, mediator mass, and coupling strength.

The analysis combines Monte Carlo event simulation with a statistical reinterpretation of **five ATLAS and CMS Run 2 searches**. Simulated signal events were produced using **MadGraph5_aMC@NLO** and **Pythia 8**, and analysed with **MadAnalysis 5**. A Python pipeline based on **Spey**, with **pyhf** workspaces where available, was used to derive **95% confidence-level exclusion limits** in the dark matter–mediator mass plane. The project also explores projected sensitivities for **Run 3** and the **High-Luminosity LHC (HL-LHC)** under specified luminosity and uncertainty-scaling assumptions.

The report linked above provides the physics background, methodology, and results. This repository contains the accompanying Python scripts and analysis materials.

## Analysis workflow

1. **Model exploration:** examine the dependence of production cross sections and mediator decay widths on masses and couplings using MadGraph results and analytical expressions.
2. **Signal simulation and selection:** generate events with MadGraph5_aMC@NLO and Pythia 8, then obtain signal-region information using MadAnalysis 5 recast analyses.
3. **Statistical reinterpretation:** combine predicted signal yields with published background and observation data, accounting for the statistical information available for each search.
4. **Exclusion plots:** calculate upper limits on signal strength, interpolate the mass-plane results, and display excluded regions.
5. **Future-LHC projections:** rescale yields and uncertainties to study the potential reach of Run 3 and the HL-LHC.

## Repository contents

| File or directory | Description |
| --- | --- |
| [`LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf`](LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf) | Full research report, including the theoretical context, methodology, and findings. |
| [`Journal_de_bord.pdf`](Journal_de_bord.pdf) | Internship log with weekly progress, installation notes, technical choices, and troubleshooting details (in French). |
| [`Code/`](Code/) | Python scripts for exploratory fits, statistical recasting, and comparison of LHC runs. |
| [`Analyses/`](Analyses/) | Supporting ATLAS/CMS MadAnalysis 5 recast materials. |

## Python scripts

### [`fit_madgraph.py`](Code/fit_madgraph.py) — exploratory MadGraph fits

Investigates how the **mediator decay width** and **simulated production cross section** depend on the model coupling and particle masses. It compares simulated decay-width values with an analytical expression, fits the width as a quadratic function of the coupling, and performs a fourth-degree polynomial fit to the cross section as a function of the coupling, including the simulation uncertainties. Additional parameter scans examine the dependence of these quantities on the dark matter and mediator masses. The script generates plots from numerical values recorded directly in the source code.

### `fit_madanalysis.py` — supplementary fitting script

This companion script is intended to document exploratory fits associated with MadAnalysis 5 outputs. **Its source is not currently accessible at `Code/fit_madanalysis.py` on the public `main` branch**, so the fitted observables, fit functions, and produced figures cannot yet be described reliably. This section should be completed once the script is available.

### [`calcul_limites_exclusion.py`](Code/calcul_limites_exclusion.py) — exclusion-limit calculation

This is the main statistical-analysis script. It extracts masses, couplings, and cross sections from simulation outputs, reads signal-region efficiencies and experimental information, and computes signal-strength upper limits with **Spey**. The statistical treatment depends on the information available for each search:

- **ATLAS searches with JSON likelihood workspaces:** signal samples are introduced into **pyhf** workspaces, which are evaluated through Spey.
- **CMS searches with covariance information:** correlated-background likelihoods incorporate the reported covariance matrices.
- **ATLAS searches without full likelihood information:** the most constraining signal region is selected from individual-region limits.

The script evaluates model points for Run 2 and can project sensitivities to Run 3 and the HL-LHC by scaling expected signal/background yields and treating statistical and systematic uncertainties separately. It saves numerical results as `.pkl` files and produces exclusion and signal-strength plots as `.png` files.

### [`comparaison_runs_lhc.py`](Code/comparaison_runs_lhc.py) — Run 2 / Run 3 / HL-LHC comparison

Loads the saved outputs of the main script for a chosen coupling and compares the exclusion regions for **Run 2**, **Run 3**, and the **HL-LHC**. It interpolates the signal-strength limits onto a common mass grid, plots the limits for each search, and constructs an overall exclusion comparison using the most constraining analysis at each point. The resulting comparison figures are saved as `.png` files.

## Running the analysis

The code was developed in a research environment rather than packaged as a standalone installation. The following dependencies and inputs are needed to reproduce the workflow:

- **Simulation and recasting:** MadGraph5_aMC@NLO, Pythia 8, and MadAnalysis 5, together with the relevant implemented ATLAS/CMS analyses.
- **Python libraries:** NumPy, SciPy, pandas, Matplotlib, Spey, and pyhf. The main script also attempts to use the JAX and Minuit backends for pyhf when available.
- **Input files:** generated simulation-point directories (including MadGraph banners and MadAnalysis cutflow outputs), experimental `.info` files, and the appropriate likelihood `.json` files.

The main scripts use **local absolute paths** that must be adjusted for a different machine. In `calcul_limites_exclusion.py`, set `base_dir` to the simulated-point directories, `info_dir` to the experimental input files, and `res_dir` to the desired output directory. The main script prompts for the coupling `Lambda` and the scenario (`2`, `3`, or `HL`). Run the main script separately for the scenarios to be compared, then run `comparaison_runs_lhc.py` on their saved outputs.

**Compatibility note:** `comparaison_runs_lhc.py` currently imports `interp_mu`, `lumi_tag_str`, and `fmt_lumi` from a module called `final_consultation_des_co`. Equivalent functions are defined in `calcul_limites_exclusion.py`; the import needs to be made consistent with the files in the working environment before executing the comparison script.

For installation history and troubleshooting notes, see the [internship log](Journal_de_bord.pdf).

## Project context

This work was completed as a **collaborative research internship at LPTHE**. The repository is provided to document the computational methodology and research outputs; it is not presented as a turnkey or independently validated software package.
