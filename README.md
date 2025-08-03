# 🦬 Bison Impact on Tallgrass Prairie Biodiversity

This project investigates the long-term ecological impact of **bison reintroduction** on grassland plant diversity in the **Konza Prairie Biological Station (KPBS)**, Kansas, USA. It replicates and extends the findings of *Ratajczak et al. (2022)* using expanded spatial data and modern data analysis techniques, including machine learning.

## 📌 Background

Tallgrass prairies are among the most threatened ecosystems in North America. The extirpation of native megafauna like bison has altered ecological processes, reducing biodiversity and resilience. This project explores how reintroducing **bison**, compared to **cattle grazing** or no grazing, affects plant diversity, ecosystem stability, and drought resilience over nearly three decades.

## 🧪 Objectives

- Quantify plant diversity using **Richness**, **Shannon**, and **Simpson** indices.
- Integrate vegetation, climate, and fire datasets into a unified analysis.
- Use **Random Forest models** to identify key environmental drivers of diversity.
- Evaluate the **resilience** of species diversity to extreme drought events (e.g., 2011–2012).

## 🗂️ Data Sources

- **Vegetation Data:**
  - `PVC021.csv` (bison-grazed plots)
  - `PBG011.csv` (cattle-grazed plots)
- **Environmental Data:**
  - `AWE012.csv` (daily weather records)
  - `Watersheds.csv` (fire intervals, seasons, watershed IDs)

## 🧠 Method Overview

### 🔹 Script 1: `New_vegetation.Rmd`
- Loads and merges bison and cattle vegetation data.
- Constructs unique `plot_ID`s from watershed, transect, soil, and date.
- Calculates:
  - **Species richness** (`specnumber()`)
  - **Simpson Index**
  - **Shannon Index**
- Outputs: Species matrix and diversity index table.

### 🔹 Script 2: `New_Environmental.Rmd`
- Processes meteorological data (TAVE, DHUMID, DSRAD, DPPT).
- Aggregates seasonal climate averages (April–October).
- Merges climate, fire, and vegetation data into a single analysis-ready file.

## 📈 Preliminary Results

- **Bison grazing** increased native plant richness by **103%** (plot scale) over 29 years.
- Biodiversity gains under bison were **resilient** to extreme drought (2011–2012).
- **Random Forest analysis** shows `RecYear`, `Watershed`, and `FireInterval_yr` as key predictors of Simpson diversity.

## 📚 Reference

Ratajczak et al. (2022). *Reintroducing bison results in long-running and resilient increases in grassland diversity*. Proceedings of the National Academy of Sciences. [https://doi.org/10.1073/pnas.2210433119](https://doi.org/10.1073/pnas.2210433119)
