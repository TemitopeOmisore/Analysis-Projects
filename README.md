# Recruitment Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendation)
- [Limitations](#limitations)
- [References](#references)


### Project Overview

The goal of this data analysis project is to optimize the recruitment process by identifying bottlenecks and improving efficiency at various stages of the hiring pipeline. By leveraging data on candidate pipelines, interview feedback, job postings, and offer statuses, the project aims to enhance time-to-hire metrics and overall hiring success rates.

## The analysis will focus on the following areas:

- Pipeline Analysis: Examine where candidates drop off in the process to identify potential bottlenecks or inefficiencies.
- Time-to-Hire Metrics: Measure the average time candidates spend at each stage of the hiring process to pinpoint delays.
- Job Postings Performance: Evaluate which job postings attract the most candidates and identify postings that require optimization to improve visibility and appeal.
- Offer Outcomes: Analyze factors that influence offer acceptance or rejection to refine strategies for closing offers effectively.

### Data Sources

The primary dataset for this analysis is the “cleaned_job_application.csv” file, which contains detailed information on job applications submitted to the company. This dataset includes variables such as applicant candidate source, job posting title, hiring stages, screening date, interview date, offer date and offer status.

## Tools

- Excel - Data cleaning
- SQL Server - Data Analysis
- PowerBI - Creating Reports

### Data Cleaning

  In the initial data preparation phase, we performed the following tasks:
  1. Data loading and inspection.
  2. Handling missing values.
  3. Data cleaning and formatting.
 
### Exploratory Data Analysis
EDA involved exploring the job applications data to answer the following questions:
- Where are candidates dropping off in the pipeline?
- What is the average time to hire at each stage?
- Which job postings attract the most candidates?
- What factors influence offer acceptance or rejection?

### Data Analysis

````Sql
    /*
Where are candidates dropping off in the pipeline?
This query identifies the hiring stages where candidates are dropping off.
It counts the total number of candidates in each hiring stage.
*/
SELECT hiring_stage, COUNT(candidate_id) AS total_candidates
FROM cleaned_job_applications_data
GROUP BY hiring_stage
ORDER BY total_candidates DESC;


/*
What is the average time to hire at each stage?
*/
SELECT
  AVG(DATEDIFF(DAY, created_at, screening_date)) AS avg_days_to_screening,
  AVG(DATEDIFF(DAY, screening_date, interview_date)) AS avg_days_to_interview,
  AVG(DATEDIFF(DAY, interview_date, offer_date)) AS avg_days_to_offer
FROM cleaned_job_applications_data;


/*
Which job postings attract the most candidates?
*/
SELECT job_posting_title, COUNT(candidate_id) AS candidate_count
FROM cleaned_job_applications_data
GROUP BY job_posting_title
ORDER BY candidate_count DESC;


/*
What factors influence offer rejection?
*/
SELECT rejection_reason, COUNT(candidate_id) AS total_rejections
FROM cleaned_job_applications_data
WHERE offer_status = 'Rejected'
GROUP BY rejection_reason
ORDER BY total_rejections DESC;
```

















