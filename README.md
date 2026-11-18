# Fiber laser cutting parameters (open data)

Starting cutting parameters for fiber laser cutting of sheet metal: mild steel, stainless steel, aluminium, brass and copper, from 0.5 kW to 80 kW. 1,128 rows, one per laser power, material, thickness and assist gas.

The same numbers are published on [sbmlaserhelp.com](https://sbmlaserhelp.com/answers/) and in the [cutting parameters table on sbmlaser.com](https://sbmlaser.com/our-services/cutting-parameters/), and are used by the SBM Laser Help app for laser cutting operators. Every row links to the matching page on sbmlaserhelp.com.

Also on Hugging Face: [SBMLaserHelp/fiber-laser-cutting-parameters](https://huggingface.co/datasets/SBMLaserHelp/fiber-laser-cutting-parameters).

## Files

| File | Format |
|---|---|
| `data/fiber-laser-cutting-parameters.csv` | CSV, UTF-8, comma-separated, header row |
| `data/fiber-laser-cutting-parameters.jsonl` | JSON Lines, one object per row, empty values are `null` |

## Columns

| Column | Unit | Meaning |
|---|---|---|
| `laser_power_w` | W | Rated laser source power |
| `material` | | `carbon_steel` (mild steel), `stainless_steel`, `aluminum`, `brass`, `copper` |
| `thickness_mm` | mm | Sheet thickness |
| `assist_gas` | | `O2`, `N2`, `Air` or `N2/Air` (nitrogen or compressed air) |
| `gas_pressure_bar` | bar | Assist gas pressure |
| `speed_min_m_min`, `speed_max_m_min` | m/min | Cutting speed range; equal values mean a single value |
| `power_percent` | % | Laser power used for cutting |
| `nozzle` | | Nozzle diameter in mm, `S` single-layer, `D` double-layer (for example `1.2D`) |
| `focus_mm` | mm | Focus position; positive is above the sheet surface, negative is inside the sheet |
| `cutting_height_min_mm`, `cutting_height_max_mm` | mm | Nozzle-to-sheet distance |
| `source_setup` | | Laser source and cutting head optics the row was set up on |
| `page_url` | | Page with this regime and alternatives on sbmlaserhelp.com |

`nozzle`, `focus_mm` and the cutting height are filled for 1.5, 2, 3, 6, 12 and 20 kW, as in the public table. For the other powers they are empty; they depend strongly on the cutting head and are available in the [SBM Laser Help app](https://sbmlaserhelp.com/).

## Example

```python
import pandas as pd

df = pd.read_csv("data/fiber-laser-cutting-parameters.csv")
row = df.query("laser_power_w == 3000 and material == 'carbon_steel' and thickness_mm == 6")
print(row[["assist_gas", "gas_pressure_bar", "speed_min_m_min", "speed_max_m_min", "nozzle", "focus_mm"]])
```

## Use with care

These are starting values for test cuts, not guaranteed production settings. The right speed, focus and pressure depend on the laser source, cutting head, nozzle, gas purity and the sheet itself. Cut a test piece first and adjust. Focus sign conventions differ between control systems: check what positive focus means on yours.

## Source and updates

The rows are compiled from parameter tables for the laser source and cutting head setups named in `source_setup`. Where several setups exist for one power, the most complete one is used. The table is exported from the same database that feeds the website and the app; the export date is in the commit history.

## License

Data: [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may copy, share and adapt it, including commercially, with attribution:

> Fiber laser cutting parameters, SBM Laser Help, https://sbmlaserhelp.com/

## About

[SBM Laser Help](https://sbmlaserhelp.com/) is a helper for fiber laser cutting operators: cutting parameter tables, cut defect diagnosis from a photo, machine and chiller error codes, calculators and a free library of DXF drawings. Web, Android, iOS and Telegram, 12 languages. Made by the team behind [SBMachines](https://sbmlaser.com/).
