# Processed data

Post-processed quantities behind the figures. Raw trajectories are archived on
Zenodo: https://doi.org/10.5281/zenodo.21438115

## MA cation orientation vectors
Orientation unit vector (C→N) of each methylammonium cation, one row per cation
per frame. Columns: `Frame, Molecule, X, Y, Z` (11 frames each).

| File | Loading case |
|------|--------------|
| `MA_orientationvectors_xten.csv`  | tension along [100] (a-axis) |
| `MA_orentationvectors_zten.csv`   | tension along [001] (c-axis) |
| `MA_orientationvectors_xcomp.csv` | compression along [100] (a-axis) |
| `MA_orientationvectors_zcomp.csv` | compression along [001] (c-axis) |

Used for the orientational-probability / cation-dynamics analysis.

## Radial distribution functions
Time-averaged RDFs written by the LAMMPS `compute rdf` / `fix ave/time` command.
Format: LAMMPS `ave/time` vector output — a `# TimeStep Number-of-rows` line per
frame followed by 20 rows of `bin  r  g(r)  coord ...` for each atom-type pair
(21 columns: `c_myRDF[1..21]`).

| File | Loading case |
|------|--------------|
| `C-N_rdf_tension_x.txt` | tension along [100] |
| `C-N_rdf_tension_z.txt` | tension along [001] |

Parsed by `../analysis/scripts/extract_rdf.ipynb`.

## Steinhardt bond-order parameters (Pb sublattice)
Per-atom Steinhardt bond-orientational order parameters for the Pb sublattice,
in LAMMPS dump format (one block per strain frame). Columns:

```
id  type  xs  ys  zs  c_boolead[1]  c_boolead[2]  c_boolead[3]  c_boolead[4]  c_boolead[5]
```
where `c_boolead[1..5]` = **Q4, Q6, Q8, Q10, Q12**. **Q6 (`c_boolead[2]`)** is the
one used to quantify amorphization — lower Q6 = more disordered lattice.

| File | Loading case |
|------|--------------|
| `q6_lead_tension_x.txt`     | tension along [100] |
| `q6_lead_tension_z.txt`     | tension along [001] |
| `q6_lead_compression_x.txt` | compression along [100] |

Parsed by `../analysis/scripts/lead_bond_order_orientational_parameter.ipynb`.
