# Pharmacy_Claims_sql

Table of Contents
Create a table of contents that will help users quickly find the information they need. Link each section to the corresponding part of the documentation.


Part 1 — Normalization
Part 2 — Primary and Foreign Key Setup in MySQL
Part 3 — Entity Relationship Diagram (ERD)
Part 4 — Analytics and Reporting
Part 1 — Normalization
Data Transformation
In this section, describe how you converted the raw data into relational tables in Excel, including the process, tools, and steps taken.

I used Microsoft Excel to transform the raw data into a set of relational tables. Here's how I did it:

Opened the raw data file in Excel.
Identified the fact and dimension tables.
Created separate worksheets for each table.
Organized the data according to the 3NF standards.
Fact and Dimension Tables
List the tables you created and explain whether they are fact tables or dimension tables.

Example:

fact_prescriptions.csv (Fact Table)
dim_drugs.csv (Dimension Table)
Fact Variable Types
Explain the type of fact (additive, semi-additive, or non-additive) for each fact variable in your fact table.

Example:

fact_prescriptions contains additive facts like total_copay, non-additive facts like member_count.
Fact Table Grain
Describe the grain of your fact table in one sentence, explaining what each fact row represents.

Example:
The fact_prescriptions table has a grain at the level of individual prescriptions, where each row represents a single prescription filled.

Part 2 — Primary and Foreign Key Setup in MySQL
Data Import
Explain how you imported the 3NF CSV files into MySQL, including any specific details and considerations.

Example:
I used the MySQL command-line tool to import the CSV files into a new database. The command used was LOAD DATA INFILE.

Primary Keys and Foreign Keys
List the primary keys (PKs) and foreign keys (FKs) you designated for each table.

Example:

fact_prescriptions PK: prescription_id (Natural Key)
dim_drugs PK: drug_id (Natural Key)
fact_prescriptions FK: drug_id (References dim_drugs(drug_id))
FK Deletion/Update Actions
Explain what actions you set for foreign keys in case of deletion or update (CASCADE, SET NULL, or RESTRICT), and justify your choice for each FK.

Example:
For the fact_prescriptions table, I set the drug_id FK to CASCADE in case of deletion. This means that if a drug is deleted from dim_drugs, all related prescriptions in fact_prescriptions will also be deleted. This choice was made because it ensures data integrity and consistency.

Part 3 — Entity Relationship Diagram (ERD)
ERD Creation
Explain how you created the ERD using MySQL or a tool like ERDPlus.

Example:
I used ERDPlus to create the ERD. I added tables for each fact and dimension table, labeled PKs and FKs, and organized the fact table in the center with dimension tables surrounding it.

Export as PDF
Provide instructions on how to export the ERD as a PDF.

Example:
To export the ERD as a PDF, click on "File," then select "Export" and choose the PDF format.

Part 4 — Analytics and Reporting
SQL Queries
Include the SQL queries for each of the three tasks described in Part 4. Additionally, provide the output of each query.

Example:

Query 1: Number of Prescriptions Grouped by Drug Name
sql
SELECT drug_name, COUNT(*) as prescription_count
FROM fact_prescriptions
GROUP BY drug_name;
Output:

lua
Copy code
| drug_name | prescription_count |
|-----------|-------------------|
| Ambien    | 120               |
| ...       | ...               |
Query 2: Total Prescriptions and Copay Sum by Age Group
sql
SELECT
  CASE
    WHEN age < 65 THEN '< 65'
    ELSE '65+'
  END AS age_group,
  COUNT(DISTINCT member_id) AS unique_members,
  COUNT(*) AS total_prescriptions,
  SUM(copay) AS total_copay
FROM fact_prescriptions
GROUP BY age_group;
Output:

yaml
Copy code
| age_group | unique_members | total_prescriptions | total_copay |
|-----------|----------------|---------------------|------------|
| < 65      | 400            | 6000                | 5000       |
| 65+       | 300            | 4500                | 3000       |
Query 3: Amount Paid by Insurance for Most Recent Prescription
sql
WITH ranked_prescriptions AS (
  SELECT
    member_id,
    member_first_name,
    member_last_name,
    drug_name,
    fill_date,
    insurance_paid,
    ROW_NUMBER() OVER (PARTITION BY member_id ORDER BY fill_date DESC) AS rn
  FROM fact_prescriptions
)
SELECT
  member_id,
  member_first_name,
  member_last_name,
  drug_name,
  fill_date,
  insurance_paid
FROM ranked_prescriptions
WHERE rn = 1;
Output:


| member_id | member_first_name | member_last_name | drug_name | fill_date  | insurance_paid |
|-----------|-------------------|------------------|-----------|------------|-----------------|
| 10003     | John              | Doe              | Lipitor   | 2023-10-01 | 40.00           |
| ...       | ...               | ...              | ...       | ...        | ...             |
Conclusion
