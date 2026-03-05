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

The filtered 311 service request dataset downloaded from the Chicago Data Portal exceeds GitHub’s 100MB file limit, so it is stored externally in Google Drive and can be accessed here: https://drive.google.com/file/d/1rYJpNKT4kix_NAPhL--LJIDq9Ctp1vhs/view

The dataset is publicly available at: https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data

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
- Grouped Community Areas into **income quartiles (Low → High income)**
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
│       ├── acs_filtered.csv
│       ├── df_311_ca.csv
│       ├── df_311_type.csv
│       ├── Boundaries_-_Community_Areas_20260301.geojson
│       └── plots/
│           ├── box_requests_income.png
│           ├── heatmap_income_services.png
│           ├── box_requests_income.html
│           └── heatmap_income_services.html
├── README.md
└── requirements.txt
```

