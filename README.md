# NYC Taxi 2024 Data Pipeline Project

An end-to-end Data Engineering pipeline designed to extract, transform, and load (ETL) over **2 Million records** of NYC Yellow Taxi and Taxi Zones data. The pipeline handles format conversion, data cleaning, type casting, and dimensional modeling (Star Schema) to prepare data for analytical insights.

---

## 📌 Architecture Overview

The pipeline follows a modern data warehousing architecture divided into distinct processing layers:

1. **Extraction (Python):** Automatically batch-converts raw `Parquet` files into standardized `CSV` format.
2. **Staging Layer (SSIS):** Ingests the raw CSV data into SQL Server Staging tables (`STG_Yellow_Trips` and `STG_Taxi_Zones`).
3. **Data Cleaning & Transformation (SSIS):** * De-duplication of staging records.
   * Type casting and schema enforcement using `Derived Column` transformation.
   * Business logic validation through `Lookup` transformations.
4. **Production Layer (Data Warehouse):** Populates the final optimized Star Schema (`producation_fact` and `Dim_Zones`) for BI tools like Power BI.

---

## 🛠️ Tech Stack & Tools

* **Programming Language:** Python (Data Format Conversion)
* **ETL Tool:** Microsoft SQL Server Integration Services (SSIS)
* **Database Management:** Microsoft SQL Server (Data Warehouse / Storage)
* **Data Modeling:** Star Schema (Fact & Dimension Tables)

---

## ⚙️ ETL Pipeline Workflow (SSIS Control Flow)

The ETL orchestrator is divided into clean, containerized tasks to ensure modular execution:

* **Staging Container:** Manages the initial landing of data from flat files.
* **Remove Duplicates Stage:** Cleans the staging environment from overlapping records.
* **Change Data Type Container:** Enforces strong typing across data fields before production movement.
* **Data Flow Task (Core Transformation):** Executes lookups, conditional routing, and tracks row counts.

---

## 📊 Data Modeling (Star Schema)

The destination production database is designed using an optimized **Star Schema** to ensure high-performance analytical queries:

* **`Dim_Zones` (Dimension Table):** Stores structural geolocation data including `Borough`, `Zone`, and `service_zone`.
* **`producation_fact` (Fact Table):** Houses transactional metrics such as `total_amount`, `tip_amount`, `fare_amount`, `tolls_amount`, and trip details. Linked via a $1:N$ relationship to the zones dimension.

---

## 🚀 Key Features Implemented

* **Scalability:** Successfully processes and filters over **2,964,624 records** without performance degradation.
* **Data Quality Assurance:** Implemented a robust `Lookup No Match Output` logic to catch and store isolated or non-matching records automatically into a `Stored not matching data` safe-keep table.
* **Auditability:** Leveraged `Row Count` components to log pipeline execution metrics.

---

## 🖼️ Project Gallery & Screenshots

Here is a visual breakdown of the pipeline architecture, SSIS packages, and database components implemented in this project:

### 1. High-Level Architecture
<p align="center">
  <img src="./Docs/NYC Taxi Data Architecture.png" alt="NYC Taxi Data Architecture" width="90%">
</p>

---

### 2. SSIS Pipeline & Packages
<table border="0">
  <tr>
    <td width="50%" align="center">
      <b>Data Pipeline Overview</b><br>
      <img src="./Docs/Data Pipeline.png" alt="Data Pipeline" width="100%">
    </td>
    <td width="50%" align="center">
      <b>Data Type Enforcement</b><br>
      <img src="./Docs/Change data type.png" alt="Change data type" width="100%">
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Lookup & Validation Logic</b><br>
      <img src="./Docs/Lookup data.png" alt="Lookup data" width="100%">
    </td>
    <td width="50%" align="center">
      <b>Final Star Schema Warehouse</b><br>
      <img src="./Docs/Star Schema.png" alt="Star Schema" width="100%">
    </td>
  </tr>
</table>

---

### 3. Power BI & Dashboards

<table border="0">
  <tr>
    <td width="50%" align="center">
      <b>First Report</b><br>
      <img src="./Docs/Dashboard 1.png" alt="Dashboard_1" width="100%">
    </td>
    <td width="50%" align="center">
      <b>Second Report</b><br>
      <img src="./Docs/Dashboard 2.png" alt="Dashboard_2" width="100%">
    </td>
  </tr>
</table>
