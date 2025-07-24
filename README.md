# Learning Seaborn 📊
A comprehensive collection of seaborn examples and techniques for statistical data visualization in Python.

## 📚 Table of Contents
- Setup & Configuration
- Datasets
- Line Plots
- Distribution Plots
- Scatter Plots
- Count Plots
- Bar Plots
- Heatmaps
- Pair Plots
- Color Palettes
- Best Practices

## 🔧 Setup & Configuration

### Required Libraries
```python
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```

### Theme Configuration
```python
sns.set_style('darkgrid')
plt.style.use('dark_background')
%matplotlib inline
```

## 📊 Datasets

### Sample Student Data
```python
roll_no = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]
marks = [23,45,67,89,56,34,21,45,67,32,67,76,33,21,45]
sample_df = pd.DataFrame({"Rollno": roll_no, "Marks":marks})
sample_df.head()
```

### HR Employee Data
```python
df = pd.read_csv('hr_data.csv')
df.head()
```

### Built-in Seaborn Datasets
```python
# Titanic dataset
titanic_df = sns.load_dataset('titanic')

# Flights dataset
flight_df = sns.load_dataset('flights')

# Penguins dataset
penguins = sns.load_dataset('penguins')
```

## 📈 Line Plots

### Basic Line Plot
```python
sns.lineplot(x='Rollno', y='Marks', data=sample_df)
plt.title('Student Marks')
```

### Multi-variable Line Plot
```python
sns.lineplot(x='number_project', y='average_montly_hours', data=df)
```

### Advanced Line Plot with Styling
```python
plt.figure(figsize=(12,6))
sns.lineplot(x='number_project', y='average_montly_hours', data=df,
             hue='left',
             style='department',
             legend='full',
             palette='flare')
```

### Line Plot by Department
```python
plt.figure(figsize=(12,6))
sns.lineplot(x='department', y='left', data=df)
```

## 📊 Distribution Plots

### Basic Distribution Plot
```python
sns.distplot(df['time_spend_company'])
```

### Distribution Plot with Custom Bins
```python
bins = [2,3,4,5,6,7,8,9,10]
sns.distplot(df['time_spend_company'], bins=bins)
plt.xticks(bins)
```

### Styled Distribution Plot
```python
sns.distplot(df['time_spend_company'], bins=bins,
             rug=True,
             color='green')
plt.xticks(bins)
```

### Multiple Distribution Plots
```python
# Time spent in company
sns.distplot(df['time_spend_company'])

# Employee turnover
sns.distplot(df['left'])

# Average monthly hours
sns.distplot(df['average_montly_hours'])
```

## 🎯 Scatter Plots

### Basic Scatter Plot
```python
sns.scatterplot(x='age', y='fare', data=titanic_df)
```

### Scatter Plot with Hue
```python
sns.scatterplot(x='age', y='fare', data=titanic_df, hue='alive')
```

### Advanced Scatter Plot
```python
plt.figure(figsize=(12,6))
sns.scatterplot(x='age', y='fare', data=titanic_df,
                hue='alive',
                style='class')
plt.title('Titanic Data Analysis')
```

### Scatter Plot with Custom Palette
```python
plt.figure(figsize=(12,6))
sns.scatterplot(x='age', y='fare', data=titanic_df,
                hue='alive',
                style='class',
                palette='inferno')
plt.title('Titanic Data Analysis')
```

### Scatter Plot with Transparency
```python
plt.figure(figsize=(12,6))
sns.scatterplot(x='age', y='fare', data=titanic_df,
                hue='alive',
                style='class',
                palette='gist_rainbow',
                alpha=0.5)
plt.title('Titanic Data Analysis')
```

### Combined Scatter and Line Plot
```python
plt.figure(figsize=(12,6))
sns.scatterplot(x='age', y='fare', data=titanic_df,
                hue='alive', style='class')
sns.lineplot(x='age', y='fare', data=titanic_df, color='green')
plt.title('Titanic Data Analysis')
```

## 📊 Count Plots

### Basic Count Plot
```python
sns.countplot(x='class', data=titanic_df)
```

## 📊 Bar Plots

### Basic Bar Plot
```python
sns.barplot(x='class', y='fare', data=titanic_df)
```

### Grouped Bar Plot
```python
sns.barplot(x='class', y='fare', data=titanic_df, hue='sex')
```

### Bar Plot with Custom Palette
```python
sns.barplot(x='class', y='fare', data=titanic_df,
            hue='sex',
            palette='icefire')
```

### Horizontal Bar Plot
```python
sns.barplot(y='class', x='fare', data=titanic_df,
            hue='sex',
            palette='inferno',
            orient='h')
```

### Bar Plot with Custom Estimator
```python
sns.barplot(x='class', y='fare', data=titanic_df,
            hue='sex',
            palette='inferno',
            estimator=np.max)
```

