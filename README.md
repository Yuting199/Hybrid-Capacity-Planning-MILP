# Hybrid Capacity Planning MILP

This folder contains the public-release notebook for annual capacity planning of an isolated hybrid energy system composed of:

- Wind turbines (`WT`)
- Photovoltaics (`PV`)
- Diesel generator (`DG`)
- Pumped hydro storage (`PHS`)

The optimization model is formulated as a mixed-integer linear programming (`MILP`) problem and solved at hourly resolution for each year in the study horizon.

## Main File

- `Hybrid-Capacity-Planning-MILP.ipynb`

This notebook is the main executable model prepared for GitHub release.

## Model Scope

For each simulated year, the model determines:

- Installed PV capacity
- Installed wind capacity
- Installed diesel capacity
- PHS energy capacity
- Hourly dispatch of PV, wind, DG, and PHS
- Hourly curtailment
- Hourly unserved load

The objective is to minimize system cost while enforcing reliability, curtailment, operational, and carbon-related constraints.

## Input Data

The notebook expects one processed input dataset with the following default file name:

- `input_data_45 El Hierro.xlsx`

The notebook searches for this file in:

1. The notebook folder
2. `Data/`
3. `../Data/`

### Required Columns

The input file should contain at least these columns:

- `Year`
- `HourOfYear`
- `Timestamp`
- `CF_Wind`
- `CF_PV`
- `Load`

## Dependencies

Typical Python packages used by the notebook include:

- `pandas`
- `numpy`
- `gurobipy`
- `openpyxl`

You also need a working Gurobi installation and a valid Gurobi license.

## How To Run

1. Place the processed input file in one of the supported locations listed above.
2. Open `Hybrid-Capacity-Planning-MILP.ipynb`.
3. Review the configuration section near the top of the notebook.
4. Run the notebook from top to bottom.

## Output

Results are exported automatically to:

- `planning_outputs/`

Typical output sheets include:

- Summary results
- Economic indicators
- Technical indicators
- Carbon indicators
- Capacity configuration results
- Energy drought metrics
- Curtailment-rate comparison tables

## Notes

- This public version keeps the core optimization logic unchanged.
- Local machine paths and notebook outputs were removed for publication.
- The notebook is organized as a research model rather than a packaged software module.

## Citation

If you use or adapt this model in research, please cite the associated paper or project documentation.
