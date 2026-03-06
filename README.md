[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/YlfKWlZ5)

# Service request and Delivery: 
## Evidence from 311 system in Chicago

**PPHA 30538 – Data Analytics and Visualization for Public Policy**  
Final Project – March 2026  
María Manjarrez & Julio Pacher  

---

## Project Overview

Chicago exhibits substantial variation in median household income across neighborhoods. At the same time, municipal service delivery — such as pothole repair, rodent complaints, and abandoned vehicle removal — may also vary across space.

Using 311 Service Request data from the City of Chicago and neighborhood-level income data from the American Community Survey (ACS), this project examines whether:

- Service demand differs systematically across income groups  
- Service types vary by neighborhood income level  
- Response times are associated with median household income  

The analysis focuses on Chicago Community Areas and evaluates both service demand (volume) and service efficiency (completion time).

---

## Research Question

> Are neighborhood income differences in Chicago associated with disparities in 311 service demand and response times across Community Areas?

---

## Data Sources

### 1. Chicago 311 Service Requests (CHI311)
Source: City of Chicago Data Portal  

- Universe of non-emergency municipal service requests  
- Includes request type, location, submission date, and completion date  
- Used to measure:
  - Service demand (requests per 1,000 residents)
  - Service efficiency (response time in days)

The filtered 311 Service Requests dataset used in this project exceeds 100MB file size limit and is therefore not included in the repository.

When running the preprocessing script, the dataset will be automatically downloaded from Google Drive if it is not already present in the repository.

The file will be downloaded to:

```bash
data/raw-data/311_request.csv
```

The filtered (and used) dataset is hosted here, a public Google drive:

https://drive.google.com/file/d/1rYJpNKT4kix_NAPhL--LJIDq9Ctp1vhs/view

No manual renaming or modification of the file is required for the code to run.

The original (unfiltered) dataset is publicly available from the City of Chicago Data Portal:

https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data

The repository’s .gitignore file is configured to ignore large raw datasets.

### 1.1 Large-file Reproducibility Note

- `data/raw-data/311_request.csv` is intentionally not tracked in GitHub due to file size limits.
- `df_311_type.csv` can also be sourced from Google Drive when absent locally.
- The code supports Drive-based loading with either:
  - `DF311_TYPE_DRIVE_URL`
  - `DF311_TYPE_DRIVE_FILE_ID`

Example:

```bash
export DF311_TYPE_DRIVE_FILE_ID=1rYJpNKT4kix_NAPhL--LJIDq9Ctp1vhs
python code/plots_static.py
streamlit run code/app.py
```

### 2. American Community Survey (ACS) 5-Year Estimates (2019–2023)
Source: U.S. Census Bureau  

- Median household income at the Community Area level  
- Used to classify neighborhoods into income quartiles  

---

## Sample Construction & Data Processing

- Filtered 311 service requests from **January 1, 2023 – December 31, 2024**
- Selected key variables:
  - Creation date  
  - Completion date  
  - Service type  
  - Status  
  - Community Area  

- Constructed:
  - **Response Time (days)** = Completion Date − Creation Date  
  - Total request volume per Community Area  
  - Requests per 1,000 residents  

- Merged 311 data with ACS median household income  
- Grouped Community Areas into **income quartiles (Low to High income)**
- Merged with Community Areas boundaries for the map in the dashboard
---

## Repository Structure

```text
streamlit-dashboard/
├── .streamlit/
│   └── config.toml                 # Streamlit configuration
├── code/
│   ├── app.py                      # Main Streamlit dashboard
│   ├── preprocessing.py            # Data cleaning and aggregation
│   └── plots_static.py             # Static plots (heatmap, boxplot)
├── data/
│   ├── raw-data/
│   │   └── community_areas.csv      # Community area metadata
│   └── derived-data/
│       ├── acs_filtered.csv         # Filtered community area metadata
│       ├── df_311_ca.csv            # Filtered 311 data 
│       ├── df_311_type.csv          # Filtered 311 data by type of service request
│       ├── Boundaries_-_Community_Areas_20260301.geojson
│       └── plots/
│           ├── box_requests_income.png
│           ├── heatmap_income_services.png
│           ├── box_requests_income.html
│           └── heatmap_income_services.html
├── Final_Writeup.pdf
├── Final_Writeup.qmd
├── README.md
├── Service request and delivery evidence from 311 Request in Chicago.pdf #final slides generated in canva
└── requirements.txt
```