### Bar Plot with Error Bars
```python
sns.barplot(x='class', y='fare', data=titanic_df,
            hue='sex',
            palette='inferno',
            ci=100,
            errcolor='#7289da',
            errwidth=3)
```

### Bar Plot with Saturation Control
```python
sns.barplot(x='class', y='fare', data=titanic_df,
            hue='sex',
            palette='inferno',
            saturation=0.9)
```

## 🔥 Heatmaps

### Data Preparation for Heatmaps
```python
flight_df = sns.load_dataset('flights')
flight_df = flight_df.pivot(index="month", columns="year", values="passengers")
flight_df.head()
```

### Basic Heatmap
```python
plt.figure(figsize=(12,6))
ax = sns.heatmap(flight_df)
```

### Annotated Heatmap
```python
plt.figure(figsize=(14,8))
ax = sns.heatmap(flight_df, annot=True, fmt='d')
```

### Heatmap with Grid Lines
```python
plt.figure(figsize=(14,8))
ax = sns.heatmap(flight_df, annot=True, fmt='d', 
                 linecolor='k', linewidths='5')
```

### Heatmap with Custom Colormap
```python
plt.figure(figsize=(14,8))
ax = sns.heatmap(flight_df, annot=True, fmt='d',
                 linecolor='k', linewidths='5',
                 cmap='Blues')
```

### Heatmap without Colorbar
```python
plt.figure(figsize=(14,8))
sns.heatmap(flight_df, cbar=False)
```

### Custom Colorbar Position
```python
grid_kws = {"height_ratios": (.3, .05), "hspace": .4}
f, (ax, cbar_ax) = plt.subplots(2, gridspec_kw=grid_kws)
ax = sns.heatmap(flight_df, cbar_kws={"orientation": "horizontal"},
                 ax=ax, cbar_ax=cbar_ax)
```

### Correlation Matrix Heatmap
```python
numerical_titanic_df = titanic_df.select_dtypes(include=np.number)

plt.figure(figsize=(12, 8))
sns.heatmap(numerical_titanic_df.corr(), annot=True, cmap='coolwarm')
plt.title('Correlation Matrix of Titanic Numerical Features')
plt.show()
```

## 👥 Pair Plots

### Basic Pair Plot
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins)
```

### Pair Plot with Hue (Sex)
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, hue='sex', palette='Reds')
```

### Pair Plot with Hue (Species)
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, hue='species', palette='Blues')
```

### Histogram Pair Plot
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, kind='hist', palette='YlOrGr')
```

### Pair Plot with Diagonal Histograms
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, hue="species", diag_kind="hist", palette='rainbow')
```

### Corner Pair Plot
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, corner=True)
```

### Pair Plot with Custom Markers
```python
plt.figure(figsize=(12,12))
sns.pairplot(penguins, hue="species", markers=["o", "s", "D"], 
             palette='inferno')
```

## 🎨 Color Palettes

### Available Palettes
- `flare` - Orange/red gradient
- `inferno` - Purple/yellow gradient  
- `icefire` - Blue/white/red
- `Blues` - Blue monochrome
- `rainbow` - Full spectrum
- `gist_rainbow` - Vibrant spectrum
- `coolwarm` - Blue/white/red diverging
- `YlOrGr` - Yellow/orange/green
- `Reds` - Red monochrome

### Using Palettes
```python
# In any plot function
palette='inferno'
palette='viridis'
palette='Set1'
```

## 💡 Best Practices

### Figure Sizing
```python
plt.figure(figsize=(12,6))  # Standard size
plt.figure(figsize=(14,8))  # Larger plots
```

### Adding Titles
```python
plt.title('Your Plot Title')
```

### Custom Tick Labels
```python
plt.xticks(bins)  # For custom x-axis ticks
```

### Transparency Control
```python
alpha=0.5  # 50% transparency
```

### Data Preprocessing
```python
# Select numerical columns only
numerical_df = df.select_dtypes(include=np.number)

# Pivot for heatmaps
pivot_df = df.pivot(index="row", columns="col", values="values")
```

### Handling Deprecated Functions
```python
# OLD (deprecated)
sns.distplot(data)

# NEW (recommended)
sns.histplot(data)  # or sns.displot(data)
```

## 🚀 Getting Started

1. Install required packages:
```bash
pip install seaborn matplotlib pandas numpy
```

2. Import libraries and set theme:
```python
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

sns.set_style('darkgrid')
plt.style.use('dark_background')
```

3. Load your data and start plotting!

## 📝 Notes

- Some functions like `distplot()` are deprecated in newer Seaborn versions
- Always check the Seaborn documentation for the latest syntax
- Use `plt.figure(figsize=(width, height))` for better plot sizing
- Experiment with different color palettes to find what works best for your data

---

**Happy Visualizing! 📊✨**
