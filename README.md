# SpaceX Falcon 9 First-Stage Landing Prediction — IBM Applied Data Science Capstone

**Author:** Hashem Almomani · **Date:** October 2026

Final project of the [IBM Data Science Professional Certificate](https://www.coursera.org/professional-certificates/ibm-data-science) (Applied Data Science Capstone).
SpaceX advertises Falcon 9 launches at ~$62M versus $165M+ for other providers because it can reuse the first stage.
This project collects the launch history, explores it, visualises it interactively and trains classifiers that predict whether the first stage will land.

## Report

* **[Data Science Capstone Project Report.pdf](Data%20Science%20Capstone%20Project%20Report.pdf)** — the full 54-slide report (PowerPoint source: `Data Science Capstone Project Report.pptx`).

## Notebooks and code (in the order of the course modules)

| # | File | Module | Content |
|---|------|--------|---------|
| 1 | `1_spacex_data_collection_api.ipynb` | Data collection | SpaceX REST API (v4) → `pandas.json_normalize` → Falcon 9 filter → `data/dataset_part_1.csv` |
| 2 | `2_spacex_web_scraping.ipynb` | Data collection | Wikipedia launch tables with `requests` + `BeautifulSoup` → `data/spacex_web_scraped.csv` (121 launches) |
| 3 | `3_spacex_data_wrangling.ipynb` | Data wrangling | value counts per site / orbit / outcome, `bad_outcomes`, binary label `Class` → `data/dataset_part_2.csv` |
| 4 | `4_spacex_eda_sql.ipynb` | EDA with SQL | SQLite + `%sql` magic, the 10 assignment queries on `data/Spacex.csv` |
| 5 | `5_spacex_eda_data_visualization.ipynb` | EDA with visualization | Seaborn/Matplotlib charts, feature engineering → `data/dataset_part_3.csv` |
| 6 | `6_spacex_folium_launch_sites.ipynb` | Interactive visual analytics | Folium map: launch sites, colour-coded outcomes (MarkerCluster), proximity distances |
| 7 | `7_spacex_dash_app.py` | Interactive visual analytics | Plotly Dash dashboard (site dropdown, payload range slider, pie + scatter callbacks) |
| 8 | `8_spacex_machine_learning_prediction.ipynb` | Predictive analysis | Logistic Regression, SVM, Decision Tree, KNN with `GridSearchCV` (cv = 10) |

`images/` contains the charts, Folium map captures and dashboard screenshots used in the report.

## Key results

* 90 Falcon 9 launches (2010 – Nov 2020); overall first-stage landing success **66.7 %**, rising from 0 % (2010-2013) to **84-90 %** in 2019-2020.
* Best launch site: **KSC LC-39A** (77 % success). Orbits ES-L1 / GEO / HEO / SSO: 100 %; GTO only 52 %.
* All four tuned classifiers reach ≥ 83.3 % test accuracy; the **Decision Tree** reaches **94.4 %** (CV accuracy 87.5 %) with a single false positive.

## How to run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn folium dash plotly beautifulsoup4 requests ipython-sql prettytable jupyter
jupyter notebook            # open any notebook; they read the data from the course URLs (copies are in data/)
python 7_spacex_dash_app.py # dashboard on http://127.0.0.1:8050  (needs data/spacex_launch_dash.csv next to the script)
```

> Note: the notebooks were re-executed on 23 Oct 2026. The live `api.spacexdata.com` endpoints returned HTTP 522 that day, so the
> enrichment cells of notebook 1 carry a note; the course-provided `dataset_part_1.csv` (the output of those steps) is used downstream.
> The intermediate files produced by notebooks 3 and 5 match the course-provided files byte for byte.
