# Identifying EdTech Opportunities in Emerging Markets

## Overview
This project analyzes global education and economic data to uncover potential business opportunities for EdTech companies. By identifying countries with strong economies but low education levels, and countries with rapidly improving education systems, EdTech companies can prioritize market entry, tailor product offerings, and build partnerships with governments to improve learning outcomes and capture market share.

---

## Tools Used
- **SQL** for data cleaning and analysis
- **Tableau** for visualizations

---

## Data Cleaning Process
The cleaning process focused on ensuring data consistency across countries and years. Key steps included:

- Removing duplicate records using **Country + Year** as a composite key.
- Handling missing data:
    - For life expectancy (if needed), **trend-based interpolation** was applied to fill in gaps using the average of the previous and following years.
- Standardizing **country status labels** (developed/developing) to align with official World Bank classifications.
- Performing **data quality checks**, including identifying countries with implausible schooling data (such as 0 years of schooling for multiple years in countries with established education systems).

### Data Quality Issues Example
- The **Republic of Korea** reported 0 years of schooling for certain periods despite its strong education system. These records were excluded from trend analysis to avoid skewing results.

---

## Initial General EDA Summary

### 1. Global Education Trends
- Average global schooling years **increased from 2007 - 2022**, with faster gains in developing countries.
- Developed countries averaged around **14 years of schooling**, while developing countries averaged closer to **10 years**.
- Some countries (e.g., **Kuwait**) showed stalled or declining schooling years, indicating potential education system strain or underreporting.

### 2. Economic Trends
- Average **GDP per capita** grew consistently across most countries, with developed economies maintaining significant advantages over developing ones.
- The correlation between **GDP per capita** and **schooling years** was calculated at **0.41**, showing a moderate positive correlation — wealthier countries tend to have better educational outcomes, though exceptions exist.

---

## Data Quality Observations
- As mentioned, countries such as **the Republic of Korea** reported unreliable schooling data (0 years reported despite advanced education systems).
- Data quality checks also flagged potential **reporting lags** in certain countries where schooling data appeared unchanged for **5+ years**, raising reliability concerns. These records were excluded from rate of change analysis to ensure only active educational progress was measured.

---

## EdTech-Focused Analysis

### Question 1: Which countries have strong economies but low education levels?
This analysis identified **wealthy but undereducated countries**, representing prime targets for **premium EdTech solutions**. The top candidates include:

- **Antigua & Barbuda** and **Equatorial Guinea** — both high-wealth, low-education countries with a clear need for supplementary education platforms.
- **Montenegro, Suriname, and Maldives** — countries with strong economies but still considerable education gaps, making them promising secondary markets.

### Criteria Used
- **Strong Economy:** GDP per capita above **$1,172**.
- **Low Education:** Average schooling below **12.1 years**.

### Query Example
```
SELECT 
    Country,
    AVG(gdp) AS avg_gdp,
    AVG(schooling) AS avg_schooling
FROM 
    world_life_expectancy
GROUP BY 
    Country
HAVING 
    avg_gdp >= 1172 AND avg_schooling <= 12.1
ORDER BY 
    (avg_gdp / avg_schooling) DESC;
```
## Target Countries - Wealthy but Undereducated

### Antigua & Barbuda
- **Average GDP per Capita:** 9,759.25
- **Average Schooling Years:** 8.84
- **Wealth-to-Education Ratio:** 1104.08

### Equatorial Guinea
- **Average GDP per Capita:** 7,902.38
- **Average Schooling Years:** 8.33
- **Wealth-to-Education Ratio:** 948.52

### Montenegro
- **Average GDP per Capita:** 4,676.50
- **Average Schooling Years:** 10.72
- **Wealth-to-Education Ratio:** 436.26

### Suriname
- **Average GDP per Capita:** 4,781.31
- **Average Schooling Years:** 11.83
- **Wealth-to-Education Ratio:** 404.15

