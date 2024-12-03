# MIST4610_COVID_Database
## Team Name:
The RockLobsters
## Team Members:
1. Brooks Ruehle | (@Brooks-Ruehle)
2. Will Jenkins | (@willjenkins-Glitch)
3. Charlie Davis | (@cbdcharlie)
4. Abhi Kode | (@)

# Table of Contents
- [Introduction](#introduction)
  - [Background](#background)
  - [Project Objectives](#project-objectives)
  - [Key Outcomes](#key-outcomes)
  - [Project Scope](#project-scope)
  - [Ensuring Data Integrity](#ensuring-data-integrity)
- [1. The Data Model](#1-the-data-model)
  - [1.1 Entities](#11-entities)
  - [1.2 Attributes](#12-attributes)
  - [1.3 Relationships](#13-relationships)
  - [1.4 Identifiers](#14-identifiers)
- [2. Data Dictionary](#2-data-dictionary)
  - [2.1 Country and Demographics](#21-country-and-demographics)
  - [2.2 Healthcare System](#22-healthcare-system)
  - [2.3 Patients and Cases](#23-patients-and-cases)
  - [2.4 Vaccination and Variants](#24-vaccination-and-variants)
- [3. SQL Queries](#3-sql-queries)
  - [Query 1: Vaccination Progress](#query-1-vaccination-progress)
- [4. Tableau Visualizations](#4-tableau-visualizations)
  - [Visualization 1](#visualization-1)
  - [Visualization 2](#visualization-2)
  - [Visualization 3](#visualization-3)
- [5. Tableau Dashboard](#5-tableau-dashboard)
- [6. Access Section (Optional)](#6-access-section-optional)
- [7. Conclusion](#7-conclusion)

# Introduction

## Background
In 2020, at the start of the COVID-19 pandemic, Johns Hopkins University released the Coronavirus Resource Center (CRC), which "collects and analyzes the best data available on cases, deaths, tests, hospitalizations, and vaccines to help the public, policymakers, and healthcare professionals worldwide respond to the pandemic." Recognized by TIME Magazine as one of the top inventions of 2020 and "2020's go-to data source," the CRC highlighted the critical role of data-driven insights in combating a global health crisis.

Inspired by this resource, this project aims to design and implement a relational database and analytical toolkit that captures the multifaceted impact of COVID-19, including vaccination progress, healthcare system strain, and economic repercussions.
## Project Objectives
The primary goal of this project is to build a comprehensive database to *analyze and visualize key aspects of the COVID-19 pandemic*. Using advanced SQL queries and Tableau dashboards, this project empowers decision-makers with actionable insights into:
- Vaccination progress across countries.
- Variants and their associated severity levels.
- Healthcare system capacity and utilization.
- Economic impacts of the pandemic on a regional and global scale.
By providing a centralized repository for pandemic-related data, the project aims to *support strategic decision-making* for organizations like the WHO (World Health Organization). For example, the WHO can use the database to determine allocation of healthcare resources or for the planning of vaccination campaigns.
## Key Outcomes
This project delivers:

- A relational database with 14 interconnected entities designed for efficient querying and analysis.
- Advanced SQL queries addressing real-world managerial questions.
- Tableau visualizations and an interactive dashboard for intuitive exploration of the data.
These deliverables collectively address key challenges faced during the pandemic, offering stakeholders a reliable tool to analyze critical data and act on insights. The usability of the database by project stakeholders was also central to designing the database. With that kept in mind, this database was made with scalability and the possiblity of another pandemic happening in the future where this type of database could be fitted to that pandemic.
## Project Scope
This project focuses on creating a robust relational database to analyze key aspects of the COVID-19 pandemic. While the goal is to simulate a database capable of supporting a global organization like the World Health Organization (WHO), the scale of data required for such a database—spanning multiple years, countries, and demographics—is beyond the capacity of a four-person team working within a limited timeframe.

To ensure feasibility and meaningful insights, the database is scoped to include data from the year 2020. This approach allows for the creation of a functional and accurate database while demonstrating its potential for scalability in future expansions.
## Ensuring Data Integrity
Data integrity was maintained through a combination of public data sources and logical data generation. Where available, information was sourced from reputable websites such as the World Health Organization, Our World in Data, and The World Bank.

For entities like patient-level records and healthcare center details, data generation was necessary due to HIPAA restrictions and the unavailability of sensitive information. Generated data was designed to align with real-world patterns for authenticity and consistency.

Hosting the database on AWS's RDS free service enabled seamless collaboration while ensuring data accuracy across all entities.
# 1. The Data Model

**Entities Listed by Functional Group**:
The database is organized into four functional groups to capture different aspects of the COVID-19 pandemic:

## 1.1 Country and Demographics
This group focuses on country-level data, including demographics, population statistics, and economic impact metrics.

**Entities**
- *Country*:
    - Tracks demographic, population, and healthcare-related metrics for each country.
- *Economic_Impact*:
    - Captures changes in GDP and employment rates due to the pandemic.
**Relationships**
- Country ↔ Economic Impact:
    - A country can have multiple economic impact records, but each record belongs to one country (idCountry FK in Economic Impact).
**Identifiers**
- Primary Keys:
    - idCountry in Country.
    - idEconomicImpact in Economic Impact.
- Foreign Keys:
    - idCountry in Economic Impact references Country.idCountry.
**Inter-Group Relationships**
- The Country and Demographics group connects to:
    - The Healthcare System group via healthcare facilities that operate within countries.
    - The Vaccination and Variants group for tracking vaccine distribution and variant origins.

## 1.2 Healthcare System
This group represents the infrastructure and personnel involved in delivering healthcare services, including vaccination efforts.

**Entities**
- *Healthcare_Facility*:
    - Represents hospitals, clinics, and other medical centers.
- *Healthcare_Worker*:
    - Logs information about staff working at healthcare facilities.
- *Vaccination_Center*:
    - Tracks vaccination sites, doses allocated, and doses used.
**Relationships**
- Healthcare Facility ↔ Healthcare Worker:
    - A facility can employ many workers, but each worker is assigned to one facility (idHealthcareFacility FK in Healthcare Worker).
- Healthcare Facility ↔ Vaccination Center:
    - A facility may host multiple vaccination centers, but each center operates within one facility (idHealthcareFacility FK in Vaccination Center).
**Identifiers**
- Primary Keys:
    - idHealthcareFacility in Healthcare Facility.
    - idHealthcareWorker in Healthcare Worker.
    - idVaccinationCenter in Vaccination Center.
- Foreign Keys:
    - idHealthcareFacility in Healthcare Worker references Healthcare Facility.idHealthcareFacility.
    - idHealthcareFacility in Vaccination Center references Healthcare Facility.idHealthcareFacility.
**Inter-Group Relationships**

- The Healthcare System group ties to:
    - The Patients and Cases group by providing healthcare services to patients.
    - The Vaccination and Variants group for administering vaccines at vaccination centers.

## 1.3 Patients and Cases
This group tracks patient-level information, COVID-19 cases, hospitalizations, and interactions for contact tracing.

**Entities**
- *Patient*:
    - Contains personal and medical information about individuals affected by COVID-19.
- *COVID_Case*:
    - Tracks individual cases, including severity, outcomes, and test results.
- *Hospitalization*:
    - Logs details of hospital admissions, ICU stays, and discharge dates.
- *Contact Tracing*:
    - Records interactions between patients to map the spread of the virus.
**Relationships**
- Patient ↔ COVID Case:
    - A patient can have multiple cases, but each case belongs to one patient (idPatient FK in COVID Case).
- Patient ↔ Hospitalization:
    - A patient can be hospitalized multiple times, but each hospitalization is linked to one patient (idPatient FK in Hospitalization).
- Patient ↔ Contact Tracing:
    - Contact tracing logs interactions between two patients (idPatient1 and idPatient2 FKs in Contact Tracing).
**Identifiers**
- Primary Keys:
    - idPatient in Patient.
    - idCOVIDCase in COVID Case.
    - idHospitalization in Hospitalization.
    - idContact in Contact Tracing.
- Foreign Keys:
    - idPatient in COVID Case references Patient.idPatient.
    - idPatient in Hospitalization references Patient.idPatient.
**Inter-Group Relationships**
- The Patients and Cases group links to:
    - The Healthcare System group through hospitalizations and healthcare facilities.
    - The Vaccination and Variants group to record patient vaccination status and variant interactions.

## 1.4 Vaccination and Variants
This group captures details about vaccines, COVID-19 variants, and the symptoms experienced by patients.

**Entities**
- *Vaccine_Type*:
    - Details vaccine names, manufacturers, approval dates, and efficiency rates.
- *Vaccine_Record*:
    - Tracks vaccine doses administered by country, age group, and dose type.
- *COVID Variant*:
    - Captures information on variants, including names, severity levels, and countries of origin.
- *Symptom*:
    - Lists possible symptoms of COVID-19, along with their severity and descriptions.
- *Patient Symptoms*:
    - Links patients to the symptoms they experienced and their duration.
**Relationships**
- Vaccine Record ↔ Country:
    - A vaccine record belongs to one country but can include multiple doses (idCountry FK in Vaccine Record).
- Patient ↔ Patient Symptoms:
    - Links patients to the symptoms they experienced (idPatient FK in Patient Symptoms).
- COVID Case ↔ COVID Variant:
    - Each COVID case is linked to one variant (idCOVIDVariant FK in COVID Case).
**Identifiers**
- Primary Keys:
    - idVaccineType in Vaccine Type.
    - idVaccineRecord in Vaccine Record.
    - idCOVIDVariant in COVID Variant.
    - idSymptom in Symptom.
- *Composite key* in Patient Symptoms (idPatient, idSymptom).
- Foreign Keys:
    - idCountry in Vaccine Record references Country.idCountry.
    - idPatient in Patient Symptoms references Patient.idPatient.
**Inter-Group Relationships**
- The Vaccination and Variants group connects to:
    - The Country and Demographics group for vaccine distribution and variant origins.
    - The Patients and Cases group to track variant-related cases and patient symptoms.

# 2. Data Dictionary
For clarity, this is organized by functional group to simplify understanding of the database.

## 2.1 Country and Demographics
This group focuses on country-level data and demographic attributes, including healthcare spending, population, and pandemic impact.


## 2.2 Healthcare System
This group includes data on healthcare facilities, workers, and vaccination centers.


## 2.3 Patients and Cases
Tracks individual-level patient data, their COVID-19 cases, and symptoms.


## 2.4 Vaccination and Variants
Tracks vaccines and COVID variants.


# 3. SQL Queries
The following SQL queries are designed to extract actionable insights from the database. Each query addresses a critical question that can guide **managerial decisions** in the context of the COVID-19 pandemic. There are five queries below.

### Query 1 Vaccination Progress (example not the actual query)
**Question**: What percentage of the population in each country is vaccinated?  
**Justification**: This query helps managers identify countries with low vaccination rates and allocate resources effectively to improve vaccination coverage.  

**Query**:
```sql
SELECT country.name, 
       (SUM(vaccine_record.dosesAdministered) / country.population) * 100 AS vaccination_rate
FROM vaccine_record
JOIN country ON vaccine_record.idCountry = country.idCountry
GROUP BY country.name
ORDER BY vaccination_rate DESC;
```
**Output**:

**Insights**:

# 4. Tableau Visualizations
The Tableau visualizations provide **actionable insights** into key areas of the COVID-19 pandemic, complementing the SQL queries with interactive and visually intuitive data analysis. These visualizations are designed for managers to easily identify trends, disparities, and areas requiring intervention. All visualizations are integrated into an interactive Tableau dashboard for better usability.

## Visualization 1: ....
image

**Description**:

**Managerial Relevance**:
## Visualization 2: ....
image

**Description**:

**Managerial Relevance**:
## Visualization 3: ....
image

**Description**:

**Managerial Relevance**:

# 5. Tableau Dashboard
The Tableau dashboard combines all three visualizations into an interactive platform, allowing users to:
- Filter data by country, region, or time period.
- Drill down into specific metrics, such as vaccination coverage or case severity.
- View economic and healthcare impacts in a unified view.
The dashboard enhances decision-making by integrating key insights into one accessible interface. Download the dashboard: **dashboard.twbx.**

# 6. Access Section (maybe add)

# 7. Conclusion
The `COVIDDatabase` provides a comprehensive relational database and analytical toolkit for understanding the COVID-19 pandemic. By integrating advanced SQL queries, Tableau visualizations, and AWS RDS hosting, the project offers actionable insights for decision-making.
