# Workshop-001: Data Engineer 💻
Data-Driven Hiring Analysis (Recruitment Data)

## Overview 

This project is a real exercise modeled after a job interview scenario for a Data Engineer role. The objective is to:
- **Migrate data** from a CSV file into a relational database.
- **Perform data cleaning and transformation** based on specific criteria.
- **Visualise metrics** using Python libraries to generate insightful charts.

## Dataset Information

The CSV contains 50k rows of candidate data (e.g., first name, last name, email, country, application date, years of experience (YOE), seniority, technology, Code Challenge Score, and Technical Interview Score). A candidate is considered **HIRED** if both the Code Challenge Score and Technical Interview Score are greater than or equal to 7.

- First Name ➜ Object
- Last Name ➜ Object
- Email ➜ Object
- Country ➜ Object
- Application Date ➜ Object
- YOE (years of experience) ➜ Integer
- Seniority ➜ Object
- Technology ➜ Object
- Code Challenge Score ➜ Integer
- Technical Interview Score ➜ Integer

## Project Structure

| Folder/File            | Description |
|------------------------|------------|
| **assets**             | Static resources (images, documentation, etc.) |
| **data/**             | Dataset used in the project |
| ├── candidates.csv    | Raw dataset |
| **functions/**        | Utility functions |
| ├── db_connection/    | Database connection module |
| │ ├── db_connection.py | Connects to PostgreSQL using SQLAlchemy |
| **env/**              | Environment variables (ignored in .gitignore) |
| ├── .env             | Stores database credentials |
| **notebooks/**        | Jupyter Notebooks with analysis |
├── 01_raw-data.ipynb    | Raw data ingestion |
├── 02_EDA-candidates.ipynb  | Exploratory Data Analysis (EDA) |
├── 03_data-load.ipynb   | Data cleansing and transformation |
| **pdf/**              | Documentation and workshop PDFs |
| ├── Workshop-001 Data engineer.pdf     | PDF with instructions for the workshop |
| **pyproject.toml**    | Poetry dependency management file |
| **README.md**         | This file |

## Tools and Libraries

- **Programming Language:** Python 3.13.1 -> [Download here](https://www.python.org/downloads/)
- **Data Handling:** pandas -> [Documentation here](https://pandas.pydata.org/)
- **Database:** PostgreSQL -> [Download here](https://www.postgresql.org/download/)
- **Database Interaction:** SQLAlchemy -> [Documentation here](https://docs.sqlalchemy.org/)
- **Visualisation:** Power BI Desktop -> [Download here](https://www.microsoft.com/es-es/power-platform/products/power-bi/desktop)
- **Environment:** Jupyter Notebook -> [VSCode tool used](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)

All the libraries are included in the Poetry project config file (_pyproject.toml_).

## Installation and Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/SEBASBELMOS/workshop-001.git
   cd workshop-001
   ````

2. **Installing the dependencies with _Poetry_**
    - Windows: 
        - In Powershell, execute this command: 
            ```powershell
            (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
            ```
            <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/poetry_installation.png" width="600"/>
        - Press Win + R, type _sysdm.cpl_, and press **Enter**. 
        - Go to the _Advanced_ tab, select _environment variable_.
        - Under System variables, select Path → Click Edit.
        - Click _Edit_ and set the path provided during the installation in **PATH** so that the `poetry` command works. ("C:\Users\username\AppData\Roaming\Python\Scripts")
        - Restart Powershell and execute _poetry --version_.

        
    - Linux
        - In a terminal, execute this command:
            ```bash
            curl -sSL https://install.python-poetry.org | python3 -
            ```
            <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/poetry_linux.png" width="600"/>
        -  Now, execute:
            ```bash
            export PATH = "/home/user/.locar/bin:$PATH"
            ```
        -Finally, restart the terminal and execute _poetry --version_.


        <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/poetry_linux_installed.png" width="400"/>

3. **Poetry Shell**
    - Enter the Poetry shell with _poetry shell_.
    - Then, execute _poetry init_, it will create a file called _pyproject.toml_
    - To add all the dependencies, execute this: 
        ```bash
        poetry add pandas matplotlib psycopg2-binary sqlalchemy python-dotenv seaborn ipykernel dotenv
        ```
    - Install the dependencies with: 
        ```bash
        poetry install
        ```
        In case of error with the .lock file, just execute _poetry lock_ to fix it.
    - Create the kernel with this command (You must choose this kernel when running the notebooks):
        ```bash
        poetry run python -m ipykernel install --user --name workshop-001 --display-name "Python (workshop-001)"
        ```

4. **PostgreSQL Database**
    - Install PostgreSQL with this [link here](https://www.postgresql.org/download/)
    - Open a terminal and execute this command, If the **postgres** user has a password, you will be prompted to enter it: 
        ```bash
        psql -U postgres
        ```
    - Create a new database with this command:
        ```bash 
        CREATE DATABASE database_name;
        ```
    - This is the information you need to add to the _.env_ file in the next step.

5. **Enviromental variables**
    >Realise this in VS Code.

    To establish a connection with the database, we use a module called _connection.py_. This Python script retrieves a file containing our environment variables. Here’s how to create it:
    1. Inside the cloned repository, create a new directory named *env/*.
    2. Within that directory, create a file called *.env*.
    3. In the *.env file*, define the following six environment variables (without double quotes around values):
        ```python
        PG_HOST = #host address, e.g. localhost or 127.0.0.1
        PG_PORT = #PostgreSQL port, e.g. 5432

        PG_USER = #your PostgreSQL user
        PG_PASSWORD = #your user password
        
        PG_DRIVER = postgresql+psycopg2
        PG_DATABASE = #your database name, e.g. postgres
        ```

---

## Workflow

### Notebooks
    
    You must run the three notebooks in the following order to ensure proper execution.

1. **01_raw-data.ipynb**:
    
    This notebook sets up our data pipeline by configuring the environment, importing essential libraries and create a SQLAlchemy engine, then loading raw candidate data from the CSV file (_candidates.csv_) into a Pandas DataFrame, transferring this data into a PostgreSQL database, and verifying the transfer with a simple query.

2. **02_EDA-candidates.ipynb**:

    This notebook focuses on conducting **Exploratory Data Analysis (EDA)** on the candidates' dataset. EDA is a fundamental step in the data analysis process, as it allows us to understand the structure and characteristics of the data. By examining the dataset, we can identify patterns, relationships, and key insights that inform further analysis and decision-making.

    In this notebook, we will explore the dataset using a range of statistical and visual techniques. We will assess the distribution of variables and investigate correlations between them. Through this process, we aim to develop a thorough understanding of the dataset and extract valuable insights.

3. **03_data-load.ipynb**:

    This notebook carries out various data analysis tasks, including data cleansing and transformation. For instance, several columns are transformed using Pandas, facilitated by a module named **connection.py**, which establishes a connection to a **PostgreSQL database** where the raw data is stored. 
    
    Subsequently, the cleaned data is loaded into a new table named **"candidates_hired"**.

---

## Key Insights & Findings  
- The hiring process is highly selective, with only **13% of applicants meeting the criteria**.  
- **Game Development**, **DevOps**, and **CMS-related roles** had the highest number of hires, reflecting industry demand.  
- Recruitment is geographically diverse, spanning **244 countries**, though some regions have notably higher selection rates.  
- **Interns reported the highest average years of experience (15.41 years)**, indicating a possible **data inconsistency**.  

## Hires by Country Over the Years (*USA, Brazil, Colombia, Ecuador*)  
- **Hiring trends have fluctuated significantly over the years** for these four countries.  
- **Brazil and Colombia experienced the highest number of hires in 2019 and 2020**, followed by a **gradual decline in subsequent years**.  
- **Ecuador also peaked in 2020**, aligning with Colombia, before following a similar downward trend.  
- **The United States exhibited a more stable pattern**, though it also experienced **some fluctuations**, with a dip in **2020**, a **partial recovery in 2021**, and then a decline in 2022.  
- By **2022, all four countries recorded their lowest number of hires**, which could suggest **a shift in recruitment strategies, decreased hiring demand, or incomplete data for that year**.  

This pattern indicates a **declining recruitment rate in recent years**, likely influenced by **economic factors, evolving industry needs, or internal policy changes**.  

Further investigation is necessary to determine if this decline is **temporary or indicative of a long-term shift**.  



## Areas for Improvement  

✅ **Data Quality & Consistency**  
- Investigate why **Interns have the highest YoE** and refine seniority classifications.  
- Ensure **application data from August to December 2022** is fully recorded.  

✅ **Scoring & Hiring Criteria**  
- Reassess the **uniformity of test scores**, ensuring **clearer candidate differentiation**.  
- Consider **adjusting the 7+ score requirement** to increase the **low selection rate (11.8%)**.  

✅ **Data Collection & Tracking**  
- Improve **tracking of reapplicants**, as **165 duplicated emails** were identified.  
- Ensure **all application records are captured** to prevent gaps in data collection.  

---

## Power BI Connection (Not necessary)
1. Open Power BI Desktop and create a new dashboard. 
2. Select the _Get data_ option, then choose the "_PostgreSQL Database_" option.

    <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/pbi.png" width="400"/>

3. Insert the _PostgreSQL Server_ and _Database Name_.
    
    <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/postgres_pbi.png" width="400"/>

4. Fill the following fields with your Postgres credentials.
    
    <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/postrgres_access_pbi.png" width="400"/>    

5. After establishing the connection, these tables will be displayed.You need to select the "_candidates_hired_" table, and then you can start creating your own dashboards.
    
    <img src="https://github.com/SEBASBELMOS/workshop-001/blob/main/assets/tables.png" width="200"/>

- Open my Power BI Visualisation [here](https://app.powerbi.com/view?r=eyJrIjoiYzVmMGFjYTktNzE2Ni00MWNhLWE2ODktOWMwZTY2OTdiMGU5IiwidCI6IjY5M2NiZWEwLTRlZjktNDI1NC04OTc3LTc2ZTA1Y2I1ZjU1NiIsImMiOjR9)

---

## **Author**  
Created by **Sebastian Belalcazar Mosquera**. Connect with me on [LinkedIn](https://www.linkedin.com/in/sebasbelmos/) for feedback, suggestions, or collaboration opportunities!

---
