# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my notebook with detailed steps here: [Skills_count.ipynb](PROJECT_1\Skills_count.ipynb)

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

### Insights 

- Python is a versatile skill, highly demanded across all three roles, but most prominent for Data Scientists (82%) and Data Engineers (68%).
- SQL is the most requested skill for Data Analysts and Data Engineers, with it in over half the job postings for both roles. For Data Scientists, SQL is the most sought-after skill, appearing in 58% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tool (Excel, Tableau). 