# Equilibration

Relaxes and thermalizes the pristine supercell before mechanical loading.

| File | Description |
|------|-------------|
| `input777` | LAMMPS input: energy minimization (`box/relax`) followed by MD equilibration — NVE, then NVT (Nosé–Hoover, 300 K), then NPT (300 K, 1 atm). Reads `mp1194604(777).data` and the MYP force field, and writes the equilibrated structure. |
| `NPT777_aniso.data` | The equilibrated 7×7×7 supercell (300 K, 1 atm) produced by `input777`. This is the structure read by every run in `../deformation/`. |

Run with:
```bash
lmp -in input777
```

> Note: `input777` reads `mp1194604(777).data` and `dlpoly2lammps.nonbonding`.
> If you run it in this folder, copy those two files here from
> `../initial_structure/`, or edit the `read_data` / `include` paths accordingly.
