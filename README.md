# ProdigyInfoTech_TASK5
## TASK 5: Analyzing Traffic Accident Data

This project analyzes traffic accident data to identify patterns related to road conditions, weather, and time of day, and visualizes accident hotspots and contributing factors.

## Dataset

The dataset used in this project is the RTA Dataset, containing information about traffic accidents.

## Steps

1. **Data Loading**: Load the dataset and explore its structure.
2. **Data Preprocessing**: Convert time columns to datetime format and explore basic information about the dataset.
3. **Visualization**: Visualize accidents by road surface conditions, weather conditions, time of day, and accident severity.
4. **Correlation Analysis**: Perform correlation analysis for numerical variables.
5. **Summary Visualization**: Display a pie chart of accident severity distribution.

## How to Run

1. Clone the repository.
2. Ensure you have the necessary libraries installed (`pandas`, `matplotlib`, `seaborn`).
3. Place the dataset (`RTA Dataset.csv`) in the same directory as the script.
4. Run the script (`traffic_accident_analysis.py`) to analyze and visualize the data.
## Code
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from IPython.display import display

# Load the dataset
df = pd.read_csv('RTA Dataset.csv')

# Convert time column to datetime format
df['Time'] = pd.to_datetime(df['Time'], format='%H:%M:%S').dt.time

# Display basic info about the dataset
print(df.info())
display(df.head())
```
![Screenshot 2024-07-06 230920](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/a54668a4-d68c-4962-9f37-dd64e9a07a83)
![Screenshot 2024-07-06 230909](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/592d8e00-3ef2-4480-8455-d8af70b49083)
![Screenshot 2024-07-06 230857](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/87ccdcba-d78f-4678-a758-7bd7e558e6ec)


```python
# Countplot of accidents by road surface conditions
custom_palette = ["#A95C68","#FFBF00","#0047AB","#008080"]
plt.figure(figsize=(10, 6))
sns.countplot(x='Road_surface_conditions', data=df,palette=custom_palette)
plt.title('Accidents by Road Surface Conditions')
plt.xticks(rotation=45)
plt.show()
```
### Accidents by Road Surface Conditions

![Screenshot 2024-07-06 230931](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/a338df4e-4329-4606-b948-85d616b1b38a)

```python
# Countplot of accidents by weather conditions
plt.figure(figsize=(10, 6))
sns.countplot(x='Weather_conditions', data=df)
plt.title('Accidents by Weather Conditions')
plt.xticks(rotation=45)
plt.savefig('assets/accidents_by_weather_conditions.png')  # Save the plot
plt.show()

```
### Accidents by Weather Conditions

![Screenshot 2024-07-06 230940](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/4c4b515e-6323-4763-9492-603ea2dc6c61)

```python
# Countplot of accidents by time of day (hour)
df['Hour'] = pd.to_datetime(df['Time'], format='%H:%M:%S').dt.hour
plt.figure(figsize=(12, 6))
sns.countplot(x='Hour', data=df)
plt.title('Accidents by Time of Day')
plt.xlabel('Hour of Day')
plt.ylabel('Number of Accidents')
plt.savefig('assets/accidents_by_time_of_day.png')  # Save the plot
plt.show()
```

### Accidents by Time of Day

![Screenshot 2024-07-06 230950](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/c86b7189-213d-4d98-abcd-6443c825ec22)


```python
# Selecting numerical columns for correlation analysis
df_num = df.select_dtypes(include=['int64', 'float64'])

# Heatmap of correlation matrix for numerical columns
plt.figure(figsize=(15, 9))
sns.heatmap(df_num.corr(), annot=True)
plt.title('Correlation Matrix of Numerical Variables')
plt.savefig('assets/correlation_matrix.png')  # Save the plot
plt.show()
```
### Correlation Matrix of Numerical Variables
![Screenshot 2024-07-06 231003](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/724f4a4d-53a7-48a0-9583-5cefe63cc092)


```python
# Pie chart of accident severity
accidents_severity = df['Accident_severity'].value_counts()
fig, ax = plt.subplots(figsize=(8, 6), subplot_kw=dict(aspect="equal"))
labels = accidents_severity.index
sizes = accidents_severity.values
ax.pie(sizes, labels=labels, autopct='%1.1f%%', pctdistance=0.85)
circle = plt.Circle((0, 0), 0.5, color='white')
p = plt.gcf()
p.gca().add_artist(circle)
ax.set_title("Accident by Severity", fontdict={'fontsize': 16})
plt.tight_layout()
plt.savefig('assets/accident_severity_pie_chart.png')  # Save the plot
plt.show()
```
### Pie Chart of Accident Severity

![Screenshot 2024-07-06 231009](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/aeb3ee47-3d11-4064-8dba-7d8dfefcb2e7)

