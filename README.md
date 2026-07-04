# SEER Cancer Data Analysis
## A Comparative Statistical Analysis of Five Major Cancers
### Breast | Liver | Lung & Bronchus | Prostate | Stomach
#### SEER Data (2000–2023) | 4,198,697 Patients

---

## About This Project
This repository contains the complete data cleaning pipeline and 
descriptive statistical analysis for five major cancer types using 
the SEER (Surveillance, Epidemiology, and End Results) Research 
Database maintained by the U.S. National Cancer Institute.

The study analyzes demographic characteristics, cancer staging, 
histological subtypes, treatment patterns, survival outcomes, 
geographic distribution, and socioeconomic factors across 
4,198,697 patients diagnosed between 2000 and 2023.

---

## Key Findings
- Prostate cancer had the highest cause-specific median survival (16 months)
- Lung cancer had the highest proportion of Stage IV diagnoses (43.3%)
- Liver cancer cases more than doubled from 2000 to 2023
- Prostate cancer showed a clear dip in 2012–2015 linked to PSA screening guideline changes

---

## Repository Structure
- `/cleaning` — Individual cancer data cleaning notebooks (Python)
- `/analysis` — Descriptive statistical analysis notebooks
- `/figures` — All generated figures (PNG, 300 DPI)
- `/results` — Summary statistics Excel files
- `/report` — Full written report

---

## Data Access
The raw SEER data is NOT included in this repository as per the 
SEER Data Use Agreement. To replicate this analysis:
1. Apply for SEER access at https://seer.cancer.gov/data/access.html
2. Download SEER*Stat software
3. Extract the following cancers from "Incidence - SEER Research Data, 
   17 Registries, Nov 2025 Sub (2000-2023)"
4. Run the cleaning notebooks in `/cleaning` in order

---

## Tools Used
- Python 3.12
- pandas, numpy, matplotlib, seaborn
- Jupyter Notebook
- SEER*Stat software
- Microsoft Excel

---

## Citation
If you use this cleaning pipeline or analysis in your work, please cite:

Kumar, S. (2026). SEER Cancer Data Cleaning and Analysis Pipeline 
SEER-Cancer-Analysis. https://github.com/sumitkumar739382-dotcom/SEER-Cancer-Analysis

Data source:
Surveillance, Epidemiology, and End Results (SEER) Program 
(www.seer.cancer.gov) SEER*Stat Database: Incidence - SEER Research Data, 
17 Registries, Nov 2025 Sub (2000-2023), National Cancer Institute, 
DCCPS, Surveillance Research Program, released April 2026.

---

## Author
**Sumit Kumar**  
Department of Statistics, Banaras Hindu University  
Supervised by: Prof. Sanjay Kumar Singh
