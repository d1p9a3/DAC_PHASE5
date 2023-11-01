# DAC_PHASE5
COVID-19 CASES ANALYSIS
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load COVID-19 data from a CSV file
url = "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv"
df = pd.read_csv(url)

# Data wrangling
df = df.drop(columns=['Lat', 'Long', 'Province/State'])
df = df.groupby('Country/Region').sum()
df = df.transpose()

# Plot total global cases over time
total_cases = df.sum(axis=1)
total_cases.plot()
plt.title("Total Global COVID-19 Cases Over Time")
plt.xlabel("Date")
plt.ylabel("Total Cases")
plt.grid()
plt.show()

# Calculate basic statistics
max_cases = total_cases.max()
min_cases = total_cases.min()
mean_cases = total_cases.mean()
median_cases = total_cases.median()

print(f"Maximum Total Cases: {max_cases}")
print(f"Minimum Total Cases: {min_cases}")
print(f"Mean Total Cases: {mean_cases}")
print(f"Median Total Cases: {median_cases}")

# Find countries with the highest and lowest total cases
highest_cases_country = total_cases.idxmax()
lowest_cases_country = total_cases.idxmin()

print(f"Country with the Highest Total Cases: {highest_cases_country} ({max_cases} cases)")
print(f"Country with the Lowest Total Cases: {lowest_cases_country} ({min_cases} cases)")

# Plot top N countries with the highest cases
top_n = 10
top_countries = total_cases.nlargest(top_n)
top_countries.plot(kind='bar')
plt.title(f"Top {top_n} Countries with the Highest Total COVID-19 Cases")
plt.xlabel("Country")
plt.ylabel("Total Cases")
plt.grid()
plt.show()
