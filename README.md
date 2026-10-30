# Growth of Piura, Peru, 2020–2025

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/appiahkubis14/piura-urban-growth-pygeovision/blob/main/piura_growth_pygeovision.ipynb)

Urban growth of Piura, Peru (2020–2025) from building footprints and rasterized population data, built with
[pygeovision](https://doi.org/10.5281/zenodo.22258220) and the Global Human Settlement Layer (GHSL).
**No Google Earth Engine account is needed**: every dataset is open and is downloaded by the notebook itself.

World Population Review calls Piura the fastest growing city in Peru. The notebook tests that claim and answers
four questions:

1. Do the datasets show the same growth rate as the web source?
2. What is the annual growth rate of building footprint extent?
3. Where is the city growing in extent?
4. Where do we observe growth in building volume?

Course: 856.114 GeoHumanitarian Action, Homework Assignment 2 (University of Salzburg, Copernicus Master in
Digital Earth).

## Run it in Google Colab

1. Click the **Open in Colab** badge above.
2. Choose **Runtime → Run all**.
3. The first code cell installs pygeovision and the other packages. If Colab shows **Restart session**,
   click it, then choose **Runtime → Run all** again.
4. The run takes a few minutes the first time: it downloads the building footprints, a Sentinel-2 image and six
   GHSL tiles.
5. The last cell downloads **`piura_figures.zip`** with every figure (PNG, 200 dpi), the interactive map
   (`interactive_map.html`) and every number used in the report (`report_values.txt`).
   Colab deletes session files when it closes, so keep this zip.

No sign-in or API key is needed at any step.

## Run it locally

```bash
git clone https://github.com/appiahkubis14/piura-urban-growth-pygeovision.git
cd piura-urban-growth-pygeovision
pip install "pygeovision[geo]==2.2.0" geopandas rasterio shapely pyproj requests folium matplotlib jupyterlab marimo

jupyter lab piura_growth_pygeovision.ipynb    # Jupyter
marimo edit piura_growth_pygeovision.py       # or marimo / molab
```

## Data

| Data | Source | Read with |
|---|---|---|
| Building footprints (Microsoft, Google Open Buildings v3, OpenStreetMap) | published datasets | pygeovision `building_footprints` |
| Built-up change 2020–2023 (Esri / Impact Observatory 10 m land cover) | Microsoft Planetary Computer | pygeovision `urban_expansion` |
| Sentinel-2 L2A true colour | Microsoft Planetary Computer | pygeovision grid reader |
| Population, built-up surface, built-up volume, 2020 and 2025 (GHSL R2023A, 100 m) | JRC open-data server | rasterio |

The study area is a 2.76 km² box on the north-eastern edge of Piura (west −80.625, south −5.180, east −80.610,
north −5.165); population is also summed for a box around the whole city (−80.70, −5.26, −80.55, −5.13).

## Main results

| | AOI | Whole city |
|---|---|---|
| Population growth (GHS_POP, 2020–2025) | 2.94 % per year | 1.16 % per year |
| Footprint extent growth (GHS_BUILT_S, 2020–2025) | 1.70 % per year | 0.13 % per year |
| Building volume growth (GHS_BUILT_V, 2020–2025) | 1.97 % per year | 0.08 % per year |

The website's 2.75 % per year is matched at the urban fringe but not city-wide. New built-up surface and volume
concentrate in a few blocks in the south-west of the study area and along the Río Piura on its western and
northern edges; growth is mostly horizontal, with a slight rise in mean building height.

## Files

| File | What it is |
|---|---|
| `piura_growth_pygeovision.ipynb` | The notebook for Google Colab, Jupyter or VS Code |
| `piura_growth_pygeovision.py` | The same notebook in marimo format (molab) |
| `figures/` | Created by the notebook: all figures, the interactive map and `report_values.txt` |

## Troubleshooting

- **`<Figure size … with N Axes>` instead of a plot:** the program showing the notebook only displays the text
  version of outputs. Use Colab, JupyterLab or VS Code, or open the PNGs in `figures/`.
- **A footprint source fails:** the status table under the pygeovision cell shows `success = False` and the
  reason (for example a busy OpenStreetMap server); run the cell again later. The rest of the notebook still runs.
- **`No module named 'exceptions'` from `docx.py`:** an old package called `docx` hides `python-docx`. The notebook
  does not need it; to clean it up run `pip uninstall docx` and `pip install python-docx`.

## Citation

If you use this work, please cite pygeovision:

> Appiah Kubi, S. (2026). *pygeovision: A Unified Open-Source Python Platform for Satellite Earth Observation AI*
> (Version 2.1.9) [Software]. Zenodo. https://doi.org/10.5281/zenodo.22258220

Data: Microsoft Global ML Building Footprints; Google Open Buildings v3; © OpenStreetMap contributors (ODbL);
GHSL R2023A, European Commission, Joint Research Centre; Esri / Impact Observatory 10 m Annual Land Use Land Cover
(CC BY 4.0); Copernicus Sentinel-2 data via the Microsoft Planetary Computer.