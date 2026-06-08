# OpenFDA Adverse Event Analysis: Amitriptyline Hydrochloride (2024)

## Project Overview

This project analyzes adverse event reports associated with **Amitriptyline Hydrochloride** using data from the OpenFDA Adverse Event API. The objective is to identify whether specific patient demographics, such as age, sex, and weight, are associated with higher frequencies of reported adverse events.

The analysis is limited to:

* Drug: Amitriptyline Hydrochloride
* Adult patients (Age ≥ 18 years)
* Reports received during 2024

---

## Problem Statement

**Are there particular patient demographics (e.g., age, sex, weight) or combinations that report higher rates of adverse events with Amitriptyline Hydrochloride?**

---

## Data Source

Data was obtained from the OpenFDA Drug Adverse Event API:

https://api.fda.gov/drug/event.json

Query Parameters:

* Medicinal Product: "AMITRIPTYLINE HYDROCHLORIDE"
* Received Date: 2024-01-01 to 2024-12-31
* Result Limit: 500 records

Example Query:

```python
url = "https://api.fda.gov/drug/event.json"

params = {
    "search": 'patient.drug.medicinalproduct:"AMITRIPTYLINE HYDROCHLORIDE" AND receivedate:[20240101 TO 20241231]',
    "limit": 500
}
```

---

## Data Preparation

### Extracted Fields

The following fields were extracted from each report:

* Patient Age
* Age Unit
* Patient Sex
* Patient Weight
* Reported Reactions

### Age Standardization

OpenFDA stores ages using different units. All age values were converted to years using the following mapping:

| Unit Code | Meaning |
| --------- | ------- |
| 800       | Decades |
| 801       | Years   |
| 802       | Months  |
| 803       | Weeks   |
| 804       | Days    |
| 805       | Hours   |

Only adult patients (Age ≥ 18 years) were retained for analysis.

### Data Cleaning

* Converted age and weight fields to numeric values
* Handled missing demographic information
* Mapped sex codes:

  * 1 = Male
  * 2 = Female
  * 0 = Unknown

---

## Exploratory Analysis

The following analyses were performed:

### Age Distribution

* Converted all age values to years.
* Examined the distribution of adult patients.

### Weight Distribution

* Converted weight values to numeric format.
* Generated descriptive statistics.

### Sex Distribution

* Counted reports by patient sex.
* Compared reporting frequency between male and female patients.

### Adverse Reactions

* Extracted reported reaction terms.
* Reviewed commonly reported adverse events.

---

## Findings

1. A total of 500 adverse event reports for Amitriptyline Hydrochloride in 2024 were analyzed due to API result limits.

2. Missing values were present in several demographic fields, including age, sex, and weight, reducing the number of records available for complete demographic analysis.

3. Among reports with available age information, adverse event reports were more frequently observed in older adults, particularly within the 60–74 year age range.

4. Female patients appeared more frequently in the available adverse event reports than male patients.

5. Weight information was incomplete, but available values were primarily concentrated within typical adult weight ranges.

6. Commonly reported adverse events included neurological, gastrointestinal, and psychiatric reactions.

---

## Limitations

* OpenFDA adverse event data is a voluntary reporting system and may contain reporting bias.
* Missing demographic information limits the completeness of the analysis.
* The API query was restricted to 500 records and may not represent all reports submitted during 2024.
* Adverse event reports do not establish causality between the drug and the reported reaction.

---

## Technologies Used

* Python
* Pandas
* Requests
* Jupyter Notebook
---
## Future Improvements

* Implement pagination to retrieve all available records.
* Perform statistical testing across demographic groups.
* Visualize age, sex, and weight distributions using charts.
* Compare adverse event patterns across multiple antidepressants.
* Build predictive models for adverse event reporting trends.