

# **COVID-19 Global Data Tracker 📊**  

## **Project Overview**  
This project is designed to analyze global **COVID-19 cases, deaths, and vaccinations** using real-world data. It applies **Python-based data analysis**, enabling users to explore trends, compare metrics across countries, and visualize the spread of COVID-19 effectively.

## **Objectives 🚀**  
✅ Load and clean global COVID-19 data  
✅ Analyze time trends (cases, deaths, vaccinations)  
✅ Compare metrics across different countries  
✅ Visualize trends using charts and maps  
✅ Summarize findings in a well-documented notebook  

---

## **Dataset 📂**  
### **Source**  
We use the **Our World in Data COVID-19 Dataset** available at:  
🔗 [Our World in Data - COVID-19](https://ourworldindata.org/covid-cases)  

### **Download Instructions:**  
1. Visit the [Our World in Data repository](https://ourworldindata.org/covid-cases).  
2. Download the dataset (`owid-covid-data.csv`).  
3. Save it in your working directory.  

---

## **Setup & Dependencies ⚙️**  
### **Install Required Libraries**  
Ensure you have the required Python packages installed:  
```bash
pip install pandas matplotlib seaborn plotly
```
### **Required Tools**  
- **Python 3.x**
- **Jupyter Notebook**
- **pandas, matplotlib, seaborn, plotly**  

---

## **Project Steps 🏗️**  

### **1️⃣ Data Loading & Exploration**  
Load the dataset, check for missing values, and explore key columns.  
```python
import pandas as pd

df = pd.read_csv("owid-covid-data.csv")
print(df.head())
print(df.info())
```

### **2️⃣ Data Cleaning**  
Handle missing values, filter countries of interest, and convert date formats.  
```python
df['date'] = pd.to_datetime(df['date'])
df.fillna(method='ffill', inplace=True)  # Fill missing values
df_filtered = df[df['location'].isin(['Kenya', 'United States', 'India'])]
```

### **3️⃣ Exploratory Data Analysis (EDA)**  
Analyze case trends, death rates, and key statistics.  
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10,5))
sns.lineplot(x='date', y='total_cases', hue='location', data=df_filtered)
plt.title("COVID-19 Cases Over Time")
plt.show()
```

### **4️⃣ Visualizing Vaccination Progress**  
Compare global vaccinations with charts and distributions.  
```python
sns.lineplot(x='date', y='total_vaccinations', hue='location', data=df_filtered)
plt.title("Total Vaccinations Over Time")
plt.show()
```

### **5️⃣ (Optional) Choropleth Map**  
Visualize cases or vaccination rates by country using Plotly.  
```python
import plotly.express as px

latest_data = df[df['date'] == df['date'].max()]
fig = px.choropleth(latest_data, locations="location", locationmode="country names",
                    color="total_cases", hover_name="location",
                    title="COVID-19 Cases Around the World", color_continuous_scale="Reds")
fig.show()
```

### **6️⃣ Insights & Reporting**  
Document key findings with markdown cells in Jupyter Notebook.  
```python
insights = [
    "India had a major spike in COVID-19 cases during the Delta wave.",
    "The USA had one of the fastest vaccination rollouts.",
    "Kenya showed slower but steady progress in vaccinations."
]

for i, insight in enumerate(insights, 1):
    print(f"{i}. {insight}")
