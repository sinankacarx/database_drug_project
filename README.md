🚀 DrugMatrix – Multi-Feature Medicine Analytics System

A comprehensive relational database designed for large-scale pharmaceutical analytics.

DrugMatrix is a relational database system developed as part of the DBMS Project Phase I requirements.
The system focuses on modeling, normalizing, and analyzing high-dimensional medical datasets, including medicines, side effects, usages, substitutes, and pharmaceutical classification attributes.

📌 Project Overview

DrugMatrix is built on MySQL 8.0 using MySQL Workbench and follows strict normalization principles (1NF–2NF–3NF).
The system supports efficient querying of medical classifications, multi-valued attributes, and cross-medicine analytical relationships.

Dataset Summary

248,218 records

58 attributes

Multi-valued fields:

Side effects

Usages

Substitutes

Rich classification data:

Chemical class

Therapeutic class

Action class

Habit forming

Dataset Link

🔗 https://www.kaggle.com/datasets/shudhanshusingh/250k-medicines-usage-side-effects-and-substitutes

👥 Team Members

Sinan Kaçar – 220709053

Sümeyye Saray – 220709070

Hakan Belen – 220709029

🗂 Database Contents

The project includes the full implementation of:

Entity-Relationship (ER) Diagram

SQL schema file containing:

Table creation scripts

Sample row inserts

Five analytical SQL queries using GROUP BY

A complete VIEW implementation

A stored procedure including IN, OUT and INOUT parameters

Full normalization of multi-valued attributes

🧬 ER Diagram Structure

The database model centers around the Medicine table.
It includes the following primary entities:

chemicalclasses

therapeuticclass

actionclass

habit_forming

usages

side_effect

substitutes

Multi-valued attributes are handled through associative junction tables:

medicine_has_usage

medicine_has_side_effect

medicine_has_substitutes

These tables ensure accurate many-to-many relationship modeling and full referential integrity through foreign key constraints.

🔬 Target Analytical Queries

DrugMatrix answers 10 analytical questions designed to explore:

Side-effect distribution

Usage patterns

Substitute diversity

Class-based medicine grouping

Habit-forming analysis

Chemical class-based drug comparisons

Multi-attribute aggregate evaluations

All analytical questions use GROUP BY + aggregate functions such as COUNT, AVG, MIN, and MAX.

Example analytical goals include:

Count of side effects per medicine

Count of usages per medicine

Number of substitutes per medicine

Number of medicines per therapeutic class

Max–min–average side effects per therapeutic class

Total unique side effects per action class

Average substitute count based on habit-forming type

Side-effect frequency across all medicines

Medicine distribution per usage category

Maximum substitute count per chemical class

🛠 Technologies Used
Component	Specification
Operating System	Windows 11 Pro
DBMS	MySQL Community Server 8.0.43
Design Tool	MySQL Workbench
Hardware	Intel i7-14700HX, 32 GB RAM
Storage	Local NVMe SSD
Data Source	Kaggle – 250k Medicines Dataset
ETL Method	Python script used for importing Excel data into SQL
📌 Key Features

Fully normalized relational schema compliant with 3NF

Junction table design for multi-valued attributes

Analytical SQL queries using GROUP BY

A powerful VIEW offering summarized medicine information

Stored procedure demonstrating IN–OUT–INOUT functionality

Strong MySQL 8.0 compatibility

Efficient data handling using Python-based ETL

📞 Contact

For any questions regarding this project:

Sinan Kaçar
Muğla Sıtkı Koçman University — Computer Engineering
📧 Email: sinank@posta.mu.edu.tr
