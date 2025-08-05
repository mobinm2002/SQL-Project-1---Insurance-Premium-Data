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

SELECT region, ROUND(AVG(charges), 2) AS avg_charges
FROM insurance_data
GROUP BY region
ORDER BY avg_charges DESC;

Q3. What is the average number of children among insured individuals by region?
SELECT region, ROUND(AVG(children), 2) AS avg_children
FROM insurance_data
GROUP BY region;

Q4. Identify the top 5 individuals with the highest charges. What common factors do they share?
SELECT *
FROM insurance_data
ORDER BY charges DESC
LIMIT 5;

Q5. How do average charges vary across different BMI categories?

SELECT 
  CASE 
    WHEN bmi < 18.5 THEN 'Underweight'
    WHEN bmi BETWEEN 18.5 AND 24.9 THEN 'Normal'
    WHEN bmi BETWEEN 25 AND 29.9 THEN 'Overweight'
    ELSE 'Obese'
  END AS bmi_category,
  ROUND(AVG(charges), 2) AS avg_charges
FROM insurance_data
GROUP BY bmi_category;

Q6. Find the average charge per age group.

SELECT 
  CASE 
    WHEN age BETWEEN 18 AND 25 THEN '18–25'
    WHEN age BETWEEN 26 AND 35 THEN '26–35'
    WHEN age BETWEEN 36 AND 50 THEN '36–50'
    ELSE '51+'
  END AS age_group,
  ROUND(AVG(charges), 2) AS avg_charges
FROM insurance_data
GROUP BY age_group
ORDER BY age_group;

Q7. Calculate the proportion of smokers in each region.

SELECT region,
       COUNT(CASE WHEN smoker = 'yes' THEN 1 END) * 1.0 / COUNT(*) AS smoker_ratio
FROM insurance_data
GROUP BY region;

Q8. What is the average charge by gender?

SELECT sex, ROUND(AVG(charges), 2) AS avg_charges
FROM insurance_data
GROUP BY sex;

Q9. List individuals with charges above the regional average.

SELECT *
FROM insurance_data AS a
WHERE charges > (
    SELECT AVG(charges)
    FROM insurance_data AS b
    WHERE a.region = b.region
);

Q10. Compare average charges for people with children vs. those without.
SELECT 
  CASE WHEN children > 0 THEN 'With Children' ELSE 'No Children' END AS child_status,
  ROUND(AVG(charges), 2) AS avg_charges
FROM insurance_data
GROUP BY child_status;




