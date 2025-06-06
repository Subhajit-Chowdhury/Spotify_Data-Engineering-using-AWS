<h1 align="center">🎧 Turning Spotify Data into Insights: Building a Modern Data Pipeline on AWS 🚀</h1>

<p align="center">
  <img src="https://img.shields.io/badge/AWS%20Glue-ETL%20Pipeline-orange?logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/S3-Data%20Storage-blue?logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Athena-Query%20Engine-yellow?logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/QuickSight-Data%20Visualization-informational?logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-Data%20Processing-green?logo=python&logoColor=white" />
  </p>


## 📌 Project Overview

This project demonstrates a **modern, end-to-end data pipeline** using AWS services with Spotify data. It simulates how a sample dataset from Spotify can be ingested, processed, queried, and visualized, leveraging:

- **AWS S3** for storing raw and transformed data
- **AWS Glue** for building scalable ETL jobs (using Python)
- **AWS Athena** for serverless querying of large datasets
- **AWS QuickSight** for intuitive and powerful dashboarding

The focus is on utilizing **serverless** and **pay-as-you-go AWS services** to minimize cost and maximize scalability — an ideal approach for real-world Data Engineering pipelines.


## ⚙️ Tech Stack & Tools

| Tool/Service     | Purpose                          |
|------------------|----------------------------------|
| AWS S3           | Raw & curated zone for data lake |
| AWS Glue         | ETL jobs to clean/transform data |
| AWS Athena       | Querying data with SQL           |
| AWS QuickSight   | Interactive dashboards & charts  |
| Python           | Automation & scripting           |

---

## 📊 Key Features

- 🔄 **Automated ETL Pipeline** with AWS Glue (PySpark script)
- 🧹 **Data Cleaning & Transformation** from raw Spotify JSON
- 📁 **Raw + Curated Zone Architecture** on S3
- 🕵️‍♂️ **Schema-on-Read** via Athena
- 📈 **Comprehensive Dashboard** using QuickSight
- 🔒 **Fully serverless** for scalability and cost-efficiency


## 📸 QuickSight Dashboard


> ![Dashboard](QuickSightDashboard.jpg)


## 📝 Introduction
Ever wondered what stories your Spotify listening habits could tell? This project transforms raw Spotify data into powerful insights. We'll construct a modern data pipeline on AWS, using S3 for robust storage, Glue for smart data processing, Athena for querying our music universe, and finally, QuickSight to bring those musical stories to life through vibrant visualizations. Get ready to unlock the power of your playlists!

## 🏗️ Project Architecture
The overall architecture illustrates the flow of data from ingestion to visualization using integrated AWS services:

![Project Architecture](Spot_DE.drawio.png) 

## 🌊 Pipeline Flow & Data Journey
The data engineering pipeline processes Spotify data through the following key stages:

1.  **📥 Ingestion & Raw Storage (Amazon S3):**
    *   Raw Spotify data (e.g., CSV files for Albums, Artists, Tracks) is ingested and stored in a designated **Amazon S3** bucket, serving as the "raw zone" of the data lake.

2.  **⚙️ ETL Processing (AWS Glue):**
    *   An **AWS Glue ETL job** (developed using the AWS Glue Visual ETL interface and detailed in the Python script) extracts data from the raw S3 locations.
    *   It performs essential transformations such as:
        *   Joining datasets (e.g., Albums with Artists, then with Tracks).
        *   Cleaning data (e.g., dropping unnecessary fields, handling nulls).
        *   Structuring data for analytics.
    *   The detailed visual workflow for this Glue job is shown below:

    ![AWS Glue ETL Job Diagram](GLUE_ETL.jpg)
    *Figure: The AWS Glue job graph showing S3 data sources (Albums, Artists, Tracks), join operations, the 'DropFields' transformation, and the final S3 data target.*

    *   The transformed and curated data is then loaded into a different **Amazon S3** bucket/prefix, designated as the "data warehouse zone."

3.  **🗺️ Schema Discovery & Cataloging (AWS Glue Crawler):**
    *   An **AWS Glue Crawler** runs against the S3 data warehouse zone.
    *   It infers the schema of the processed data and creates/updates table definitions in the **AWS Glue Data Catalog**.

4.  **🔍 Querying & Analysis (Amazon Athena):**
    *   **Amazon Athena** utilizes metadata from the AWS Glue Data Catalog to execute standard SQL queries directly on the data stored in the S3 data warehouse zone.
    *   This enables ad-hoc analysis and data exploration without the need to load data into a traditional database. Query results can also be saved back to S3.

