# Cancer3D Validation

**Validation code for a 3D hybrid mechanistic model of tumor growth**  
*Bouchnita Lab · University of Texas at El Paso*

---

## Overview

This repository provides the code to reproduce the model validation results reported in the **Model Validation** section of our paper. It compares outputs from two complementary cancer growth models against *in vitro* experimental data across two receptor density conditions (6 receptors and 24 receptors):

- A **continuous PDE-based model** — fast, analytically tractable representation of tumor cell dynamics
- A **3D hybrid agent-based model** — spatially explicit, stochastic simulation of individual cell behavior in three dimensions

Agreement between both models and wet-lab measurements validates the underlying biological assumptions and parameter choices of Cancer3D.

---

## Repository Structure

```
Cancer3D_validation/
├── continuous_val.py          # Runs the continuous (PDE) model
├── 3Dhybrid_val.py            # Compiles and runs the 3D hybrid (C++) model
├── plot_validation.py         # Generates the combined validation figure
├── 06receptors/base/          # Output directory for 6-receptor hybrid simulations
├── 24receptors/base/          # Output directory for 24-receptor hybrid simulations
└── README.md
```

---

## Requirements

| Component | Version |
|-----------|---------|
| Python    | 3.x (scripts 1–2) · 2.x (plotting script) |
| C++ compiler | g++ (installed automatically by `3Dhybrid_val.py`) |
| CMake     | ≥ 3.x (installed automatically) |
| Python packages | numpy, matplotlib, pandas (install via `pip`) |

> **OS:** Linux is assumed. The build step in `3Dhybrid_val.py` uses `apt` to install system dependencies. On macOS, you may need to install `cmake` and `g++` manually via Homebrew.

---

## Quickstart

### 1. Clone the repository
```bash
git clone https://github.com/Romasa/Cancer3D_validation.git
cd Cancer3D_validation
```

### 2. Run the continuous model
Generates cell count CSVs for both receptor conditions:
```bash
python3 continuous_val.py
```
**Output:** `cell_count_6_receptors.csv`, `cell_count_24_receptors.csv`

### 3. Run the 3D hybrid model
Installs dependencies, compiles the C++ simulation, and runs it:
```bash
python3 3Dhybrid_val.py
```
> ⚠️ This step may take **several minutes**. The paper reports results as the median ± confidence interval over **25 independent runs**; this script performs a single run, so results will vary slightly from published figures.

**Output:** `06receptors/base/data.txt`, `24receptors/base/data.txt`

### 4. Generate the validation figure
```bash
python2 plot_validation.py
```
**Output:** `validation_combined.png` — a figure overlaying both model outputs against experimental measurements.

---

## Scientific Context

Tumor growth is governed by a complex interplay of cell proliferation, nutrient availability, mechanical pressure, and receptor-ligand signaling. Cancer3D captures these dynamics by coupling:

- A **continuous phase** modeling oxygen/nutrient diffusion and average cell density fields
- A **discrete (agent-based) phase** tracking individual cell fate decisions (proliferation, migration, death)

The receptor density parameter (6 vs. 24 receptors per cell) modulates ligand-binding rates and downstream proliferative signaling, serving as a key axis of validation against experimental growth curves.

---

## Citation

> *If a preprint or publication is associated with this work, please add the citation here.*  
> **Romasa Qasim**, et al. Cancer3D: A 3D Hybrid Mechanistic Model of Tumor Growth. *(in preparation / under review)*

---

## Contact

**Romasa Qasim** — PhD Candidate, Computational Science  
University of Texas at El Paso · Bouchnita Lab  
📧 rqasim@miners.utep.edu  
🔗 [LinkedIn](https://linkedin.com/in/romasa-qasim-a5916a1a) · [GitHub](https://github.com/Romasa)
