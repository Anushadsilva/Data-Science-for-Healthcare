# Nitroglycerin Adverse Event Analysis (FAERS 2024)

## 📊 Project Overview

This project analyzes **adverse event reports associated with Nitroglycerin** using the OpenFDA FAERS (FDA Adverse Event Reporting System) API.

The goal is to determine whether **adverse reaction patterns differ based on the route of drug administration** in adult patients.

---

## ❓ Problem Statement

**Do reported adverse reactions for Nitroglycerin differ based on the medication’s route of administration in adult patients (age ≥ 18) during 2024?**

---

## 📦 Data Source

Data is retrieved from the OpenFDA Drug Event API:

https://api.fda.gov/drug/event.json

### Query Used:

* Drug: Nitroglycerin
* Date range: 2024 (receivedate filter)
* Limit: 600 records

---

## ⚙️ Data Processing Steps

### 1. Data Extraction

* Retrieved FAERS adverse event reports using OpenFDA API
* Extracted:

  * Patient age, sex, weight
  * Drug names
  * Drug administration routes
  * Reported reactions

---

### 2. Data Cleaning

* Converted age to numeric format
* Filtered adult patients (age ≥ 18)
* Removed missing values in key fields
* Normalized drug and reaction lists

---

### 3. Filtering

* Filtered records containing **Nitroglycerin**
* Extracted all associated administration routes
* Exploded nested lists for analysis

---

### 4. Feature Engineering

* Grouped data by:

  * Drug administration route
  * Reported adverse reaction
* Created frequency counts of reactions per route

---

## 📈 Analysis Performed

### 1. Route Distribution

* Identified most common routes of administration for Nitroglycerin

### 2. Reaction Frequency

* Extracted most frequently reported adverse reactions

### 3. Route vs Reaction Relationship

* Built a pivot table:

  * Rows: Drug administration route
  * Columns: Adverse reactions
  * Values: Report counts

---

## 📊 Visualization

A heatmap was generated to visualize the relationship between:

* Drug administration routes
* Reported adverse reactions

### Key Insight:

The heatmap highlights differences in reaction reporting patterns across routes, with certain reactions appearing more frequently for specific administration methods.

---

## 🧠 Key Findings

* Nitroglycerin adverse event reports show variation in reaction frequency based on route of administration.
* Common reactions include cardiovascular and neurological effects such as:

  * Hypotension
  * Headache
  * Dizziness
* Certain routes show stronger association with specific reaction clusters.
* Reporting bias and missing route data may influence results.

---

## ⚠️ Limitations

* FAERS is a **voluntary reporting system**, not a controlled clinical dataset.
* Missing or inconsistent route information exists in many reports.
* No exposure denominator (cannot compute true incidence rates).
* Data reflects reporting frequency, not causal relationships.

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* OpenFDA API

---

## 📌 Conclusion

This analysis demonstrates that adverse event patterns for Nitroglycerin vary by administration route in reported FAERS data. However, results should be interpreted as **reporting trends rather than clinical incidence differences**.

---

## 🚀 Future Work

* Improve route standardization (IV, sublingual, transdermal normalization)
* Expand dataset beyond API limit (pagination)
* Perform statistical significance testing
* Build predictive model for reaction risk by patient profile
