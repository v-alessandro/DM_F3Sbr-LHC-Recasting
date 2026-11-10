# F3Sbr Dark Matter: LHC Recasting and Exclusion Limits

Research internship at the Laboratoire de Physique Théorique et Hautes Énergies (LPTHE), Paris — June–July 2026.

Project by Victor Alessandro Sales Lopez, Sidi-Mansour Malagouen and Laëtitia Renard.  
Supervised by Benjamin Fuks and Silvia Manconi.

[Read the internship report (PDF)](LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf)

## About the project

During this internship, we studied the F3Sbr simplified dark matter model, in which a dark matter particle interacts with Standard Model particles through a mediator. Our goal was to use results from LHC experiments to constrain the model's parameters, particularly the masses of the dark matter particle and mediator, and their coupling.

We started by exploring the model with MadGraph5_aMC@NLO, then used Pythia 8 and MadAnalysis 5 to simulate and analyse collision events. We developed a Python-based statistical analysis using Spey to reinterpret five ATLAS and CMS Run 2 searches and obtain exclusion limits at 95% confidence level. We also studied how these limits could evolve with Run 3 and the High-Luminosity LHC (HL-LHC).

The [full report](LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf) explains the physics, methods and results in more detail. This repository contains the code and supporting materials from the project.

## Repository contents

| File or folder | Contents |
| --- | --- |
| [Internship report](LPTHE_Internship_DarkMatter_Exclusion_Limits.pdf) | Full report on the project and its results. |
| [Research journal](Journal_de_bord.pdf) | Week-by-week notes, including setup, progress and problems encountered (in French). |
| [Code](Code/) | Python scripts used throughout the project. |
| [Analyses](Analyses/) | ATLAS and CMS analyses used with MadAnalysis 5. |

## Python scripts

### [fit_madgraph.py](Code/fit_madgraph.py)

An exploratory script used to understand how the mediator decay width and production cross section change with the model's masses and coupling. It compares MadGraph results with analytical expressions, performs numerical fits and produces plots of the different parameter scans.

### fit_madanalysis.py

A companion script for the initial exploration of results from MadAnalysis 5, before moving on to the statistical reinterpretation of the LHC searches.

### [calcul_limites_exclusion.py](Code/calcul_limites_exclusion.py)

The main analysis script. It uses the simulated signal events and the experimental information from ATLAS and CMS to calculate exclusion limits with Spey (and pyhf where appropriate). It also provides projections for Run 3 and the HL-LHC, and saves the results and plots for later comparison.

### [comparaison_runs_lhc.py](Code/comparaison_runs_lhc.py)

Uses the results of the main script to compare the exclusion limits from Run 2, Run 3 and the HL-LHC, both for individual searches and for the most constraining result across the analyses.

## Using the code

The analysis relies on MadGraph5_aMC@NLO, Pythia 8 and MadAnalysis 5, along with Python libraries such as NumPy, SciPy, Matplotlib, Spey and pyhf. The statistical scripts also use simulation outputs and experimental input files, and their local directory paths need to be adapted to the user's setup.

The main script calculates the limits for a chosen coupling and LHC scenario; the comparison script then brings together the saved results. More information about the setup and the steps followed during the internship can be found in the [research journal](Journal_de_bord.pdf).
