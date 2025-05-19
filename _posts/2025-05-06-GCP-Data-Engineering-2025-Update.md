---
title: GCP Data Engineering 2025 Update
date: 2025-05-06 14:30:00 +0800
categories: [Data Engineering]
tags: [Cloud Data Platform]
---

I’ve been actively keeping up with GCP data technologies since earning my certification in 2019. Over the past two years, the GCP data ecosystem has evolved rapidly, with the introduction of new services and the expansion of existing ones. While these updates add powerful capabilities, they also increase the platform’s complexity—making it more challenging to navigate and master than it once was.

In this blog post, I’ll summarize key components of the current GCP data landscape. To provide context, I’ll occasionally refer to similar tools from other platforms. These references are meant as rough comparisons—not exact equivalents—since each tool has unique behaviors, limitations, and design philosophies. Technology comparisons are rarely apples-to-apples, and small implementation details often matter greatly.

### What’s New and Interesting Compared to 2+ Years Ago?
1. **Dataform** – GCP’s native offering for SQL-based data transformation workflows in BigQuery. Similar in concept to dbt, Dataform allows teams—especially those with strong SQL skills—to manage dependencies, version control, and testing of transformations using SQL without needing to resort to PySpark or Dataflow pipelines. It’s well-suited for ELT-style development within BigQuery.

2. **BigQuery Omni** – A multicloud analytics solution that brings BigQuery’s familiar interface and query engine to data stored in AWS S3 or Azure Blob Storage. Rather than moving data into GCP, Omni runs the queries in-place using Anthos-based infrastructure. This can help reduce egress costs and latency, especially for hybrid cloud and multicloud architectures.

3. **Generative AI Workflows with Gemini in BigQuery** – Gemini has been integrated into the BigQuery UI, offering natural language interaction for data exploration and transformation. Data analysts can use features like “Chat with your data” directly in the BigQuery editor, while data scientists can leverage Gemini for assisted data preparation and code generation. The new Data Canvas also provides a low-code interface to combine structured data workflows with GenAI-powered enhancements.

---

## Overall picture first.. What are the key technologies in GCP Data engineering landscape?

### 1. Data Engineering Tools

- **Dataflow** — Stream/batch data processing (Apache Beam)
- **Pub/Sub** — Messaging and streaming ingestion
- **Dataproc** — Managed Spark and Hadoop
- **Cloud Composer** — Managed Airflow
- **BigQuery EL(T):**
  - `bq cp` — Command-line tool for loading data from Cloud Storage
  - **Dataform** — SQL-based transformations (similar to dbt)
  - **BigQuery Transfer Service** — Zero-code ingestion from supported sources
- **Cloud Data Fusion** — ETL tool (like Azure Data Factory)
- **Dataprep** — UI-based data cleaning (like Azure Data Wrangler)

> Note: Automation can also be achieved using **Cloud Scheduler** (time-based), **Cloud Run**, or **EventArc** (event-based). However, Airflow via Composer supports both triggers natively.

### 2. Data Lakehouse / Warehouse

- **Cloud Storage** — Object storage layer
- **BigQuery** — GCP’s analytics warehouse, Snowflake competitor
  - Deployment: GCP native or BigQuery Omni (on AWS/Azure)
  - **BigLake / External Tables** — Access multicloud data (zero-copy)
    - More: [External Data Source Comparison](https://cloud.google.com/bigquery/docs/external-data-sources#external_data_source_feature_comparison)
  - **BigFrame** — 
    - `bigframes.pandas` (Pandas equivalent)
    - `bigframes.ml` (Scikit-learn equivalent)
  - **GenAI Data Workflows** (Gemini-powered):
    - Data Canvas
    - AI-driven Data Preparation

### 3. Data Governance

- **Dataplex** — Like Microsoft Purview or Collibra
  - Functions:
    - Data Dictionary / Business Glossary
    - Data Lineage / Profiling / Quality Tasks
    - Access Control
  - **Data Catalog** — Also referred to as BigQuery Universal Catalog, part of Dataplex

### 4. Data Sharing

- **Analytics Hub** — For inter-organizational or cross-project data sharing

### 5. Specialized Storage

- **HTAP:** AlloyDB (Hybrid Transaction/Analytical Processing)
- **NoSQL:** Bigtable
- **Vector DB:** AlloyDB + Vector Search

> Note: Cloud SQL, Firestore, and Spanner are OLTP-focused and less common in Data & AI scenarios.

### 6. Data Migration

- **gcloud storage CLI** — Efficient transfer of small/local files
- **Database Migration Service (DMS)** — Relational DB migrations (like AWS DMS)
- **Storage Transfer Service** — Transfers between object/file stores (e.g., HDFS, S3, ADLS)
- **Transfer Appliance** — Large-scale on-prem to cloud data movement
- **Datastream** — Change Data Capture (CDC) for real-time sync to GCS/BigQuery

> Note: All options above can be used for analytical data migration depending on the organization’s needs.

---

## Choosing Dataform (SQL) vs. Spark/Dataflow

| Consideration               | Dataform (SQL-based)                                  | Spark / Dataflow                               |
| --------------------------- | ----------------------------------------------------- | ---------------------------------------------- |
| **Use Case Focus**          | Batch-heavy                                           | Streaming and complex pipelines                |
| **Programming Model**       | SQL (like dbt)                                        | Code (Python, Java, Scala)                     |
| **State Handling**          | Stateless only (requires temp tables/views for state) | Handles stateful processing natively           |
| **Semi-structured Support** | Limited (mostly JSON)                                 | JSON, XML, and more                            |
| **Integration Scope**       | BigQuery only                                         | Multiple sources: GCS, BigQuery, Pub/Sub, etc. |
| **Cost**                    | Lower                                                 | Higher (distributed compute overhead)          |
| **Real-Time Streaming**     | Not designed for it                                   | Designed for streaming use cases               |
| **Error Handling**          | Limited                                               | Advanced error recovery & retries              |

> To get the best of both worlds:

- **Batch:**
  - Ingestion: BigQuery Transfer Service / Data Fusion / DMS / Datastream / Storage Transfer / Spark or Dataflow
  - Staging: GCS → BQ Bronze → BQ Silver → BQ Gold (Dataform)
  - Orchestration: Composer

- **Streaming:**
  - Pub/Sub → Dataflow → BigQuery

---

## How to choose between Spark Dataproc and Dataflow?
GCP recommends Dataflow for new projects. However, market availability of Spark talent makes Dataproc more accessible for many organizations. Evaluate based on team skills and use case complexity.

## Other consideration when architecting your data engineering technology stack
1. **Everything Is a Trade-off**  
   You can’t optimize for scalability, cost-efficiency, and maintainability all at once. Use software architecture quality attributes to clarify and prioritize.

2. **Start Simple, Evolve as Needed**  
   Resist premature optimization. Build iteratively based on feedback and measurable needs.


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
