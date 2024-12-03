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
## Project Objectives

## Key Outcomes

## Project Scope

## Ensuring Data Integrity

# 1. The Data Model

## 1.1 Entities

## 1.2 Attributes

## 1.3 Relationships

## 1.4 Identifiers

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
