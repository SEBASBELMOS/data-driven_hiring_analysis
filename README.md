# Data-Driven Hiring Analytics

## Project Overview

This project demonstrates end-to-end data engineering capabilities through a realistic recruitment analytics scenario. It showcases the complete data pipeline: from raw data ingestion through ETL processes, data quality assessment, transformation, and visualisation—mirroring the workflows encountered in professional data engineering environments.

The analysis examines 50,000 candidate records to derive actionable hiring insights, including candidate performance metrics, recruitment trends across regions and technologies, and identification of hiring patterns that inform strategic talent acquisition decisions.

---

## Skills Demonstrated

This project showcases the following competencies valued in data engineering roles:

| Skill Category | Technologies & Techniques |
|----------------|---------------------------|
| **Data Pipeline Engineering** | ETL workflows, data migration, SQLAlchemy, PostgreSQL |
| **Data Analysis** | Exploratory Data Analysis (EDA), statistical analysis, Pandas |
| **Data Visualisation** | Matplotlib, Seaborn, Power BI |
| **Environment Management** | Poetry dependency management, virtual environments |
| **Version Control** | Git, GitHub |
| **Documentation** | Technical documentation, portfolio presentation |

---

## Dataset Description

The dataset comprises 50,000 candidate records with the following attributes:

| Column | Data Type | Description |
|--------|-----------|-------------|
| First Name | String | Candidate's first name |
| Last Name | String | Candidate's surname |
| Email | String | Contact email address |
| Application Date | Date | Date of application submission |
| Country | String | Candidate's country of residence |
| YOE (Years of Experience) | Integer | Professional experience in years |
| Seniority | String | Position level (Intern, Trainee, Junior, Mid-Level, Senior, Lead, Architect) |
| Technology | String | Technical domain/role applied for |
| Code Challenge Score | Integer | Assessment score (0-10) |
| Technical Interview Score | Integer | Interview performance (0-10) |

**Hiring Criteria**: A candidate is classified as **HIRED** when both the Code Challenge Score and Technical Interview Score are greater than or equal to 7.

---

## Project Architecture

```
talent-insight/
├── assets/                     # Visual resources and documentation
│   ├── poetry_installation.png
│   ├── poetry_linux.png
│   ├── poetry_linux_installed.png
│   ├── pbi.png
│   ├── postgres_pbi.png
│   ├── postrgres_access_pbi.png
│   └── tables.png
├── data/
│   └── candidates.csv          # Raw candidate data (50,000 records)
├── functions/
│   └── db_connection/
│       ├── __init__.py
│       └── connection.py       # SQLAlchemy database connection module
├── notebooks/
│   ├── 01_raw-data.ipynb       # Data ingestion pipeline
│   ├── 02_EDA-candidates.ipynb # Exploratory Data Analysis
│   └── 03_data-load.ipynb      # Data transformation and loading
├── env/
│   └── .env                    # Environment variables (database credentials)
├── pdf/
│   └── Workshop-001 Data engineer.pdf
├── pyproject.toml              # Poetry dependency configuration
└── README.md                   # This file
```

---

## Technical Implementation

### Phase 1: Data Ingestion

The initial phase establishes the data infrastructure:

1. **Environment Configuration**: Poetry manages Python dependencies, ensuring reproducible environments across systems
2. **Database Setup**: PostgreSQL provides the relational database infrastructure
3. **Data Loading**: Raw CSV data (50,000 records) is migrated into the PostgreSQL database using SQLAlchemy
4. **Connection Management**: A modular connection.py function handles secure database connectivity through environment variables

```python
# Key implementation details
- SQLAlchemy engine creation for database connectivity
- Environment variable management via python-dotenv
- Pandas for data manipulation and transfer
```

### Phase 2: Exploratory Data Analysis

Comprehensive EDA reveals dataset characteristics and identifies quality issues:

- **Data Quality Assessment**: Completeness checks, duplicate detection, distribution analysis
- **Statistical Summary**: Descriptive statistics for numerical variables
- **Performance Metrics**: Score distributions, pass rates, correlation analysis
- **Temporal Analysis**: Application trends by year and month
- **Categorical Analysis**: Seniority levels, technologies, geographic distribution

**Key Findings from EDA**:
- The hiring process is highly selective, with only **13% of applicants** meeting the criteria
- 165 duplicate email addresses detected, indicating potential re-applicants
- Application data spans January 2018 to July 2022 (2022 data incomplete)
- Significant data quality issues identified (e.g., interns with 15+ years experience)

### Phase 3: Data Transformation

The final phase prepares clean, analysis-ready datasets:

1. **Column Standardisation**: snake_case naming convention for consistency
2. **Technology Categorisation**: Grouped 24 individual technologies into 10 broader categories
3. **Hiring Classification**: Boolean flag created based on scoring criteria
4. **Data Export**: Cleaned dataset loaded into `candidates_hired` table

---

## Business Insights & Results

### Hiring Performance Overview

