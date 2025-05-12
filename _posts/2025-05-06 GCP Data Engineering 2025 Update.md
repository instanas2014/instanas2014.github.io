---
title: GCP Data Engineering 2025 Update
date: 2025-05-06 14:30:00 +0800
categories: [Data Engineering]
tags: [Cloud Data Platform]
---

I have been keeping myself up-to-date on GCP data technology since I first get myself certified on 2019.
Many new features and capability has been added into GCP data technology landscape in these past 2 years and I think it make it actually harder to learn than it used to be.
I will use this blogpost to summarize some of the key features
I will use some other more famous product to help relate them back to what its commonly see in the market, please do not take it as a statement that it is an apple-to-apple the same. its more a "by-and-large similar" reference
History tell me, its hard to compare technology apple-to-apple as it always have some small detail make them different from one to another

---

## Overall picture first.. What are the key technologies in GCP Data engineering landscape?

1. Data Engineering
   1. Dataflow
   2. Pub/Sub
   3. Dataproc (for Spark)
   4. Cloud Composer (aka Airflow) 
   5. Big Query EL(T)
      1.  bq command line ( bq cp) -- for copy data from cloud storage into BQ ,
      2.  Dataform (similar to dbt, handling Transform within BIg Query)
      3.  Big Query Transfer Service (UI based or bq command line or API ) for selected supported source (zero code)
   6. Cloud Data Fusion (similar to Azure Data Factory)
   7. Dataprep (Similar to Azure Data Wrangler)
   
   Note: GCP has proposed other automation options: Cloud Scheduler (Time-based trigger),Cloud Run Or EventArc (for Event Trigger). However, you can do both time-based trigger and event-based trigger in Airflow.
   

2. Data Lakehouse / Warehouse
   1. Cloud Storage
   2. BigQuery - their product to compete with Snowflake
      1. two deployment flavour -- Big Query Omni (on AWS or Azure) and Big Query on GCP
      2. BigLake Table / External Table - for multicloud data storage data access . refer to this link for more details (https://cloud.google.com/bigquery/docs/external-data-sources#external_data_source_feature_comparison) . Be ware of limitation. Zero-copy approach
      3. BigFrame.pandas (Pandas equivalent), BigFrame.ML (Sklearn equivalent)
      4. Gen AI data workflow (powered by Gemini)
         1. Data Canvas
         2. Data Preparation (Essentially Dataform + Gemini)
   

3. Data Governance
   1. Dataplex (similar to Purview or Collibra) - do 4 thing data dictionary, business glossary, data lineage, data profiling
      1. Data Catalog (existing product , its also called Big Query Unversal Catalog.. essentially the same thing)
         1. data dictionary, business glossary
      2. Data Quality
         1. Data Lineage
         2. Data Profiling
         3. Data Quality Task
      3. Access Control
   
4. Data Sharing: Analytics Hub
5. specialized storage
   1. HTAP (Hybrid Transaction Analytica Use Case) - AlloyDB
   2. NoSQL - BigTable
   3. Vector DB - AlloyDB , Vector Search 
   4. Notes: I excluded these storage option as they are OLTP oriented and rarely use in Data and AI use cases, namely : Cloud SQL, Firestore, Spanner

6. Migration to Cloud
   1. gcloud storage command (1TB +100 GBps) - for local small file
   2. Database Migration Service - for application database (similar to AWS DMS)  from database to database
   3. Storage Transfer Service  (in between) - for object store (HDFS, S3, Azure ADLS) , file system
   4. Transfer Appliance (1TB + 100 MBps) for massive move from onprem to cloud, for object store/file system
   5. Datastream - CDC stream to cloud storage or big query -- for ongoing streaming database and keep DB in-sync
   6. Notes: in the context of analytical data migration, all 5 services are possible to be used depends on the company specific context

---
## Key consideration of choose Dataform SQL-based data engineering pattern vs Spark/Dataflow data engineering pattern

| Considerations                    | Dataform (SQL-based)                                                 | Spark/Dataflow                                                                        |
| --------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Organization Use Case Focus**   | a lot more Batch processing heavy use cases                          | a lot more streaming processing use cases                                             |
| **Programming Model**             | SQL-based (similar to dbt)                                           | Code-based (Python, Java, Scala for Spark; Python, Java for Dataflow)                 |  |
| **Data Engineering Complexity**   | ideal for stateless (or you need to use a lot temp table, temp view) | easier for handling stateful data processing                                          |
| **Semi-structured data handling** | can work with json only                                              | can deal with both json and xml                                                       |
| **Integration**                   | Works natively with BigQuery                                         | Works with multiple data sources (e.g., Cloud Storage, BigQuery, Pub/Sub, HDFS, etc.) |
| **Cost**                          | Lower cost                                                           | Higher cost due to distributed compute resources                                      |
| **Real-Time Processing**          | Not designed for real-time streaming                                 | Supports real-time streaming (e.g., via Spark Streaming or Dataflow)                  |
| **Error Handling**                | Limited error handling; relies on BigQuery's error reporting         | Advanced error handling and retry mechanisms                                          |

One way to get the best of both world 
Batch -->
Source Ingestion to BQ or GCS : Big Query Transfer Service / Cloud Data fusion (supported source, SFTP) or DMS/Datastream (RDBMS) or Storage Transfer Service (Object store/file system) or Datastream or Spark/Dataflow (API) 
GCS to BQ Bronze: Big Query Transfer Service
Bronze to Silver: Dataform
Silver to Gold: Dataform
Orchestration: Composer

Streaming --> Pub/Sub , Dataflow, BQ


## How to choose between Spark Dataproc and Dataflow?
GCP recommendation is to go with Dataflow. I think the consideration mainly boils down to talent pool. Definitely,we have a lot more Spark talent in the market vs Dataflow

## Other consideration when architecting your data engineering technology stack
1. It is all about **trade-off**. Commonly, we hear that we want everything scalablity, maintainability , cost ..etc in single solution. The reality is trade off. Especially, when comes to cost. Software Architecture Quality Attribute is the good starting point to list out and make decision around the trade off between different metric
2. Start simple and add complexity as needed.


## Big Query OBT or Star schema?
In its early days, BigQuery promoted the One Big Table (OBT) approach—denormalizing data into a single wide table—to reduce the need for joins and improve query performance. This strategy was also common during the Hadoop era, where distributed systems favored wide, flat data structures for efficiency.

Today, BigQuery offers robust support for star schema modeling, which remains the standard for many analytical and BI use cases. With improvements in join performance, materialized views, and caching mechanisms like BI Engine, star schemas are not only viable but often preferred for their maintainability, scalability, and semantic clarity.

A unique strength of BigQuery is its native support for nested and repeated fields, enabling efficient representation of hierarchical or array-based data structures within a single table. When used effectively, these features can simplify schema design and enhance performance—though they require careful query planning and understanding. For example, power BI does not natively support nested field, which means you will always need to unnest it when bring the data to Power BI

With these advancements, BigQuery stands as a strong competitor to platforms like Databricks and Snowflake, while continuing to offer distinctive capabilities that set it apart in the modern data platform landscape.

https://cloud.google.com/bigquery/docs/migration/schema-data-overview
https://cloud.google.com/bigquery/docs/best-practices-performance-nested


---
## Key learning material
<To be added>
