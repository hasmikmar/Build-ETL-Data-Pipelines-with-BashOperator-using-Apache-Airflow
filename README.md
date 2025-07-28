# 🛠️ ETL Data Pipeline with Apache Airflow (BashOperator)

## 📘 Project Scenario

You are a data engineer at a data analytics consulting company. You have been assigned a project to **decongest the national highways** by analyzing the road traffic data from different toll plazas. Each highway is operated by a different toll operator with a different IT setup that uses various file formats.

Your job is to **collect toll data available in multiple formats and consolidate it into a single structured dataset** for analysis.

---

## 🎯 Objectives

In this assignment, I developed an **Apache Airflow DAG** that will:

- Extract data from a `.csv` file  
- Extract data from a `.tsv` file  
- Extract data from a **fixed-width text** file  
- Consolidate all extracted data  
- Transform a specific column (vehicle type) to uppercase  
- Load the final result into a staging area

---

## 🔧 Tools & Technologies

- Apache Airflow  
- BashOperator  
- Shell commands: `cut`, `awk`, `paste`, `tr`, `tar`  
- Linux environment  
- Python  

---

## ⚙️ DAG Tasks Overview

The pipeline is implemented in a DAG named **`ETL_toll_data`**, and it runs **daily**.

### 1. `unzip_data`
Unzips a compressed `.tar.gz` file containing raw toll data files.

### 2. `extract_data_from_csv`
Extracts the following fields from `vehicle-data.csv`:
- Rowid  
- Timestamp  
- Anonymized Vehicle Number  
- Vehicle Type  

Saves result to `csv_data.csv`.

### 3. `extract_data_from_tsv`
Extracts the following fields from `tollplaza-data.tsv`:
- Number of Axles  
- Toll Plaza ID  
- Toll Plaza Code  

Saves result to `tsv_data.csv`.

### 4. `extract_data_from_fixed_width`
Extracts the following fields from `payment-data.txt`:
- Type of Payment Code  
- Vehicle Code  

Saves result to `fixed_width_data.csv`.

### 5. `consolidate_data`
Combines all extracted data files (`csv_data.csv`, `tsv_data.csv`, `fixed_width_data.csv`) into a single file called `extracted_data.csv`.  
Used `paste` command to merge files column-wise.

### 6. `transform_data`
Converts the `vehicle_type` field in `extracted_data.csv` to **uppercase** using `tr`, and saves the output to `transformed_data.csv`.

---

## 🧱 DAG Structure

The tasks follow a linear dependency chain:

```
unzip_data
   ↓
extract_data_from_csv
   ↓
extract_data_from_tsv
   ↓
extract_data_from_fixed_width
   ↓
consolidate_data
   ↓
transform_data
```

---

## 📂 Folder Structure

```
.
├── ETL_toll_data.py           # Main Airflow DAG file
├── data/                      # Raw input files (csv, tsv, fixed-width)
└── output/                    # Extracted and transformed CSVs
```

---

## ✅ Outcome

By building this ETL pipeline, I demonstrated how to:
- Automate data ingestion and transformation across inconsistent formats  
- Use BashOperator in Apache Airflow to execute shell-based processing  
- Design a clear, modular, and maintainable DAG

---

## 👩‍💻 Author

**Hasmik Margaryan**  
*Data Engineer | Data Science *