| Metric | Value |
|--------|-------|
| Total Applications | 50,000 |
| Candidates Hired | 6,698 |
| Hiring Rate | 13.4% |
| Code Challenge Pass Rate (≥7) | 36.5% |
| Technical Interview Pass Rate (≥7) | 36.5% |

### Technology Trends

**Highest Hiring Volumes**:
- Game Development
- DevOps
- Development - CMS (Backend/Frontend)
- Systems Administration and Management

These areas demonstrate strong demand for technical talent, suggesting strategic focus areas for recruitment campaigns.

### Geographic Distribution

The organisation attracted talent from **244 countries**, demonstrating global reach. Key observations:

- Recruitment is geographically diverse
- Selection rates vary significantly by region
- Latin American markets (Brazil, Colombia, Ecuador) showed strong hiring volumes in 2019-2020

### Temporal Trends

Hiring patterns reveal significant fluctuations:
- **2018-2021**: Consistent application volumes (~11,000 per year)
- **2020 Peak**: Brazil and Colombia experienced highest hiring volumes
- **2022 Decline**: All major markets showed reduced hiring activity
- **Data Gap**: August-December 2022 data incomplete

### Data Quality Issues Identified

The analysis uncovered several data quality concerns requiring attention:

| Issue | Impact | Recommendation |
|-------|--------|----------------|
| Interns with 15+ YOE | Data inconsistency | Review seniority classification criteria |
| 165 duplicate emails | Potential re-applicants | Implement applicant tracking system |
| 2022 H2 data missing | Incomplete analysis | Ensure complete data capture |
| Uniform score distribution | Limited differentiation | Review assessment scoring methodology |

---

## Visualisation Dashboard

Interactive Power BI dashboards provide real-time recruitment analytics:

**Dashboard Features**:
- Hiring trends over time
- Geographic distribution maps
- Technology category performance
- Seniority level analysis
- Score distribution visualisations

**Power BI Connection**:

To connect Power BI to the processed data:

1. Open Power BI Desktop → Get Data → PostgreSQL Database
2. Enter server details (localhost) and database name
3. Authenticate with PostgreSQL credentials
4. Select the `candidates_hired` table

<img src="assets/postgres_pbi.png" width="400"/>

[View Interactive Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYzVmMGFjYTktNzE2Ni00MWNhLWE2ODktOWMwZTY2OTdiMGU5IiwidCI6IjY5M2NiZWEwLTRlZjktNDI1NC04OTc3LTc2ZTA1Y2I1ZjU1NiIsImMiOjR9)

---

## Getting Started

### Prerequisites

- Python 3.13+
- PostgreSQL
- Power BI Desktop (optional, for visualisations)

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/SEBASBELMOS/data-driven_hiring_analysis.git
   cd data-driven_hiring_analysis
   ```

2. **Install Poetry** (if not already installed):
   ```powershell
   # Windows
   (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
   ```
   
   ```bash
   # Linux/macOS
   curl -sSL https://install.python-poetry.org | python3 -
   ```

3. **Configure Environment**:
   ```bash
   poetry install
   poetry shell
   poetry run python -m ipykernel install --user --name talent-insight --display-name "Python (talent-insight)"
   ```

4. **Set Up PostgreSQL**:
   ```bash
   # Create database
   psql -U postgres
   CREATE DATABASE recruitment_db;
   ```

5. **Configure Environment Variables**:
   
   Create `env/.env` file:
   ```env
   PG_HOST=localhost
   PG_PORT=5432
   PG_USER=your_username
   PG_PASSWORD=your_password
   PG_DRIVER=postgresql+psycopg2
   PG_DATABASE=recruitment_db
   ```

### Running the Notebooks

Execute notebooks in the following sequence:

1. **01_raw-data.ipynb**: Loads raw CSV data into PostgreSQL
2. **02_EDA-candidates.ipynb**: Performs exploratory data analysis
3. **03_data-load.ipynb**: Transforms and loads cleaned data

---

## Technologies Used

| Category | Tool | Purpose |
|----------|------|---------|
| Programming Language | Python 3.13 | Core development |
| Data Manipulation | Pandas | Data analysis and transformation |
| Database | PostgreSQL | Relational data storage |
| ORM | SQLAlchemy | Database connectivity |
| Visualisation | Matplotlib, Seaborn | Static charts and graphs |
| Business Intelligence | Power BI | Interactive dashboards |
| Environment Management | Poetry | Dependency management |
| IDE | VS Code | Development environment |

---


## Author

**Sebastian Belalcazar Mosquera**

<p align="left">
  <a href="https://www.linkedin.com/in/sebasbelmos/">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
  <a href="https://github.com/SEBASBELMOS">
    <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
  <a href="https://www.youtube.com/channel/UCeYaQhjA-N6YVd6RNTdhBeA">
    <img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="YouTube">
  </a>
</p>

Data Engineer passionate about transforming raw data into actionable business insights. This project demonstrates practical experience with modern data engineering tools and methodologies.

---

## License

This project is available for educational and portfolio purposes.
