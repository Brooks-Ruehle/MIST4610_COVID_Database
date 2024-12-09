# MIST4610_COVID_Database
## Team Name:
The RockLobsters
## Team Members:
1. Brooks Ruehle | (@Brooks-Ruehle)
2. Will Jenkins | (@willjenkins-Glitch)
3. Charlie Davis | (@cbdcharlie)
4. Abhi Kode | (@abikod)

# Table of Contents
- [Introduction](#introduction)
  - [Background](#background)
  - [Project Objectives](#project-objectives)
  - [Key Outcomes](#key-outcomes)
  - [Project Scope](#project-scope)
  - [Ensuring Data Integrity](#ensuring-data-integrity)
- [1. The Data Model](#1-the-data-model)
  - [1.1 Country and Demographics](#11-country-and-demographics)
  - [1.2 Healthcare System](#12-healthcare-system)
  - [1.3 Patients and Cases](#13-patients-and-cases)
  - [1.4 Vaccination and Variants](#14-vaccination-and-variants)
  - [1.5 ERR Diagram](#15-err-diagram)
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
- [8. Conclusion](#8-conclusion)

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
    - Modality: Not mandatory for Economic Impact as not every country has economic data.
    - Type: One-to-Many, Non-Identifying; a country can have multiple economic impact records, but each record exists independently of the country.
    - Foreign Key: idCountry in Economic Impact references Country.idCountry..
 
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
    - Modality: Optional for Healthcare Worker as not all facilities have associated workers in their records.
    - Type:  One-to-Many, Non-identifying; a worker’s existence does not depend on a healthcare facility because they do not have to currently work at a healthcare facility.
    - Foreign Key: idHealthcareFacility in Healthcare Worker references Healthcare Facility.idHealthcareFacility.
- Healthcare Facility ↔ Vaccination Center:
    - Modality: Mandatory for Vaccination Center as every center must belong to a healthcare facility.
    - Type: One-to-One, Non-Identifying; the vaccination center exists independently of the facility but is logically tied to it.
    - Foreign Key: idHealthcareFacility in Vaccination Center references Healthcare Facility.idHealthcareFacility.
- Healthcare Worker ↔ Healthcare Worker (recursive to signify worker working for boss)
    - Modality: Non-mandatory, not every healthcare worker has another worker working for them.
    - Type: one-to-many, non-identifying, a worker does not depend on another worker to work at a healthcare facility
    - Foreign Key: idBoss in Healthcare Worker signifies the worker's boss and who they work for.
  
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
    - Modality: Optional for COVID Case since not all COVID cases are associated with a patient (e.g., unreported or anonymous cases).
    - Type: One-to-Many, Non-Identifying; the case exists independently of a patient.
    - Foreign Key: idPatient in COVID Case references Patient.idPatient.
- Patient ↔ Hospitalization:
    - Modality: Optional for Hospitalization as not all patients are hospitalized.
    - Type: One-to-Many, Identifying; the hospitalization record depends on the existence of a patient.
    - Foreign Key: idPatient in Hospitalization references Patient.idPatient.
- Patient ↔ Contact Tracing:
    - Modality: Optional for Contact Tracing as not all patients are involved in tracing efforts.
    - Type: Many-to-Many, Non-Identifying; the tracing records exist to map interactions but do not depend on patients for their logical existence.
    - Foreign Keys: idPatient1 and idPatient2 in Contact Tracing reference Patient.idPatient.

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
    - Modality: Optional for Vaccine Record since not all countries have vaccination records in the database.
    - Type: Many-to-One, Identifying; the vaccine record depends on a specific country for its existence.
    - Foreign Key: idCountry in Vaccine Record references Country.idCountry.
- Patient ↔ Patient Symptoms:
    - Modality: Optional for Patient Symptoms as not all patients experience symptoms.
    - Type: Many-to-Many, Identifying; the record depends on both the patient and the symptom for its existence.
    - Foreign Keys: idPatient in Patient Symptoms references Patient.idPatient; idSymptom references Symptom.idSymptom.
- COVID Case ↔ COVID Variant:
    - Modality: Mandatory for COVID Case since each case must be associated with a variant.
    - Type: Many-to-One, Non-Identifying; multiple cases can belong to one variant, but the cases exist independently of the variant.
    - Foreign Key: idCOVIDVariant in COVID Case references COVID Variant.idCOVIDVariant.
  
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
 
## 1.5 ERR Diagram
![image](https://github.com/user-attachments/assets/a2a939fd-941d-4d40-bd00-98fb23ff39de)



# 2. Data Dictionary
For clarity, this is organized by functional group to simplify understanding of the database.

## 2.1 Country and Demographics
This group focuses on country-level data and demographic attributes, including healthcare spending, population, and pandemic impact.
### Country
![image](https://github.com/user-attachments/assets/9f6c59c1-89f9-44ae-90bb-ca097025d67f)
(only for the year 2020)
### Economic Impact
![image](https://github.com/user-attachments/assets/92dc8c8e-4e39-47bb-a15b-cab344a4a893)
(only for the year 2020)
## 2.2 Healthcare System
This group includes data on healthcare facilities, workers, and vaccination centers.
### Healthcare Facility
![image](https://github.com/user-attachments/assets/0a6d031c-8207-4020-9fec-9dd496a9243b)
### Healthcare Worker
![image](https://github.com/user-attachments/assets/9937f14a-a188-4964-99fe-fbc40638a93b)
### Vaccination Center
![image](https://github.com/user-attachments/assets/e307297c-80d4-4ac0-b89f-ffbdd4727cb2)
## 2.3 Patients and Cases
Tracks individual-level patient data, their COVID-19 cases, and symptoms.
### Patient
![image](https://github.com/user-attachments/assets/1c512943-d5cf-4322-b7e0-7193d883cf02)
### Covid Case
![image](https://github.com/user-attachments/assets/eb587bad-3381-42d1-bc10-3bb734096405)
### Hospitalization
![image](https://github.com/user-attachments/assets/5305107d-bf99-4bc2-a586-50585b261ce9)
### Contact Tracing
![image](https://github.com/user-attachments/assets/94bd41a1-a955-4e60-9ec3-18335a71d556)
## 2.4 Vaccination and Variants
Tracks vaccines and COVID variants.
### Vaccine Type
![image](https://github.com/user-attachments/assets/ab370992-faa1-42ea-8dbb-741219564766)
### Vaccine Record
![image](https://github.com/user-attachments/assets/8f67a87d-8255-4220-8e96-186ad24e841d)
### COVID Variant
![image](https://github.com/user-attachments/assets/3e984e37-2b1c-462c-a3fd-1b55d0d047ce)
### Symptom
![image](https://github.com/user-attachments/assets/00ed90f8-7d3b-4341-8f9c-fe53b608594a)
### Patient Symptoms
![image](https://github.com/user-attachments/assets/2ae76338-b99d-4336-a8ff-9e590a75c54c)
# 3. SQL Queries
The following SQL queries are designed to extract actionable insights from the database. Each query addresses a critical question that can guide **managerial decisions** in the context of the COVID-19 pandemic. There are five queries below.

### Query 1 GDP Change against average deathes per region
**Question**: What is the average GDP change in Q2 against the average number of deathes per region.

**Justification**: This query helps to show how average deathes might relate to GDP changes by region. A stakeholder in the database, like a manager at WHO, can use this to determine which regions were most affected and therefore send more aid to those regions.

**Query**:

```
SELECT 
    Country.region AS Region, 
    (SUM(Country.total_Deaths) / SUM(Country.population)) * 100000 AS Deaths_Per_100K,
    AVG(Economic_Impact.GDP_Change) AS Avg_GDP_Change_Q2
FROM 
    Country
JOIN 
    Economic_Impact ON Country.idCountry = Economic_Impact.idCountry
WHERE 
    Economic_Impact.quarter = 2
GROUP BY 
    Country.region
ORDER BY 
    Deaths_Per_100K DESC;
```

**Output**:

<img width="386" alt="Screenshot 2024-12-03 at 9 15 48 PM" src="https://github.com/user-attachments/assets/49f2e505-4802-403a-8f62-cdad70de9c8d">


**Insights**:

Regions with lower average death rates seem to also have lower GDP canges in Quarter 2 of 2020. This is likely because regions with hgiher death rates and more exposure and transmission of the disease had to shut down more business and reduce activities in a wider range of industries that affect GDP more.
### Query 2 Beds Per Person in each Country
**Question**: What is the number of hospital beds available per person in each country, and how does this vary across nations?

**Justification**: This query provides critical insights for public health planning and crisis management. By calculating the number of beds per person, managers can gain a better understanding of the readiness of each country's healthcare system and identify countries with insufficient healthcare systems to more effectively allocate resources.

**Query**:

```
SELECT 
    Country.name, 
    Country.population AS Population,
    SUM(Healthcare_Facility.capacity) AS Total_Beds,
    SUM(Healthcare_Facility.capacity) / Country.population AS Beds_Per_Person
FROM 
    Country
JOIN 
    Healthcare_Facility ON Country.idCountry = Healthcare_Facility.idCountry
GROUP BY 
    Country.idCountry
ORDER BY 
    Beds_Per_Person DESC;
```

**Output**:

<img width="461" alt="Screenshot 2024-12-03 at 9 06 42 PM" src="https://github.com/user-attachments/assets/abcf5ecf-a035-4ed5-a67a-fd83bb43349c">


**Insights**: The results highlight significant disparities in healthcare capacity across countries, with some nations having a much higher number of beds per person compared to others. Countries with higher beds per person are likely better equipped to manage healthcare emergencies like COVID-19, while those with lower ratios may not be able to provide adequate care. This data underscores the need for certain investments in healthcare infrastructure in regions with not enough healthcare facility capacity. It also provides actionable insights for international aid and public health planning on a global scale.


### Query 3 Hospitalizations per Healthcare Facility
**Question**: Which healthcare facilities handle the highest number of hospitalizations, and how does the distribution of hospitalizations vary across facilities?

**Justification**: This query is useful for evaluating the workload and capacity of healthcare facilities. By finding facilities with the most hospitalizations, managers can focus on facilities that may need extra staff, equipment, or funding to meet demand in times of crisis. It can also allow managers to optimize resource allocation by shifting patients or resources to less burdened facilities and identify trends in hospitalization demand to inform long-term planning and policy decisions about those hospitals.
**Query**:

```
SELECT 
    Healthcare_Facility.idHealthcare_Facility, 
    Healthcare_Facility.name AS healthcare_facility_name,
    COUNT(Hospitalization.idHospitalization) AS number_of_hospitalizations
FROM 
    Healthcare_Facility
JOIN 
    Hospitalization ON Healthcare_Facility.idHealthcare_Facility = Hospitalization.idHealthcare_Facility
GROUP BY 
    Healthcare_Facility.idHealthcare_Facility, 
    Healthcare_Facility.name
ORDER BY 
    number_of_hospitalizations DESC;
```

**Output**:

<img width="475" alt="Screenshot 2024-12-03 at 9 10 36 PM" src="https://github.com/user-attachments/assets/1b82757c-1c25-4780-afb3-8497a67de524">

### Query 4 Average Stay  per Healthcare Facility
**Question**: Which healthcare facilities have the highest average stay length per individual?

**Justification**: This query is useful for evaluating the average stay that a person stays at each healthcare facility. It could be indicative of where there might need to be more people to help out in each facility. There can be facilities that have an average longer stay also due to where they stay and also due to how many total patients they have.
**Query**:

```
SELECT 
    Healthcare_Facility.type AS facility_type,
    COUNT(Hospitalization.idHospitalization) AS total_patients,
    AVG(Hospitalization.length_of_stay) AS avg_stay_length
FROM 
    Healthcare_Facility
JOIN 
    Hospitalization ON Healthcare_Facility.idHealthcare_Facility = Hospitalization.idHealthcare_Facility
GROUP BY 
    Healthcare_Facility.type
ORDER BY 
    avg_stay_length DESC;
```

**Insights**: The results reveal that facilities can vary greatly on how many patients they have along with the average stay for each patient. Patients that stay longer could stay longer due to other factors and the data might not be indicative of what each facility actually needs.

**Output**:

<img width="312" alt="Screenshot 2024-12-08 at 8 19 57 PM" src="https://github.com/user-attachments/assets/f9b40976-4e89-4953-b713-b1979d5b28b3">

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

# 7. What Could Be Improved?

# 8. Conclusion
The `COVIDDatabase` provides a comprehensive relational database and analytical toolkit for understanding the COVID-19 pandemic. By integrating advanced SQL queries, Tableau visualizations, and AWS RDS hosting, the project offers actionable insights for decision-making.
