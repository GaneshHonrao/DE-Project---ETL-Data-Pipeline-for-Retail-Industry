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

### 5. Project Architecture
  
![Pasted image 20231217185040](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/a197ad7d-19b8-4498-9129-344b94ff1741)

### 6. Project Structure
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
  
![Pasted image 20231217185826](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/11d6afab-6211-4ae0-b86e-eb57656ab933)

- Tables and Data Snapshots -
	- Data and schema received from transactional table into s3 -

   1. Sales (Fact) Table -
	  		
	  ![Pasted image 20231218202856](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/b8a0d5e7-73fd-4354-8994-de34289a6ec1)
			

  2. Customer (Dimension) Table -		
	  
	  ![Pasted image 20231218203415](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/d35b1e18-c67e-4afc-b42a-3aac845cd2ff)
	
		- Customers Table Data -		
	  
	  ![Pasted image 20231218203445](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/0a7031bc-64c8-4a5e-98e6-edd292e2a834)
			
		
  3. Store (Dimension) Table -		
	  
	  ![Pasted image 20231218203745](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/71761c4b-50b0-43bb-923c-ebdab8817803)
	
		- Store Table Data -		
	  
	  ![Pasted image 20231218203835](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/c3de9f36-bd9a-4cd6-8127-8ac4bde5700a)
			
		
  4. Product (Dimension) Table -		
	  
	  ![Pasted image 20231218203908](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/160ce636-b3d4-4ff9-9dbd-d218fd9a67bf)
	
		- Product Table Data -		
	  
	  ![Pasted image 20231218204002](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/44347469-11bb-41ab-96f3-5a46c3b03964)
			
		
  5. Sales Team (Dimension) Table -		
	  
	  ![Pasted image 20231218204054](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/7fe31486-9ae8-4b6e-b839-b3e74f5d0d69)
	
		- Sales Team Table Data -		
	  
	  ![Pasted image 20231218204148](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/538163c5-ae80-453e-8748-269a73a984f5)
			

   6. Staging Table (For Auditing & Process Track) -		
	  
	  ![Pasted image 20231218204313](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/efcf49d0-9a9e-47a1-ab68-79179035a4b8)
	
		- Status - A - Process is Active and failed
		- Status - I - Process is Inactive and completed
		- Purpose of Staging table is to indicate the stage started, inactive and failed
			
		
  7. Customer Data Mart -
	  
	  ![Pasted image 20231218204415](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/0ad2171b-759e-4544-9615-2af4296b38c0)
	
		- Using this Data Mart we can generate dynamic coupon code.

 
		
  8. Sales Team Data Mart -		
	  
	  ![Pasted image 20231218204503](https://github.com/GaneshHonrao/DE-Project-ETL-Data-Pipeline-for-Retail-Industry/assets/144705832/3808c80b-1d8d-4268-bf77-80e61401f5ec)
		- Incentive is set for top 1st sales person, by default 1% of total sales per month.
