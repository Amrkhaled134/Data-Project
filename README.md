# Overview

Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from [Luke Barousse's Python Course](https://lukebarousse.com/python) which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

# The Questions

Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 

# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
    - **Pandas Library:** This was used to analyze the data. 
    - **Matplotlib Library:** I visualized the data.
    - **Seaborn Library:** Helped me create more advanced visuals. 
- **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Data Preparation and Cleanup

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

## Import & Clean Up Data

I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Loading Data
df = pd.read_csv(r"C:\Users\SAMA\Downloads\data_jobs.csv")

# Data Cleanup
def clean(skills):
    
    if pd.notna(skills):
        
        return ast.literal_eval(skills)
    
    else :
        
        return skills
    
df['job_skills']=df['job_skills'].apply(clean)  
```
## Filter US Jobs

To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'United States']

```
# The Analysis

Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting. 

View my notebook with detailed steps here: [2_Skill_Demand](2_Skills_demand.ipynb).

### Visualize Data

```python
fig,ax=plt.subplots(len(jobs),1)
sns.set_theme(style='ticks')
for i, job_title in enumerate(jobs):

    df_plot = df_joined[df_joined['job_title_short'] == job_title].head().copy()
    
    sns.barplot(df_plot,
                x='skill_percent',
                y='job_skills',
                hue='skill_percent',
                palette='crest',
                ax=ax[i],
                legend=False)

        # Add percentage labels
    for p in ax[i].patches:
        ax[i].annotate(
            f'{p.get_width():.0f}%',
            (p.get_width(), p.get_y() + p.get_height()/2),
            xytext=(5, 0),
            textcoords='offset points',
            ha='left',
            va='center',
            fontsize=10
        )

    if i!=len(jobs)-1:
        ax[i].set_xticks([])
        
    
    ax[i].set_title(job_title,fontsize=14)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_xlim(0,80)

fig.suptitle(f'Likelihood of Skills Requested in US Job Postings',fontsize=17)    
fig.tight_layout()
'''

### Results
![Likelihood of Skills Requested in US Job Postings](Images\Likelihood_of_Skills_Requested_in_US_Job_Postings.png)

