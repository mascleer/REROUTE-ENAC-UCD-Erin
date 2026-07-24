# RE-ROUTE Dublin Traffic Congestion Demonstrator
<img width="585" height="337" alt="re-route-logo" src="https://github.com/user-attachments/assets/4aa8a90b-460f-46be-8ccb-05f1996faf1c" />
A one-month student project using public Dublin traffic data to develop a lightweight, explainable congestion-detection and local rerouting demonstrator.

## Project information

- **Project:** RE-ROUTE, *integRated intElligent multi-modal tRanspOrt infrastrUcTurE*
- **Seconded researcher:** Erin Masclet, ENAC
- **Host institution:** University College Dublin
- **Duration:** One month
- **Primary language:** Python
- **Recommended operating system:** Windows, macOS, or Linux
- **Recommended development environment:** Visual Studio Code and Jupyter Notebook

## 1. Project summary

The objective is to analyse traffic-volume measurements from signalised junctions in Dublin and build a small proof-of-concept system that:

1. downloads and prepares public traffic data;
2. models normal traffic patterns for selected junctions;
3. identifies unusually high traffic volumes;
4. assigns an explainable congestion score;
5. visualises congestion geographically and over time; and
6. recommends less-congested alternatives among a small set of nearby junctions.

The final system is not intended to be a full navigation or traffic-control platform. It is a reproducible research demonstrator showing how lightweight analytics could support localised or edge-assisted transport decisions within the RE-ROUTE project.

## 2. Research question

> Can a lightweight, explainable algorithm identify unusual traffic congestion at Dublin junctions and generate simple local traffic-management recommendations using recent and historical traffic-volume observations?

## 3. Primary public dataset

### Dublin City Council SCATS traffic volumes

The main dataset is published by Dublin City Council through the Smart Dublin Open Data portal.

**Recommended dataset page:**

- [Traffic Volumes from SCATS Traffic Management System, January to June 2025](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025)

The dataset contains traffic counts collected from detectors associated with signalised junctions managed using the Sydney Coordinated Adaptive Traffic System, SCATS.

Typical fields include:

- observation date and time;
- SCATS site or junction identifier;
- detector identifier;
- traffic-volume total;
- average traffic volume for the measurement interval; and
- region or related location information, depending on the resource.

The dataset page may contain several monthly ZIP files. For a one-month project, begin with **one month of data**, rather than downloading the entire six-month collection.

### Recommended first file

Start with one monthly resource, for example:

- [SCATS traffic volumes, April 2025](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025/resource/708c46d2-ea5c-4172-be9a-021cfa0069df)

Direct download links on the portal may change. The safest procedure is to open the dataset page, select a monthly resource, and use the **Download** button.

### Alternative smaller introductory dataset

Some monthly SCATS files can be large. For initial testing of the code and folder structure, the aggregated January to June 2020 file is considerably smaller:

- [SCATS aggregated daily traffic volumes, January to June 2020](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2020/resource/5f9946a8-f800-4813-9c63-8742df0f15c5)

This aggregated file is useful for learning the workflow, but it has less temporal detail than the monthly detector files. The main analysis should use a detailed monthly file where possible.

## 4. Optional supporting datasets

### SCATS site locations

Search the Smart Dublin portal for a SCATS sites or traffic-signal locations file:

