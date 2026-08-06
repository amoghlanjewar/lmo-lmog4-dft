# La₂Mo₂O₉ (LMO) and La₁.₆Gd₀.₄Mo₁.₇W₀.₃O₉ (LMOG4): DFT Electronic Structure & Supercell Data

This repository contains the input files, raw output data, analysis notebooks, and
figures accompanying the manuscript:

> **Atomistic Insights into the Role of Gd/W Co-doping on the Electronic Structure and
> Phase Stability of La₂Mo₂O₉: A First-Principles Supercell Investigation**
> A. U. Lanjewar, S. Acharya — Advanced Materials Research Laboratory, Department of
> Physics, Rashtrasant Tukadoji Maharaj Nagpur University, Nagpur, India.

The study compares the parent oxide **LMO** (La₂Mo₂O₉) with the Gd/W co-doped derivative
**LMOG4** (La₁.₆Gd₀.₄Mo₁.₇W₀.₃O₉) using DFT (Quantum ESPRESSO, PBE-GGA, spin-polarised)
and magnetic-supercell generation via **SuperHEX**.

> **Note on naming:** Some files in this repository were generated with the working
> labels `LMX`/`LMXG4`. These refer to the *same materials* as `LMO`/`LMOG4` used
> throughout the manuscript. We recommend renaming files to the `LMO`/`LMOG4`
> convention before archiving (see suggested structure below) to avoid confusion for
> readers.

---

## Repository structure (suggested)

```
repo/
├── README.md
├── LICENSE
│
├── dft_inputs/
│   ├── LMO.in                      # Quantum ESPRESSO SCF input (was LMX.in)
│   ├── LMOG4.in                    # Quantum ESPRESSO SCF input (was LMXG4.in)
│   ├── LMO.vasp                    # Structure file used for SuperHEX (LMX.vasp)
│   ├── LMOG4.vasp                  # Structure file used for SuperHEX (LMXG4.vasp)
│   └── pseudopotentials/           # (or a note on where to obtain them, if not redistributable)
│
├── superhex/
│   ├── input_LMO.json              # SuperHEX config for LMO (volumes 1–16, Mo magnetic)
│   ├── input_LMOG4.json            # SuperHEX config for LMOG4
│   ├── struct_analysis_LMO.csv     # SuperHEX supercell ranking output
│   ├── struct_analysis_LMOG4.csv
│   └── selected_supercells/
│       ├── LMO_cell-vol4-num9.vasp     # Supercell chosen for this study
│       └── LMOG4_cell-vol4-num9.vasp
│
├── dos_pdos_analysis/
│   ├── DOS.ipynb                   # Jupyter notebook: DOS/PDOS plotting + physics analysis
│   ├── analysis_report.txt         # Auto-generated DOS/PDOS summary report
│   └── physics.txt                 # Auto-generated comprehensive physics report
│
├── figures/
│   ├── LMO_Normal1.tif              # Unit cell visualization (was LMX_Normal1.tif)
│   ├── LMO_Supercell.tif            # Supercell visualization (was LMX_Supercell.tif)
│   ├── LMOG4_Normal1.tif            # (was LMXG4_Normal1.tif)
│   ├── LMOG4_Supercell1.tif         # (was LMXG4_Supercell1.tif)
│   ├── FIG2_LMO_PDOS_Stacked.png    # Orbital-resolved PDOS, LMO
│   ├── FIG2_LMOG4_PDOS_Stacked.png  # Orbital-resolved PDOS, LMOG4
│   ├── FIG7_LMO_Heatmap.png         # PDOS intensity heatmap, LMO
│   └── FIG7_LMOG4_Heatmap.png       # PDOS intensity heatmap, LMOG4
│
└── manuscript/
    ├── main.tex                    # Top-level LaTeX source (\input{} the section files)
    ├── introduction.tex
    ├── method.tex
    ├── results.tex
    ├── conclusions.tex
    ├── acknowledgement.tex
    ├── data_availability.tex
    └── references.bib
```

---

## What to upload here

