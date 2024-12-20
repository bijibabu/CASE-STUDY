 # DATA LAKE HOUSE PROJECT
 
 A Data Lake house is a centralized repository designed to store, process, and manage large volumes of structured, semi-structured, and unstructured data.A data lake centralizes raw data, allowing easy storage and access. It supports effective data management and analysis, enhancing decision-making. This setup ensures scalability and cost-efficiency. Key components include data ingestion, storage, processing, and governance
            
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
* azure synapse analytics

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
HTTP API (from[https://AdventureWorks_Sales_2015.com/products] in JSON format)
  
## Step 3: Azure Environment Setup
* Create Resource Group: Set up a new resource group in Azure.
* Create an Azure Data Factory instance.
* Set up Azure Data Lake Storage with bronze, silver, and gold containers.
## Ingest Data with ADF
###  created a self-hosted integration runtime

 Go to  Integration Runtimes in ADF → Click on + New to Add Integration Runtime →
Select "Self-Hosted" Runtime and Continue → Name the Integration Runtime and Create →
Download SHIR Software and Copy Authentication Key → Install SHIR Software on Host Machine → Paste Authentication Key During Setup → Verify Installation in ADF (Status: Running) →Test Connectivity to On-Premises Resources →SHIR Ready for Use

 ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/integration%20runtime.png?raw=true)
 ## GitHub Integration:
 
* Linked ADF to a GitHub repository for version control and team collaboration.
* I made sure the repository was connected to the Dev branch. 


 ### create linked service in ADF
 
 1.Microsoft SQL Server 
     ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/ssmslink.png?raw=true)
 2. HTTP API 
![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/httplink.png?raw=true)


###  Creating Pipelines in ADF    
 1.Microsoft SQL Server to Storage:
  * Created a linked service for Microsoft SQL Server using a self-hosted integration 
    runtime. This enabled  to connect to the opremise  
  *  Used the Copy Data activity to copy data from Microsoft SQL Server to the raw
      container in ADLS Gen2 in CSV format.    
  ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/ssms%20pipiline.png?raw=true)

2.HTTP API to Storage:
* Created a linked service for[https://dummyjson.com/products] to fetch data in JSON 
  format. 
*  Used Copy Data activity to fetch data from the HTTP API and save it in the raw
 container in Azure Data Lake Storage (ADLS) in Parquet format. 
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20pipeline.png?raw=true)

## Triggers for Data Pipelines
Used time-based triggers to initiate data pipelines for periodic data ingestion.
A trigger was set for Pipeline 1 to pull the HTTP API  scheduled time.
A trigger for Pipeline 2 to pull data from SQL Server on a regular basis.

## Quality Assurance Process
 ### Creating a QA Branch 
* After creating and testing the pipelines in the Dev branch, create a QA branch in the 
  GitHub repository. 
* Do the pull request from the Dev branch to the QA branch. 
* After the pull request was approved, confirme the pipelines were deployed 
  successfully in the QA branch of Data Factory.
  
# Data Transformation in Databricks
* Created a Databricks workspace and mounted the raw containers from 
 ADLS Gen2 to Databricks using secret scopes for secure access by using
 service principle. 

## on-premise
*  Here using service princple mounted both raw and processed containers.
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20start.png?raw=true)
    ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/mount%20onpremise.png?raw=true)
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/mount%20processed.png?raw=true)

* Readin and cleaning the data
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20read.png?raw=true)
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20r.png?raw=true)
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20s.png?raw=true)
   ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20b.png?raw=true)
    ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/onpremise%20m.png?raw=true)
  * After the that the data is transfered to the processed container
  * then we read the data from the processed container
  * mount the processed container and gold container
   ## http data
  ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20m.png?raw=true)
  ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20r.png?raw=true)
 ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20r2.png?raw=true)
 ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20r3.png?raw=true)
![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/http%20delta.png?raw=true)

 ### Azure synapse
 * Created an external table in Azure Synapse Analytics to to enable querying the processed data. This step allowed
 * users to run SQL queries over the Gold container's data for reporting, analysis, and decision-making.
   ## steps for cteating a dedicated pool
* Navigate to Synapse Workspace
* Open the Azure portal and navigate to your Synapse workspace.
* Create a Dedicated SQL Pool: Go to SQL Pools under Synapse Studio > Manage.
* Click New SQL Pool.
* give it a name
* Performance Level: Choose the desired performance level as 0
* Click Create and wait for deployment.
   
 ![image alt](https://github.com/bijibabu/CASE-STUDY/blob/main/Retail/screenshot/azure%20synapse.png?raw=true)
  
