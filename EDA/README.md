# Exploratory Data Analysis (EDA) – Global Education Data (2007-2022)

## Project Overview
This exploratory data analysis (EDA) investigates **global education trends** between 2007-2022. Using SQL, I cleaned, transformed, and analyzed data to uncover **countries with the fastest educational improvements, wealth-education correlations, and potential EdTech markets**.

---

## Dataset
- **Source:** `WorldLifeExpectancy.csv`  
- **Key Columns Used:**  
    - `Country`  
    - `Year`  
    - `GDP` (Gross Domestic Product per capita)  
    - `Schooling` (Average years of schooling)

---

## Data Preparation
### Key Cleaning Steps:
Removed rows with null `Schooling` or `GDP`  
Filtered to data from **2007 to 2022**  
Aggregated to **average schooling and GDP per country**  
Created categories (buckets) for GDP and Schooling levels to segment countries

---

## Key Analytical Questions
### Which Wealthy Countries Have Low Schooling Levels?
- **Why it matters:** Wealthy countries with lower-than-expected schooling are prime **premium EdTech targets**.
- **SQL Process:** Calculated average `Schooling` and `GDP` per country, then filtered for high GDP & low schooling.

### Which Countries Improved Their Education Systems the Fastest?
- **Why it matters:** Countries rapidly improving schooling indicate **active government reforms**, creating strong **partnership potential** for EdTech companies.
- **SQL Process:** Calculated **average annual schooling increase** per country between 2007-2022.

### Does Wealth Correlate with Education?
- **Why it matters:** Understanding the relationship between wealth & schooling helps **position pricing strategies** and identify **outliers**.
- **SQL Process:** Used SQL to calculate **Pearson correlation** between GDP & Schooling.

---

## Key Findings
| Insight | Key Result |
|---|---|
| **Premium Market Targets** | Wealthy countries with low schooling include **Antigua & Barbuda**, **Equatorial Guinea**, and **Montenegro**. |
| **Fastest Improvers** | **Montenegro**, **Bosnia & Herzegovina**, and **Timor-Leste** showed the fastest education improvement. |
| **Wealth-Education Correlation** | Correlation of **0.41** – moderate positive correlation (wealthier countries tend to have better education). |

---

## Files in this Folder
| File | Description |
|---|---|
| `SQL_Queries.sql` | All queries used for cleaning, aggregation, and analysis |
| `Original_Dataset.csv` | Raw data file |
| `Processed_Data.csv` | Cleaned and aggregated data ready for visualization |
| `README.md` | This file – explaining process & results |

---

## Next Steps
Insights from this EDA feed directly into the **Tableau Dashboard**, where the findings are visually presented for business stakeholders.

View the next phase in [Dashboard Project](https://github.com/tirop/Global_Education_Analysis/blob/main/Dashboard/README.md)

---

## Contact & Connect
[LinkedIn](https://www.linkedin.com/in/joshuakendagor/) | [Your Email](jtkendagor@gmail.com)

---

## Related Projects
- [Dashboard Project](https://github.com/tirop/Global_Education_Analysis/blob/main/Dashboard/README.md)


