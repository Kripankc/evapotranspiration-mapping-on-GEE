# evapotranspiration-mapping-on-GEE

Day 1 evapotranspiration mapping using Google Earth Engine (GEE) and Python.

Badges
- [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE) <!-- replace when you add a license -->
- [![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org)

Overview
--------
This repository contains code and notebooks to compute and map evapotranspiration (ET) using Google Earth Engine (GEE) and Python. The project aims to provide reproducible scripts for deriving ET maps from remote sensing data and exporting results as GeoTIFFs and web-ready visualizations.

Features
- Scripts to compute evapotranspiration on GEE (Python + Earth Engine API)
- Example notebook(s) demonstrating workflow and visualization
- Export routines to GeoTIFF / assets
- Minimal starter configuration for running locally

Table of contents
-----------------
- [Requirements](#requirements)
- [Quick start](#quick-start)
- [Usage examples](#usage-examples)
- [Repository structure](#repository-structure)
- [Recommended workflow (GEE auth)](#recommended-workflow-gee-auth)
- [Outputs](#outputs)
- [Citations & algorithm](#citations--algorithm)
- [Contributing](#contributing)
- [License](#license)
- [Improvements & roadmap](#improvements--roadmap)

Requirements
------------
- Python 3.8+
- Google Earth Engine account (https://earthengine.google.com/) with access to the datasets you intend to use
- Packages (example):
  - earthengine-api
  - geemap (recommended for interactive mapping)
  - numpy, pandas
  - rasterio (for reading/writing GeoTIFFs)
  - geopandas (optional, for vector processing)
  - matplotlib / folium (visualization)

Install example (recommended)
-----------------------------
1. Clone the repo:
   git clone https://github.com/Kripankc/evapotranspiration-mapping-on-GEE.git
2. Create and activate a virtual environment:
   python -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   .venv\Scripts\activate     # Windows
3. Install dependencies:
   pip install -r requirements.txt
   (or: pip install earthengine-api geemap numpy pandas rasterio geopandas matplotlib)

Quick start
-----------
1. Authenticate Earth Engine:
   - From the terminal: `earthengine authenticate`
   - Or in a notebook: use geemap/ee.Authenticate() followed by ee.Initialize()
2. Run an example notebook:
   - Open `notebooks/example_et_workflow.ipynb` and run cells to compute and visualize ET.
3. Run script (if provided):
   - python scripts/run_et.py --start 2025-01-01 --end 2025-01-31 --roi path/to/roi.geojson

Usage examples
--------------
Example: compute monthly ET for a region (pseudo)
```python
from et_pipeline import compute_et, export_tiff
import ee
ee.Initialize()

roi = ee.FeatureCollection('users/you/roi')
et_image = compute_et(start='2025-01-01', end='2025-01-31', region=roi)
export_tiff(et_image, 'monthly_et_202501.tif', region=roi)
```

Repository structure
--------------------
(Example — adapt to your actual layout)
- README.md
- requirements.txt
- notebooks/
  - example_et_workflow.ipynb
- scripts/
  - run_et.py
  - utils.py
- data/
  - sample_roi.geojson
- outputs/
  - (exported GeoTIFFs and maps)
- LICENSE
- CONTRIBUTING.md

Recommended workflow (GEE auth)
------------------------------
- For local runs: use `earthengine authenticate` in your dev environment and `ee.Initialize()`.
- For CI or automated runs: use a Google Cloud service account with a key stored in GitHub Secrets. DO NOT commit service account keys to the repo. Use environment variables to load credentials (document the process in this README).

Outputs
-------
- GeoTIFF exports (per-timestep or composites)
- Visualizations: static PNGs or interactive maps (folium/geemap)
- (Optional) Earth Engine assets if you prefer to export to your GEE account

Citations & algorithm
---------------------
Document the ET algorithm(s) used in this project (e.g., FAO Penman-Monteith, SEBAL, METRIC, SSEBop, or others). Provide references and, if applicable, parameter choices and validation sources.

Contributing
------------
Contributions welcome! Please open an issue for discussion before submitting major changes. A minimal CONTRIBUTING.md with coding style, branch strategy, and PR template is recommended.


Improvements & roadmap
----------------------
See the "Improvements & roadmap" section below for recommended enhancements to make this repository more usable and reproducible.

Contact
-------
Created by Kripankc. For questions open an issue or contact via GitHub.