5.  **📊 Visualization & Reporting (Amazon QuickSight):**
    *   **Amazon QuickSight** connects to Amazon Athena as its data source.
    *   It fetches query results to build interactive dashboards, reports, and visualizations, facilitating valuable insights 💡 into the Spotify data.

## 🎨 AWS Glue Studio Interface
The ETL jobs are developed and managed within the AWS Glue Studio environment, which provides a comprehensive visual interface for designing and monitoring data integration workflows.

![AWS Glue Visual ETL interface for Spotify Project](AWS_Glue.jpg) 

*Figure: The AWS Glue console displaying the "Spotify Project." The "Visual" tab shows the ETL job graph, and the left-hand navigation provides access to various Glue features.*

## 🐍✨ Core ETL Script (`Spotify Project.py`)
The engine driving the data transformation in this project is the Python script `Spotify Project.py`. This script is designed for execution as an **AWS Glue ETL job**, leveraging the capabilities of PySpark for efficient, distributed data processing.

**🔗 Script Location:**
*   Access the complete script here:
    [`Spotify Project.py`](https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/Spotify%20Project.py)

**🚀 Core Responsibilities & Functionality:**
This script translates the visual ETL design into executable code, performing the following critical operations:

1.  **🎬 Initialization:** Establishes the Spark and AWS Glue execution environment.
2.  **📥 Data Extraction (Extract):** Reads `albums.csv`, `artists.csv`, and `tracks.csv` from S3.
3.  **🛠️ Data Transformation (Transform):** Executes joins, cleaning, and structuring of the data.
4.  **💾 Data Loading (Load):** Writes the final, unified dataset to the S3 data warehouse zone, typically in Parquet format.

**💻 Technologies Leveraged within the Script:**
*   **Python (🐍):** Primary language for ETL logic.
*   **PySpark (✨):** Framework for distributed data processing.
*   **AWS Glue Libraries:** For seamless integration with the Glue environment (`GlueContext`, `DynamicFrame`).

**💡 Execution Note:** This script is intended for deployment as an AWS Glue ETL job, requiring proper IAM permissions and S3 path configurations.

## 🧾 Dataset Utilized
This project uses a modified version of the "Spotify Dataset 2023," structured into three separate CSV files for processing. The original dataset is dedicated to the public domain.

