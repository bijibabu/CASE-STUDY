 # DATA LAKE PROJECT
 
 A Data Lake is a centralized repository designed to store, process, and manage large volumes of structured, semi-structured, and unstructured data.A data lake centralizes raw data, allowing easy storage and access. It supports effective data management and analysis, enhancing decision-making. This setup ensures scalability and cost-efficiency. Key components include data ingestion, storage, processing, and governance
            
 ## Prerequisites
 * An Azure account with sufficient credits.
 * Access to an on-premises SQL Server database.
 * Access to an http api database

## Technology Stack
* Azure Data Factory (ADF): For orchestrating data movement and transformation.
* Azure Data Lake Storage (ADLS): For storing raw and processed data.
* Azure Databricks: For data transformation and processing.
* SQL Server (On-Premises): Source of data.
* Http API :source of data
* GitHub : for version control and managing the source code.

 ## Step 1:  on-premises SQL Server database
 SQL Server Management Studio (SSMS) is a powerful tool for managing SQL Server databases
 ### Install SSMS:
* Download the installer from the official Microsoft SSMS page.
* Run the installer and follow the prompts to complete the installation.
   ### Creating the tables
  * Create a new database for your dataset
  * Click on new query and write a SQL query to create a table.

    ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/ssmslogin.png?raw=true)

## Step 2: HTTP API database
HTTP API (from[https://dummyjson.com/products] in JSON format)
  
## Step 3: Azure Environment Setup
* Create Resource Group: Set up a new resource group in Azure.
* Create an Azure Data Factory instance.
* Set up Azure Data Lake Storage with bronze, silver, and gold containers.
## Ingest Data with ADF
### Microsoft SQL Server to Storage: 
 *  created a self-hosted integration runtime. This enabled  to connect to the opremise 
   SQL Server. 

   Go to  Integration Runtimes in ADF → Click on + New to Add Integration Runtime →
Select "Self-Hosted" Runtime and Continue → Name the Integration Runtime and Create →
Download SHIR Software and Copy Authentication Key → Install SHIR Software on Host Machine → Paste Authentication Key During Setup → Verify Installation in ADF (Status: Running) →Test Connectivity to On-Premises Resources →SHIR Ready for Use

 ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/integration%20runtime.png?raw=true)
 
 ### create linked service in ADF
 
 1.Microsoft SQL Server 
     ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/ssmslink.png?raw=true)
 2. HTTP API 
![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/httplink.png?raw=true)

###  Creating Pipelines in ADF    
  1.Microsoft SQL Server to Storage:
  * Created a linked service for Microsoft SQL Server using a self-hosted integration 
    runtime. 
  * The data from SQL Server was transferred to the raw container in ADLS Gen2 
    in CSV format. 
  ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/sqlserver%20pipeline.png?raw=true)
2.HTTP API to Storage:
* Created a linked service for[https://dummyjson.com/products] to fetch data in JSON 
  format. 
* The data was stored in the raw container in Azure Data Lake Storage (ADLS) 
  Gen2 in Parquet format.
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20pipeline.png?raw=true)

  
