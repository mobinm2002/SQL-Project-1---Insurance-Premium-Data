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



smoker    | average
----------|---------
no        | 8434.27
yes       | 32050.23

Key Finding:
Individuals who smoke incur insurance charges nearly 280% higher than non-smokers (₹32,050 vs ₹8,434 on average).

**Q2.Which region has the highest average insurance charge?**




