# Programming Assignment 4

**Student Name:** Laguna, Carlvinz E.  
**Section:** 2ECE-B  
**Course Code:** ECE2112  

---

## Intended Learning Outcomes
1. To identify the codes and functions needed in cleaning and visualizing data
2. To be able to apply and use the different codes and functions in creating a Python program that will
be used in data wrangling and data visualization

---

## What to Expect
This README documents two Python programs:
1. Problem 1 (extracting subsets of the DataFrame based on conditions)
2. Problem 2 (visualizing factors that may affect the Average score)

Each section includes the actual code with line-by-line explanations inside the code comments, describing the process and why each function or operation is used.

---

## Table of Contents
1. [Intended Learning Outcomes](#intended-learning-outcomes)  
2. [What to Expect](#what-to-expect)  
3. [Problem 1A](#problem-1a)
4. [Problem 1B](#problem-1b)
5. [Problem 2](#problem-2)  
6. [Conclusion](#-conclusion)
7. [Programming Assignment 4 .ipynb file](Laguna_Pandas-P1.py)

---

## Problem 1A
### Problem Description
The goal of this problem is to load an Excel file into a pandas DataFrame and extract a subset of students who belong to the Instrumentation track. Specifically, the task is to create a new DataFrame that includes only the Name, GEAS, and Electronics columns for these students. Additional derived information is added by creating a Boolean column that indicates whether the Electronics score is greater than 70, as well as constant columns for Track and Hometown. This problem provides practice with filtering data using conditional selection, selecting specific columns, and creating new columns in a pandas DataFrame.

### Code

```python
# Import pandas for data wrangling
import pandas as pd

# Load the dataset from the Excel file
df = pd.read_excel("board2.xlsx")

# Filter rows where Track is 'Instrumentation'
Instru = df[df["Track"] == "Instrumentation"][["Name", "GEAS", "Electronics"]].copy()

# Add a new column 'Electronics >70'
Instru["Electronics >70"] = Instru["Electronics"] > 70

# Add constant column 'Track' with value 'Instrumentation'
Instru["Track"] = "Instrumentation"

# Add constant column 'Hometown' with value 'Luzon'
Instru["Hometown"] = "Luzon"

# Display the final Instru DataFrame
Instru
```

**Step 1: Import the pandas library**
- We import the pandas library and assign it the alias pd.
- This makes pandas available throughout the script, allowing us to read Excel files and manipulate DataFrames.

```python
import pandas as pd
```
**Step 2: Load the Excel file into a DataFrame**
- pd.read_excel("board2.xlsx") reads the file named board2.xlsx and stores it in a DataFrame called df.
- This creates the main dataset we will manipulate to extract the required subset of students.

```python
df = pd.read_excel("board2.xlsx")
```
**Step 3: Filter rows where Track is 'Instrumentation'**
- df[df["Track"] == "Instrumentation"] filters the DataFrame to include only rows where the Track column has the value Instrumentation.
- [["Name", "GEAS", "Electronics"]] selects only the relevant columns: Name, GEAS, and Electronics.
- .copy() ensures a new DataFrame is created, preventing warnings when modifying it later.

```python
Instru = df[df["Track"] == "Instrumentation"][["Name", "GEAS", "Electronics"]].copy()
```
**Step 4: Add a new column "Electronics >70"**
- Instru["Electronics >70"] = Instru["Electronics"] > 70 creates a new column that checks whether each student’s Electronics score is greater than 70.
- The result is a Boolean column (True or False).

```python
Instru["Electronics >70"] = Instru["Electronics"] > 70
```
**Step 5: Add a constant column "Track" with value 'Instrumentation'**
- Instru["Track"] = "Instrumentation" adds a new column named Track.
- Every row gets the constant value Instrumentation to clearly indicate the student’s track.

```python
Instru["Track"] = "Instrumentation"
```
**Step 6: Add a constant column "Hometown" with value 'Luzon'**
- Instru["Hometown"] = "Luzon" adds a new column named Hometown.
- Every row is assigned the constant value Luzon as required.

```python
Instru["Hometown"] = "Luzon"
```
**Step 7: Display the resulting DataFrame**
- Writing Instru as the last line in the script tells pandas to display the DataFrame.
- The table shows only Instrumentation students, their selected subjects, and the new columns we created.

```python
Instru
```

## Takeaways
1. import pandas as pd allows us to use pandas for data manipulation with a simple alias.
2. pd.read_excel() is used to load Excel files into a DataFrame for analysis.
3. Filtering with df[df["Track"] == "Instrumentation"] selects only the rows where the Track is Instrumentation.
4. Adding [["Name", "GEAS", "Electronics"]] after filtering keeps only the chosen columns.
5. .copy() creates a new DataFrame so we can safely add or modify columns without warnings.
6. Creating a new column like Instru["Electronics >70"] adds a Boolean condition (True/False) for quick evaluation.
7. Adding constant columns such as Instru["Track"] = "Instrumentation" or Instru["Hometown"] = "Luzon" labels the data clearly.
8. Displaying the DataFrame variable (Instru) shows the final filtered and modified table neatly without using print().

---

## Problem 1B
### Problem Description
The goal of this problem is to filter the dataset to identify female students from Mindanao who have an average grade greater than or equal to 55. The resulting DataFrame keeps only selected columns such as Name, Track, Electronics, and Average. A new column is added to indicate whether each student’s average meets the ≥55 requirement. This problem provides practice in applying multiple conditions for filtering, calculating new columns from existing data, and working with Boolean indicators in pandas.

### Code

```python
# Import pandas for data wrangling
import pandas as pd

# Load the dataset
df = pd.read_excel("board2.xlsx")

# Compute Average as the mean of the 4 subjects
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)

# Filter rows where Hometown = 'Mindanao' AND Gender = 'Female'
Mindy = df[(df["Hometown"] == "Mindanao") & (df["Gender"] == "Female")].copy()

# Keep only the required columns: Name, Track, Electronics, Average
Mindy = Mindy[["Name", "Track", "Electronics", "Average"]]

# Further filter rows where Average >= 55
Mindy = Mindy[Mindy["Average"] >= 55]

# Add a new column 'Average >=55' with constant value True
Mindy["Average >=55"] = True

# Display the final Mindy DataFrame
Mindy
```

**Step 1: Import the pandas library**
- We import the pandas library and give it the alias pd.
- This provides DataFrame functionality and Excel reading capabilities.

```python
import pandas as pd
```
**Step 2: Load the Excel file into a DataFrame**
- pd.read_excel("board2.xlsx") reads the Excel workbook and stores it in the DataFrame df.
- This becomes the base dataset we will manipulate.

```python
df = pd.read_excel("board2.xlsx")
```
**Step 3: Compute Average as the mean of the 4 subjects**
- df[["Math", "Electronics", "GEAS", "Communication"]] selects the subject columns.
- .mean(axis=1) computes the row-wise average across those columns (axis=1 = across columns for each row).
- The result is stored in a new column df["Average"].

```python
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)
```
**Step 4: Filter rows where Hometown == 'Mindanao' AND Gender == 'Female'**
- The boolean mask (df["Hometown"] == "Mindanao") & (df["Gender"] == "Female") selects only rows matching both conditions.
- .copy() creates an independent DataFrame Mindy so we can safely modify it later without warnings.

```python
Mindy = df[(df["Hometown"] == "Mindanao") & (df["Gender"] == "Female")].copy()
```
**Step 5: Keep only the required columns**
- Mindy[["Name", "Track", "Electronics", "Average"]] narrows the DataFrame to the columns needed for this task.
- This simplifies subsequent filtering and output.

```python
Mindy = Mindy[["Name", "Track", "Electronics", "Average"]]
```
**Step 6: Further filter rows where Average >= 55**
- Mindy[Mindy["Average"] >= 55] keeps only students whose computed average is 55 or higher.
- This enforces the minimum-average requirement from the problem.

```python
Mindy = Mindy[Mindy["Average"] >= 55]
```
**Step 7: Add a new column Average >=55 with constant value True**
- Mindy["Average >=55"] = True inserts a Boolean indicator column.
- Since we already filtered for Average >= 55, every row will have True (useful for explicit labeling).

```python
Mindy["Average >=55"] = True
```
**Step 8: Display the final Mindy DataFrame**
- Putting Mindy as the last line in a Jupyter notebook cell will render the DataFrame as a neat table.

```python
Mindy
```

## Takeaways
1. import pandas as pd allows us to use pandas efficiently with the short alias pd.
2. pd.read_excel() loads Excel files directly into a DataFrame for easy data manipulation.
3. .mean(axis=1) calculates the row-wise average across multiple subject columns.
4. Boolean conditions with & let us filter rows that satisfy two or more conditions simultaneously.
5. .copy() ensures we create a safe copy of filtered data to avoid modification warnings.
6. Selecting columns with double brackets [[ ]] keeps only the required fields in the DataFrame.
7. Further filtering (df[df["Average"] >= 55]) allows us to apply numeric thresholds after initial selection.
8. Adding a constant column (e.g., Mindy["Average >=55"] = True) explicitly labels rows that meet criteria.
9. Displaying the DataFrame variable directly in Jupyter shows a clean, tabular output.

---

## Problem 2
### Problem Description
The goal of this problem is to compute average grades from multiple subject columns and visualize how different factors may affect student performance. The task involves adding a new column Average (calculated from Math, Electronics, GEAS, and Communication) and creating bar charts that compare average scores by Gender, Track, and Hometown. This problem provides practice with data aggregation using groupby, creating new columns with calculated values, and using matplotlib to generate simple visualizations that highlight possible relationships between categorical variables and student performance.

### Code

```python
# Import pandas for handling Excel files
import pandas as pd

# Import matplotlib for plotting graphs
import matplotlib.pyplot as plt

# Load the dataset from the Excel file
df = pd.read_excel("board2.xlsx")

# Compute the Average grade from Math, Electronics, GEAS, and Communication
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)

# Visualization by Gender

# Set figure size for the chart
plt.figure(figsize=(6,4))

# Group by Gender and compute the mean of Average, then plot as bar chart
df.groupby("Gender")["Average"].mean().plot(kind="bar", color="skyblue")

# Add a title to the chart
plt.title("Average Grade by Gender")

# Label the y-axis
plt.ylabel("Average Score")

# Label the x-axis
plt.xlabel("Gender")

# Show the chart
plt.show()

# Visualization by Track

# Set figure size for the chart
plt.figure(figsize=(6,4))

# Group by Track and compute the mean of Average, then plot as bar chart
df.groupby("Track")["Average"].mean().plot(kind="bar", color="lightgreen")

# Add a title to the chart
plt.title("Average Grade by Track")

# Label the y-axis
plt.ylabel("Average Score")

# Label the x-axis
plt.xlabel("Track")

# Show the chart
plt.show()

# Visualization by Hometown

# Set figure size for the chart
plt.figure(figsize=(6,4))

# Group by Hometown and compute the mean of Average, then plot as bar chart
df.groupby("Hometown")["Average"].mean().plot(kind="bar", color="salmon")

# Add a title to the chart
plt.title("Average Grade by Hometown")

# Label the y-axis
plt.ylabel("Average Score")

# Label the x-axis
plt.xlabel("Hometown")

# Show the chart
plt.show()
```

**Step 1: Import pandas for handling Excel files**
- We import the pandas library and give it the alias pd.
- This lets us read the Excel file and work with DataFrames.

```python
import pandas as pd
```
**Step 2: Import matplotlib for plotting graphs**
- We import matplotlib.pyplot and alias it as plt.
- plt provides plotting functions (figure creation, titles, labels, showing plots).

```python
import matplotlib.pyplot as plt
```
**Step 3: Load the dataset from the Excel file**
- pd.read_excel("board2.xlsx") reads the Excel file into a DataFrame named df.
- This df is the main dataset we will aggregate and plot.

```python
df = pd.read_excel("board2.xlsx")
```
**Step 4: Compute the Average grade from subject columns**
- df[["Math", "Electronics", "GEAS", "Communication"]] selects the four subject columns.
- .mean(axis=1) computes the row-wise mean (average) across those columns.
- The result is saved in a new column df["Average"] for later grouping/plotting.

```python
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)
```
**Step 5: Visualization by Gender — set up figure and plot average by Gender**
- plt.figure(figsize=(6,4)) creates a new figure with a specified size to keep plots readable.
- df.groupby("Gender")["Average"].mean().plot(kind="bar", color="skyblue") groups rows by Gender, computes the mean Average per group, and draws a bar chart.
- plt.title, plt.ylabel, and plt.xlabel add a title and axis labels to make the chart interpretable.
- plt.show() renders the chart to the screen.

```python
plt.figure(figsize=(6,4))
df.groupby("Gender")["Average"].mean().plot(kind="bar", color="skyblue")
plt.title("Average Grade by Gender")
plt.ylabel("Average Score")
plt.xlabel("Gender")
plt.show()
```
**Step 6: Visualization by Track — set up figure and plot average by Track**
- Create a fresh figure for the track chart so it doesn't overlap previous plots.
- Group by Track, compute mean Average, and plot a bar chart to compare tracks.
- Add title and axis labels, then display the chart.

```python
plt.figure(figsize=(6,4))
df.groupby("Track")["Average"].mean().plot(kind="bar", color="lightgreen")
plt.title("Average Grade by Track")
plt.ylabel("Average Score")
plt.xlabel("Track")
plt.show()
```
**Step 7: Visualization by Hometown — set up figure and plot average by Hometown**
- New figure for hometown comparison.
- Group by Hometown, compute mean Average, and plot a bar chart to compare regions.
- Add title and labels, then show the plot.

```python
plt.figure(figsize=(6,4))
df.groupby("Hometown")["Average"].mean().plot(kind="bar", color="salmon")
plt.title("Average Grade by Hometown")
plt.ylabel("Average Score")
plt.xlabel("Hometown")
plt.show()
```

Yes, the chosen track in college, gender, and hometown all show some contribution to the differences in average scores, but not equally.

Track: The bar chart shows that students in certain tracks (e.g., Instrumentation or Electronics) tend to achieve slightly higher average scores compared to others like Communication. This suggests that the track may influence performance, possibly due to curriculum focus or student strengths.

Gender: The average scores between male and female students are close, with only a small difference observed. This indicates that gender does not strongly determine academic performance in this dataset.

Hometown: There are visible variations in average scores depending on the hometown (Luzon, Visayas, Mindanao). Students from certain regions slightly outperform others, which may reflect differences in background preparation or learning environments.

Among the three factors, Track and Hometown contribute more noticeably to higher average scores, while Gender has minimal effect on overall performance.

## Takeaways
1. import pandas as pd lets us load and process Excel data easily with pandas DataFrames.
2. import matplotlib.pyplot as plt provides tools for visualizing data with customizable plots.
3. pd.read_excel() loads an Excel file directly into a DataFrame for analysis.
4. Creating a new column with .mean(axis=1) allows us to compute averages across multiple subject columns.
5. .groupby() combined with .mean() is powerful for summarizing data by categories like Gender, Track, or Hometown.
6. .plot(kind="bar") generates quick bar charts for comparing group averages.
7. plt.figure(figsize=(6,4)) ensures each chart is readable and doesn’t overlap with others.
8. Titles and axis labels (plt.title, plt.xlabel, plt.ylabel) make visualizations clearer and more informative.
9. plt.show() displays each chart, ensuring results are presented one at a time.
10. This workflow demonstrates how to connect data analysis (pandas) with data visualization (matplotlib) for insights.

---

# 📌 Conclusion

In this assignment, I implemented and explained three Python problems in detail:

1. **Problem 1A – Filtering Data by Track (Instrumentation)** → Showed how to load an Excel dataset into pandas, subset specific rows based on the "Track" column, and add both conditional and constant columns. This problem demonstrated practical filtering, column selection, and augmentation of a DataFrame.
2. **Problem 1B – Conditional Filtering with Multiple Criteria (Mindanao & Female)** → Expanded on filtering by applying multiple conditions simultaneously using boolean operators. It also included calculating an average grade column, narrowing down the dataset to essential fields, and labeling rows that meet a threshold. This reinforced skills in conditional filtering and data preparation.
3. **Problem 2 – Visualizing Factors Affecting Average Grades** → Combined pandas and matplotlib to analyze how Gender, Track, and Hometown influence student averages. Grouping and aggregation were used to compute mean scores, and bar charts were plotted for clear comparison. This problem highlighted the integration of data analysis with visualization for meaningful insights.

Across these three problems, several important data analysis concepts were reinforced:
- DataFrames are central to organizing, filtering, and analyzing tabular datasets.
- Boolean indexing enables precise filtering using multiple conditions.
- Column creation allows both calculated fields (e.g., averages) and constant labels to enrich datasets.
- Grouping and aggregation (groupby + mean) provide summaries that reveal patterns across categories.
- Visualization with matplotlib enhances understanding by turning raw numbers into clear, interpretable graphs.
- Direct display of DataFrames (without print) produces professional tabular outputs suitable for reports.

Overall, these exercises taught me how to load, filter, manipulate, and visualize real datasets using Python. They reinforced not only technical coding skills but also the importance of documenting steps clearly, making the work easier to understand, reproducible, and applicable to real-world data analysis tasks.

---