| Category | Files | Notes |
|---|---|---|
| **DFT inputs** | `LMX.in` → rename `LMO.in`; `LMXG4.in` → rename `LMOG4.in` | Full QE `&CONTROL/&SYSTEM/&ELECTRONS` blocks, atomic positions, k-points, Hubbard U on Gd-4f |
| **Structure files** | `LMX.vasp`, `LMXG4.vasp` | Referenced by the SuperHEX `input.txt` files |
| **SuperHEX configuration** | the two `input.txt`-style JSON files you pasted (rename e.g. `input_LMO.json`, `input_LMOG4.json`) | Contains `volumes`, `magnetic_atoms`, `cutoff_radius`, `n_configs`, etc. |
| **SuperHEX output** | `struct_analysis.csv` (one per material), `log.txt` (optional — can be large) | Needed so readers can reproduce the choice of `cell-vol4-num9` |
| **Selected supercell** | the specific `cell-vol4-num9.vasp` file used for the reported exchange/PDOS calculations | This is the actual structure the paper's results are based on |
| **Analysis notebook** | `DOS.ipynb` | Contains all three analysis passes (DOS/PDOS plotting, physics engine, band-gap engine) — keep as-is; it is self-documenting |
| **Analysis reports** | `analysis_report.txt`, `physics.txt` | Auto-generated text reports referenced by the manuscript's Results section |
| **Figures** | `LMX_Normal1.tif`, `LMX_Supercell.tif`, `LMXG4_Normal1.tif`, `LMXG4_Supercell1.tif`, `FIG2_LMO_PDOS_Stacked.png`, `FIG2_LMOG4_PDOS_Stacked.png`, `FIG7_LMO_Heatmap.png`, `FIG7_LMOG4_Heatmap.png` | Rename with `LMO`/`LMOG4` prefixes for consistency with the manuscript |
| **Manuscript source** | the `.tex` section files and the corresponding `.bib` file(s) | So the paper is fully reproducible from source |

**Do not upload** copyrighted third-party material as-is (e.g. `PhysRevB_111_144419.pdf`) —
cite it in `references.bib` instead and link to the publisher's page/DOI.

---

## Reproducing the supercell selection

1. Run SuperHEX with the provided `input_LMO.json` / `input_LMOG4.json` against the
   corresponding `.vasp` structure file.
2. Inspect `struct_analysis.csv` (columns: supercell volume `m`, structure index `n`,
   rank, farthest permitted exchange interaction, % independent configurations,
   lattice-vector variation).
3. `grep` for the desired interaction range (e.g. `grep J7 struct_analysis.csv`) and
   balance against available computational resources.
4. This study selected **`cell-vol4-num9`** as the working supercell for both LMO and
   LMOG4.

## Reproducing the DOS/PDOS analysis

Open `DOS.ipynb` in the `dos_pdos_analysis/` folder. It expects `LMO.dos`,
`LMOG4.dos`, `LMO.pdos_tot`, `LMOG4.pdos_tot`, and the per-orbital
`*.pdos_atm#*` files (from Quantum ESPRESSO's `dos.x`/`projwfc.x`) to be present in
the working directory. Running all cells regenerates every figure and both text
reports referenced in the manuscript.

## Requirements

- Quantum ESPRESSO (tested with the pseudopotentials listed in `LMO.in` / `LMOG4.in`)
- [SuperHEX](https://superhex.readthedocs.io/en/latest/) for magnetic supercell enumeration
- Python ≥ 3.10 with `numpy`, `pandas`, `scipy`, `matplotlib` for the analysis notebook

## Citation

If you use this data or code, please cite the associated manuscript (see
`manuscript/references.bib` for the BibTeX entry once the paper is published/posted
on arXiv).

## License

Add a license (e.g. MIT for code/scripts, CC-BY-4.0 for data/figures) appropriate to
your institution's policy before making the repository public.

## Contact

Amogh U. Lanjewar, Smita Acharya — Advanced Materials Research Laboratory,
Department of Physics, Rashtrasant Tukadoji Maharaj Nagpur University, Nagpur, India.# La2Mo2O9
