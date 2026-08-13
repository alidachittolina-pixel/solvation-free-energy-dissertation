# Machine-Learning Prediction of Solvation Free Energy

This repository accompanies Alida Chittolina's 2026 MSc dissertation at Queen Mary University of London:

*Machine-Learning Prediction of Solvation Free Energy: Fingerprints, Physicochemical Descriptors, and Molecular Graph Networks*.

## Project overview

The project investigates how molecular representation and evaluation protocol affect machine-learning predictions of solvation free energy. It compares:

1. 2048-bit Morgan fingerprints.
2. RDKit physicochemical descriptors.
3. Three-dimensional molecular graphs using ALIGNN and a molecular graph transformer (MGT).

The models were examined using fixed-random, entity-disjoint, scaffold-disjoint, and water-holdout evaluations. A separate density-functional-theory comparison used Gaussian 16, M05-2X, and the SMD water model.

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── 01_fingerprint_models.ipynb
│   ├── 02_descriptor_models.ipynb
│   └── 03_graph_models.ipynb
└── data/
    ├── SAMPL.csv
    ├── ML_Gibbs_Full_Database.csv
    └── dft/
        ├── dft_summary_20260724.csv
        └── dft_file_audit_20260724.csv
```

## Notebooks

- `01_fingerprint_models.ipynb`: aqueous SAMPL baseline using Morgan fingerprints and classical regression.
- `02_descriptor_models.ipynb`: fingerprint and RDKit-descriptor results, including entity-disjoint and water-holdout comparisons.
- `03_graph_models.ipynb`: preparation and evaluation of ALIGNN and MGT molecular-graph models.

Notebook outputs and execution counts were cleared to produce a compact, privacy-safe public repository. Some graph-training sections refer to HPC, prediction, split, or model artefacts that are not included in this compact release; the notebook retains the methodology and reported results.

## Data

- `SAMPL.csv`: 642 aqueous molecules with SMILES, experimental hydration free energies, and calculated reference values.
- `ML_Gibbs_Full_Database.csv`: 6,239 solute-solvent pairs, molecular identifiers, solvent classes, paired RDKit descriptors, and the `dG` target.
- `dft_summary_20260724.csv`: gas- and water-phase Gibbs energies, calculated DFT hydration free energies, frequency checks, status, and notes.
- `dft_file_audit_20260724.csv`: audit of Gaussian termination, optimisation, frequencies, thermochemistry, warnings, and failure reasons.

The DFT hydration free energy was calculated as:

```text
Delta G_solv = (G_SMD,water - G_gas) × 627.509474
```

The dissertation's final DFT/model comparison used the audited 55-molecule intersection. The DFT CSVs retain the wider candidate set so that the audit decisions remain transparent.

## Installation

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

Graph-model execution may additionally require compatible CUDA builds of PyTorch and DGL, ALIGNN, the MGT implementation used in the project, and suitable GPU resources.

## Citation

Alida Chittolina, *Machine-Learning Prediction of Solvation Free Energy: Fingerprints, Physicochemical Descriptors, and Molecular Graph Networks*, MSc dissertation, Queen Mary University of London, 2026.
