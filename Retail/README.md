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
    ![](https://i.imgur.com/ssmslogin.png)

## Step 2: HTTP API database
* Choose a framework/platform (e.g., Flask, Express.js, ASP.NET).
* Define API endpoints and HTTP methods (GET, POST, PUT, DELETE).
* Implement request handling and data processing logic.
* Return responses in formats like JSON or XML.
* Secure the API with authentication, authorization, and encryption.
* Test the API using tools like Postman.
* Deploy the API to a hosting platform for access.

   Here we are mimicing the http api by just taking the url from github.after uploading the data into it or by using sample public api.Here all the data is been provided by the backend team for the project
  
## Step 3: Azure Environment Setup
* Create Resource Group: Set up a new resource group in Azure.
* Create an Azure Data Factory instance.
* Set up Azure Data Lake Storage with bronze, silver, and gold containers.
### Ingest Data with ADF
 * setting up of Integration Runtime in Azure Data Factory
 * create linked service for sql server and adls
 * use countineous integration to the pipeline
 * create dataset for adls and sql server
 * upload the data to the source and the sink
 * click publish and trigger
   
Data has been succesfully transfered from sql server &api to the bronze container in datalake storage account   
  
