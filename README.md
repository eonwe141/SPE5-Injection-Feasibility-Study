# SPE5 Gas Injection Feasibility Study

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18335824.svg)](https://doi.org/10.5281/zenodo.18335824)

## Overview

This repository contains modified input files and results from a parametric sensitivity study of compositional gas injection in the SPE5 benchmark reservoir using **OPM Flow**, an open-source reservoir simulator.

The study investigates the relationship between injection rate, numerical solver convergence, and stability boundaries—critical metrics for designing CO₂-EOR injection strategies.

---

## Repository Contents

SPE5-Injection-Feasibility-Study/
├── README.md # This file
├── LICENSE # MIT License
├── input-files/ # Modified SPE5 input decks
│ ├── SPE5_baseline_12000.DATA # 12,000 rb/day (baseline)
│ ├── SPE5_elevated_14000.DATA # 14,000 rb/day (+16.7%)
│ └── SPE5_critical_15000.DATA # 15,000 rb/day (+25%, fails)
├── results/
│ └── performance_metrics.csv # Simulation performance data
└── figures/
└── (to be added)

text

---

## Key Findings

- **16.7% increase** in injection rate → **3.5% increase** in linearizations
- **Sub-linear computational scaling** within stable operational envelope
- **Numerical stability boundary** identified at ~15,000 rb/day
- Solver fails to converge beyond stability limit

---

## Methodology

### Software
- **Simulator:** OPM Flow version 2025.10
- **Platform:** Ubuntu 22.04 LTS (WSL2)
- **Benchmark:** SPE5 Compositional (7×7×3 grid, 6-component EOS)

### Parametrization
Modified `WCONINJE` keyword to vary gas injection rate:
- Baseline: 12,000 rb/day
- Elevated: 14,000 rb/day
- Critical: 15,000 rb/day

All other parameters (grid, properties, well geometry) kept constant.

---

## How to Run

### Prerequisites
1. Install OPM Flow: [Installation Guide](https://opm-project.org/?page_id=245)
2. Download SPE5 benchmark: [OPM Tests](https://github.com/OPM/opm-tests)

### Execution

```bash
# Baseline case (12,000 rb/day)
flow input-files/SPE5_baseline_12000.DATA --enable-tuning=true

# Elevated case (14,000 rb/day)
flow input-files/SPE5_elevated_14000.DATA --enable-tuning=true

# Critical case (15,000 rb/day - will fail to converge)
flow input-files/SPE5_critical_15000.DATA --enable-tuning=true
Results
Case	Injection Rate (rb/day)	Timesteps	Wall Time (s)	Linearizations	Newton Iterations	Status
Baseline	12,000	277	4.19	1,289	1,013	✅ Converged
Elevated	14,000	275	4.11	1,334	1,060	✅ Converged
Critical	15,000	—	—	—	—	❌ Failed
Citation
If you use this work, please cite:

Padder, A. N. (2026). Compositional Reservoir Simulation and Gas Injection Feasibility: Implications for CO₂-EOR Using OPM Flow. Technical Report. Zenodo. https://doi.org/10.5281/zenodo.18335824

BibTeX:

text
@techreport{padder2026spe5,
  title={Compositional Reservoir Simulation and Gas Injection Feasibility: Implications for CO₂-EOR Using OPM Flow},
  author={Padder, Athar Nisar},
  year={2026},
  institution={Zenodo},
  doi={10.5281/zenodo.18335824},
  url={https://doi.org/10.5281/zenodo.18335824}
}
Related Publications
Technical Report: Zenodo DOI: 10.5281/zenodo.18335824

GitHub Repository: [This repository]

Author
Athar Nisar Padder
Email: anpadder@gmail.com
GitHub: @eonwe141

License
This work is licensed under the MIT License.

The SPE5 benchmark case is publicly available through the OPM Project.

Acknowledgments
Open Porous Media (OPM) Initiative for OPM Flow simulator

SPE (Society of Petroleum Engineers) for benchmark specifications
