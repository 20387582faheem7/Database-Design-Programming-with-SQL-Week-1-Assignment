# Database-Design-Programming-with-SQL-Week-1-Assignment
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load and explore the dataset
try:
    data = pd.read_csv("your_dataset.csv")  # Replace with actual file path
    print("Dataset loaded successfully.")
except FileNotFoundError:
    print("Error: The specified file could not be found.")
    exit()

# Display basic dataset details
print("\nFirst five rows of the dataset:")
print(data.head())

print("\nDataset Overview:")
print(data.info())

print("\nMissing Values Count:")
print(data.isnull().sum())

# Handle missing values (if any)
data.fillna(data.mean(), inplace=True)

# Perform basic statistical analysis
print("\nStatistical Summary:")
print(data.describe())

# Grouping data (Example: Compute mean based on a categorical column)
if "CategoryColumn" in data.columns:
    category_mean = data.groupby("CategoryColumn")["NumericalColumn"].mean()
    print("\nAverage values grouped by category:")
    print(category_mean)

# Set visualization style
sns.set(style="whitegrid")

# Line Plot: Time-Series Trend Analysis
if "DateColumn" in data.columns and "ValueColumn" in data.columns:
    data["DateColumn"] = pd.to_datetime(data["DateColumn"])
    data.sort_values("DateColumn", inplace=True)
    plt.figure(figsize=(10, 5))
    plt.plot(data["DateColumn"], data["ValueColumn"], marker="o", linestyle="-")
    plt.xlabel("Date")
    plt.ylabel("Value")
    plt.title("Trend Over Time")
    plt.xticks(rotation=45)
    plt.show()

# Bar Chart: Comparison Across Categories
if "CategoryColumn" in data.columns and "ValueColumn" in data.columns:
    plt.figure(figsize=(8, 5))
    sns.barplot(x="CategoryColumn", y="ValueColumn", data=data)
    plt.xlabel("Category")
    plt.ylabel("Value")
    plt.title("Comparison Across Categories")
    plt.xticks(rotation=45)
    plt.show()

# Histogram: Distribution of a Numerical Column
if "NumericalColumn" in data.columns:
    plt.figure(figsize=(8, 5))
    sns.histplot(data["NumericalColumn"], bins=20, kde=True)
    plt.xlabel("Numerical Column")
    plt.title("Distribution Analysis")
    plt.show()

# Scatter Plot: Relationship Between Two Numerical Columns
if "NumericalColumn1" in data.columns and "NumericalColumn2" in data.columns:
    plt.figure(figsize=(8, 5))
    sns.scatterplot(x="NumericalColumn1", y="NumericalColumn2", data=data)
    plt.xlabel("Numerical Column 1")
    plt.ylabel("Numerical Column 2")
    plt.title("Scatter Plot Analysis")
    plt.show()

print("\nAnalysis and visualization successfully completed!")

