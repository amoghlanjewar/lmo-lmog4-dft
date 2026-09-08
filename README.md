
---

## Repository structure

```
repo/
├── README.md
│
├── dft_inputs/
│   ├── LMO.in                      # Quantum ESPRESSO SCF input (was LMX.in)
│   ├── LMOG4.in                    # Quantum ESPRESSO SCF input (was LMXG4.in)
│   ├── LMO.vasp                    # Structure file used for SuperHEX (LMX.vasp)
│   ├── LMOG4.vasp                  # Structure file used for SuperHEX (LMXG4.vasp)
│   └── pseudopotentials/           # (or a note on where to obtain them, if not redistributable)
│
├── superhex/
    ├── input_LMO.json              # SuperHEX config for LMO (volumes 1–16, Mo magnetic)
    ├── input_LMOG4.json            # SuperHEX config for LMOG4
    ├── struct_analysis_LMO.csv     # SuperHEX supercell ranking output
    ├── struct_analysis_LMOG4.csv
    └── selected_supercells/
        ├── LMO_cell-vol4-num9.vasp     # Supercell chosen for this study
        └── LMOG4_cell-vol4-num9.vasp
```

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


##  Contact

**Amogh U. Lanjewar**  
Project Fellow, Advanced Materials Research Laboratory (AMRL)  
Department of Physics  
Rashtrasant Tukadoji Maharaj Nagpur University  
Nagpur, Maharashtra, India  

 **Email:** amoghlanjewar@gmail.com
