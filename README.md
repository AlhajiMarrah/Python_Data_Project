## Overview

Welcome to my analysis of the data job market, focusing on data analysis roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal opportunities for data analysis.

The data sourced from [Luke Barousse's Python Course](https://youtu.be/wUSDVGivd-8) which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersections of demand and salary in data analytics.

## The Questions

Below are the questions I want to answer in my project:
1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for Data Analysts to learn? (High Demand & High Paying)

## Tools I Used

For my deep dive into the data analysts job market, I harnessed the power of several key tools:
- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights. I also use the following python libraries.

  - **Pandas Library:** This was to analyze the data
  - **Matplotlib Library:** I used this to visualize the data
  - **Seaborn Library:** This helped me create more advanced visuals

- **Jupyter Notebooks:** The tool I used to run my python scripts which let me easily include my notes and analysis
- **Visual Studio Code:** My go-to for executing my python scripts.
- **Git & Github:** Essential for version control and sharing my python code and analysis. ensuring collaboration and teamwork.

## Data Preparation and Cleanup

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

### Import & Clean Up Data

I start by importing the necessary libraries and loading the dataset, followed by initial data cleaning task to ensure usability.

# The Analysis

Each jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here's how I approached each question.

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skill I should pay attention to depending on the role I'm targeting.

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

    plt.show()
```

### Results

![Visualization of top skills for data analysts](images\skills_demand_all_data_roles.png)


### Insights

- Python is versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%). 
- SQL is the most requested skill for Data Analysts and Data Scientists with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specializez technical skills (AWS, AZURE, SPARK) compare to Data Analysts and Data Scientists who are expected to be more proficient in general data management and analysis tools (Excel, Tableau). 

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False,palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results

![Trending top skills for data analysts in the US](images\skills_trend_DA.png)

*Bar graph visualizing for trending top skills for data analysts in the US 2023.*

### Insights

- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around september, surpassing both python and tableau by the end of the year.
- Both python and tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts.
Power BI, while less demanded compared to the other, shows slight upward trend towards the year's end.

## 3. How well do jobs and skills pay for data analysts?

### Salary Analysis for Data Nerds

### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

tick_x = plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')
plt.gca().xaxis.set_major_formatter(tick_x)
plt.show()

```

### Results

![salary distributions for data jobs in the US](images\salary_analysis.png)
*Box plot visualizing salary distributions for the top 6 data job titles*

### Insights

- There's is a significant variation in salary ranges across diffirent job titles. Senior data scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value place on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end on the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more constency in salary with fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Seniro Data Engineer) not only have higher median salaries but also larger diffirences in typical salaries, relfecting greater variances in compensation as responsibilities increase.

## 4. Highest paid & most demand skills for Data Analyst.

### Visualize Data

```python
fig, ax = plt.subplots(2, 1)

sns.set_theme(style='ticks')

# Top 10 Highest Paid Skills for Data Analyst
sns.barplot(data=df_DA_top_pay.head(10), x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')

#Top 10 Most In-Demand Skills for Data Analyst
sns.barplot(data=df_DA_skills.head(10), x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')

plt.show()

```

## Results

Here's the breakdown of the highest-paid in-demand skills for data analysts in the US

![The highest paid & most in-demand skills for data analysts in the US](images\top_10_paid_skills.png)

*Two seperate bar graphs visualizing the highest paid & most in_demand skills for data analysts in the US.*

## Insights

- The top graph shows specialized technical skills like `dplyr`, `bitbucket`, `gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical profiency can increase earning potential.

- The bottom graph highlights that foundational skills like `Excel`, `PowerPoint`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data Analysts aiming to maximize their career potential should consider developing a diverse skills that includes both high-paying specialized skills and widely demanded foundational skills. 

## 5. What is the most optimal skill to learn for Data Analyst?

#### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pylot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show

```

### Results

![Most optimal skills for Data Analysts in the US](images\most_optimal_skills_for_data_analysts_in_the_US_with_coloring_by_technology.png)

*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

### Insights

- The scatter plot shows that most of the `programming` skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefit within the data analytics field.

- Analyst tools (colored orange), including tableau and Power Bi, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also verstile across diffirent types of data tasks.

- The database skills (colored green), such as oracle and SQL server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.

## What I Learned

Through out this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in python, especially in data manipulation and visualization. Here are few specific things that I learned:

- **Advanced Python Usage:** Utilizing librabries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization and other libraries helped me perform complex data analysis task more efficiently.
- **Data Cleaning Importance:** I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
- **Strategic Skill Analysis:** The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.

### Insights

This project provided several general insights into the data job market for analysts:

- **Skill Demand and Salary Correlation:** There is a clear correlation between the demand and specific skills and salaries these skills command. Advanced and specialized skills like Python and Oracle can lead to higher salaries.
- **Market Trends:** There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
- **Economic Value of Skills:** Understanding which skills are both in-demand and well-compensated can guide data analysts prioritize learning and maximize their economic return.

## Challenges I Faced

This project was not without its chanllenges, but it provided good learning opportunities:

- **Data Inconsistencies:** Handling missing or inconsistent data entries requires careful consideration and thorough analyst's techniques to ensure the integrity of the analysis.
- **Complex Data Visualization:** Designing effective visual representations of complex datasets was challenging in conveying insights clearly and compellingly.
- **Balancing Breadth and Depth:** Deciding how deeply to dive into each analysis while maintaining a broad over landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

## Concluion

This exploration into the data analyst job market has been incredebly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a foundation for future explorations and underscores the importance of continues learning and adaptation in the data field.