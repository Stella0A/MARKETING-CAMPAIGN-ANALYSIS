# MARKETING CAMPAIGN ANALYSIS 
## Overview
I served as a marketing analyst for a marketing campaign comprising data for 2,240 customers of Maven Marketing. My responsibilities included analysing customer profiles, identifying product preferences, evaluating campaign successes and failures, and assessing channel performance. Through this analysis, I uncovered actionable insights that helped optimise marketing strategies, improve customer segmentation, and enhance overall campaign effectiveness.

## Tools Used for Analysis
- Python
- Numpy 
- Pandas 
- Seaborn
- Matplotlib

## Recommended Analysis
1. Are there any null values or outliers? How will you handle them?
2. What factors are significantly related to the number of web purchases?
3. Which marketing campaign was the most successful?
4. What does the average customer look like?
5. Which products are performing best?
6. Which channels are underperforming?
#### IMPORT RELEVANT LIBRARIES
    import numpy as np
    import pandas as pd
    import seaborn as sns
    import matplotlib.pyplot as plt

#### LOAD DATA
    df = pd.read_csv(r"C:\Users\STELLA\OneDrive - University of Bradford\Desktop\DATA SCIENCE\PERSONAL PROJECTS\Project Marketing Campaign Analysis\marketing_data.csv")

#### Viewing the data
    df.head()
![image](https://github.com/user-attachments/assets/37b04c76-7ecd-4a37-8fc7-aab7996bc3b8)
![image](https://github.com/user-attachments/assets/fb29644a-865e-4f34-bd03-19e96d4d24b2)

#### Viewing the shape of the data
    df.shape
    (2240, 28)

#### Descriptive Analysis
    df.describe()
    ![image](https://github.com/user-attachments/assets/f9ac9fdc-a356-4c0a-a1fb-582d0510f243)

  
