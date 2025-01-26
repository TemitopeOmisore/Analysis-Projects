# Recruitment Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
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

```Sql
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

### Results

The analysis results are summarized below:

1. There’s a large drop-off from Applicants to Screening (63.4%) and from Offer to Hire (89.7%), indicating candidates are filtered early, and many offers are declined.
2. The overall average time to hire is 7 days, with approximately 2 days at each stage until the final offer.
3. The job postings with more applicnts are IT Support Specialist (320 applicants), followed by Content Editor (295 applicants), and other remote roles, highlighting the demand for flexible positions.
4. The top reasons for offer rejection are relocation requirements (565 cases), company culture mismatch (540 cases), compensation concerns (538 cases), and better opportunities elsewhere (529 cases).

## PowerBI Visualization

![Dashboard]

![snapshot 1](https://github.com/user-attachments/assets/9a28f2cf-8de1-47bf-8292-c26790eda4ae)


![snapshot 2](https://github.com/user-attachments/assets/cce05beb-bc37-403b-a0f1-41600ab3eaf2)


![snapshot 3](https://github.com/user-attachments/assets/2d0a2b8f-ca7c-40e4-80c9-1defcd137de3)


![snapshot 4](https://github.com/user-attachments/assets/8ae63332-b854-4eeb-8585-20754a40d1ac)



### Recommendations

Based on the analysis, I recommend the following actions to improve your hiring process:

1. Address compensation concerns by benchmarking salaries against industry standards and offering additional benefits like health insurance and bonuses.

2. Revise job descriptions for roles like Junior IT Support Specialist and Sales Specialist to highlight growth opportunities, perks, and work-life balance, making them more appealing to candidates.

3. Ensure candidates clearly understand role expectations, compensation, and company culture during the interview process to reduce late-stage drop-offs and increase offer acceptance rates.

4. Regularly analyze each stage of the hiring pipeline to identify bottlenecks and areas where candidates are dropping off, and make improvements to streamline the process.

### Limitations

In my analysis, even though the timing data for each stage of the recruitment process was missing, key trends in the overall pipeline were still identified. However, the absence of candidate feedback in the data limited the ability to make fully informed decisions about why candidates dropped off or rejected offers. Despite these gaps, the insights that were available still provided valuable guidance for improving the recruitment process.

### References

1. "SQL for Data Analysis” by Cathy Tanimura
2. "Microsoft Excel 365 Bible" by Michael Alexander









