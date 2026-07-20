# Role of A-Site Cation Dynamics in Anisotropic Deformation of Orthorhombic MAPbI₃: A Molecular Dynamics Study

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21438115.svg)](https://doi.org/10.5281/zenodo.21438115)

Input files, force-field parameters, LAMMPS scripts, analysis notebooks, and
processed data.

---

## What this study does

We use classical molecular dynamics (LAMMPS) to study the anisotropic mechanical
response of orthorhombic MAPbI₃ (space group *Pnma*) under uniaxial tension and
compression along the [100], [010], and [001] directions. The system is a 7×7×7
supercell (16,464 atoms) modelled with the **MYP force field** (GAFF for the
organic methylammonium cation, Buckingham for the inorganic Pb–I cage, and a
Buckingham + electrostatic + Lennard-Jones description of the hybrid interactions).

Workflow: **initial structure → equilibration → uniaxial deformation → analysis**.

---

## Repository layout

```
repo/
├── README.md                     # this file
├── LICENSE                       # MIT license
├── CITATION.cff                  # how to cite this work
├── .gitignore
│
├── initial_structure/            # starting structure + force field
│   ├── H6PbCI3N.cif              # MAPbI3 orthorhombic unit cell (CIF)
│   ├── mp1194604(777).data       # pristine 7x7x7 supercell (Materials Project mp-1194604)
│   ├── lammps.nonbonding  # MYP non-bonded pair coefficients
│   └── README.md
│
├── equilibration/
│   ├── input777                  # minimize -> NVE -> NVT -> NPT protocol
│   ├── NPT777_aniso.data         # equilibrated structure used for all deformation runs
│   └── README.md
│
├── deformation/
│   ├── tension/                  # input_x/y/z + log_x/y/z.lammps  (uniaxial tension)
│   ├── compression/              # input_x/y/z + log_x/y/z.lammps  (uniaxial compression)
│   └── README.md
│
├── data/                         # processed data behind the figures
│   ├── q6_lead_tension_x.txt     # Steinhardt bond-order (Q4..Q12) of Pb sublattice
│   ├── q6_lead_tension_z.txt
│   ├── q6_lead_compression_x.txt
│   ├── C-N_rdf_tension_x.txt     # radial distribution functions
│   ├── C-N_rdf_tension_z.txt
│   ├── MA_orientation_vectors.csv# MA cation orientation unit vectors per frame
│   └── README.md
│
└── analysis/
    └── scripts/                  # Jupyter notebooks that turn raw output into figures
        ├── plot_property.ipynb
        ├── lead_bond_order_orientational_parameter.ipynb
        ├── extract_rdf.ipynb
        └── README.md
```

---

## Software requirements

| Tool | Purpose |
|------|---------|
| [LAMMPS](https://www.lammps.org) (KSPACE, MOLECULE, EXTRA-PAIR, RIGID packages) | MD simulation |
| Python ≥ 3.8 with `numpy`, `pandas`, `matplotlib`, `jupyter` | analysis notebooks |
| [OVITO](https://www.ovito.org) *(optional)* | trajectory visualization |
| [TRAVIS](http://www.travis-analyzer.de) *(optional)* | C–N autocorrelation / H-bond statistics |

---

## How to reproduce

1. **Equilibrate** (or use the provided `equilibration/NPT777_aniso.data`):
   ```bash
   cd equilibration
   lmp -in input777          # reads mp1194604(777).data, writes NPT777_aniso.data
   ```
2. **Deform** along any direction and mode:
   ```bash
   cd deformation/tension
   lmp -in input_x           # x, y, or z; likewise in deformation/compression
   ```
   Deformation uses `fix deform` at an engineering strain rate of 0.01 ps⁻¹ under
   an anisotropic NPT ensemble (lateral pressures held at 1 atm). Stress, strain,
   and energies are written to the `log_*.lammps` files.
3. **Analyze** by running the notebooks in `analysis/scripts/` (see that folder's
   README for which raw/processed files each one reads).

---

## Data availability

All inputs, scripts, and processed data are in this repository. The large raw
trajectory dump files are too large
for GitHub and are archived on **Zenodo**:

> Zenodo: https://zenodo.org/records/21438115 — DOI: [10.5281/zenodo.21438115](https://doi.org/10.5281/zenodo.21438115)

## License

Released under the MIT License (see `LICENSE`). Please cite the manuscript above.
