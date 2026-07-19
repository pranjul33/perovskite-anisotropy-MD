# Uniaxial deformation runs

Production runs that deform the equilibrated structure and record the
stress–strain response.

## Folders
- `tension/` — uniaxial tensile loading
- `compression/` — uniaxial compressive loading

## Files in each folder
| File | Loading direction |
|------|-------------------|
| `input_x`, `log_x.lammps` | [100] (a-axis) |
| `input_y`, `log_y.lammps` | [010] (b-axis) |
| `input_z`, `log_z.lammps` | [001] (c-axis) |

`input_*` are the LAMMPS input scripts; `log_*.lammps` are the corresponding
run logs containing the thermodynamic output (strain, von Mises stress, energies,
temperature, MSD, etc.).

## Method
Each run reads `NPT777_aniso.data` and the MYP force field, then applies
`fix deform` along the loading axis at an engineering strain rate of
**0.01 ps⁻¹** (1×10¹⁰ s⁻¹) under an **anisotropic NPT** ensemble, with the two
lateral directions barostatted to 1 atm so the sample can relax transversely.
Tension and compression differ only in the sign of the strain rate
(`+v_srate` vs `-v_srate`).

Von Mises stress is computed on the fly from the six pressure components; the
per-run trajectory (`deform.dump`, not included here — archived on Zenodo at
https://doi.org/10.5281/zenodo.21438115) is what the `../analysis` notebooks
post-process.

Run any case with, e.g.:
```bash
lmp -in input_x
```
