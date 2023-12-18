## Project Overview

### 1. Key Aspects of this Project
1. Production Grade Project
2. Secure Data Handling with Encryption Decryption
3. Comprehensive Logging
4. AWS Integration with Boto3
5. Data Marts for Targeted Insights

### 2. What's Happening: A Dive into Our Project Actions
1. Reading Transactional Data from AWS S3 Bucket
2. Validation of Input Data
3. Transforming the Data based on Business use case
4. Loading Data into the Data Mart

### 3. Why It Matters: An Exploration of the Problem Statement
1. In an effort to motivate the billing team, the business unit wants to provide incentives tied to total sales.
2. In an effort to enhance customer engagement, the business wants to track its customer base and offer corresponding coupons or discounts.
3. It is required to produce a report on a daily basis.
4. It is necessary to generate a monthly report at the end of every month.

### 4. How We're Achieving It: Unveiling Our Project Approach
1. Utilized Apache Spark for seamless Data Transformation
2. Data volume is generated at 15 GB per day
3. The S3 Boto3 SDK has been used to connect with Amazon S3.
4. Data is Loaded to the Data Mart for further processing by the Reporting tool.

### 6. Project Architecture
![[Pasted image 20231217185040.png]]

### 5. Project Structure
```md
Project structure:-
my_project/
├── docs/
│   └── readme.md
├── resources/
│   ├── __init__.py
│   ├── dev/
│   │    ├── config.py
│   │    └── requirement.txt
│   └── qa/
│   │    ├── config.py
│   │    └── requirement.txt
│   └── prod/
│   │    ├── config.py
│   │    └── requirement.txt
│   ├── sql_scripts/
│   │    └── table_scripts.sql
├── src/
│   ├── main/
│   │    ├── __init__.py
│   │    └── delete/
│   │    │      ├── aws_delete.py
│   │    │      ├── database_delete.py
│   │    │      └── local_file_delete.py
│   │    └── download/
│   │    │      └── aws_file_download.py
│   │    └── move/
│   │    │      └── move_files.py
│   │    └── read/
│   │    │      ├── aws_read.py
│   │    │      └── database_read.py
│   │    └── transformations/
│   │    │      └── jobs/
│   │    │      │     ├── customer_mart_sql_transform_write.py
│   │    │      │     ├── dimension_tables_join.py
│   │    │      │     ├── main.py
│   │    │      │     └──sales_mart_sql_transform_write.py
│   │    └── upload/
│   │    │      └── upload_to_s3.py
│   │    └── utility/
│   │    │      ├── encrypt_decrypt.py
│   │    │      ├── logging_config.py
│   │    │      ├── s3_client_object.py
│   │    │      ├── spark_session.py
│   │    │      └── my_sql_session.py
│   │    └── write/
│   │    │      ├── database_write.py
│   │    │      └── parquet_write.py
│   ├── test/
│   │    ├── scratch_pad.py.py
│   │    └── generate_csv_data.py
```

### 7. Schema, Tables and Data
- Star Schema -
![[Pasted image 20231217185826.png]]

- Tables and Data Snapshots -
- Data and schema received from transactional table into s3 -
	1. Sales (Fact) Table -		
		![[Pasted image 20231218202856.png]]
		
	2. Customer (Dimension) Table -		
		![[Pasted image 20231218203415.png]]
		- Customers Table Data -		
		![[Pasted image 20231218203445.png]]
		
	3. Store (Dimension) Table -		
		![[Pasted image 20231218203745.png]]
		- Store Table Data -		
		![[Pasted image 20231218203835.png]]
		
	4. Product (Dimension) Table -		
		![[Pasted image 20231218203908.png]]
		- Product Table Data -		
		![[Pasted image 20231218204002.png]]
		
	5. Sales Team (Dimension) Table -		
		![[Pasted image 20231218204054.png]]
		- Sales Team Table Data -		
		![[Pasted image 20231218204148.png]]
		
	6. Staging Table (For Auditing & Process Track) -		
		![[Pasted image 20231218204313.png]]
		- Status - A - Process is Active and failed
		- Status - I - Process is Inactive and completed
		- Purpose of Staging table is to indicate the stage started, inactive and failed
		
	1. Customer Data Mart -
		![[Pasted image 20231218204415.png]]
		- Using this Data Mart we can generate dynamic coupon code.
		
	8. Sales Team Data Mart -		
		![[Pasted image 20231218204503.png]]
		- Incentive is set for top 1st sales person, by default 1% of total sales per month.
