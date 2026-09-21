# ppea02-data

Stable copies of the public datasets used in the practical sessions of **Artificial Intelligence for
Social Impact** (PPEA02, LUISS Guido Carli, academic year 2026/27). The sessions run in Google Colab and
load these files by URL, so the URLs must not change during the semester: that is the only reason this
repository exists. Nothing here is original work; the sources and their terms are listed below.

## Files

| File | Rows | Columns | Load in Colab |
|---|---|---|---|
| `compas/compas-two-years.csv` | 7,214 | 50 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/compas/compas-two-years.csv")` |
| `adult/adult.csv` | 32,561 | 15 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/adult/adult.csv")` |

## Provenance

### COMPAS (`compas/`)

- **Source**: ProPublica, *compas-analysis* repository, file `compas-scores-two-years.csv`
  (https://github.com/propublica/compas-analysis), the data behind *Machine Bias* (Angwin, Larson,
  Mattu & Kirchner, ProPublica, 23 May 2016) and its methodology note *How We Analyzed the COMPAS
  Recidivism Algorithm* (Larson, Mattu, Kirchner & Angwin, 2016).
- **What a row is**: one person screened with the COMPAS tool in Broward County, Florida, between
  2013-01-01 and 2014-12-31, with the risk decile assigned and whether a new offence was recorded
  within two years.
- **What was changed**: the three name columns (`name`, `first`, `last`) were removed, so the copy has
  50 columns instead of 53. No row was added, removed or edited. The original file is at the source
  above.
- **Terms**: the data was obtained by ProPublica through public records requests and released with their
  analysis; this copy is redistributed for teaching, with attribution. ProPublica is not affiliated with
  this course.

### Adult / Census Income (`adult/`)

- **Source**: UCI Machine Learning Repository, *Adult* dataset (Becker & Kohavi, 1996), file
  `adult.data`, https://archive.ics.uci.edu/dataset/2/adult. Extracted from the 1994 US Census
  database.
- **What a row is**: one person, with demographic and employment attributes and whether their income
  exceeded 50,000 USD.
- **What was changed**: a header row was added with the column names from `adult.names`; leading spaces
  were stripped; the `?` placeholder was converted to an empty value. The training split only
  (32,561 rows); `adult.names` is kept for reference.
- **Terms**: CC BY 4.0 (UCI Machine Learning Repository).

## Reference figures

These are the numbers a notebook can check its own output against. They were computed on the files in
this repository; a different number means the file did not load as expected.

### `compas/compas-two-years.csv`

| Check | Value |
|---|---|
| rows, columns | 7,214 × 50 |
| `race` | African-American 3,696 · Caucasian 2,454 · Hispanic 637 · Other 377 · Asian 32 · Native American 18 |
| `sex` | Male 5,819 · Female 1,395 |
| `age_cat` | 25 - 45: 4,109 · Greater than 45: 1,576 · Less than 25: 1,529 |
| `score_text` | Low 3,897 · Medium 1,914 · High 1,403 |
| `two_year_recid` | 0: 3,963 · 1: 3,251 |
| `c_charge_degree` | F 4,666 · M 2,548 |
| people under 25 | 1,529 |
| `age` range | 18 to 96 |
| `decile_score` range | 1 to 10 |
| missing values, examples | `days_b_screening_arrest` 307 · `c_jail_in` 307 · `c_offense_date` 1,159 · `c_arrest_date` 6,077 |
| `compas_screening_date` range | 2013-01-01 to 2014-12-31 |

### `adult/adult.csv`

| Check | Value |
|---|---|
| rows, columns | 32,561 × 15 |
| `sex` | Male 21,790 · Female 10,771 |
| `race` | White 27,816 · Black 3,124 · Asian-Pac-Islander 1,039 · Amer-Indian-Eskimo 311 · Other 271 |
| `income` | <=50K 24,720 · >50K 7,841 |
| people under 25 | 5,570 |
| missing values | `workclass` 1,836 · `occupation` 1,843 · `native_country` 583 |
