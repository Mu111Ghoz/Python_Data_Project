# The Analysis

## 1. What are the most demanded skills for the Top 3 most popular data roles?

To find the most demanded skills for the Top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles their top skills, showing which skills I should pay attention to depending on the role I am targeting. 

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](2_Skill_Demand.ipynb)


### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1,figsize=(10, 6))

sns.set_theme(style="ticks")

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], palette='dark:b_r', hue='skill_count', orient='h')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].get_legend().remove()  # Remove legend for cleaner look
    ax[i].set_xlim(0, 78)  # Set x-axis limit for better comparison

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v+1, n, f"{v:.0f}%", ha='left', va='center', color='black', fontsize=11, 
                  bbox=dict(facecolor='white', alpha=0.5, edgecolor='none', boxstyle='round,pad=0.2'))
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])  # Set x-ticks for better readability

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
plt.tight_layout(rect=[0, 0.03, 1, 0.95])  # Adjust layout to make room for the title
plt.show()
```

### Results

![Visualization of Top Skills for Data Nerds](images/Likelihood_of_Skills_Requested_in_US_Job_Postings.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most thought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).