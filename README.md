# Retail Data Analysis | Data Engineering project using Azure

📄 [Live case study: Retail Data Validation Pipeline with Azure Databricks](https://pushpakvootla.cloud/projects/retail-databricks-validation-pipeline)

## Introduction
This project leverages Azure's robust data engineering ecosystem to analyze retail data, utilizing Azure Data Lake Storage Gen2 (ADLS) for scalable storage , Azure SQL Database for relational data management, Amazon S3 for data ingestion, Azure Data Factory for data integration, and Azure Databricks for data transformation and analytics. The project aims to provide actionable insights from retail data, enabling informed business decisions. By integrating these Azure services, the project ensures a seamless data pipeline, from data ingestion to visualization.

## Technology used
1. Programming Language - Pyspark
2. Scripting Language - SQL
3. Azure Cloud Platform
   - Azure Data Lake Storage (ADLS Gen2)
   - Azure SQL Database
   - Azure Key Vault
   - Azure Data Factory
   - Azure Triggers
   - Azure Databricks
4. Amazon Web Services (AWS Cloud)
   - Amazon S3

## Architecture
![Project Architecture](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Pipeline_Architecture.jpg)

The diagram depicts a retail customer data pipeline architecture. This pipeline is responsible for processing orders data, order items data and customer data to ultimately load it into an Azure SQL database. Here's a breakdown of the components and how they work together:

### Data Sources & Storage:

1. Orders Data:  The pipeline starts with order data coming from an external source to ADLS Gen2. This represents the raw, initial data about customer orders. Data will be CSV format
2. Customers Data: This data comes from a pre-existing database, in this case, an Azure SQL database.
3. Order Items Data: The data is coming from external cloud storage service S3 (from AWS) holds the order_items data and landing into ADLS Gen2. Data will be in JSON fromat

### Data Transformation and Processing:

1. Azure Data Factory: This is a cloud-based data integration service that orchestrates data movement and transformation. In this pipeline, it plays a crucial role in:
   - Copying Order Items Data: The data factory is configured to copy order_items data from the S3 bucket to the ADLS Gen2 container. This involves setting up a connection to S3, defining the copy operation, and specifying the destination location in ADLS Gen2.

2. Data Bricks: This is a cloud-based platform for data engineering and analytics. It uses Apache Spark for processing data at scale. Here's how it's used in the pipeline:
   - Data Processing: Data Bricks processes the raw order data and customer data. This involves:
     1.  Data cleaning and transformation.
     2.  Applying business logic (e.g., calculating total order value, grouping items by category).
     3.  Joining order data with customer data for a more comprehensive view.
3. Data Loading: Once the data is processed, it's loaded into the Azure SQL database.

### Data Destination for serving layer: 

1. Azure SQL DB: This is the final destination for the processed data. It's a fully managed relational database service offered by Azure. By
   storing the data in an SQL database, it becomes easily queryable and accessible for reporting and analytics purposes.
   
### Key Points:
1. Data Pipeline: The entire process from data ingestion to loading into the SQL database is orchestrated as a data pipeline. This ensures consistent data flow, handling of changes, and data quality.
   
2. Data Security: Security measures are implemented throughout the pipeline, including secure access control to ADLS Gen2 and the Azure SQL database, S3 Bucket encryption in transit and at rest, and data masking or anonymization where necessary in data.
   
   - Databricks Access Token: Instead of hardcoding the Databricks access token within the Data Factory pipeline or other components, store it securely in Azure Key Vault. The pipeline can then retrieve this token during execution using the Key Vault API.
     
   - Database Credentials: Similarly, store the database connection information (username, password) for the Azure SQL DB in Key Vault. This prevents exposing these sensitive credentials directly in your code.
     
   - Secure Access Credentials: The solution utilizes Azure Key Vault to securely store sensitive credentials such as AWS access keys for accessing the S3 bucket. This eliminates the need to hardcode credentials directly into the code, ensuring a more robust and secure environment.
     
4. Scalability: The pipeline utilizes cloud services like Azure Data Lake Storage and Azure Data Factory, making it highly scalable to handle large volumes of data.
   
6. Orchestration: Azure Data Factory simplifies the orchestration of the entire data pipeline, ensuring that the transformation and loading processes happen in a defined sequence.
   
7. Transformation: Data Bricks allows for sophisticated data transformation logic, enabling data cleaning, aggregation, and feature engineering.
   
8. Monitoring: The Azure Data Factory can be configured to monitor the pipeline activities, including trigger executions, transformation performance, and data loading.

The architecture illustrates a typical process for ingesting raw customer data, transforming it for analysis, and storing it in a database. This approach provides the flexibility and scalability needed for a modern retail analytics pipeline.

## Datasets used
1. Customers: Represents customers who place orders.
2. Orders: Represents individual orders placed by customers.
3. Order Items: Represents the individual items included within an order.

Here is the link to the datasets - https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/tree/main/Datasets

## Data Model
![Data Model](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/ER.png)

This diagram shows a database schema, which describes the structure of a database. The database is about orders, customers, and the items in those orders. Here's a breakdown of the entities and their relationships:

### Entities:

1. Customers: Represents customers who place orders. Includes information like customer ID, first and last name, username, password, address, city, state, and postal code.
   
3. Orders: Represents individual orders placed by customers. Includes information like order ID, order date, customer ID, and order status.
   
4. Order Items: Represents the individual items included within an order. Includes information like order item ID, the order ID it belongs to, the product ID, quantity, subtotal, and product price.
   
### Relationships:

1. Customers and Orders: A customer can place multiple orders (1-to-many relationship). Each order is associated with a single customer.
2. Orders and Order Items: Each order can have multiple items (1-to-many relationship). Each item belongs to a single order.

## Databricks Notebook
[project_source_code](Sales_Project.ipynb)

## Basic Flow for creating this project

Subscription Needed -  Azure & AWS Cloud (Free Trail subscription also works fine)

## Resource Group creation

In Azure, a resource group is a container that holds related resources for an application. It is a logical grouping of resources that can be managed together. Resource groups provide a way to organize and manage resources in Azure, making it easier to perform actions on a group of resources as a single unit.

Creating a Resource Group using Azure Portal

To create a resource group using the Azure portal, follow these steps:

- Step 1: Log in to Azure Portal
  
  Open a web browser and navigate to the Azure portal (https://portal.azure.com). Log in with your Azure account credentials.
  
- Step 2: Click on "Resource groups"
  
  In the Azure portal, click on the "Resource groups" button in the navigation menu.

- Step 3: Click on "New resource group"
  
  Click on the "New resource group" button.

- Step 4: Enter Resource Group Details
  
  In the "Create a resource group" page, enter the following details:

  Resource group name: Enter a unique name for your resource group (e.g., "EcommerceApp").
  
  Subscription: Select the Azure subscription you want to use for this resource group.
  
  Resource group location: Select the location for your resource group (e.g., "West US").
  
  Tags: Optionally, you can add tags to your resource group to categorize and filter resources.
  
- Step 5: Click "Create"
  
  Click the "Create" button to create the resource group.

- Step 6: Verify Resource Group Creation
  Once the resource group is created, you will see it listed in the "Resource groups" page. You can click on the resource group to view its 
  details and add resources to it.
  
A resource group name *retaildbproject* is created as shown.

![Resource Group](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/Resource%20group.png)

## Azure Data Lake Storage (ADLS Gen2) creation:
   
- Step 1: Click on "Storage accounts"

  In the Azure portal, click on the "Storage accounts" button in the navigation menu.

- Step 2: Click on "New storage account"

  Click on the "New storage account" button.

- Step 3: Enter Storage Account Details

  In the "Create a storage account" page, enter the following details:

  1. Storage account name: Enter a unique name for your storage account (e.g., "myadlsgen2").
  2. Subscription: Select the Azure subscription you want to use for this storage account.
  3. Resource group: Select the resource group you created earlier (e.g., "EcommerceApp").
  4. Location: Select the location for your storage account (e.g., "West US").
  5. Performance: Select the performance tier for your storage account (e.g., "Standard").
  6. Account kind: Select "StorageV2" as the account kind.
  7. Hierarchical namespace: Select "Enabled" to enable hierarchical namespace for ADLS Gen2.
     
- Step 4: Click "Review + create"

  Click the "Review + create" button to review your storage account settings.

- Step 5: Click "Create"

  Click the "Create" button to create the storage account.

- Step 6: Verify Storage Account Creation

  Once the storage account is created, you will see it listed in the "Storage accounts" page. You can click on the storage account to view its 
  details and configure additional settings.

  A *retaildbsales* storage account is created. A new container named *sales* is created in which *folders - landing(for uploading order file)*, *order_items (for receiving the order_items from S3 bucket)*, *discarded folder (to store the files having duplication and non valid order_status)*, *customers folder will have customers data file* are created group as shown.

![folders created](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/ADLS_files.png)

 ## Azure SQL Database Creation:
   
- Step 1: Click on "SQL databases"

  In the Azure portal, click on the "SQL databases" button in the navigation menu.

- Step 2: Click on "New SQL Database"

  Click on the "New SQL Database" button.

- Step 3: Enter Database Details

 In the "Create a SQL Database" page, enter the following details:

 1. Database name: Enter the name for your SQL database (e.g., "retaildb").
 2. Subscription: Select the Azure subscription you want to use for this database.
 3. Resource group: Select the resource group you created earlier (e.g., "EcommerceApp").
 4. Server: Create a new server with the name "retaildb-sales". You will need to provide an administrator username and password.
 5. Pricing tier: Select the pricing tier for your database (e.g., "Basic", "Standard", or "Premium").

- Step 4: Click "Review + create"

  Click the "Review + create" button to review your database settings.

- Step 5: Click "Create"

  Click the "Create" button to create the database.

- Step 6: Verify Database Creation

  Once the database is created, you will see it listed in the "SQL databases" page. You can click on the database to view its details and 
  configure additional settings.

  *retaildb* database is created. Two tables *customers & valid_order_status for validating the order_status* are created with SQL code below and the *sales_reporting* table will be auto generated after processing completion in databricks

![data base creation](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/Azure%20sql%20database.png)

SQL Code for creating valid_order_status table

```ruby
create table valid_order_status (status_name varchar(50));
insert into valid_order_status values
('ON_HOLD'),('PAYMENT_REVIEW'),('PROCESSING'),('CLOSED'),('SUSPECTED_FRAUD'),('COMPLETE'),('PENDING'),('CANCELED'),
('PENDING_PAYMENT')
```

SQL Code for creating customer table (*Data will be inserted into table from ADLS Gen2 customers folder having csv file using copy through dta factory*)

```ruby
CREATE TABLE customers (
customer_id INT NOT NULL,
customer_fname VARCHAR(45) NOT NULL,
customer_lname VARCHAR(45) NOT NULL,
customer_email VARCHAR(45) NOT NULL,
customer_password VARCHAR(45) NOT NULL,
customer_street VARCHAR(255) NOT NULL,
customer_city VARCHAR(45) NOT NULL,
customer_state VARCHAR(45) NOT NULL,
customer_zipcode VARCHAR(45) NOT NULL,
PRIMARY KEY (customer_id)
);
```
## Creating Databricks workspace:

- Step 1: Click on "Databricks"

  In the Azure portal, click on the "Databricks" button in the navigation menu.

- Step 2: Click on "New Databricks Workspace"

  Click on the "New Databricks Workspace" button.

- Step 3: Enter Workspace Details

  In the "Create a Databricks Workspace" page, enter the following details:

  1. Workspace name: Enter the name for your Databricks workspace (e.g., "retaidb-sales-databricks").
  2. Subscription: Select the Azure subscription you want to use for this workspace.
  3. Resource group: Select the resource group you created earlier (e.g., "EcommerceApp").
  4. Location: Select the location for your workspace (e.g., "East US").
  5. Pricing tier: Select the pricing tier for your workspace (e.g., "Standard" or "Premium").
     
Step 4: Click "Review + create"

Click the "Review + create" button to review your workspace settings.

Step 5: Click "Create"

Click the "Create" button to create the workspace.

Step 6: Verify Workspace Creation

Once the workspace is created, you will see it listed in the "Databricks" page. You can click on the launch workspace to view its details and configure additional settings.

![Databricks creation](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/Databricks_workspace.png)

## Creation of Data Factory

Step 1: Go to Azure Data Factory Studio

Open a web browser and navigate to the Azure Data Factory Studio.

Step 2: Create a new data factory

In the Azure Data Factory Studio, click on the "Create a new data factory" button.

Step 3: Enter Data Factory Details

In the "Create a data factory" page, enter the following details:

1. Name: Enter retail-sales-df as the name of your data factory.
2. Subscription: Select the Azure subscription you want to use for this data factory.
3. Resource group: Select the resource group you created earlier (e.g., "EcommerceApp").
4. Location: Select the location for your data factory (e.g., "East US").
5. Step 4: Click "Create"

Click the "Create" button to create the data factory.

Step 5: Verify Data Factory Creation

Once the data factory is created, you will see it listed in the "Data factories" page. You can click on the launch data factory to view its details and configure additional settings.

![data factory creation](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/azure-data-factory-launch-studio.png)

## Generation of Access keys and creation S3 bucket in AWS

1. Generate Access Keys:

Step 1: Log in to the AWS Management Console

Go to the AWS website and log in to the AWS Management Console using your AWS account credentials.

Step 2: Navigate to the IAM Dashboard

Click on the "IAM" button in the navigation menu to navigate to the IAM dashboard.

Step 3: Click on "Users"

In the IAM dashboard, click on the "Users" button in the navigation menu.

Step 4: Select the User

Select the user for which you want to generate access keys.

Step 5: Click on "Security Credentials"

Click on the "Security Credentials" tab.

Step 6: Click on "Create Access Key"

Click on the "Create Access Key" button.

Step 7: Download the Access Key File

Download the access key file (.csv) and store it securely.

2. Create an S3 Bucket:

Step 1: Log in to the AWS Management Console

Go to the AWS website and log in to the AWS Management Console using your AWS account credentials.

Step 2: Navigate to the S3 Dashboard

Click on the "S3" button in the navigation menu to navigate to the S3 dashboard.

Step 3: Click on "Create Bucket"

Click on the "Create Bucket" button.

Step 4: Enter Bucket Details

Enter the following details:

Bucket name: Enter a unique name for your S3 bucket.
Region: Select the region where you want to create the bucket.
Bucket settings: Choose the bucket settings as per your requirements.
Step 5: Click "Create Bucket"

Click the "Create Bucket" button to create the S3 bucket.

Step 6: Verify Bucket Creation

Once the bucket is created, you will see it listed in the S3 dashboard. You can click on the bucket to view its details and configure additional settings.

![s3 bucket creation](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/s3_bucket.png)

## Creation of linked service for storage account(ADLS Gen2), Data bricks, Key Vault, S3, Azure SQL Database

 1. Create Linked Service for Storage Account:

Step 1: Go to Azure Data Factory Studio

Open a web browser and navigate to the Azure Data Factory Studio.

Step 2: Click on "Author & Monitor"

Click on the "Author & Monitor" button in the navigation menu.

Step 3: Click on "Connections"

Click on the "Connections" button in the navigation menu.

Step 4: Click on "New"

Click on the "New" button to create a new linked service.

Step 5: Select "Azure Blob Storage"

Select "Azure Blob Storage" as the type of linked service.

Step 6: Enter Storage Account Details

Enter the following details:

Name: Enter a name for your linked service.
Storage account name: Enter the name of your Azure Storage account.
Storage account key: Enter the access key for your Azure Storage account.
Tenant ID: Enter the tenant ID for your Azure Storage account.
Step 7: Click "Create"

Click the "Create" button to create the linked service.

 2. Create Linked Service for Databricks:
   
    a. Generation of access token in data bricks and storing it in key vault
   
     1. Generate Access Token in Databricks:
        
        Step 1: Log in to Databricks
        
        Go to the Databricks website and log in to your Databricks account.

        Step 2: Click on "Settings"

        Click on the "Settings" icon in the top right corner of the Databricks dashboard.

        Step 3: Click on "User Settings"

        Click on the "User Settings" button.

        Step 4: Click on "Access Tokens"

        Click on the "Access Tokens" tab.

        Step 5: Click on "Generate New Token"

        Click on the "Generate New Token" button.

        Step 6: Enter Token Details

        Enter the following details:

        Token name: Enter a name for your access token.
        Token description: Enter a description for your access token.
        Expiration period: Select the expiration period for your access token.

        Step 7: Click "Generate"

        Click the "Generate" button to generate the access token.

   2. Store Access Token in Azure Key Vault:

       Step 1: Log in to Azure Portal

       Go to the Azure portal website and log in to your Azure account.

       Step 2: Navigate to Key Vault

       Navigate to the Key Vault service in the Azure portal.

       Step 3: Select the Key Vault

       Select the Key Vault where you want to store the access token.

       Step 4: Click on "Secrets"

       Click on the "Secrets" button in the navigation menu.

       Step 5: Click on "Generate/Import"

       Click on the "Generate/Import" button.

       Step 6: Enter Secret Details

       Enter the following details:
   
       Secret name: Enter a name for your secret.
       Secret value: Enter the access token generated in Databricks.
       Content type: Select "text" as the content type.

       Step 7: Click "Create"

       Click the "Create" button to create the secret.

4. Store the Key Vault Secret ID in Azure Data Factory:

Step 1: Go to Azure Data Factory Studio

Open a web browser and navigate to the Azure Data Factory Studio.

Step 2: Click on "Author & Monitor"

Click on the "Author & Monitor" button in the navigation menu.

Step 3: Click on "Connections"

Click on the "Connections" button in the navigation menu.

Step 4: Select the Linked Service

Select the linked service for Databricks that you created earlier.

Step 5: Click on "Edit"

Click on the "Edit" button to edit the linked service.

Step 6: Enter Key Vault Secret ID

Enter the Secret ID of the access token stored in Key Vault.

Step 7: Click "Save"

Click the "Save" button to save the changes.

Note: Make sure to replace the placeholders with the actual values for your Databricks access token and Key Vault secret.

3. Linked service for S3

Create Linked Service for S3:

Step 1: Go to Azure Data Factory Studio

Open a web browser and navigate to the Azure Data Factory Studio.

Step 2: Click on "Author & Monitor"

Click on the "Author & Monitor" button in the navigation menu.

Step 3: Click on "Connections"

Click on the "Connections" button in the navigation menu.

Step 4: Click on "New"

Click on the "New" button to create a new linked service.

Step 5: Select "Amazon S3"

Select "Amazon S3" as the type of linked service.

Step 6: Enter S3 Details

Enter the following details:

Name: Enter a name for your linked service.
Service URL: Enter the URL of your S3 bucket.[Dont fill anything]
Access Key ID: Enter the access key ID for your S3 bucket.[use key vault in storing Key id & key]
Secret Access Key: Enter the secret access key for your S3 bucket.
Step 7: Click "Create"

Click the "Create" button to create the linked service.

4. Linked service for Azure SQL Database

Create Linked Service for Azure SQL Database:

Step 1: Go to Azure Data Factory Studio

Open a web browser and navigate to the Azure Data Factory Studio.

Step 2: Click on "Author & Monitor"

Click on the "Author & Monitor" button in the navigation menu.

Step 3: Click on "Connections"

Click on the "Connections" button in the navigation menu.

Step 4: Click on "New"

Click on the "New" button to create a new linked service.

Step 5: Select "Azure SQL Database"

Select "Azure SQL Database" as the type of linked service.

Step 6: Enter Azure SQL Database Details

Enter the following details:

Name: Enter a name for your linked service.
Server name: Enter the server name of your Azure SQL Database.
Database name: Enter the database name of your Azure SQL Database.
Username: Enter the username to connect to your Azure SQL Database.[use key vault to store]
Password: Enter the password to connect to your Azure SQL Database.[use key vault to store]
Step 7: Click "Create"

Click the "Create" button to create the linked service.

![key vault](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/Azure%20Key_vault.png)

![linked services](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/Linked_services.png)

## Creating Data sets in Azure Data Factory

1. Data Set for Order_Items data coming from S3 bucket

Step 1: Create a New Dataset

Log in to your Azure Data Factory instance

Click on the Author & Monitor button

Click on the Create button and select Dataset from the dropdown menu

Select Azure Data Lake Storage Gen2 as the dataset type (since S3 is an S3-compatible storage)

Click Continue

Step 2: Configure the S3 Connection

In the New dataset page, click on the New button next to Linked service

Select Amazon S3 as the linked service type

Enter the following details:

Name: Enter a name for your S3 linked service

Authentication type: Select Access key

Access key ID: Enter your S3 access key ID

Secret access key: Enter your S3 secret access key

Bucket name: Enter the name of your S3 bucket

File path: Enter the path to the JSON file in your S3 bucket (e.g., path/to/your/file.json)
Click Create

Step 3: Configure the JSON Dataset

In the New dataset page, select the S3 linked service you created in Step 2

Enter the following details:

Name: Enter a name for your dataset
File format: Select JSON
Compression type: Select None (or select a compression type if your JSON file is compressed)
JSON settings: Select Single document (or select Array of documents if your JSON file contains an array of documents)
Click Create

Step 4: Validate the Dataset

Click on the Validate button to validate the dataset

ADF will connect to your S3 bucket and validate the JSON file

![linked services](https://github.com/PushpakVootla21/Retail_Data_Engineering_Project/blob/main/Project_Ref_Images/order_items_json_s3_ds.png)

## Developing Logic using Interactive Databricks Cluster

1. Create an interactive cluster in databricks that will execute the databricks notebook.

2. Perform the following in the Databricks Notebook :
   a. Create a Mount Point.
   
   b. Create a Dataframe.
   
   c. Load the orders.csv file into a Dataframe and perform first validation(checking for duplicates order_id in order_status).
   
   d. We need to apply the second validation that is whether the order_status fields in the data are valid or not. To do this we need to make connectivity to Azure SQL DB from our databricks 
      notebook.
   
      Note: Establish a connection with Azure SQL Server from databricks. During this process, a secret scope has to be created so that databricks can access the sql-password which is stored in 
      the key vault.

   ### Creating a secret scope in databricks

   Step 1: Navigate to the Secret Scope Creation Page Navigate to the following URL to create a new secret scope:
   
   https://<your-databricks-instance-url>/#secrets/create

   Replace <your-databricks-instance-url> with the URL of your Databricks instance.

   Step 2: Enter the Secret Scope Name and Azure Key Vault DNS Name Enter a name for your secret scope and the DNS name of your Azure Key Vault.

   The DNS name should be in the format https://<your-key-vault-name>.vault.azure.net/.

   Step 3: Authenticate with Azure Key Vault Authenticate with your Azure Key Vault using the Service Principal or Managed Identity method.

   Step 4: Configure the Secret Scope Configure the secret scope by specifying the Azure Key Vault credentials and the secret name that contains
   the SQL password.

   Step 5: Save the Secret Scope Save the secret scope. Once saved, you can use the secret scope in your Databricks notebooks to access the SQL 
   password stored in the Key Vault.

   e. First Validation Check - If there are any duplicate order_ids. Once the validation is successful, create a Spark Table from Dataframe

    ```ruby
    errorFlg = False
    ordersCount = ordersDf.count()
    distinctOrdersCount = ordersDf.select(‘order_id’).distinct().count()
    
    if ordersCount != distinctOrdersCount
      errorFlg = True
    if errorFlg :
            dbutils.fs.mv(‘/mnt/sales/landing/orders.csv’,’/mnt/sales/discarded’)
            dbutil.notebook.exit(‘{“errorFlg”: “true”, “errorMsg”: “Orderid is repeated”}’)
    ordersDf.createOrReplaceTempView(“orders”)
    ```

    f. Then the second validation(check for valid orders_status) is evaluated.
       For this validation, we need to connect to Azure SQL DB from the databricks notebook. The following details are required for connecting to the SQL DB dbServer
       dbPort
       dbName
       dbUser
       dbPassword
       databricksScope
   ```ruby
      connectionUrl = ‘jdbc:sqlserver://{}.database.windows.net:{};database={};user={};’.format(dbServer, dbPort, dbName, dbUser)
                      dbPassword = dbutils.secrets.get(scope = databricksScope,key=’sql-password’)
      connectionProperties = {‘password’ : dbPassword,‘driver’: ‘com.microsoft.sqlserver.jdbc.SQLServerDriver’}
    ```

   g. Once the second validation is also successful, notebook will exit by giving the following message and the file is moved to the staging folder.

   ```ruby
      Notebook exited: {"errorflag:"false","errorMsg:"All Good"}
   ```


### Creating a Pipeline in Azure Data Factory (Automating the pipeline execution)
    



   


