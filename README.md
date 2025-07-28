# 🛠️ ETL Data Pipeline with Apache Airflow (BashOperator)

## 📘 Project Scenario

You are a data engineer at a data analytics consulting company. You have been assigned to a project that aims to **de-congest the national highways** by analyzing the road traffic data from different toll plazas. Each highway is operated by a different toll operator with a different IT setup using different file formats.  

Your job is to **collect data available in multiple formats and consolidate it into a single file** for further processing and analysis.

---

## 📝 Objectives

In this project, you will create a **shell script using Bash commands** to:

- Extract data from a CSV file  
- Extract data from a TSV file  
- Extract data from a fixed-width file  
- Transform the data  
- Load the transformed data into a new CSV file  

You will then create an **Apache Airflow DAG** to call the shell script and automate the ETL process.

---

## 📦 Dataset

The dataset used in this project can be downloaded using the `wget` command:

```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0250EN-SkillsNetwork/labs/Final%20Assignment/tolldata.tgz
```

> 💡 Make sure to download the dataset to your Airflow DAGs folder (e.g. `/home/airflow/dags`) and use `sudo` if required.

---

## 🗺 Directions

### 🔹 Task 1.1 - Define DAG Arguments

Define the DAG arguments as follows:

| Parameter         | Value                   |
|------------------|-------------------------|
| `owner`          | *any dummy name*        |
| `start_date`     | today                   |
| `email`          | *any dummy email*       |
| `email_on_failure` | True                 |
| `email_on_retry` | True                    |
| `retries`        | 1                       |
| `retry_delay`    | 5 minutes               |

---

### 🔹 Task 1.2 - Define the DAG

| Parameter     | Value                      |
|---------------|----------------------------|
| `dag_id`      | ETL_toll_data              |
| `schedule`    | Daily once                 |
| `default_args`| As defined above           |
| `description` | Apache Airflow Project     |

---

### 🔹 Task 1.3 - Create Shell Script: `Extract_Transform_data.sh`

- Unzip the `tolldata.tgz` archive using `tar`
- Read the `fileformats.txt` file to understand column structure

---

### 🔹 Task 1.4 - Extract Data from CSV

Extract the following fields from `vehicle-data.csv`:
- Rowid  
- Timestamp  
- Anonymized Vehicle Number  
- Vehicle Type  

Save output to `csv_data.csv`

---

### 🔹 Task 1.5 - Extract Data from TSV

Extract the following fields from `tollplaza-data.tsv`:
- Number of Axles  
- Tollplaza ID  
- Tollplaza Code  

Save output to `tsv_data.csv`

---

### 🔹 Task 1.6 - Extract Data from Fixed-width File

Extract the following fields from `payment-data.txt`:
- Type of Payment Code  
- Vehicle Code  

Save output to `fixed_width_data.csv`

---

### 🔹 Task 1.7 - Consolidate Extracted Data

Merge the extracted files into one:
```
paste csv_data.csv tsv_data.csv fixed_width_data.csv > extracted_data.csv
```

Fields order in `extracted_data.csv`:
1. Rowid  
2. Timestamp  
3. Anonymized Vehicle Number  
4. Vehicle Type  
5. Number of Axles  
6. Tollplaza ID  
7. Tollplaza Code  
8. Type of Payment Code  
9. Vehicle Code

---

### 🔹 Task 1.8 - Transform the Data

Transform the `vehicle_type` column in `extracted_data.csv` into **uppercase** and save the result to `staging/transformed_data.csv` using:
```
tr '[a-z]' '[A-Z]'
```

---

### 🔹 Task 1.9 - Create the DAG

- Create a Python DAG file: `ETL_toll_data.py`  
- Use `BashOperator` to call `Extract_Transform_data.sh` from your DAG  
- Define a task named `extract_transform_load` that links to the script  
- Set up the task pipeline accordingly

---

## 📂 Folder Structure

```
.
├── dags/
│   ├── ETL_toll_data.py              # Airflow DAG
│   ├── Extract_Transform_data.sh     # Shell script with ETL logic
│   ├── tolldata.tgz                  # Raw data archive (downloaded)
│   └── staging/
│       └── transformed_data.csv      # Final output
```

---

## ✅ Outcome

This project demonstrates how to:

- Create a reusable Bash-based ETL pipeline
- Automate the workflow using Apache Airflow
- Process multiple data formats into a single structured dataset

---

## 🚀 Reach/Follow Me

- [LinkedIn]([(https://www.linkedin.com/in/hasmikmargaryan/)])

---

## 👩‍💻 Author

**Hasmik Margaryan**  
*Data Engineer | Data Science*
