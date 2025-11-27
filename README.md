DBMS PROJECT PHASE I - DrugMatrix – Multi‑Feature Drug Analysis System

1. Team Members
•	220709053 Sinan KAÇAR
•	220709070 Sümeyye SARAY
•	220709029 Hakan BELEN

2. Project Description
We selected a large – scale pharmaceutical dataset (≈250K rows, 58 columns) because it provides a rich, real world structure for database normalization, relational modeling, and analytics. The dataset includes medicine names, usages, substitutes, side effects, chemical/therapeutic/action classes, and habit forming information.
1.	Raw Data Information 
•	Dataset link: https://www.kaggle.com/datasets/shudhanshusingh/250k-medicines-usage-side-effects-and-substitutes
•	Number of files: 1
•	Rows: 248,218
•	Columns: 58
•	Non-numeric column: 57
•	Github Link: https://github.com/sinankacarx/database_drug_project
3.Target English Queries 
Questions that use the “group by” structure with min/max/avg/sum/count that data and the system can answer:
•	Record the total number of side effects associated with every medicine.
•	Determine how many usage indications are listed for individual medicines.
•	Identify the number of substitute options available for each drug.
•	Calculate the count of medicines categorized under every therapeutic class.
•	Analyze therapeutic classes to find the average, minimum, and maximum side-effect counts per medicine.
•	Measure how many medicines and how many unique side effects correspond to each action class.
•	Group medicines by habit-forming status and compute their counts and the average number of substitutes.
•	Check how many medicines exhibit each specific side effect.
•	Find the number of medicines linked to every usage (indication) category.
•	Evaluate chemical classes by counting their medicines and identifying the highest substitute count within the group.
4. ER Diagram
 
Şekil 1: Medicine's ER Diagram
The database schema is centered around the Medicine entity, which stores the fundamental attributes of each drug. Several additional entities—ChemicalClasses, TherapeuticClass, ActionClass, and Habit_Forming—define the categorical classifications of medicines. Each medicine references these tables through foreign keys, ensuring a fully normalized structure and eliminating data redundancy.
To represent multi-valued attributes present in the raw dataset (such as usages, side effects, and substitutes), the design incorporates three junction tables: Medicine_has_Usage, Medicine_has_Side_Effect, and Medicine_has_Substitutes. These associative relations enable the modeling of many-to-many relationships in a consistent and scalable manner. The supporting entities Usages, Side_Effect, and Substitutes store the distinct textual descriptors for these attributes.
Overall, the schema provides a clean, normalized, and relationally consistent representation of the pharmaceutical dataset, allowing efficient querying of drug properties, classifications, usages, side effects, and alternative substitutes.

5. SQL Implementations
Five SQL statements using GROUP BY statements from questions in the third article were cited as examples (side effects, substitutions, uses, therapeutic classes, etc.).


 	 
 	 
 	


6. Overview
The database loading process is designed in two main stages: (1) bulk import from an online dataset, and (2) optional incremental updates via a web-based interface. This ensures both scalability and ease of maintenance.
6.1 Loading Data from Online Sources
The primary data source is a publicly available medicine dataset containing approximately 250,000 rows and 50+ columns. This dataset, downloaded from platforms such as Kaggle, includes medicine names, classes, usages, side effects, and substitutes.
6.1.1. Column-to-Table Mapping
• medicine_name → Medicine
• chemicalclasses, therapeuticclasses, action_class, habit_forming → Lookup tables
• side_effect_0…n → Side_Effect + Medicine_has_Side_Effect
• use_0…n → Usages + Medicine_has_Usage
• substitute_0…n → Substitutes + Medicine_has_Substitutes
6.1.2. Deduplication and Key Generation
Distinct values from each lookup column are extracted in Excel or Python, assigned unique IDs, and exported as CSV files. This ensures clean and normalized population of lookup tables.
6.1.3. Handling Multi-Valued Cells
Side effects, usages, and substitutes often appear in comma-separated form in the raw dataset. These are split into individual records to populate many-to-many relationships.
6.1.4. Cleaning & Type Conversion
• Text normalization (trimming, UTF-8 conversion)
• Length control for VARCHAR(250)
• Replacing unknown or missing values with NULL
6.1.5. Importing into MySQL
Using MySQL Workbench's Import Wizard or LOAD DATA INFILE, data is imported in the following order:
• Lookup tables
• Medicine table
• Junction tables (Medicine_has_Usage, Medicine_has_Substitutes, Medicine_has_Side_Effect)
Foreign key checks are temporarily disabled to prevent constraint issues during bulk loading.

6.2 Loading Data via a WWW / Form-Based Interface
A web-based admin interface can be used to insert or modify data. This interface includes forms where administrators can select lookup values from dropdowns and choose multiple items (side effects, usages, substitutes) via checkboxes or multi-select lists.
Possible Issues with the Interface
• Data validation
• Avoiding duplicates
• Maintaining referential integrity
• Performance considerations for large datasets
• Security and authentication


7. View and Stored Procedure 
  
 

8.Database Platform Details
For this project, I am using MySQL 8.0 Community Edition as my database management system, and I perform all schema design, ER modeling and SQL execution through MySQL Workbench 8.0. I am running MySQL locally on my personal computer, which uses Windows 11 Pro as the operating system.
My development machine is equipped with an Intel Core i7-14700HX processor, 32 GB of RAM and a 1 TB SSD, providing more than enough performance for handling large datasets, executing complex SQL operations, and performing multi-table joins efficiently. Since my dataset contains over 248,000 rows and more than 50 columns, having sufficient RAM and SSD storage played an important role in ensuring fast data processing and smooth query execution.
For data import, I wrote and executed a custom Python script to load the raw Excel file into MySQL. Instead of using the Table Data Import Wizard, I preferred Python because it gave me more control over data cleaning, type handling and batch insertion. After loading the dataset into a staging table, I normalized the data and distributed it into the relational tables defined in my ER diagram.
During the implementation, I encountered several challenges. The Excel file was quite large, so importing it into MySQL took noticeable time. Designing a proper ER diagram also required careful attention, especially while defining the foreign keys and establishing many-to-many relationships. Making the entire schema fully consistent with Third Normal Form (3NF) was another challenging step, since the dataset included many multivalued attributes such as side effects, usage information and substitutes. Additionally, I had to adjust and refine my Python scripts multiple times to ensure clean data loading without violating referential integrity constraints.
Despite these challenges, MySQL Workbench and Python together provided a powerful development environment, and running everything on my own machine allowed me to test, modify and validate the database design efficiently.

