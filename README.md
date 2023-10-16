# Pharmacy_Claims_sql


In the course of completing this assignment, I undertook several critical tasks that culminated in the creation of a well-structured and functional database. Below is a concise summary of the key activities and findings:

Part 1 - Normalization:

In this initial phase, the raw data underwent a transformation process aimed at bringing it in line with the principles of the Third Normal Form (3NF). This involved creating a set of relational tables directly within Microsoft Excel. The following highlights are noteworthy:

Data Transformation:The data transformation was conducted in Microsoft Excel, a versatile tool that allowed for seamless organization and restructuring of the data.

Fact and Dimension Tables: I categorized the tables as either fact tables or dimension tables, according to their nature in the data model.

Fact Variable Types: I identified the type of facts within the fact table as either additive, semi-additive, or non-additive.

Fact Table Grain: Each row within the fact table represents a distinct prescription, with a unique prescription identifier serving as the grain of the table.

Part 2 - Primary and Foreign Key Setup in MySQL:

Following the data transformation and structuring, the next step was to import the 3NF data into a MySQL database, and to establish primary and foreign keys. Key considerations include:

Data Import:The data, now organized into 3NF tables, was imported into MySQL, either into a new database or an existing one. I utilized the `LOAD DATA INFILE` command for this task.

- **Primary and Foreign Keys:** Primary keys, natural keys used to uniquely identify each row, were assigned for each table. Foreign keys were employed to establish relationships between tables.

FK Deletion/Update Actions: I specified how foreign keys should behave in case of deletion or update by choosing one of the following options: CASCADE, SET NULL, or RESTRICT.

Part 3 - Entity Relationship Diagram (ERD):

A critical component of this project was the creation of an Entity Relationship Diagram (ERD), which is essential for conveying the table structure and relationships to stakeholders. Key highlights include:

ERD Creation: I used ERDPlus to generate a clear and visually appealing ERD. Each table was represented, and primary keys and foreign keys were visibly labeled.

Export as PDF:The ERD was exported as a single-page PDF to make it easily accessible to all stakeholders.

Part 4 - Analytics and Reporting:**

In this final section, I developed SQL queries to facilitate data analysis and reporting. These queries provide valuable insights into the data, and the results were as follows:

Query 1: I identified the number of prescriptions grouped by drug name, providing a summary of prescription data. For instance, there were 120 prescriptions filled for the drug "Ambien."

Query 2: This query counted total prescriptions, unique members, and the sum of copay for members grouped by age, categorizing members as 'age 65+' or '< 65'.

Query 3: It identified the amount paid by insurance for the most recent prescription fill date using SQL Window functions. This query returned a table with the member's ID, first name, last name, drug name, fill date, and the most recent insurance payment.

This repository now serves as a comprehensive resource for database professionals, enabling them to understand the entire process of database design, normalization, SQL query development, and ERD creation. It is a living resource, ready to adapt and grow as the project advances and evolves to handle more extensive datasets.

For questions, suggestions, or further inquiries, please feel free to reach out. 

