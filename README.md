# MADT 7202 · Mid-Term Applied Case

**Which supplier group should BMA Internal Audit sample first in FY2570?**
A supplier ↔ supplier co-presence network built from Bangkok district-office procurement awards.

## Files

| File | What it is |
|---|---|
| `MADT7202_midterm_procurement.ipynb` | Full analysis with all outputs: data loading, exclusions, graph construction (raw count vs Jaccard), robustness sweep, degree-preserving null model, figure, data export |
| `district_awards_pseudonymised.csv` | The analysis dataset: 1,948 district-office awards (FY2568–69), one row per award, natural persons hashed and names removed |
| `figure.png` | The network figure used in the report |

## Data

- **Source:** Bangkok Metropolitan Administration (BMA) Open Contract, OCDS publication via the Open Contracting Partnership Data Registry: https://data.open-contracting.org/en/publication/158
- **File:** `2026.csv.tar.gz` (CSV), downloaded 13 Oct 2026
- **Licence:** CC BY 4.0. No scraping.
- The raw download is **not** included, because it contains the tax IDs of sole traders (which are national ID numbers). `district_awards_pseudonymised.csv` is the cleaned version used in the analysis.

**Columns:** `ocid` (OCDS contracting-process ID, links back to the public source) · `fy` · `district_office` · `supplier_id` (tax ID for companies, `P-` hash for individuals) · `supplier_name` (`(individual)` for natural persons) · `individual` · `excluded_state_body` · `procurement_method` · `award_value_thb`

## How to reproduce

1. Download `2026.csv.tar.gz` from the link above and extract it, so a folder named `2026/` sits next to the notebook.
2. Set a private salt for pseudonymisation, e.g. `export PDPA_SALT=<any secret text>`.
3. Run the notebook top to bottom (Python 3, pandas, networkx, matplotlib).

The registry updates weekly, so a later download may add records and shift counts slightly.

## Privacy (PDPA)

Immediately after loading, every natural person's tax ID is replaced by a salted SHA-256 hash and their name is dropped. The salt used for the committed outputs is not stored anywhere, so the hashes cannot be reversed. Companies and partnerships keep their public tax IDs. The report labels the six sole traders T1–T6. The `P-` hashes in the CSV match those in the committed notebook outputs.

## Note

A shared district is a pattern worth sampling, not evidence of wrongdoing. See section 8 of the report.
