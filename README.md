# ppea02-data

Stable copies of the public datasets used in the practical sessions of **Artificial Intelligence for
Social Impact** (PPEA02, LUISS Guido Carli, academic year 2026/27). The sessions run in Google Colab and
load these files by URL, so the URLs must not change during the semester: that is the only reason this
repository exists. The data comes from public sources, listed below with their terms; the only addition
is the party, chamber and state of each member in `congress-twitter/congress_nodes.csv`, described in
its section.

## Files

| File | Rows | Columns | Load in Colab |
|---|---|---|---|
| `compas/compas-two-years.csv` | 7,214 | 50 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/compas/compas-two-years.csv")` |
| `adult/adult.csv` | 32,561 | 15 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/adult/adult.csv")` |
| `polblogs/polblogs_nodes.csv` | 1,490 | 3 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/polblogs/polblogs_nodes.csv")` |
| `polblogs/polblogs_edges.csv` | 19,022 | 2 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/polblogs/polblogs_edges.csv")` |
| `congress-twitter/congress_nodes.csv` | 475 | 7 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/congress-twitter/congress_nodes.csv")` |
| `congress-twitter/congress_edges.csv` | 13,289 | 3 | `pd.read_csv("https://raw.githubusercontent.com/XectX/ppea02-data/main/congress-twitter/congress_edges.csv")` |

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

### Political blogs, 2004 (`polblogs/`)

- **Source**: Adamic, L. A. & Glance, N. (2005). *The political blogosphere and the 2004 U.S.
  election: divided they blog*. LinkKDD '05, 36–43, doi:10.1145/1134271.1134277. File `polblogs` from
  Mark Newman's network data collection.
- **What a row is**: in `polblogs_nodes.csv`, one blog with its camp (`liberal` or `conservative`); in
  `polblogs_edges.csv`, one link from the blog `source` to the blog `target`.
- **What was changed**: the original file was converted to two CSV files for the course lectures. The
  edge file holds 19,022 distinct directed links, with no self-links.
- **Terms**: redistributed for teaching, with attribution; cite Adamic & Glance (2005).

### US Congress on Twitter, 117th Congress (`congress-twitter/`)

- **Source**: Fink, C. G., Omodt, N., Zinnecker, S. & Sprint, G. (2023). *A Congressional Twitter
  network dataset quantifying pairwise probability of influence*. Data in Brief, 50, 109521,
  doi:10.1016/j.dib.2023.109521. Downloaded from https://snap.stanford.edu/data/congress-twitter.html.
- **What a row is**: in `congress_nodes.csv`, one member account with at least 100 tweets between
  9 February and 9 June 2022 (475 accounts, a subset of the members of Congress). In
  `congress_edges.csv`, an edge from A to B means that B reacted to a tweet of A (retweet, quote, reply
  or mention): the information goes from A to B. The `weight` is the probability of influence estimated
  by the authors, a number between 0 and 1.
- **What was added**: the columns `name`, `party`, `chamber` (`rep` or `sen`), `state` and
  `party_source`. For 461 accounts they come from the public list `unitedstates/congress-legislators`
  (June 2022 version); 14 personal accounts absent from that list were assigned by hand from the account
  name (`party_source` = `assigned by hand`) and are unverified individually.
- **Terms**: redistributed for teaching, with attribution; cite Fink et al. (2023).

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

### `polblogs/`

| Check | Value |
|---|---|
| blogs, links | 1,490 · 19,022 |
| `camp` | liberal 758 · conservative 732 |
| links between blogs of the same camp | 17,339 of 19,022 (91.2%) |
| missing values | none |

### `congress-twitter/`

| Check | Value |
|---|---|
| members, edges | 475 · 13,289 |
| `party` | Democrat 253 · Republican 220 · Independent 2 |
| `chamber` | rep 383 · sen 92 |
| `party_source` | official list 461 · assigned by hand 14 |
| edges between members of the same party | 11,364 of 13,289 (85.5%) |
| `weight` range | 0.000526 to 0.130564 |
| missing values | none |
