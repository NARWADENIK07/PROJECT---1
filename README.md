# 🌍 Global City Environmental Clustering

**Unsupervised clustering of world cities by Air Quality and Water Pollution using K-Means, with interactive geospatial visualisation via Folium.**

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NARWADENIK07/DEMO/blob/main/Untitled1.ipynb)
![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-KMeans-orange?logo=scikit-learn)
![Folium](https://img.shields.io/badge/Folium-Map-green?logo=leaflet)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Overview

This project applies **K-Means clustering** to a dataset of ~3,963 cities across 177 countries to group them by their environmental health indicators — **Air Quality** and **Water Pollution** index scores. Cities are then **geocoded** and plotted on an interactive world map using **Folium**, with each cluster shown in a distinct colour.

The optimal number of clusters is determined using the **Silhouette Score**, making the analysis data-driven rather than arbitrary.

---

## 📂 Dataset

| Field | Details |
|---|---|
| **Source** | `cities_air_quality_water_pollution.18-10-2021.csv` |
| **Rows** | 3,963 cities |
| **Countries** | 177 |
| **Key Columns** | `City`, `Region`, `Country`, `AirQuality` (0–100), `WaterPollution` (0–100) |

> Higher `AirQuality` score = better air. Higher `WaterPollution` score = more polluted water.

---

## 🔬 Methodology

```
Raw CSV  →  Clean & Standardise  →  Silhouette Analysis  →  K-Means Clustering
    →  Geocode Cities (geopy)  →  Interactive Map (Folium)
```

### Steps

1. **Data Cleaning** — Strip whitespace and quotes from column names; drop rows with missing `AirQuality` or `WaterPollution` values.
2. **Feature Scaling** — `StandardScaler` normalises both features to zero mean and unit variance.
3. **Optimal K Selection** — Silhouette scores computed for k = 2–7; best k chosen automatically via `argmax`.
4. **K-Means Clustering** — Final model fit with `n_init=20` and `random_state=42` for reproducibility; cluster labels appended to the dataframe.
5. **Geocoding** — City + Country strings resolved to `(latitude, longitude)` using `geopy` Nominatim with a rate limiter to respect API limits.
6. **Map Visualisation** — Each city rendered as a `CircleMarker` on a Folium world map, colour-coded by cluster, with a popup showing city name and cluster ID. Map saved as `cluster_map.html`.

---

## 🗂️ Project Structure

```
DEMO/
├── Untitled1.ipynb          # Main notebook
├── cluster_map.html         # Output: interactive Folium map
└── README.md
```

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `scikit-learn` | StandardScaler, KMeans, silhouette_score |
| `geopy` | City → (lat, lon) geocoding via Nominatim |
| `folium` | Interactive Leaflet.js map rendering |
| `matplotlib` | Silhouette score plot |
| `python-pptx` | (imported, for future slide export) |

---

## ▶️ Getting Started

### Run on Google Colab (recommended)

Click the badge at the top, or open directly:

```
https://colab.research.google.com/github/NARWADENIK07/DEMO/blob/main/Untitled1.ipynb
```

### Run locally

```bash
git clone https://github.com/NARWADENIK07/DEMO.git
cd DEMO
pip install pandas numpy scikit-learn geopy folium matplotlib python-pptx
jupyter notebook Untitled1.ipynb
```

> **Note:** Place the dataset CSV in the same directory as the notebook, or update the file path in Cell 3.

---

## 📊 Results

- **Best k** selected automatically based on silhouette score across k = 2–7
- Cities grouped into clusters representing distinct environmental profiles (e.g. high pollution / low air quality vs. clean cities)
- Output: `cluster_map.html` — an interactive world map you can open in any browser, with colour-coded city markers and cluster labels

---

## 📈 Sample Cluster Profiles

| Cluster | Typical Profile | Example Cities |
|---|---|---|
| 0 (red) | Moderate air, moderate water pollution | Cordoba, Segovia, Vic |
| 1 (blue) | Poor air quality, high water pollution | Yanbu and similar industrial cities |
| 2+ | Cleaner environments or mixed profiles | Varies by region |

> Exact profiles depend on the silhouette-optimal k selected at runtime.

---

## 👤 Author

**Nikhil Santosh Narwade**
B.E. Electronics & Telecommunication — Government College of Engineering, Karad
[GitHub](https://github.com/NARWADENIK07)

---

## 📄 License

This project is open source under the [MIT License](LICENSE).
