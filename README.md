## 📌 Introduction

Dive into the **data job market**! This project zooms in on **Data Analyst roles**, exploring:

- 💰 **Top-paying jobs**  
- 🔥 **In-demand skills**  
- 📈 Where **salary potential** meets **skill demand**

🔍 **SQL queries** for the full analysis live in the [`project_sql/`](./project_sql) folder.

## 🧠 Background

This project was created as part of a **SQL course** to explore key questions in the Data Analyst job landscape:

- **Highest-paying roles**: Identify where top salaries lie  
- **Required skills**: Discover what skills employers value most  
- **In-demand skills**: Highlight the tools and technologies most frequently requested  
- **Salary impact**: Analyze which skills correlate with higher pay  
- **Optimal skills to learn**: Combine demand and salary insights for career focus

🗂️ The dataset includes job titles, locations, salaries, and associated skills—providing a comprehensive view of the market.

## 🛠️ Tools & Languages Used

- **SQL**: Core query language for data extraction, aggregation, and analysis  
- **PostgreSQL**: Relational database engine hosting the job postings dataset  
- **Visual Studio Code**: IDE for writing and running SQL scripts with extensions (e.g., SQLTools)  
- **Git & GitHub**: Version control for tracking changes, collaborating, and publishing code  

## 🔍 Analysis

Each query dives into a different angle of the remote Data Analyst landscape. Below is a concise walkthrough of the questions, SQL logic, and key findings.

---

### 1. Top Paying Data Analyst Jobs
To identify the highest-paying roles, I filtered data analyst positions by average yearly salary and location, focusing on remote jobs. This query highlights the high paying opportunities in the field.

```sql
SELECT	
	job_id,
	job_title,
	job_location,
	job_schedule_type,
	salary_year_avg,
	job_posted_date,
    name AS company_name
FROM
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'Anywhere' AND 
    salary_year_avg IS NOT NULL
ORDER BY
    salary_year_avg DESC
LIMIT 10;
```
Here's the breakdown of the top data analyst jobs in 2023:
- **Wide Salary Range:** Top 10 paying data analyst roles span from $184,000 to $650,000, indicating significant salary potential in the field.
- **Diverse Employers:** Companies like SmartAsset, Meta, and AT&T are among those offering high salaries, showing a broad interest across different industries.
- **Job Title Variety:** There's a high diversity in job titles, from Data Analyst to Director of Analytics, reflecting varied roles and specializations within data analytics.

### 2. Skills for Top Paying Jobs
To understand what skills are required for the top-paying jobs, I joined the job postings with the skills data, providing insights into what employers value for high-compensation roles.
```sql
WITH top_paying_jobs AS (
    SELECT	
        job_id,
        job_title,
        salary_year_avg,
        name AS company_name
    FROM
        job_postings_fact
    LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
    WHERE
        job_title_short = 'Data Analyst' AND 
        job_location = 'Anywhere' AND 
        salary_year_avg IS NOT NULL
    ORDER BY
        salary_year_avg DESC
    LIMIT 10
)

SELECT 
    top_paying_jobs.*,
    skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
    salary_year_avg DESC;
```
Here's the breakdown of the most demanded skills for the top 10 highest paying data analyst jobs in 2023:
- **SQL** is leading with a bold count of 8.
- **Python** follows closely with a bold count of 7.
- **Tableau** is also highly sought after, with a bold count of 6.
Other skills like **R**, **Snowflake**, **Pandas**, and **Excel** show varying degrees of demand.

### 3. In-Demand Skills for Data Analysts

This query helped identify the skills most frequently requested in job postings, directing focus to areas with high demand.

```sql
SELECT 
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' 
    AND job_work_from_home = True 
GROUP BY
    skills
ORDER BY
    demand_count DESC
LIMIT 5;
```
Here's the breakdown of the most demanded skills for data analysts in 2023
- **SQL** and **Excel** remain fundamental, emphasizing the need for strong foundational skills in data processing and spreadsheet manipulation.
- **Programming** and **Visualization Tools** like **Python**, **Tableau**, and **Power BI** are essential, pointing towards the increasing importance of technical skills in data storytelling and decision support.

| Skills   | Demand Count |
|----------|--------------|
| SQL      | 7291         |
| Excel    | 4611         |
| Python   | 4330         |
| Tableau  | 3745         |
| Power BI | 2609         |

*Table of the demand for the top 5 skills in data analyst job postings*

## 📘 What I Learned

- 🧩 **Advanced SQL Crafting**: Built complex queries using `JOIN`, `WITH`, `GROUP BY`, `HAVING` and `CTE querries`to answer real-world questions  
- 📊 **Data Aggregation & Analysis**: Leveraged aggregate functions (`COUNT()`, `AVG()`) to quantify demand and salary trends  
- 💡 **Translating Business Needs**: Converted project requirements into actionable analytical queries and clear insights  
- 🔄 **Version Control Workflow**: Strengthened Git & GitHub skills—initializing repos, committing changes, and managing remote pushes  
- 🚀 **Visualization Integration**: Prepared data for charts and tables, enhancing the readability of results in documentation  

## ✅ Conclusion 

- 🎯 **Key Takeaways**  
  - Top-paying and in-demand roles both highlight the importance of **SQL**, **Python**, and **cloud/big-data tools**.  
  - Specialized skills (e.g., **PySpark**, **Snowflake**, **Airflow**) command premium salaries.  
  - Core tools (Excel, Tableau, Power BI) remain essential for broad market opportunities.

- 🚀 **Career Implications**  
  - Focus on mastering **high-ROI skills** that blend demand and salary potential.  
  - Build real projects showcasing both analytical and engineering capabilities.

- 🔗 **Next Steps**  
  - Explore the [project_sql/](./project_sql/) folder for full query details.b 
  - ⭐ Star & fork this repo to track updates or contribute your own analyses!

> Thank you for exploring this project—happy analyzing! 👩‍💻👨‍💻  