### Maldives
- **Average GDP per Capita:** 3,818.38
- **Average Schooling Years:** 12.00
- **Wealth-to-Education Ratio:** 318.20

---

## Analysis
These countries represent potential **premium EdTech markets**. They have the financial capacity to invest in educational tools but still experience clear educational gaps.

---

## Question 2: Which countries are improving their education systems the fastest?
To identify **fast improvers**, we calculated the **average annual increase in schooling years** for each country between **2007 and 2022**. Countries were ranked based on this rate of change, and the **top 10% of countries** (19 out of 193) were selected as leading improvers.

### Query
```
SELECT 
    Country,
    ROUND(MAX(Schooling), 1) - ROUND(MIN(Schooling), 1) AS Schooling_Improvement
FROM 
    world_life_expectancy
GROUP BY 
    Country
ORDER BY 
    Schooling_Improvement DESC;
```
## Top 5 Countries - Fastest Educational Improvement

1. **Montenegro** — 1.01 years per year
2. **Bosnia and Herzegovina** — 0.95 years per year
3. **Antigua and Barbuda** — 0.93 years per year
4. **Timor-Leste** — 0.83 years per year
5. **Micronesia** — 0.78 years per year

These countries are actively investing in **education reform**, making them natural partners for **EdTech companies**. Governments and institutions in these countries are already demonstrating commitment to educational progress, creating strong alignment with EdTech solutions aimed at:

- **Digitizing curricula**
- **Expanding teacher training on digital tools**
- **Supporting localized learning content development**

For EdTech companies, this presents **highly favorable conditions for market entry**, particularly for products and services that align with **national education reform agendas**.  
Countries showing both **rapid educational improvement** and **strong GDP growth** (such as **Antigua and Barbuda**) are especially attractive because they combine **ability to pay** with **clear demand for modern educational solutions**.

---

## Key Insights

### 1. Wealth ≠ Education
Several countries demonstrated **economic strength** but **low educational attainment**, highlighting opportunities to bridge the gap with **premium EdTech products** targeted at middle- and upper-class families seeking **quality supplemental education**.

### 2. Fast Improvers Want Partnerships
Countries rapidly improving their education systems are actively investing in reform — they represent **low-hanging fruit** for **collaborative EdTech pilots**, especially if companies can demonstrate **alignment with government education goals**.

---

## Query
```
WITH 
    stats AS (
        SELECT 
            COUNT(*) AS n,
            SUM(gdp) AS sum_x,
            SUM(schooling) AS sum_y,
            SUM(gdp * schooling) AS sum_xy,
            SUM(gdp * gdp) AS sum_x2,
            SUM(schooling * schooling) AS sum_y2
        FROM 
            world_life_expectancy
    )
SELECT 
    (n * sum_xy - sum_x * sum_y) / 
    (SQRT((n * sum_x2 - sum_x * sum_x) * (n * sum_y2 - sum_y * sum_y))) AS correlation
FROM 
    stats;
```
## Insight

The **correlation** was calculated at **0.41**, indicating a **moderate positive correlation** — wealthier countries tend to have **better education**, but **exceptions exist**, creating **niche opportunities** for targeted EdTech products.

---

## Strategic Recommendations for EdTech Companies

- **Target Wealthy but Undereducated Markets**  
    Focus on **premium-priced learning platforms** in countries that have **financial capacity** but **low educational attainment**. These markets present clear gaps EdTech can help fill.

- **Partner with Fast-Improving Education Systems**  
    Collaborate with **governments and institutions** in countries actively investing in education reform. These partnerships build **credibility** and open doors to **key decision-makers** and networks.

- **Localize Content & Offer Hybrid Delivery Models**  
    Each market has **distinct linguistic, cultural, and infrastructural needs**.  
    Successful EdTech solutions should:

    - **Adapt content to local languages and curricula**
    - **Combine online platforms with teacher training and classroom support**
    - **Align products with national education priorities** for seamless integration into existing systems.

By addressing these areas, EdTech companies can **increase adoption rates** and drive **long-term impact**.

