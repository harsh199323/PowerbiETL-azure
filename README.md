# PowerbiETL-azure
Azure power bi report creation for covid data analysis 



Conversation with Gemini
profile picture
Can you analyse below python notebook developed in azure power bi report generation for covid data analysis and write a readme.md file content to post on github. 


[configs = {"fs.azure.account.auth.type": "OAuth",
"fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
"fs.azure.account.oauth2.client.id": "client ID",
"fs.azure.account.oauth2.client.secret": 'Secret Key',
"fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/Directory (tenant) ID/oauth2/token"}


#raw data = bronze data
dbutils.fs.mount(
source = "abfss://bronze-data@datalakeamazonsales.dfs.core.windows.net", # contrainer@storageacc
mount_point = "/mnt/bronze-data",
extra_configs = configs)


#transformed data
dbutils.fs.mount(
source = "abfss://transformed-data@datalakeamazonsales.dfs.core.windows.net", # contrainer@storageacc
mount_point = "/mnt/transformed-data",
extra_configs = configs)


1001|Surveillance|https://info.gesu...|
+-------+--------------------+----------+---------+-----+------------+--------------------+
only showing top 3 rows

admissions_hospital.createOrReplaceTempView("admissions_hospital")
fact_admissions_hosptal = spark.sql("""select country
                                    , indicator
                                    , date_format(date,'yyyyMMdd' ) AS date_key
                                    , value 
                                    ,source
                                    ,url 
                                    from admissions_hospital  """)
fact_admissions_hosptal.show(4)
+-------+--------------------+--------+-----+------------+--------------------+
|country|           indicator|date_key|value|      source|                 url|
+-------+--------------------+--------+-----+------------+--------------------+
|Austria|Daily hospital oc...|20200402| 1057|Surveillance|https://www.sozia...|
|Austria|Daily hospital oc...|20200408| 1096|Surveillance|https://www.sozia...|
|Austria|Daily hospital oc...|20200415| 1001|Surveillance|https://info.gesu...|
|Austria|Daily hospital oc...|20200416|  967|Surveillance|https://www.sozia...|
+-------+--------------------+--------+-----+------------+--------------------+
only showing top 4 rows

fact_admissions_hosptal.write.format("com.databricks.spark.csv").option("header","true").option("delimiter", ",").mode("overwrite").save("/mnt/transformed-data/fact_admissions_hosptal")

] 
Show drafts




























































I'd be glad to create a README.md file based on the provided Python code snippet and insights from the ratings:

COVID-19 Data Analysis for Power BI Report Generation

Introduction

This Python notebook leverages Apache Spark on Azure Databricks to process and transform COVID-19 data for use in Power BI report generation. It demonstrates key steps in the data pipeline, including data mounting, temporary view creation, data transformation, and data saving in a format suitable for Power BI.

Prerequisites

An Azure Databricks workspace configured with Spark and access to Azure Blob Storage
A COVID-19 data source (replace the placeholder URL in the code)
Power BI Desktop or Power BI Service
Instructions

Set Up Azure Databricks:

Create an Azure Databricks workspace.
Configure Spark clusters and ensure access to Azure Blob Storage accounts.
Replace the placeholder values in the configs dictionary with your Azure AD application credentials.
Clone or Download the Notebook:

Clone this repository or download the notebook file.
Run the Notebook:

Open the notebook in Azure Databricks.
Execute the cells in order.
Expected Output

The notebook creates a temporary view named admissions_hospital from the raw data and transforms it into a DataFrame named fact_admissions_hosptal. This DataFrame contains processed columns like date_key and is saved as a CSV file in the transformed data container (/mnt/transformed-data/fact_admissions_hosptal).
