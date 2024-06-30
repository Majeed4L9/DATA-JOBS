# The Analysis

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