### 🔗 Original Source & Inspiration
*   **Platform:** Kaggle
*   **Dataset Name:** Spotify Dataset 2023
*   **Uploader:** Tony Gordon Jr.
*   **Kaggle Link:** [https://www.kaggle.com/datasets/tonygordonjr/spotify-dataset-2023](https://www.kaggle.com/datasets/tonygordonjr/spotify-dataset-2023)
*   **License:** **CC0: Public Domain** (The creator has waived all copyright and related rights to this work.)

### 📂 Project Dataset Structure
The dataset for this project is organized into the following three CSV files, ingested into the `raw/` S3 zone:

1.  **💿 `albums.csv`:** Information on Spotify albums.
    *   **Source File:** [`data/albums.csv`](https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/data/albums.csv)
    *   *(Key columns: `album_id`, `name`, `release_date`, `total_tracks`, `artists_id_array`)*
2.  **🎤 `artists.csv`:** Details about Spotify artists.
    *   **Source File:** [`data/artists.csv`](https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/data/artists.csv)
    *   *(Key columns: `artist_id`, `name`, `genres`, `popularity`)*
3.  **🎶 `tracks.csv`:** Attributes for individual Spotify tracks.
    *   **Source File:** [`data/tracks.csv`](https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/data/tracks.csv)
    *   *(Key columns: `track_id`, `name`, `album_id`, `artists_id_array`, `duration_ms`, `explicit`, `popularity`)*

**Note:** Inspect files via GitHub links for full column details. These are joined in AWS Glue.

## 🚀 Project Demonstrations
To provide a clearer understanding of the project's components and workflow in action, short video demonstrations have been recorded:

*   **AWS Glue - ETL Process:**
    *   🎬 **Watch Demo:** [https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/AWS%20GLUE%20Overview.mp4]
    *   *Description:* Showcases AWS Glue job execution and data transformation.
*   **Amazon Athena - Querying Data:**
    *   🔍 **Watch Demo:** [https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/Athena%20Overview.mp4]
    *   *Description:* Demonstrates querying processed data in S3 using Athena.
*   **Amazon QuickSight - Data Visualization:**
    *   📊 **Watch Demo:** [https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/blob/main/QuickSight_Dashboard.mp4]
    *   *Description:* Walkthrough of the interactive QuickSight dashboard.

## 📈 QuickSight Dashboard - Spotify Insights
The culmination of this data pipeline is an interactive dashboard built in Amazon QuickSight, providing insights into the Spotify dataset.

**Key Visualizations Uncover:**
*   How album popularity is distributed across the music catalog!
*   Which artists command the highest track counts based on their popularity!
*   The ebb and flow of track releases across different eras!

**Dashboard Snapshot:**

![QuickSight Dashboard - Overview](QS_Dash.png) 
*(Caption: Overview of the main Spotify analytics dashboard, revealing interesting patterns in your music world!)*


## ⚙️ How to Run / Setup (High-Level)
To replicate this project, you would typically follow these steps:

1.  **Prerequisites:**
    *   An AWS Account with appropriate permissions.
    *   Download the Spotify dataset from Kaggle and split it into `albums.csv`, `artists.csv`, and `tracks.csv`.
2.  **S3 Setup:**
    *   Create S3 buckets for different zones: `your-raw-bucket`, `your-staging-bucket`, `your-datawarehouse-bucket`, `your-athena-query-results-bucket`.
    *   Upload the raw CSV files to the `your-raw-bucket`.
3.  **AWS Glue Setup:**
    *   Create an AWS Glue ETL job, providing the `Spotify Project.py` script.
    *   Configure the job with appropriate IAM roles, data source paths (pointing to raw S3 data), and data target paths (pointing to the S3 data warehouse zone).
    *   Create an AWS Glue Crawler to scan the S3 data warehouse zone and populate the Glue Data Catalog.
4.  **Amazon Athena Setup:**
    *   Ensure a database is created in Athena (the Crawler usually handles this).
    *   Verify that tables corresponding to your processed data are available and queryable.
5.  **Amazon QuickSight Setup:**
    *   Connect QuickSight to Athena as a data source.
    *   Create a new dataset in QuickSight based on your Athena table(s).
    *   Build your dashboard using the created dataset.
6.  **IAM Roles & Permissions:** Ensure all services (Glue, Athena, QuickSight) have the necessary IAM permissions to access S3 and other required resources.

*(This is a high-level guide. Specific configurations might vary.)*

## 🙏 Acknowledgements & Educational Foundation
The development of this project was significantly informed and inspired by the invaluable educational content from the **DateWithData** YouTube channel. Their comprehensive playlists and practical demonstrations provided a strong foundation and clear learning path for building modern data pipelines.

Explore their excellent resources for further learning:

*   📺 **YouTube Channel:** [DateWithData](https://www.youtube.com/@datewithdata123)
*   📚 **Relevant Playlist:** [Real-Time DE Project: AWS to Snowflake](https://www.youtube.com/watch?v=BMp8j6lM6Qg&list=PLRRQG4QYcyEUXmIZQr_bty7sFtp3SLOiP)

Sincere gratitude to the DateWithData team for generously sharing their expertise and fostering learning within the data engineering community.

## 🏁 Conclusion
This project successfully demonstrates the construction of an **end-to-end, serverless data engineering pipeline** on AWS for Spotify data analytics. By ingesting raw data, performing robust ETL transformations with AWS Glue and PySpark, enabling ad-hoc querying with Amazon Athena, and delivering insights through Amazon QuickSight, we've showcased a practical approach to turning data into valuable knowledge. This pipeline not only provides a framework for analyzing music trends but also serves as a testament to the power and flexibility of cloud-based data solutions.

## 📜 License
This project is licensed under the [MIT License](LICENSE). Please see the `LICENSE` file for more details.
The dataset used is under the CC0: Public Domain license, as specified by its Kaggle source.

## 🤝 Contributing
Contributions, issues, and feature requests are welcome!  
Feel free to check the [issues page](https://github.com/Subhajit-Chowdhury/Spotify_Data-Engineering-using-AWS/issues) or submit a PR.


## 🛠 How to Use This Project

1. **Fork/Clone the Repo**
2. Replace with your own Spotify JSON export or streaming history
3. Upload it to your own AWS S3 bucket
4. Deploy the Glue ETL script (from `/scripts/`)
5. Run Athena queries from provided notebook
6. Connect QuickSight to Athena and build your dashboard!


## 💡 Learning Outcomes

- Build and deploy your own **modern data lake**
- Understand **AWS Glue, S3, Athena, and QuickSight**
- Learn how to design **ETL pipelines** for analytics
- Practice **serverless architecture** and data modeling


## 📬 Contact

Created with ❤️ by [Subhajit Chowdhury](https://github.com/Subhajit-Chowdhury)  
📧 Email: *er.subhajitchowdhury@gmail.com*  
🔗 LinkedIn: [@subhajit-chowdhury](https://www.linkedin.com/in/subhajitch0wdhury/)


⭐️ **Give this repo a star** if it helped you learn something new!
