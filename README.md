# Two-Stage PPS Sampling App (WFP Somali Region)

Implements:
- **Stage 1 (PPS per kebele)** with Balanced MOS = `min(E,I)` (default) or `sqrt(E×I)`; if all `min(E,I)=0` in a kebele → fallback to `E+I`.
- **Targets & rules**: 15 E + 15 I per selected village; rebalance to **30 per group** within kebele; if **Ineligible < 30** at kebele → **skip I**; if one village can host **30 E**, use **only that village**.
- **Stage 2**: Systematic WOR within each `Kebele × Village × Group` cell; **Replacements** = `ceil(rate% × primaries)` from remainder (no overlap).
- **Export**: single Excel with `Primaries`, `Replacements`, `Selected_Villages`, `Allocation_Summary`, `Settings_Log`; optional per‑kebele printable sheets and MoDa tracking fields.

## Run locally
```bash
pip install -r requirements.txt
streamlit run app.py
```

## Input Excel
- Sheet **`Frame_Villages`**: `Kebele, Village, E_count, I_count` (or `Eligible/Ineligible` or `E/I`).
- Sheet **`Frame_HHs`**: `Kebele, Village, Group (E/I), HH_ID` + optional columns (e.g., Head_Name, Phone, Address).

Use the **“Input Template (.xlsx)”** download button in the app to get a starter file.

## Settings
- MOS method, Max villages per kebele, Seed mode (Data-derived / Fixed / Manual)
- **Replacement rate (%)** (default 25)
- Include MoDa fields, Printable per‑kebele sheets

## Outputs
One Excel: `Primaries`, `Replacements`, `Selected_Villages`, `Allocation_Summary`, `Settings_Log` (+ optional printable sheets).
