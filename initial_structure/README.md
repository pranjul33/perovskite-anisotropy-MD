# Initial structure & force field

Starting point for the simulations, before equilibration.

| File | Description |
|------|-------------|
| `H6PbCI3N.cif` | Orthorhombic MAPbI₃ (*Pnma*) unit cell in CIF format. |
| `mp1194604(777).data` | Pristine 7×7×7 supercell (16,464 atoms) in LAMMPS `data` format, built by replicating the unit cell taken from the Materials Project (entry mp-1194604). Contains atom coordinates, bonds, angles, and dihedrals. |
| `dlpoly2lammps.nonbonding` | MYP force-field non-bonded parameters (`pair_coeff` lines: Buckingham for the inorganic Pb–I interactions, Lennard-Jones/charmm for the hybrid interactions). Included via `include dlpoly2lammps.nonbonding` in every LAMMPS input. |

Atom type mapping: 1 = Pb, 2 = I, 3 = H (ammonium), 4 = N, 5 = C, 6 = H (methyl).

This pristine `.data` file is read by `equilibration/input777`, which produces the
equilibrated structure used for all deformation runs.
