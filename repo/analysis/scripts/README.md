# Analysis scripts

Jupyter notebooks that convert the raw LAMMPS output and the files in `../../data/`
into the figures of the manuscript.

| Notebook | What it does | Reads |
|----------|--------------|-------|
| `plot_property.ipynb` | Parses LAMMPS `log_*.lammps` thermo data and plots stress–strain and energy–strain curves (Figure 1a,b). | `../../deformation/*/log_*.lammps` |
| `lead_bond_order_orientational_parameter.ipynb` | Extracts the Q6 (and Q4/Q8/Q10/Q12) values of the Pb sublattice per strain frame and plots the evolution of amorphization (Figure 1c). | `../../data/q6_lead_*.txt` |
| `extract_rdf.ipynb` | Parses the time-averaged RDF output and plots C–N (and other) pair distribution functions at selected strains. | `../../data/C-N_rdf_*.txt` |

## Requirements
```bash
pip install numpy pandas matplotlib jupyter
```
Open with `jupyter notebook` (or JupyterLab / VS Code) and run the cells.
Adjust the input file paths at the top of each notebook if you reorganize folders.
