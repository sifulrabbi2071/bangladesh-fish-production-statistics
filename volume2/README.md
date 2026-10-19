# Bangladesh Fish Production Statistics, Volume 2: Detailed Data Files (v1.0)

Machine-readable tables compiled from the Department of Fisheries (DoF) yearbooks of fisheries statistics, **2002-03 to 2024-25 (23 yearbooks)**, plus the national back series printed in those yearbooks (1983-84 to 2001-02).
For easy-to-read summary tables, see **Volume 1: Summary Tables** (PDF, Word and Excel).

**Compiled by:** Md Siful Islam Rabbi, Noakhali Science and Technology University, Noakhali-3814, Bangladesh

> Not an official DoF publication. All values come from DoF yearbooks; any transcription errors are the compiler's. Please cite both this dataset and the yearbooks.

**Unit:** metric tonnes (t); area in hectares (ha). **Years:** Bangladesh fiscal years (July-June), written as `2024-25`.

## Files

| File | Content |
|---|---|
| `csv/sector_production.csv` | National production by fishery sector (river, beel, floodplain, pond, shrimp farm, marine, etc.), 1983-84 to 2024-25, with water area where printed. Two value columns: current DoF series and as first published. |
| `csv/species_national.csv` | National production by species group, 2002-03 to 2024-25, with inland/marine split. |
| `csv/district_waterbody.csv` | Inland production by district and waterbody, every year 2002-03 to 2024-25 (64 districts). |
| `csv/species_waterbody.csv` | Inland production by species (or species group) and waterbody, 2002-03 to 2024-25 (2021-22 missing). |
| `csv/species_detail_beel_kaptai.csv` | Species tables for beels and Kaptai Lake as printed, 2002-03 to 2024-25. |
| `csv/printed_totals.csv` | National and inland totals printed in the yearbooks, for checking sums. |
| `csv/data_issues.csv` | 56 notes on breaks, reclassifications and source errors. Referenced by the 'flags' column. |
| `csv/crosswalks.csv` | Names as printed in each yearbook mapped to the names used in this dataset (sectors, species groups, districts). |
| `csv/sources.csv` | The 23 Department of Fisheries yearbooks used and how each was read. |
| `csv/codebook.csv` | Description of every column |
| `Bangladesh_Fish_Production_Statistics_Vol2_v1.0.xlsx` | All tables above in one workbook |

CSV files are UTF-8, comma-separated, long format (one row per number).

## Coverage

| Table | Years |
|---|---|
| Sector production (national) | 1983-84 to 2024-25 (42 years, no gaps) |
| Species groups (national) | 2002-03 to 2024-25 |
| District x waterbody | 2002-03 to 2024-25 (64 districts each year; Khagrachhari missing in 2002-03) |
| Species x waterbody | 2002-03 to 2024-25 except 2021-22 |
| Beel and Kaptai species detail | 2002-03 to 2024-25 |

## How to use

- **Two versions of some numbers.** The Department of Fisheries later revised a few years. `production_t` / `total_t` = latest DoF revision (use for time series); `*_as_published_t` = the figure in that year's own yearbook (use when citing a specific yearbook). They differ only for 2005-06 to 2008-09 and 2011-12 (sectors) and 2012-13 (species).
- **Check `flags`** before reading trends. Key breaks:
  - I04/I05/I27/I39: seasonal culture waterbodies counted as floodplain *capture* until 2004-05 (original yearbooks: until 2008-09); later counted as *culture*.
  - I06: pangas and tilapia split out of "Other catfish"/"Other inland fish" in 2013-14. I30: carp group definitions change in 2009-10.
  - I07: 2016-17 river/hilsa jump. I09: 2024-25 marine data source updated.
  - I28/I46: the 2016-17 and 2017-18 district tables do not add up in the yearbooks themselves.
  - I13/I42: Kaptai species detail lost from 2011-12; small native fish only in "Other inland fish".
- **Zeros:** in district and species-by-waterbody tables, 0 means zero or an empty cell in the yearbook (most often the waterbody does not exist in that district, e.g. Kaptai Lake outside Rangamati).
- **No double counting:** data tables contain components; totals are in `printed_totals`, and district totals appear as the waterbody "All inland (printed district total)".

## Quality control

- Text-layer PDFs were extracted programmatically; scanned yearbooks (2004-05, 2008-09, 2020-21, 2021-22, 2022-23, 2024-25) were read from page images.
- Every table was checked against the totals printed in the same yearbook: row totals, division subtotals, national totals.
- Recomputing national totals from `sector_production` reproduces the printed country total for all 42 years (both value columns).
- Overlapping years printed in different yearbooks were compared; all differences are documented in `data_issues`.
- Remaining mismatches are in the yearbooks themselves: 2010-11 species x waterbody (489 t), 2015-16 districts (rounding, 68 t), 2016-17 and 2017-18 districts, 2017-18 species (1 t).

## Example (R)

```r
library(readr); library(dplyr)
sec <- read_csv("csv/sector_production.csv")
sec |> group_by(fiscal_year, system) |> summarise(t = sum(production_t))
```

## Example (Python)

```python
import pandas as pd
d = pd.read_csv("csv/district_waterbody.csv")
d[d.waterbody.str.startswith("All inland")].pivot_table(index="district", columns="fiscal_year", values="production_t")
```

## Suggested citation

Md Siful Islam Rabbi (2026). Bangladesh Fish Production Statistics, 1983-84 to 2024-25: Summary Tables and Harmonized Data (Version 1.0) [Data set]. Zenodo.
Compiled from Department of Fisheries yearbooks of fisheries statistics, 2002-03 to 2024-25.

## License

This compilation is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0). The underlying statistics are from the Department of Fisheries, Bangladesh; please cite both this dataset and the yearbooks.

## Changelog

- **v1.0** (2026-10-19): complete release, 23 yearbooks (2002-03 to 2024-25) and national back series from 1983-84.
- v0.1 (2026-10-19): pilot from the 2002-03 and 2024-25 yearbooks.

---

## বাংলা সারসংক্ষেপ

মৎস্য অধিদপ্তরের ২৩টি বার্ষিক পরিসংখ্যান বই (২০০২-০৩ থেকে ২০২৪-২৫) থেকে নেওয়া ডাটা, সাথে ১৯৮৩-৮৪ থেকে জাতীয় সিরিজ।

- **দুই ধরনের সংখ্যা:** `production_t` হলো অধিদপ্তরের সর্বশেষ সংশোধিত সংখ্যা, যা সময়ের ধারা দেখতে ব্যবহার করুন। `*_as_published_t` হলো সংশ্লিষ্ট বছরের বইয়ে প্রথম ছাপা সংখ্যা।
- **প্রবণতা বিশ্লেষণের আগে** `flags` কলাম আর `data_issues` টেবিল দেখুন।
- **শূন্য (0):** সাধারণত বোঝায় ওই জেলায় ওই জলাশয় নেই।
- **২০১৬-১৭ ও ২০১৭-১৮:** এই দুই বছরের জেলা টেবিল মূল বইয়েই মেলে না, তাই সাবধানে ব্যবহার করুন।
- **লাইসেন্স:** CC BY 4.0। যে কেউ ব্যবহার, শেয়ার ও পরিবর্তন করতে পারবেন, শর্ত হলো উৎস হিসেবে এই ডাটাসেটের উল্লেখ করতে হবে।
- **এটি সরকারি প্রকাশনা নয়।** ব্যবহারের সময় এই ডাটাসেট আর মূল বই দুটোই উল্লেখ করুন।
