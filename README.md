# project_movies_c- Part 1

> Data Mining course project — building a dataset of 5,000 movies with titles starting with **C**, combining IMDb, Wikipedia scraping, and the OMDb API.

**Team Members:**  
Ziv Nagad &
Tifferet Baluka

---

## Repository Structure

```
project_part1/
│
├── project_part1_final.ipynb       # Main notebook — full data collection pipeline
├── dataset25.csv        # Final cleaned dataset (5,000 movies, 13 columns)
├── rדוח איסוף נתוני סרטים סופי1.pdf           # Full project report
└── README.md            # This file
```

---

## Dataset Overview

The final dataset contains **5,000 movies** collected from three sources:

| Field | Type | Source |
|-------|------|--------|
| `tconst` | string | IMDb |
| `primaryTitle` | string | IMDb |
| `startYear` | int | IMDb |
| `genres` | list | IMDb |
| `lead_actors_ids` | list | IMDb |
| `runtimeMinutes` | int | IMDb |
| `averageRating` | float | IMDb |
| `numVotes` | int | IMDb |
| `Language` | string | Wikipedia |
| `Country` | string | Wikipedia |
| `budget` | string | Wikipedia |
| `BoxOffice` | string | Wikipedia |
| `plot` | string | OMDb |

---

## How It Works

The data collection pipeline runs in 4 steps:

1. **Load** — Download IMDb public datasets (`title.basics`, `title.ratings`, `title.principals`, `name.basics`)
2. **Filter** — Keep only movies starting with **C**, released by 2024, between 60–300 minutes
3. **Rank & Select** — Compute `success_score = averageRating × log(1 + numVotes)` and select top 5,000
4. **Enrich** — Wikipedia Search API + scraping for Language, Country, budget, BoxOffice. OMDb API for plot

---

## How to Run

### Requirements

- Python 3.8+
- Jupyter Notebook

### Install Libraries

```bash
pip install pandas numpy requests beautifulsoup4 ast time re
```

### Setup

Download the following files from [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/) and place them in the same folder as the notebook:

- `title.basics.tsv.gz`
- `title.ratings.tsv.gz`
- `title.principals.tsv.gz`
- `name.basics.tsv.gz`

### Steps

1. Open `project_part1_final.ipynb.ipynb` in Jupyter
2. Run all cells from top to bottom
3. The Wikipedia scraping section takes **several hours** due to rate limiting
4. When done, `dataset25.csv` will be saved in the current folder

> ⚠️ **Note:** The final `dataset25.csv` is already included in the repository so you don't need to re-run everything.

---

## Missing Values Summary

| Column | Missing Values | Missing % |
|--------|---------------|-----------|
| `tconst` | 0 | 0.00% |
| `primaryTitle` | 0 | 0.00% |
| `startYear` | 0 | 0.00% |
| `genres` | 0 | 0.00% |
| `lead_actors_ids` | 0 | 0.00% |
| `runtimeMinutes` | 0 | 0.00% |
| `averageRating` | 0 | 0.00% |
| `numVotes` | 0 | 0.00% |
| `Language` | 1,264 | 25.28% |
| `Country` | 1,263 | 25.26% |
| `budget` | 3,650 | 73.00% |
| `BoxOffice` | 3,316 | 66.32% |
| `plot` | 255 | 5.10% |

---

## Notes

- `budget` and `BoxOffice` high missingness is expected — most films do not publicly disclose financial data on Wikipedia.
- `Language` and `Country` missingness is due to Wikipedia pages that were blocked (HTTP 403) or not found.
- The OMDb API key is included in the notebook.
