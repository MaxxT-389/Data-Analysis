# Data-Analysis

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
file_path = "/mnt/data/2016_-_2017_Computer_Science_Report_20250402.csv"
df = pd.read_csv(file_path)

# Missing school names are filled with 'Unknown'
df['School Name'].fillna('Unknown', inplace=True)

# Displays first few rows
print("First few rows of the dataset:")
print(df.head())

# Checks for missing values
print("\nMissing values in dataset:")
print(df.isnull().sum())

# Dataset Info
print("\nDataset Information:")
print(df.info())

# Task 2: Basic Data Analysis
# Computes summary statistics
print("\nBasic Statistics:")
print(df.describe())

# Groups by School and compute mean for CS courses
grouped_data = df.groupby('School Name')[['# of Comp Sci Courses', '# of AP Comp Sci Courses', '# of Full CS Courses', '# of Partial CS Courses']].mean()
print("\nAverage CS Courses per School:")
print(grouped_data)

# Task 3: Data Visualization
plt.figure(figsize=(12, 8))

# Line Chart (Trend in total CS courses per school, ordered by number of courses)
df_sorted = df.sort_values(by='# of Comp Sci Courses', ascending=False)
plt.subplot(2, 2, 1)
sns.lineplot(data=df_sorted, x=df_sorted.index, y='# of Comp Sci Courses')
plt.title("Total CS Courses per School")
plt.xlabel("School Index")
plt.ylabel("# of CS Courses")

# Bar Chart (Comparison of AP CS courses across schools)
plt.subplot(2, 2, 2)
sns.barplot(x=df_sorted['School Name'][:10], y=df_sorted['# of AP Comp Sci Courses'][:10])
plt.title("Top 10 Schools with AP CS Courses")
plt.xticks(rotation=90)
plt.xlabel("School Name")
plt.ylabel("# of AP CS Courses")

# Histogram (Distribution of total CS courses)
plt.subplot(2, 2, 3)
sns.histplot(df['# of Comp Sci Courses'], bins=20, kde=True)
plt.title("Distribution of CS Courses")
plt.xlabel("# of CS Courses")

# Scatter Plot (Relationship between Full and Partial CS Courses)
plt.subplot(2, 2, 4)
sns.scatterplot(x=df['# of Full CS Courses'], y=df['# of Partial CS Courses'])
plt.title("Full vs. Partial CS Courses")
plt.xlabel("# of Full CS Courses")
plt.ylabel("# of Partial CS Courses")

plt.tight_layout()
plt.show()
