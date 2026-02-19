# ⚡ Appliances Energy Prediction: Big Data Analytics

This project implements a scalable Big Data solution to predict household energy consumption. By integrating **Apache Spark** for distributed machine learning and **Snowflake** for cloud data warehousing, the system processes high-volume environmental sensor data to forecast energy demand accurately.

---

## 📋 Table of Contents
* [Project Overview](#project-overview)
* [Architecture](#architecture)
* [Technologies Used](#technologies-used)
* [Machine Learning Pipeline](#machine-learning-pipeline)
* [Data Source](#data-source)
* [Setup & Installation](#setup--installation)

---

## 🔍 Project Overview
Predicting energy usage is a cornerstone of smart grid technology. This project analyzes a dataset containing temperature and humidity readings from a wireless sensor network, combined with weather station data, to build predictive models that help optimize energy efficiency in residential buildings.

## 🏗 Architecture
The system utilizes a modern cloud-based Big Data stack:



1.  **Snowflake:** Acts as the primary Cloud Data Warehouse for high-speed data ingestion and structured storage.
2.  **Apache Spark:** Used as the unified analytics engine to perform distributed data processing and model training.
3.  **Databricks:** The collaborative environment used to orchestrate the Spark clusters and Python notebooks.

---

## 🛠 Technologies Used
* **Apache Spark (PySpark):** Distributed computing and Spark SQL.
* **Snowflake:** Cloud-native storage and compute (DWaaS).
* **Spark MLlib:** Distributed Machine Learning library.
* **Python:** Programming language for data transformation and modeling.
* **VectorAssembler:** Spark feature engineering tool for vectorizing input variables.

---

## 🤖 Machine Learning Pipeline
We implemented and compared multiple regression algorithms to identify the best predictor for appliance energy consumption:



* **Linear Regression:** Establishing a statistical baseline.
* **Decision Tree & Random Forest Regressors:** Handling non-linear features and improving accuracy.
* **GBT (Gradient-Boosted Tree) Regressor:** Our high-performance model designed to minimize prediction error through boosting.

### **Evaluation Metrics**
* **Root Mean Squared Error (RMSE):** Measuring the average magnitude of the error.
* **R-squared ($R^2$):** Determining the proportion of variance explained by the model.

---

## 📊 Data Source
The dataset includes:
* **Indoor Sensors:** Temperature and Humidity from 9 different rooms (T1-T9, RH1-RH9).
* **Outdoor Weather:** Pressure, Humidity, Wind speed, and Visibility from a local airport station.
* **Temporal Data:** Time of day and day of the week to capture usage patterns.

---

## 🚀 Setup & Installation

### 1. Snowflake Configuration
Ensure your Snowflake account is set up with a database (`ENERGY_DATA`) and a warehouse. Configure your Spark session with the following connection parameters:
```python
sfOptions = {
  "sfURL": "<account_identifier>.snowflakecomputing.com",
  "sfUser": "<username>",
  "sfPassword": "<password>",
  "sfDatabase": "ENERGY_DATA",
  "sfSchema": "PUBLIC"
}


from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

# Feature vectorization
assembler = VectorAssembler(inputCols=["T1", "RH1", "T_out", "Press_mm_hg"], outputCol="features")

# Model training
gbt = GBTRegressor(labelCol="Appliances", featuresCol="features")
model = gbt.fit(trainingData)