- [Smart Dublin Open Data portal](https://data.smartdublin.ie/)
- Suggested search terms: `SCATS sites`, `SCATS locations`, `traffic signal junctions`, or `traffic detectors`

A site-location file is required for the map-based part of the project. It should contain, at minimum:

- SCATS site identifier;
- junction or site name;
- latitude and longitude, or another geographic reference.

If a compatible SCATS site-location file cannot be found, the project can still be completed using time-series plots and a table of congestion states. A small manually prepared lookup table for 10 to 20 selected junctions may also be used, provided its sources are documented.

### Optional public-transport extension

The National Transport Authority provides Irish public-transport schedule and real-time services:

- [NTA Developer Portal](https://developer.nationaltransport.ie/)
- [NTA GTFS datasets](https://developer.nationaltransport.ie/GTFS)

GTFS-Realtime services require registration and an API key. They are an optional extension and are not necessary for completion of the core project.

## 5. Dataset licence and attribution

Check the licence shown on each dataset page before redistributing any data. The SCATS resources are generally published with an open-data or Creative Commons attribution licence.

The repository should preferably contain:

- scripts that download or prepare the data;
- instructions linking to the original source;
- a small processed sample, only where permitted; and
- attribution to Dublin City Council and Smart Dublin.

Do not commit the complete raw monthly datasets to GitHub because they may be large and may have redistribution conditions.

Suggested attribution:

> Traffic-volume data provided by Dublin City Council through the Smart Dublin Open Data portal.

## 6. Expected repository structure

```text
reroute-dublin-traffic/
|
|-- README.md
|-- LICENSE
|-- requirements.txt
|-- .gitignore
|
|-- config/
|   `-- config.yaml
|
|-- data/
|   |-- README.md
|   |-- raw/
|   |   |-- .gitkeep
|   |   `-- scats/
|   |       `-- .gitkeep
|   |
|   |-- interim/
|   |   `-- .gitkeep
|   |
|   |-- processed/
|   |   `-- .gitkeep
|   |
|   `-- external/
|       |-- .gitkeep
|       `-- scats_sites.csv
|
|-- notebooks/
|   |-- 01_data_inspection.ipynb
|   |-- 02_data_cleaning.ipynb
|   |-- 03_exploratory_analysis.ipynb
|   |-- 04_congestion_detection.ipynb
|   `-- 05_evaluation.ipynb
|
|-- src/
|   |-- __init__.py
|   |-- download_data.py
|   |-- prepare_data.py
|   |-- congestion.py
|   |-- routing.py
|   |-- visualisation.py
|   `-- utils.py
|
|-- dashboard/
|   `-- app.py
|
|-- outputs/
|   |-- figures/
|   |-- maps/
|   |-- tables/
|   `-- reports/
|
|-- tests/
|   |-- test_congestion.py
|   `-- test_prepare_data.py
|
`-- docs/
    |-- methodology.md
    |-- data_dictionary.md
    `-- final_report.md
```

## 7. Folder descriptions

| Folder | Purpose |
|---|---|
| `config/` | Parameters such as input paths, selected sites, thresholds and time intervals |
| `data/raw/` | Original downloaded files, unchanged |
| `data/interim/` | Extracted, combined or partially cleaned data |
| `data/processed/` | Final analysis-ready datasets |
| `data/external/` | Supporting data, such as SCATS site coordinates |
| `notebooks/` | Step-by-step exploratory and analytical work |
| `src/` | Reusable Python functions |
| `dashboard/` | Streamlit visual demonstrator |
| `outputs/figures/` | Static charts |
| `outputs/maps/` | HTML maps or map images |
| `outputs/tables/` | Summary CSV files |
| `outputs/reports/` | Generated reports or presentation material |
| `tests/` | Basic automated tests |
| `docs/` | Methodology, data documentation and final report |

## 8. Installation

### 8.1 Install Python

Install Python 3.11 or newer:

- [Python downloads](https://www.python.org/downloads/)

During installation on Windows, select:

```text
Add Python to PATH
```

Confirm the installation:

```bash
python --version
```

On some Windows systems, use:

```bash
py --version
```

### 8.2 Install Git

Download Git:

- [Git downloads](https://git-scm.com/downloads)

Confirm the installation:

```bash
git --version
```

### 8.3 Clone the repository

```bash
git clone https://github.com/ORGANISATION/reroute-dublin-traffic.git
cd reroute-dublin-traffic
```

Replace `ORGANISATION` with the GitHub organisation or account hosting the project.

### 8.4 Create a virtual environment

#### Windows PowerShell

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run the following command once in the current terminal:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate the environment again:

```powershell
.venv\Scripts\Activate.ps1
```

#### Windows Command Prompt

```cmd
py -m venv .venv
.venv\Scripts\activate.bat
```

#### macOS or Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 8.5 Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Suggested `requirements.txt`:

```text
pandas
numpy
matplotlib
jupyter
scipy
scikit-learn
geopandas
folium
streamlit
pyyaml
pytest
```

GeoPandas is only required for geographic analysis. Folium can create an interactive map without requiring a complex web framework.

## 9. How to obtain the data

### Option A, manual download, recommended for the first week

1. Open the [January to June 2025 SCATS dataset page](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025).
2. Review the dataset description and licence.
3. Select one monthly ZIP resource.
4. Click **Download**.
5. Save the ZIP file in:

```text
data/raw/scats/
```

6. Extract it into a month-specific folder, for example:

```text
data/raw/scats/2025-04/
```

7. Do not rename or edit the original source files.
8. Record the download date and source URL in:

```text
data/README.md
```

Example `data/README.md` entry:

```markdown
## SCATS April 2025

- Publisher: Dublin City Council
- Portal: Smart Dublin Open Data
- Dataset page: https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025
- Resource page: https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025/resource/708c46d2-ea5c-4172-be9a-021cfa0069df
- Downloaded: YYYY-MM-DD
- Stored locally in: data/raw/scats/2025-04/
- Licence: Check the resource page
```

### Option B, scripted download

A download script may be added once a stable direct resource URL has been confirmed.

Example:

```python
from pathlib import Path
from urllib.request import urlretrieve

DATA_URL = "PASTE_DIRECT_DOWNLOAD_URL_HERE"
OUTPUT_PATH = Path("data/raw/scats/scats_month.zip")

OUTPUT_PATH.parent.mkdir(parents=True, exist_ok=True)
urlretrieve(DATA_URL, OUTPUT_PATH)

print(f"Downloaded data to {OUTPUT_PATH}")
```

Run it with:

```bash
python src/download_data.py
```

Do not hard-code an unverified URL. Obtain the current direct URL from the resource page's **Download** button.

## 10. Initial data inspection

Launch Jupyter:

```bash
jupyter notebook
```

Open:

```text
notebooks/01_data_inspection.ipynb
```

The first notebook should:

1. locate the downloaded CSV file;
2. load a small sample;
3. print column names and data types;
4. inspect missing values;
5. identify the timestamp, site, detector and volume columns;
6. determine the temporal resolution; and
7. estimate memory usage before loading the complete file.

Example:

```python
from pathlib import Path
import pandas as pd

files = list(Path("data/raw/scats").rglob("*.csv"))

if not files:
    raise FileNotFoundError(
        "No CSV file found. Download and extract a SCATS resource first."
    )

data_file = files[0]
print(f"Reading: {data_file}")

sample = pd.read_csv(data_file, nrows=10_000)

print(sample.head())
print(sample.columns.tolist())
print(sample.dtypes)
print(sample.isna().sum())
```

Because source schemas can change, inspect the actual column names before writing the full cleaning pipeline.

## 11. Data preparation

The data-preparation pipeline should:

1. standardise column names;
2. parse timestamps;
3. convert traffic-volume fields to numeric values;
4. remove exact duplicate records;
5. flag rather than silently delete invalid measurements;
6. aggregate detector-level observations to site level where appropriate;
7. add weekday, hour and date fields;
8. select 10 to 20 sites for the initial demonstrator; and
9. save an analysis-ready file in `data/processed/`.

Suggested processed schema:

| Column | Description |
|---|---|
| `timestamp` | End of the observation interval |
| `site_id` | SCATS site identifier |
| `detector_id` | Detector identifier, where retained |
| `traffic_volume` | Observed volume |
| `date` | Calendar date |
| `weekday` | Day of the week |
| `hour` | Hour of day |
| `is_weekend` | Weekend indicator |
| `baseline_mean` | Expected volume for the same site and period |
| `baseline_std` | Historical standard deviation |
| `congestion_score` | Standardised congestion score |
| `congestion_state` | Normal, busy or congested |

Run the preparation script:

```bash
python src/prepare_data.py
```

Expected output:

```text
data/processed/scats_selected_sites.csv
```

## 12. Congestion-detection method

For each site and time period, estimate a historical baseline using observations from comparable weekdays and times.

A basic congestion score is:

```text
congestion_score =
    (observed_volume - baseline_mean) /
    (baseline_standard_deviation + epsilon)
```

where `epsilon` is a small value preventing division by zero.

Suggested initial classification:

| Congestion score | State |
|---:|---|
| `< 1.0` | Normal |
| `1.0 to < 2.0` | Busy |
| `>= 2.0` | Congested |

These are starting thresholds, not validated operational limits. Erin should evaluate and adjust them after inspecting the data.

Example implementation:

```python
from __future__ import annotations

import pandas as pd


def classify_congestion(score: float) -> str:
    """Convert a congestion score into an explainable category."""
    if pd.isna(score):
        return "unknown"
    if score >= 2.0:
        return "congested"
    if score >= 1.0:
        return "busy"
    return "normal"


def add_congestion_score(
    frame: pd.DataFrame,
    epsilon: float = 1e-6,
) -> pd.DataFrame:
    """Calculate a standardised congestion score."""
    required = {
        "traffic_volume",
        "baseline_mean",
        "baseline_std",
    }
    missing = required.difference(frame.columns)

    if missing:
        raise ValueError(f"Missing required columns: {sorted(missing)}")

    result = frame.copy()
    result["congestion_score"] = (
        result["traffic_volume"] - result["baseline_mean"]
    ) / (result["baseline_std"] + epsilon)

    result["congestion_state"] = result["congestion_score"].apply(
        classify_congestion
    )

    return result
```

## 13. Local recommendation logic

The recommendation component should remain simple and transparent.

For a selected congested site:

1. identify nearby candidate sites from the site-location table;
2. obtain the latest congestion score for each candidate;
3. exclude candidates with missing or stale observations;
4. rank the remaining sites by congestion score; and
5. recommend the lowest-scoring candidate.

This is a local traffic-management recommendation, not a complete route calculation. It does not account for road direction, legal turns, travel time, road closures or vehicle destination.

Example output:

```text
Current site: 205
State: Congested
Congestion score: 2.74

Suggested alternative monitored site: 198
Alternative state: Normal
Alternative congestion score: 0.63
Distance between monitored sites: 0.8 km
```

The limitations must be clearly displayed in the dashboard and final report.

## 14. Visualisations

The project should produce at least the following:

1. traffic volume by hour for selected sites;
2. weekday versus weekend patterns;
3. observed volume compared with the historical baseline;
4. congestion score over time;
5. number of congested periods by site;
6. map of selected sites labelled by congestion state; and
7. a table of local recommendations.

Save all figures in:

```text
outputs/figures/
```

Save interactive maps in:

```text
outputs/maps/
```

## 15. Running the dashboard

The preferred demonstrator is a small Streamlit application.

Run:

```bash
streamlit run dashboard/app.py
```

The dashboard should include:

- date and time selection;
- site selection;
- current traffic volume;
- expected traffic volume;
- congestion score and state;
- recent time-series chart;
- map of selected sites;
- ranked alternative sites; and
- a clear limitations statement.

A dashboard is a stretch goal. If time is limited, an organised Jupyter Notebook with saved charts and maps is an acceptable final demonstrator.

## 16. Testing

Run the tests with:

```bash
pytest
```

Minimum tests should cover:

- timestamp parsing;
- required-column validation;
- congestion-score calculation;
- handling of zero standard deviation;
- classification thresholds;
- missing values; and
- ranking of alternative sites.

## 17. Four-week plan

### Week 1, data acquisition and inspection

- Set up Python, Git and the repository.
- Download one month of SCATS data.
- Create the data documentation.
- Inspect the schema and file size.
- Select 10 to 20 sites.
- Produce initial traffic-volume plots.

**Milestone:** A reproducible notebook loads and describes the selected dataset.

### Week 2, cleaning and baseline modelling

- Build the reusable data-preparation script.
- Aggregate observations appropriately.
- Analyse daily and hourly traffic patterns.
- Calculate historical baselines.
- Implement the congestion score and categories.

**Milestone:** A processed dataset contains baseline values and congestion states.

### Week 3, recommendations and visualisation

- Obtain or prepare the site-location lookup.
- Create site-level maps.
- Implement the local recommendation logic.
- Develop the Streamlit interface or final analysis notebook.
- Measure execution time for the lightweight method.

**Milestone:** The demonstrator identifies congested sites and ranks alternatives.

### Week 4, evaluation and documentation

- Evaluate sensitivity to threshold choices.
- Check false alarms and unusual data periods.
- Add tests and improve code quality.
- Complete the methodology and data dictionary.
- Prepare the final report and presentation.
- Demonstrate the project to the RE-ROUTE team.

**Milestone:** Reproducible repository, report and working demonstration.

## 18. Expected outcomes

### Minimum viable outcome

The project is successful if it delivers:

- a documented GitHub repository;
- a repeatable data-preparation workflow;
- analysis of at least 10 SCATS sites;
- historical traffic baselines;
- an explainable congestion score;
- classification of normal, busy and congested periods;
- at least five useful visualisations;
- a notebook or dashboard demonstrating the results; and
- a short technical report describing methods, findings and limitations.

### Preferred outcome

In addition to the minimum outcome:

- an interactive map displays the selected sites;
- local alternative-site recommendations are generated;
- the code is organised into reusable Python modules;
- basic automated tests are included;
- configuration is separated from source code; and
- execution time is reported to demonstrate suitability for lightweight local processing.

### Stretch outcome

Subject to time and data availability:

- compare statistical thresholds with Isolation Forest or another simple anomaly detector;
- add an NTA GTFS or GTFS-Realtime data source;
- compare normal weekdays with event or disruption periods;
- simulate an incoming stream by replaying historical observations;
- package the system with Docker; or
- deploy the Streamlit dashboard internally.

## 19. Final deliverables

| Deliverable | Expected content |
|---|---|
| `D1` Data documentation | Sources, licences, fields, download dates and limitations |
| `D2` Prepared dataset | Selected sites and analysis-ready observations |
| `D3` Analysis notebooks | Inspection, cleaning, exploratory analysis and evaluation |
| `D4` Python modules | Preparation, congestion detection, recommendations and visualisation |
| `D5` Demonstrator | Streamlit dashboard or polished final notebook |
| `D6` Figures and tables | Saved outputs suitable for presentation |
| `D7` Technical report | Approximately 5 to 8 pages |
| `D8` Final presentation | Approximately 10 minutes plus demonstration |

## 20. Definition of done

The repository is considered complete when a new user can:

1. clone it;
2. create the Python environment;
3. follow the dataset download instructions;
4. run the preparation pipeline;
5. reproduce the main congestion results;
6. launch the dashboard or final notebook; and
7. understand the assumptions and limitations without additional verbal instructions.

## 21. Limitations

The demonstrator must state that:

- detector counts are not complete measurements of all road traffic;
- a vehicle may be counted at multiple junctions;
- detectors may not cover every approach to a junction;
- unusually high volume does not always mean congestion;
- unusually low volume may indicate detector failure or a road closure;
- the method does not estimate complete origin-to-destination routes;
- nearby monitored sites are not automatically valid route alternatives;
- geographic and road-network constraints require further work; and
- findings are research outputs, not operational traffic instructions.

## 22. Git workflow

Use small and descriptive commits:

```bash
git status
git add .
git commit -m "Add initial SCATS data inspection notebook"
git push
```

Recommended branches:

```text
main
data-preparation
congestion-model
dashboard
documentation
```

Create a branch:

```bash
git checkout -b congestion-model
```

Return to the main branch:

```bash
git checkout main
```

Merge completed work only after checking that notebooks and scripts run correctly.

## 23. Data and files excluded from Git

Suggested `.gitignore`:

```gitignore
# Python
__pycache__/
*.py[cod]
.pytest_cache/

# Virtual environments
.venv/
venv/

# Jupyter
.ipynb_checkpoints/

# Raw and generated data
data/raw/*
data/interim/*
data/processed/*
!data/raw/.gitkeep
!data/interim/.gitkeep
!data/processed/.gitkeep
!data/README.md

# Generated outputs
outputs/figures/*
outputs/maps/*
outputs/tables/*
!outputs/figures/.gitkeep
!outputs/maps/.gitkeep
!outputs/tables/.gitkeep

# Operating systems and editors
.DS_Store
Thumbs.db
.vscode/
```

## 24. Documentation requirements

The final report should address:

1. project motivation and relationship to RE-ROUTE;
2. dataset source, licence and limitations;
3. data-cleaning decisions;
4. selected sites and study period;
5. baseline method;
6. congestion-score definition;
7. recommendation method;
8. results and visualisations;
9. runtime and computational requirements;
10. validity threats and ethical considerations;
11. lessons learned; and
12. possible future extensions.

## 25. Responsible use

This project uses aggregated traffic measurements and should not require personal data. Nevertheless:

- use only public datasets;
- do not attempt to identify individual travellers;
- document every external data source;
- respect source licences and API conditions;
- avoid presenting experimental recommendations as official advice; and
- report data-quality issues transparently.

## 26. Useful links

- [RE-ROUTE project, CORDIS](https://cordis.europa.eu/project/id/101086343)
- [Smart Dublin Open Data](https://data.smartdublin.ie/)
- [Dublin City Council SCATS data, January to June 2025](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025)
- [Example April 2025 SCATS resource](https://data.smartdublin.ie/dataset/dcc-scats-detector-volume-jan-jun-2025/resource/708c46d2-ea5c-4172-be9a-021cfa0069df)
- [NTA Developer Portal](https://developer.nationaltransport.ie/)
- [NTA GTFS datasets](https://developer.nationaltransport.ie/GTFS)
- [Python](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Jupyter documentation](https://docs.jupyter.org/)
- [pandas documentation](https://pandas.pydata.org/docs/)
- [GeoPandas documentation](https://geopandas.org/)
- [Folium documentation](https://python-visualization.github.io/folium/)
- [Streamlit documentation](https://docs.streamlit.io/)

## 27. Acknowledgement

This work is undertaken as part of the RE-ROUTE project, Grant Agreement No. 101086343, funded through the Horizon Europe Marie Skłodowska-Curie Actions Staff Exchanges programme.

Traffic data are provided by Dublin City Council through the Smart Dublin Open Data portal.
