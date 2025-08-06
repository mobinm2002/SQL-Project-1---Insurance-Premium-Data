# SQL-Project-1---Insurance-Premium-Data
About dataset: Health Insurance Premium charges based on Gender, BMI and other characteristics

Welcome to my SQL-based data analysis project on health insurance costs. This project explores how demographic and lifestyle factors like
**age**, **BMI**, **smoking habits**, and **region** influence insurance charges. 
The goal is to uncover actuarial insights that help inform **risk segmentation**, **pricing models**, and **underwriting decisions**.

## 📁 Dataset Overview
The dataset contains the following features:

| Column       | Description                                      |
|--------------|--------------------------------------------------|
| `age`        | Age of the policyholder                          |
| `sex`        | Gender of the policyholder                       |
| `bmi`        | Body Mass Index                                  |
| `children`   | Number of children covered under the policy      |
| `smoker`     | Whether the person is a smoker (`yes` or `no`)   |
| `region`     | Residential region in the US                     |
| `charges`    | Medical insurance costs charged to the customer  |


## 🔍 Objectives

- Identify key cost drivers in insurance data.
- Segment risk based on smoking, BMI, and region.
- Evaluate demographic impact on premiums.
- Build insights relevant for actuarial pricing and underwriting.

---

## 🧠 Questions Answered

1. 📌 What is the average insurance charge for smokers vs non-smokers?
2. 📌 Which region has the highest average insurance charge?
3. 📌 What is the average number of children among insured individuals by region?
4. 📌 Identify the top 5 individuals with the highest charges. What common factors do they share?
5. 📌 How do average charges vary across different BMI categories?
6. 📌 Find the average charge per age group (18–25, 26–35, etc.)
7. 📌 Calculate the proportion of smokers in each region.
8. 📌 What is the average charge by gender?
9. 📌 List individuals whose charges are above the average for their region.
10. 📌 Compare average charges for people with children vs. without children.

**Q1.What is the average insurance charge for smokers vs non-smokers?**

SELECT smoker, ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY smoker;

smoker    | average
----------|---------
no        | 8434.27
yes       | 32050.23

Key Finding:
Individuals who smoke incur insurance charges nearly 280% higher than non-smokers (₹32,050 vs ₹8,434 on average).

**Q2.Which region has the highest average insurance charge?**

SELECT region, ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY region\
ORDER BY avg_charges DESC;

**Result**

Region     | Average Charges
-----------|-----------------
Southeast  | ₹14,735.41

Key Finding:
The Southeast region has the highest average insurance charge of ₹14,735.41 among all regions in the dataset.


**Q3. What is the average number of children among insured individuals by region?**
SELECT region, ROUND(AVG(children), 2) AS avg_children\
FROM insurance_data\
GROUP BY region;

**Result**

Region     | Avg Number of Children
-----------|------------------------
Southeast  | 1.05  
Northeast  | 1.05  
Southwest  | 1.14  
Northwest  | 1.15

Key Finding:
The Northwest region has the highest average number of children per insured individual at 1.15, while Southeast and Northeast tie for the lowest at 1.05.


**Q4. Identify the top 5 individuals with the highest charges. What common factors do they share?**
SELECT *\
FROM insurance_data\
ORDER BY charges DESC\
LIMIT 5;

**Result**

age | sex  | bmi | children | smoker | region    | charges
----|------|-----|----------|--------|-----------|---------
18  | male | 23  | 0        | no     | southeast | 1121.87
18  | male | 30  | 0        | no     | southeast | 1131.51
18  | male | 33  | 0        | no     | southeast | 1135.94
18  | male | 34  | 0        | no     | southeast | 1136.40
18  | male | 34  | 0        | no     | southeast | 1137.01

Observation:
All 5 individuals are 18-year-old non-smoking males from the Southeast region, with 0 children, and charges between ₹1121–₹1137.



**Q5. How do average charges vary across different BMI categories?**

SELECT 
  CASE\
    WHEN bmi < 18.5 THEN 'Underweight'\
    WHEN bmi BETWEEN 18.5 AND 24.9 THEN 'Normal'\
    WHEN bmi BETWEEN 25 AND 29.9 THEN 'Overweight'\
    ELSE 'Obese'\
  END AS bmi_category,\
  ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY bmi_category;

**Result**

BMI Category   | Average Charges (₹)
---------------|---------------------
Underweight    |  5,638.03
Normal         | 10,171.33
Overweight     | 11,020.57
Obese          | 15,312.98

Key Finding:

Insurance charges increase consistently with BMI, from ₹5,638 in the underweight category to over ₹15,300 in the obese category — a nearly 3x rise.


**Q6. Find the average charge per age group.**

SELECT \
  CASE \
    WHEN age BETWEEN 18 AND 25 THEN '18–25'\
    WHEN age BETWEEN 26 AND 35 THEN '26–35'\
    WHEN age BETWEEN 36 AND 50 THEN '36–50'\
    ELSE '51+'\
  END AS age_group,\
  ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY age_group\
ORDER BY age_group;

**Result**

Age Group   | Average Charges (₹)
------------|---------------------
18–25       |  9,087.02
26–35       | 10,495.16
36–50       | 14,030.00
51+         | 18,084.99

Key Finding:

Insurance charges increase steadily with age, rising from ₹9,087 in the 18–25 group to ₹18,085 for those aged 51+, effectively doubling across the age spectrum.

**Q7. Calculate the proportion of smokers in each region.**

SELECT region,\
       COUNT(CASE WHEN smoker = 'yes' THEN 1 END) * 1.0 / COUNT(*) AS smoker_ratio\
FROM insurance_data\
GROUP BY region;

**Result**

Region     | Proportion of Smokers
-----------|------------------------
Southwest  | 0.1785  (~17.85%)
Southeast  | 0.2500  (25.00%)
Northwest  | 0.1785  (~17.85%)
Northeast  | 0.2068  (~20.68%)

Key Finding:

The Southeast region has the highest proportion of smokers at 25%, while the Southwest and Northwest are tied for the lowest at 17.85%.


Q8. What is the average charge by gender?

SELECT sex, ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY sex;

**Result**

Gender | Average Charges (₹)
--------|---------------------
Female | 12,569.58  
Male   | 13,956.75  

Key Finding:

On average, males are charged ₹1,387 more than females — about 11% higher.


**Q9. Compare average charges for people with children vs. those without.**
SELECT 
  CASE WHEN children > 0 THEN 'With Children' ELSE 'No Children' END AS child_status,\
  ROUND(AVG(charges), 2) AS avg_charges\
FROM insurance_data\
GROUP BY child_status;

**Result**

| Children Status | Average Charges |
| --------------- | --------------- |
| No Child        | ₹12,365.98      |
| Have Child      | ₹13,949.94      |

Key Insights:
Charges are ~12.8% Higher for people with children:

₹13,949.94 vs ₹12,365.98 . ₹1,584 difference on average.

Reflects additional financial risk taken by the insurer due to family size.

May also include family plans or additional coverage riders.







