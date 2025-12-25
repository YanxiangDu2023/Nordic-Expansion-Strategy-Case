
# Sweden Demographic Analysis — Nordic Expansion Strategy Case

Author: Yanxiang Du  
Date: November 2025  

This repo contains the code, notebooks and figures used to analyse Sweden’s demographic trends for retail market entry.

---

## 1. Project Structure

Repository root (inside `nordic-expansion-analysis/`):

```text

├── data/
│   └── geoparquet/
│       ├── befolkning_1km_2015_2024.parquet   # merged 1km population data (2015–2024)
        
├── figures/                           # all generated charts
├── src/
│   ├── anaylysispopulation.ipynb      # main analysis notebook
│   ├── female.ipynb                   # female 15–24 / 25–44 analysis
│   └── Population Pyramid.ipynb       # national age & gender structure
├── PRESENTATION.md                    # Marp slide deck
└── README.md
````

---

## 2. Python & Environment

### 2.1 Python version

This project uses **Python 3.11.9**.

You can install it for example via:

```bash
# pyenv (recommended)
pyenv install 3.11.9
pyenv local 3.11.9

# or Conda
conda create -n sweden311 python=3.11.9
conda activate sweden311
```

---

### 2.2 Required packages

Install dependencies from the terminal:

```bash
python -m pip install -U pip
python -m pip install \
  geopandas pyproj shapely fiona pandas pyarrow matplotlib scikit-learn pathlib
```

If installing from inside Jupyter, you can instead run:

```python
%pip install -U pip
%pip install geopandas pyproj shapely fiona pandas pyarrow matplotlib scikit-learn pathlib
```

Quick check:

```python
import sys
print(sys.executable)

import pandas as pd, geopandas as gpd, pyproj, shapely
print(pd.__version__, gpd.__version__, pyproj.__version__, shapely.__version__)
```

---

## 3. Data

The notebooks expect the processed merged file at:

```text
data/geoparquet/befolkning_1km_2015_2024.parquet
```

No raw SCB source files are required at runtime: all analysis uses this merged 2015–2024 GeoParquet.

---

## 4. How to Run the Notebooks

All notebooks live in `src/`.

### 4.1 `anaylysispopulation.ipynb` (main analysis)

* This file contains some **earlier raw-data processing cells** that are no longer needed.
* Please **scroll to the cell marked**:

```python
# Start Point

import sys
print(sys.executable)

import pandas as pd, geopandas as gpd, pyproj, shapely
print(pd.__version__, gpd.__version__, pyproj.__version__, shapely.__version__)

%pip install -U pip
%pip install geopandas pyproj shapely fiona pandas pyarrow matplotlib pandas scikit-learn pathlib


df_all = gpd.read_parquet(DATA_DIR / "befolkning_1km_2015_2024.parquet")

```

From this cell onwards the notebook:

* sets up `PROJECT_ROOT`, `DATA_DIR`, `FIG_DIR`
* reads `befolkning_1km_2015_2024.parquet`
* performs all aggregation (5 km grid, 20 km city buffers, growth, age structure, retail proxies)
* saves figures into `figures/`

👉 **Start execution from `# Start Point` and run all following cells.**
You may only need to adjust the path logic if your folder structure differs.

---

### 4.2 `female.ipynb`

* Uses the same merged dataset.
* Can be run **from the first cell**.
* Computes:

  * female population 15–24 and 25–44
  * aggregation within 20 km city buffers
  * growth curves for each city

Outputs are written to `figures/`.

---

### 4.3 `Population Pyramid.ipynb`

* Also uses `befolkning_1km_2015_2024.parquet`.
* Can be run **from the first cell**.
* Produces:

  * national population pyramid by 5-year age band and sex (approx.)
  * overall segment shares (0–14, 15–24, 25–44, 45–64, 65+)

Figures are saved to `figures/`.

---

## 5. Presentation

The final CEO-oriented presentation is in:

```text
PRESENTATION.md
```

It is built with **Marp**. In VS Code, install the *Marp for VS Code* extension and open `PRESENTATION.md` to preview the slides.

Note:
All visual outputs used in the Marp slide deck were converted and manually compressed into JPG format to reduce file size and improve presentation performance.

---

