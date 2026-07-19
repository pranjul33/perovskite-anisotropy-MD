# Processed data

Post-processed quantities behind the figures. Raw trajectories are on Zenodo
(see the top-level README).

## Steinhardt bond-order parameters
`q6_lead_tension_x.txt`, `q6_lead_tension_z.txt`, `q6_lead_compression_x.txt`

Per-atom Steinhardt bond-orientational order parameters for the **Pb sublattice**,
in LAMMPS dump format (one block per strain frame; 31 frames each). Columns:

```
id  type  xs  ys  zs  c_boolead[1]  c_boolead[2]  c_boolead[3]  c_boolead[4]  c_boolead[5]
```
where `c_boolead[1..5]` = **Q4, Q6, Q8, Q10, Q12**. **Q6 (`c_boolead[2]`)** is the
one used to quantify amorphization — a lower Q6 means a more disordered lattice.
Parsed by `../analysis/scripts/lead_bond_order_orientational_parameter.ipynb`.

## Radial distribution functions
`C-N_rdf_tension_x.txt`, `C-N_rdf_tension_z.txt`

Time-averaged RDFs written by the LAMMPS `compute rdf` / `fix ave/time` command
(21 columns: bin coordinate plus g(r) and coordination for each atom-type pair).
Parsed by `../analysis/scripts/extract_rdf.ipynb`.

## MA cation orientation
`MA_orientation_vectors.csv`

Orientation unit vector of each methylammonium (C→N) cation per frame.
Columns: `Frame, Molecule, X, Y, Z`. Used for the orientational-probability /
cation-dynamics analysis.
