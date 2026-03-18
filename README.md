# Annual MILP Capacity Planning for a Hybrid Wind-PV-DG-PHS System

This repository contains the main optimization program used for annual capacity planning of an off-grid hybrid energy system with:

- Wind turbines (`WT`)
- Photovoltaics (`PV`)
- Diesel generator (`DG`)
- Pumped hydro storage (`PHS`)

The model is formulated as a mixed-integer linear programming (`MILP`) problem at hourly resolution and is solved independently for each year in the study horizon. The objective is to minimize the levelized cost of energy (`LCOE`) under reliability, curtailment, operational, and carbon-intensity constraints.

## Main Program

- `W-PV-DG-PHS_V10 - PHS - 45 years configuration +curtailment iteration.ipynb`

This notebook is the main program used for the annual capacity-planning analysis.

## Model Summary

For each simulated year, the optimization simultaneously determines:

- Installed PV capacity
- Installed WT capacity
- Installed DG capacity
- Fixed PHS energy capacity and fixed PHS power capacities
- Hourly dispatch of PV, WT, DG, and PHS
- Hourly curtailment and unserved load
- PHS charging/generating operating states

The base model includes:

- Hourly energy balance
- PHS energy balance
- Mutually exclusive PHS pumping/generating modes
- DG capacity limit
- Reliability constraint via `LPSP`
- Curtailment-rate constraint
- Carbon-intensity constraint

## Study Design

The annual model is solved independently for each year over the study horizon:

- Time resolution: hourly
- Simulation horizon per run: `8760` hours
- Study period: `45` years
- Default notebook setting: full 45-year range

This structure is used to capture inter-annual climate variability while keeping the optimization problem tractable.

## Load Scenarios

The notebook currently supports two load-adjustment modes:

1. `load_multiplier`
   - Uniform scaling of the original load profile
   - Examples:
     - `1.0`: baseline load
     - `0.8`: -20% load volume
     - `1.2`: +20% load volume

2. `load_shape_factor`
   - Energy-preserving shape adjustment
   - Formula:
     - `L'_t = mu + kappa * (L_t - mu)`
   - Examples:
     - `1.0`: original shape
     - `< 1.0`: flatter profile
     - `> 1.0`: peakier profile

## Input File

The notebook is configured to read one integrated input file from the working directory:

- `input_data_45y.csv`

### Expected Columns

`input_data_45y.csv`

- `Year`
- `HourOfYear`
- `Timestamp`
- `CF_Wind`
- `CF_PV`
- `Load`

This single file contains the baseline hourly wind/PV capacity factors and load data. Load-volume and load-shape variations are implemented inside the main program through:

- `load_multiplier`
- `load_shape_factor`

## Final Public Release Structure

The final public release is intended to contain only three files:

- `README.md`
- `input_data_45y.csv`
- `W-PV-DG-PHS_V10 - PHS - 45 years configuration +curtailment iteration.ipynb`

## Solver

The optimization model uses:

- `Python`
- `gurobipy`
- `Gurobi Optimizer`

Default solver settings in the notebook:

- `MIPGap = 0.01`
- `TimeLimit = 240 s`

## Output

Results are written to:

- `planning_outputs/`

Typical outputs include:

- Summary tables
- Economic indicators
- Technical indicators
- Carbon-emissions indicators
- Capacity results
- Energy-drought metrics
- Curtailment comparison tables

## Notes

- This repository is intended to provide the main research code used in the study.
- The notebook is the main executable program.
- The repository is organized for transparency of model formulation and parameter settings rather than for full packaged reproducibility.
- Users should ensure that Gurobi is properly installed and licensed before running the notebook.

## Citation

If you use this code or adapt the model, please cite the associated paper.
