# # Drug Side Effects Analysis

Exploratory data analysis of a 2,931-drug dataset from Drugs.com, focused on cleaning, encoding, and uncovering patterns across medical conditions, drug classes, and reported side effects.

## Overview

This project cleans and analyzes a real-world pharmaceutical dataset to answer three questions:
- Which medical conditions have the most drugs associated with them?
- Which side effects are most frequently reported across all drugs?
- Are there measurable associations between drug attributes (condition, class, prescription status, pregnancy category, alcohol interaction) once encoded numerically?

## Dataset

- **Source:** `drugs_side_effects_drugs_com.csv` (Drugs.com side-effects dataset)
- **Size:** 2,931 rows × 17 columns
- **Key fields:** `drug_name`, `medical_condition`, `side_effects`, `generic_name`, `drug_classes`, `brand_names`, `activity`, `rx_otc`, `pregnancy_category`, `csa`, `alcohol`, `related_drugs`, `rating`, `no_of_reviews`

## Data Cleaning & Preparation

- Converted `rating` and `no_of_reviews` to numeric types (coercing invalid entries)
- Parsed `activity` from a percentage string into a numeric float
- Handled missing values contextually per column:
  - `alcohol`: missing → assumed no interaction (`0`), `'X'` → interaction present (`1`)
  - `side_effects`, `related_drugs`, `generic_name`, `drug_classes`: missing → labeled `'Unknown'`
  - `rating`, `no_of_reviews`: missing → filled with `0`
  - `rx_otc`, `pregnancy_category`: missing → labeled `'Unknown'`
- **Reduced total missing values by 83%** (7,439 → 1,247) through the imputation steps above
- Verified zero duplicate rows

## Feature Engineering & Encoding

- Label-encoded categorical fields (`csa`, `rx_otc`, `generic_name`, `medical_condition`, `pregnancy_category`, `side_effects`) for correlation analysis
- Standardized encoded features (mean 0, standard deviation 1) using `StandardScaler` so no single column dominates the correlation heatmap due to scale
- Split multi-value fields (`side_effects` on `;`, `drug_classes` on `,`) to count individual occurrences rather than treating combined strings as single categories
- Engineered boolean flag columns for specific side effects (Hives, Difficult Breathing, Itching) and drug classes (Upper Respiratory Combinations, Topical Steroids) for targeted analysis

## Key Findings

**Top medical conditions by drug count:**
| Condition | Drug Count |
| Pain | 264 |
| Colds & Flu | 245 |
| Acne | 238 |
| Hypertension | 177 |
| Osteoarthritis | 129 |

**Most frequently reported side effects** (individual mentions after splitting multi-value entries):
| Side Effect | Mentions |
| Hives | 1,788 |
| Difficult breathing | 1,130 |
| Difficulty breathing | 450 |
| Itching | 275 |
| Light-headedness / feeling faint | 272 |

**Top drug classes by frequency:**
| Drug Class | Count |
|---|---|
| Upper respiratory combinations | 245 |
| Topical acne agents | 125 |
| Topical steroids | 94 |
| Antihistamines | 82 |

A correlation heatmap of the encoded, standardized features was generated to explore associations between condition, drug class, prescription status, and pregnancy category — noting that since most inputs are label-encoded categories rather than continuous variables, these values reflect association patterns in the encoding rather than strict linear relationships.

## Tech Stack

- **Language:** Python
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Plotly, Scikit-learn (`LabelEncoder`, `StandardScaler`)
- **Environment:** Google Colab / Jupyter Notebook

## Project Structure

```
├── drugs_side_effects_drugs_com.csv     # Raw dataset
├── drug_sideeffects_project.ipynb       # Full analysis notebook
├── medical_condition_counts.csv         # Exported frequency table
├── side_effect_counts.csv               # Exported frequency table
├── drug_classes_counts.csv              # Exported frequency table
└── README.md

## Author

**Kesar Gautam**
[GitHub](https://github.com/Stats-With-Kesar) · [LinkedIn](https://linkedin.com/in/kesar2105)
