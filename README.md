# Project Unified Retail: How I Solved Data Consolidation for an FMCG Merger

[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=Databricks&logoColor=white)](https://community.cloud.databricks.com/)  [![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apache-spark&logoColor=white)](https://spark.apache.org/)  [![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)  [![AWS S3](https://img.shields.io/badge/Amazon_S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)](https://aws.amazon.com/s3/) 

## 🎯 The Challenge: Two Companies, Two Messy Data Systems
I decided to tackle a real-world industry headache: **Mergers and Acquisitions (M&A)**. 

Imagine a massive retail giant acquires a smaller competitor. On Day 1, the executives want to see "Total Global Sales," but the data is a mess—different currencies, conflicting product IDs, and siloed storage. To solve this, I built an end-to-end Lakehouse solution on **Databricks** that unifies these two worlds into one clean, "AI-ready" source of truth! 

---

## 🏗️ My Solution: The Medallion Architecture
To make the data flow smoothly from "raw" to "ready," I implemented a **Medallion Architecture**. This ensures that even if the source data changes or has errors, the final dashboard stays accurate. 

### The Visual Workflow 
Here is the high-level ETL pipeline I designed within Databricks to handle the data movement:

![ETL Pipeline](dashboards/ETL%20Pipeline.png)

### The Tech Stack I Used:
* **Engine:** Databricks (Free Community Edition) & Apache Spark 
* **Storage:** Amazon S3 (as the landing zone) 
* **Languages:** PySpark for complex logic and Spark SQL for data modeling 
* **AI/BI:** Databricks SQL & Genie for natural language insights 

---

## ⚙️ How I Built the Pipeline

### 1. The Ingestion Stage (Bronze)
First, I set up a connection to **Amazon S3** to ingest raw files from both the "Acquiring" and "Acquired" companies. I used Delta Lake here to ensure I had a reliable record of exactly what came in. 

### 2. The Refinement Stage (Silver)
This is where the heavy lifting happened! I wrote transformation logic to:
* Standardize different currency formats 
* Deduplicate customer records that appeared in both systems 
* Map disparate product categories into a single hierarchy 

### 3. The Analytics Stage (Gold)
Finally, I modeled the data into **Fact and Dimension tables**. I optimized these using features like Z-Ordering so that the charts load instantly even with millions of rows! 

---

## 📊 The Results: From Data to Decisions
Once the pipeline was running, I built a BI Dashboard to show the combined health of the new, larger company. 

![BI Dashboard](dashboards/Sales%20Insight%20Dashboard.png)

**The "Cool" Part:** I integrated **Databricks Genie**. This means instead of waiting for a Data Engineer to write a SQL query, a business user can just type: *"Show me the top-selling product from the newly acquired stores"*—and the AI generates the answer from my Gold layer! 

---

## 💡 What I Learned
Through this project, I gained hands-on experience in:
* Translating a complex business problem (M&A) into a technical pipeline 
* Managing data quality boundaries using **Bronze -> Silver -> Gold** logic 
* Optimizing Spark jobs to run efficiently on limited resources 
* Democratizing data by using AI tools like Genie to bridge the gap between "Code" and "Business" 

---

## 📂 Repository Structure
```text
.
├── code
│   ├── 1_setup/                      # Initial config and storage mounts
│   ├── 2_dimension_data_processing/  # ETL logic for product/store dimensions
│   └── 3_fact_data_processing/       # ETL logic for sales fact data
├── dashboards/                       # Visualizations and Pipeline screenshots
└── README.md
