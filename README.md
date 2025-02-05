# MARKETING CAMPAIGN ANALYSIS 
## Overview
Using the marketing campaign data of 2,240 customers from Maven Analytics. I served as a marketing analyst to analyse customer profiles, identify product preferences, evaluate campaign successes and failures, and assess channel performance. Through this analysis, I uncovered actionable insights that can help optimise marketing strategies, improve customer segmentation, and enhance overall campaign effectiveness.

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



#### Business Questions
    1. Are there any null values or outliers? How will you handle them?
![image](https://github.com/user-attachments/assets/44a0fd57-7f32-4c30-a503-202996621f56)

# Data Preprocessing
##### Removing whitespace from my columns
    df.columns = df.columns.str.replace(' ', '', regex=False)
    
##### Derive Age form Year_birth (this is to know the age range of our customers) 
    df['Age'] = 2025 - df['Year_Birth']

##### Convert the 'JoinDate' column to datetime (to convert the joindate from sting to datetime)
    df['JoinDate'] = pd.to_datetime(df['Dt_Customer'])

##### Calculate the total years since the customer joined (to know how long our customers have been with us- helps to calculate retention rate)
    current_date = pd.Timestamp.now()  # Current date and time
    df['YearsSinceJoined'] = (current_date - df['JoinDate']).dt.days // 365

##### Normalizing the marital status categories (categorizing the data into same classes e.g along as single)
    df.Marital_Status = df.Marital_Status.str.replace('Alone', 'Single', regex=False)
    df.Marital_Status = df.Marital_Status.str.replace('Together', 'Dating', regex=False)
    df.Marital_Status = df.Marital_Status.str.replace('YOLO', 'Single', regex=False)
    df.Marital_Status = df.Marital_Status.str.replace('Absurd', 'Single', regex=False)

##### Normalizing the Education categories (categorizing the data into same classes e.g 2n cycle as masters)
    df.Education = df.Education.str.replace('2n Cycle', 'Masters', regex=False)
    df.Education = df.Education.str.replace('Basic', 'High School', regex=False)
    df.Education = df.Education.str.replace('Masterss', 'Masters', regex=False)
    df.Education = df.Education.str.replace('Graduation', 'Undergraduate', regex=False)

##### Define the custom age ranges (e.g., 29-40, 41-50, etc.) (bining the ages to create a range for analysis)
    bins = [29, 40, 60, 80, float('inf')]  # 'inf' ensures it captures 81 and above
    labels = ['29-40', '41-60', '61-80', '81+']

##### Create a new column for Age Brackets
    df['Age_Category'] = pd.cut(df['Age'], bins=bins, labels=labels, right=True)
    print(df)
    
##### Correlation Analysis - Heatmap of correlations
    numeric_cols = ['Age', 'Income', 'Kidhome', 'Teenhome', 'MntWines', 'MntFruits', 'MntMeatProducts', 'MntFishProducts', 'MntSweetProducts', 'MntGoldProds']
    correlation = df[numeric_cols].corr() 
    plt.figure(figsize=(10, 6))
    sns.heatmap(correlation, annot=True, cmap='coolwarm', fmt=".2f")
    plt.title('Correlation between Demographics and Spending')
    plt.show()
    
### Analysis
### CUSTOMER PURCHASING BEHAVIOUR
   ##### Select the relevant columns for products counts -  Calculate total purchases for each channel
    products = ['MntWines', 
    'MntFruits', 
    'MntMeatProducts', 
    'MntFishProducts', 
    'MntSweetProducts', 
    'MntGoldProds']
    total_products = df[products].sum()

### Which product do customers spend more on/purchase more?
   ##### Plotting the total purchases as a pie chart
      plt.figure(figsize=(8, 8))
      total_products.plot(
          kind='pie', 
          autopct='%1.1f%%',  # Display percentages
          startangle=90,  # Rotate the chart for better readability
          colors=['skyblue', 'orange', 'green', 'purple']  # Custom colours)
      plt.title("Total Purchases by Products", fontsize=14)
      plt.ylabel("")  # Remove the default y-axis label
      plt.tight_layout()
      plt.show()
