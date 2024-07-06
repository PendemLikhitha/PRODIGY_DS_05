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
![Screenshot 2024-07-06 204321](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/75af8f3d-ab31-42d8-bc91-1ba8e68f0732)
![Screenshot 2024-07-06 204310](https://github.com/PendemLikhitha/PRODIGY_DS_05/assets/159911587/244b7b9e-62c1-44b3-9da6-22ec568e1600)
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

![Screenshot 2024-07-03 210554](https://github.com/PendemLikhitha/ProdigyInfoTech_TASK5/assets/159911587/43907dca-9eef-4ef0-9a70-94d6ccd0a7a2)
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

![Screenshot 2024-07-03 210605](https://github.com/PendemLikhitha/ProdigyInfoTech_TASK5/assets/159911587/dd7b1707-9393-47c4-bcde-03063779c9b4)
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

![Screenshot 2024-07-03 210617](https://github.com/PendemLikhitha/ProdigyInfoTech_TASK5/assets/159911587/5f8ed9ba-9763-4dde-94e0-523b2044f63e)

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

![Screenshot 2024-07-03 210637](https://github.com/PendemLikhitha/ProdigyInfoTech_TASK5/assets/159911587/f5843827-c5ce-4bc2-83e2-b4ead31adcbe)

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

![Screenshot 2024-07-03 210644](https://github.com/PendemLikhitha/ProdigyInfoTech_TASK5/assets/159911587/90c91453-9111-4741-9bee-3c389f8d64c9)
