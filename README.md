# Overview

Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for Data Analysts.

The data sourced from [Luke Barousse's Python Course](https://youtu.be/wUSDVGivd-8?si=D1XtcYGplEhBkbkH) which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in Data Analytics.

# The Questions
Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for Data Analysts to learn?
(High Demand AND High Paying)

# Tools I Used

For my deep dive into the Data Analyst job market, I harnessed the power of several key tools:

- **Python**: The backbone of my analysis, allowing me to analyze the data and find critical insights.
  - **Pandas Library**: The Python library used to analyze the data.
  - **Matplotlib Library**: The library I used to visualize my data.
  - **Seaborn Library**: The library I used to create more advanced visuals.

- **Jupyter Notebooks**: The tool I used to run my Python scripts, which let me easily include my notes and analysis.
- **Visual Studio Code**: My go-to IDE for accessing/editing my Python scripts.
- **Git & GitHub**: Essential for version control and sharing my Python code and projects, ensuring collaboration.

# Data Preparation and Cleanup

This section outlines the steps taken to preapare the data for analysis, ensuring accuracy and usability.

## Import & Clean Up Data

I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

```python
#Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import ast 

#Loading Data
raw_data = pd.read_csv(r'C:\Users\MAJEED\Desktop\APPS\data_jobs.csv')
df = raw_data.copy()

#Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df.dropna(subset = ['job_skills'], inplace = True)
def clean_list(skill_clean):
    return ast.literal_eval(skill_clean)
df['job_skills'] = df['job_skills'].apply(clean_list)

```

## Filter US Jobs
To focus my anlysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'United States']

```

# The Analysis

Each jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here's how I approached each question:

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my notebook with detailed steps here: [Skills_count.ipynb](PROJECT_1\2_Skills_count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(1, len(job_titles), figsize=(9, 6))

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='job_skills', y='skill_percent', ax=ax[i], palette='dark:b')
    
plt.show()
```

### Results

![Visualization of Top Skills for Data Nerds](PROJECT_1\Images\skilll_demand_all_data_roles.png)
*Bar graph visualizing the top skills for Data Nerds in the US.*

### Insights 

- Python is a versatile skill, highly demanded across all three roles, but most prominent for Data Scientists (82%) and Data Engineers (68%).
- SQL is the most requested skill for Data Analysts and Data Engineers, with it in over half the job postings for both roles. For Data Scientists, SQL is the most sought-after skill, appearing in 58% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tool (Excel, Tableau).

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

sns.lineplot(data = df_plot, dashes = False, palette = 'tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals = 0))

plt.show()

```

### Results

![Trending Top Skills for Data Analysts in the US](PROJECT_1\Images\skill_trend_DA.png)
*Line graph visualizing the trending top skills for Data Analysts in the US in 2023.*

### Insights:
- SQL is consistently the most in-demand skill throughout the year, with the highest likelihood of being requested in job postings. It consistently remains above 50%.
- Excel follows SQL as the second most sought-after skill. Proficiency in Excel remains valuable for data analysts.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for Data Analysts
- SAS remains relatively stable throughout the year, with a slight increase around April, then dips back to 20% in June. It maintains a presence among the top skills for data analysts.
- Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

#### Visualize Data 

```python
sns.boxplot(data = df_US_top6, x = 'salary_year_avg', y = 'job_title_short', order = job_order)

plt.gca().xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))

plt.show()

```

#### Results

![Salary Distribution of Data Jobs in the US](PROJECT_1\Images\salary_anlysis_DA.png)
*Box plot visualizing the salary distribution for the top 6 data job titles.*

#### Insights
- There is a significant variations in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600k, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with their fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles(Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

### Highest Paid & Most Demanded Skills for Data Analysts

#### Visualize Data

```python

fig, ax = plt.subplots(1,2, figsize = (10,6))

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data = df_DA_top_pay, y = 'median', x = df_DA_top_pay.index, ax = ax[0], palette = 'dark:b')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data = df_DA_skills, y = 'median', x = df_DA_skills.index, ax = ax[1], palette = 'light:b_r')

plt.show()

```

#### Results

Here's the breakdown of the highest paid and most demanded skills for Data Analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](PROJECT_1\Images\Highest_Paid_and_Most_In_Demand_Skills_for_Data_Analysts_in_the_US.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for Data Analysts in the US.*

#### Insights:

- The first graph shows specialized technical skills like `dplyr`, `Bitbucket`, and `Gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.

- The second graph highlights that foundational skills like `Excel`, `PowerPoint`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data Analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

## 4. What is the most optimal skill to learn for Data Analysts?

#### Visualize Data

```python
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

sns.scatterplot(data = df_plot, x = 'skill_percent', y = 'median_salary', hue = 'technology')

adjust_text(texts, arrowprops = dict(arrowstyle = '->', color = 'gray'))
    
plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
plt.gca().xaxis.set_major_formatter(PercentFormatter(decimals = 0))

plt.show()

```

#### Results

![Most Optimal Skills for Data Analysts in the US](PROJECT_1\Images\Most_Optimal_Skills.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

#### Insights
- The scatter plot shows that most of the `programming` skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the Data analytics field.

- Analyst tools (colored orange), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and Data analysis software are crucial for current data roles. This category not only has good salaries but it is also versatile across different types of data tasks.

- The database skills (colored green and red), such as SQL server and Oracle, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.

# What I learned

Throughout this project, I deepened my understanding of the Data Analyst job market and enhanced my techical skills in Python, especially in data manipulation and visualization. Here are few specific things I learned:

- **Advanced Python Usage:** Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
- **Data Cleaning Importance:** I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
- **Strategic Skill Analysis:** The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.

# Insights

This project provided several insights into the data job market for analysts:

- **Skill Demand and Salary Correlation:** There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skills like Python and Oracle often lead to higher salaries
- **Market Trends:** There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
- **Economic Value of Skills:** Understanding which skills are both in-demand and well-compensated can guide data analysts in priortizing learning to maximize their econmomic returns

# Challenges I Faced

This project was not without its challenges, but it provided good learning opportunities:

- **Data Inconsistencies:** Handling missing or inconsistent data entries requires careful consideration and thorough techniques to ensure the integrity of the analysis.
- **Complex Data Visualization:** Designing effective visual representations of complex datasets was challenging, conveying insights clearly and compellingly.
- **Balancing Breadth and Depth:** Deciding how deeply to dive into each analysis while maintaining a broad overview of the landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

# Conclusion
This exploration into the Data Analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field. 