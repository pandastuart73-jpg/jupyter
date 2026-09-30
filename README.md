# jupyter
code
UGANDA CHRISTIAN UNIVERSITY
Faculty of Engineering, Design and Technology
Department of Computing and Technology
DATA VISUALIZATION IN PYTHON
Group Research Report
Item	Details
Programme	Bachelor of Science in Information Technology
Year / Semester	Year 1, Semester 2
Course	MTH1203 Probability and Statistics
Assessment	Group Research Work (Advent 2026)
Due date	25/09/2026

Group members
No.	Name	Registration No.
1	Wamala stuart	M26b13/040
2	Ssettuba imran	M26b13/058
3	Ndahayo dieu est la	M26b13/071
4	Kaineyesu melissa	M26b13/021


1. Introduction to Data Visualization
1.1 What is data visualization?
Data visualization is the practice of representing data in a graphical form, such as charts, plots and maps, so that patterns, trends, differences and unusual values can be seen quickly. Instead of reading hundreds of numbers in a table, a reader can look at one well-designed picture and understand the story the data is telling.
1.2 Its role in statistics and data analysis
In statistics, visualization plays two connected roles:
•Exploring data (exploratory data analysis). Before calculating any statistic, an analyst plots the data to see its shape, spot outliers and errors, and decide which statistical methods are suitable (Tukey, 1977). A histogram, for example, shows whether a variable is roughly symmetric or skewed, which affects whether the mean or the median is the better measure of centre.
•Communicating results. Findings are easier to understand and remember when shown as a chart, especially for people who are not statisticians. Good graphics support decisions in business, health, education and government.
1.3 Why summary statistics are not enough
Anscombe (1973) built four small datasets that have practically the same mean, variance, correlation coefficient (r = 0.82) and regression line (y = 3.00 + 0.50x). Yet when plotted (Figure 1), one is a normal linear trend, one is a curve, one has a single outlier, and one is driven by a single extreme point. Numbers alone would have hidden these differences. This is why visualization is an essential part of statistics rather than a decoration.

Figure 1: Anscombe's quartet – identical statistics, very different data (produced in our notebook).
1.4 Why Python?
Python is free, easy to learn and has a rich ecosystem of libraries for handling and plotting data. Charts are produced by code, so they are reproducible: the same script always produces the same chart, and updating it for new data takes seconds. Python also works well with Jupyter notebooks, which combine code, plots and explanation in a single document.
2. Python Visualization Libraries
Python has many visualization libraries. This section describes the four required by the assignment and compares them. All of them are installed with pip (for example, pip install matplotlib seaborn plotly pandas).
2.1 Matplotlib
Matplotlib is the foundation of plotting in Python. It was created by John Hunter in 2003 and gives detailed control over every element of a figure (Hunter, 2007). It produces static, publication-quality images (PNG, PDF, SVG).
•Key features: many plot types; full control of titles, axes, ticks, colours and layout; multi-panel figures with subplots; export to many file formats.
•Strengths: very flexible; the base that other libraries build on; huge community and documentation.
•Weaknesses: code can be long for complex plots; default styling looks plain; charts are not interactive by default.
import matplotlib.pyplot as plt
 
plt.plot([1, 2, 3, 4], [10, 20, 25, 30], marker="o")
plt.title("A simple line chart")
plt.xlabel("Week"); plt.ylabel("Score")
plt.show()
2.2 Seaborn
Seaborn is built on top of Matplotlib and is designed for statistical graphics (Waskom, 2021). It works directly with Pandas DataFrames, has attractive default styles, and can compute and draw statistics (such as distributions, confidence intervals and regression lines) automatically.
•Key features: histograms with density curves, box and violin plots, pair plots, heatmaps, regression plots; built-in themes and colour palettes; grouping with the hue argument.
•Strengths: good-looking charts with very little code; ideal for exploring relationships between variables.
•Weaknesses: less flexible for unusual custom charts; still static; fine-tuning often requires Matplotlib commands.
import seaborn as sns
 
sns.histplot(data=df, x="Score", bins=6)
2.3 Plotly
Plotly (Plotly Technologies Inc., 2015) creates interactive, web-based charts. Users can hover to see exact values, zoom, pan, and click legend entries to show or hide data. Its high-level interface, Plotly Express, produces a complete chart in one function call.
•Key features: interactive charts; many chart types including 3D and maps; charts can be embedded in web pages and dashboards (for example with Dash).
•Strengths: engaging, interactive results; excellent for presentations on screen and for dashboards.
•Weaknesses: heavier than Matplotlib; interactivity does not appear in printed reports; saving static images needs an extra package.
import plotly.express as px
 
fig = px.scatter(df, x="LabHours", y="Score", color="Track")
fig.show()
2.4 Pandas plotting
Pandas (McKinney, 2010) is mainly a data-analysis library, but every DataFrame and Series has a built-in .plot() method that draws charts using Matplotlib underneath. It is the fastest way to get a quick look at data.
•Key features: one-line charts (line, bar, hist, box, scatter, pie, area) directly from a table.
•Strengths: minimal code; no need to reshape data; ideal during exploration.
•Weaknesses: limited customisation on its own (you use Matplotlib to refine the chart); fewer statistical features than Seaborn.
df["Attendance"].plot(kind="hist", bins=6)
df.groupby("Sex")["Score"].mean().plot(kind="bar")
2.5 Comparison
Feature	Matplotlib	Seaborn	Plotly	Pandas plot
Main purpose	General plotting, full control	Statistical graphics	Interactive charts	Quick exploration
Ease of use	Moderate	Easy	Easy (Express)	Very easy
Interactivity	No (static)	No (static)	Yes	No (static)
Customisation	Very high	Medium	High	Low
Default look	Plain	Attractive	Modern	Plain
Built on	Core library (NumPy)	Matplotlib + Pandas	Own engine (JavaScript)	Matplotlib
Best for	Reports, custom figures	Distributions and relationships	Dashboards, web, demos	First look at data

**In practice the libraries are combined:** Pandas to prepare the data, Seaborn for fast statistical plots, Matplotlib to fine-tune titles and layout, and Plotly when interactivity is needed.
3. Types of Plots and When to Use Them
Choosing the right chart depends on the type of variable (categorical or numerical) and on the question being asked. Table 1 summarises the common chart types; each is then explained with example code and the plot produced by our notebook. The examples use the trainees dataset df (12 trainees, described in Section 5).
Chart	What it shows	Use it when…
Bar chart	A value for each category	Comparing categories (counts, means, totals)
Line chart	How a value changes across an ordered scale	Showing trends over time
Histogram	Distribution of one numerical variable	You need shape, centre, spread, skewness
Scatter plot	Relationship between two numerical variables	Checking correlation, trends and outliers
Box plot	Median, quartiles and outliers	Comparing distributions across groups
Pie chart	Parts of a whole (percentages)	There are few categories (about 5 or fewer)
Heatmap	Values in a matrix as colours	Displaying correlation matrices or many-by-many tables
Table 1: Summary of common chart types.
3.1 Bar chart
What it shows: the size of a value (count, mean, total) for each category, using bars whose lengths are proportional to the values. When to use: to compare separate categories, such as average scores per training track. Sort the bars, keep the baseline at zero and use horizontal bars if labels are long.
avg = df.groupby("Track")["Score"].mean().sort_values(ascending=False)
fig, ax = plt.subplots()
bars = ax.bar(avg.index, avg.values, color="#2A6F97")
ax.bar_label(bars, fmt="%.1f")
ax.set_title("Average score by training track")
ax.set_xlabel("Track"); ax.set_ylabel("Mean score (%)")
ax.set_ylim(0, 100)

Figure 2: Bar chart of mean score by training track.
3.2 Line chart
What it shows: how a value changes along a continuous or ordered scale, usually time, by joining points with lines. When to use: for trends over time. Our trainees dataset has no date column, so we order the trainees by lab hours and show how score and attendance change along that scale. Several lines can be compared, but keep them to a small number.
df_sorted = df.sort_values("LabHours")      # order trainees by lab hours
fig, ax = plt.subplots()
ax.plot(df_sorted["LabHours"], df_sorted["Score"], marker="o", label="Score")
ax.plot(df_sorted["LabHours"], df_sorted["Attendance"], marker="s", label="Attendance")
ax.set_title("Score and attendance as lab hours increase")
ax.set_xlabel("Lab hours"); ax.set_ylabel("Percentage (%)"); ax.legend()

Figure 3: Line chart of score and attendance against lab hours.
3.3 Histogram
What it shows: the distribution of one numerical variable. The data is split into intervals (bins) and the height of each bar is the number of observations in the bin. When to use: to see whether data is symmetric, skewed or has several peaks, and how spread out it is. Try different numbers of bins because too few or too many can hide the real shape; with only 12 values we use a few wide bins.
sns.histplot(df["Score"], bins=6)
plt.axvline(df["Score"].mean(), color="red", linestyle="--")
plt.title("Distribution of trainee scores")
plt.xlabel("Score (%)"); plt.ylabel("Number of trainees")

Figure 4: Histogram of trainee scores with the mean marked.
3.4 Scatter plot
What it shows: each observation as a point, positioned by two numerical variables. When to use: to examine the relationship between two variables (positive, negative or none), see how strong it is, and identify outliers. Colour can add a third (categorical) variable. A visible relationship shows association, not necessarily cause.
sns.scatterplot(data=df, x="LabHours", y="Score", hue="Track")
plt.title("Lab hours vs score")
plt.xlabel("Lab hours"); plt.ylabel("Score (%)")

Figure 5: Scatter plot of lab hours against score with line of best fit (r = 0.99).
3.5 Box plot
What it shows: the five-number summary of a numerical variable: minimum, first quartile (Q1), median, third quartile (Q3) and maximum. The box covers Q1 to Q3 (the middle 50% of data), the line inside is the median, the whiskers show the typical range and dots mark possible outliers. When to use: to compare distributions across several groups side by side. When groups are small (here only 4 trainees per track), draw the individual points on top of the boxes.
sns.boxplot(data=df, x="Track", y="Score", hue="Track", legend=False, showfliers=False)
sns.stripplot(data=df, x="Track", y="Score", color="black")   # show each trainee
plt.title("Score distribution by track")

Figure 6: Box plots of score for each track, with individual trainees shown as points.
3.6 Pie chart
What it shows: how a whole is divided into parts, each slice being a share of 100%. When to use: only with a small number of categories (about five or fewer) with clearly different sizes. People judge lengths more accurately than angles (Cleveland & McGill, 1984), so a bar chart is often the better option, especially for many categories or close values.
counts = df["Certified"].value_counts()
plt.pie(counts.values, labels=counts.index, autopct="%1.1f%%", startangle=90)
plt.title("Share of trainees who are certified")

Figure 7: Pie chart of the share of certified trainees.
3.7 Heatmap
What it shows: a table of values where each cell is coloured according to its value. When to use: most commonly for a correlation matrix, or any large grid of numbers where a colour scale reveals patterns faster than digits. Use a sensible colour map (a diverging map with a neutral centre for correlations) and print the values on the cells.
corr = df[["LabHours", "Attendance", "Score"]].corr()
sns.heatmap(corr, annot=True, fmt=".2f", cmap="coolwarm", vmin=-1, vmax=1)
plt.title("Correlation between numerical variables")

Figure 8: Heatmap of the correlation matrix (all values close to 1).
3.8 Pandas plotting and Plotly examples
The same charts can be produced with other libraries. Pandas draws a chart straight from a DataFrame (Figure 9), and Plotly makes it interactive:
# Pandas: two charts using one line each
df.groupby("Sex")["Score"].mean().plot(kind="bar")
df["Attendance"].plot(kind="hist", bins=6)
 
# Plotly Express: interactive box plot (hover, zoom, hide groups)
import plotly.express as px
px.box(df, x="Track", y="Score", color="Track", points="all", hover_name="Trainee").show()

Figure 9: Bar chart and histogram created with Pandas plotting.
The interactive Plotly charts run in the Jupyter notebook and cannot be shown in a printed report.
4. Best Practices for Effective Visualization
A visualization is successful when the reader understands the message quickly, correctly and honestly. The principles below follow the guidance of Tufte (2001), Cleveland and McGill (1984) and Wilke (2019).
4.1 Choose the right chart
Start with the question, not the chart. Table 2 gives a quick guide.
Question	Suitable chart
Compare values between categories?	Bar chart
How does something change over time?	Line chart
What does the distribution of one variable look like?	Histogram (or box plot)
Are two numerical variables related?	Scatter plot
How do groups differ in spread and median?	Box plot
What share does each part contribute?	Pie chart (few parts) or stacked bar
Which variables are related to which?	Heatmap of correlations
Table 2: Matching a question to a chart type.
4.2 Use clear titles, labels and legends
•Give every chart a descriptive title that says what is shown (better still, the main finding).
•Label both axes and include units (for example “Score (%)”).
•Use a legend only when several groups are shown, and give it a title. Where possible label lines or bars directly.
•Use text that is large enough to read when projected or printed.
4.3 Use colour sensibly
•Use colour to carry meaning (to separate groups or highlight one item), not just for decoration.
•Limit the palette, and use a sequential scale for ordered values, a diverging scale for values with a meaningful centre (such as correlation) and distinct colours for categories.
•Design for colour-blind readers: avoid relying on red versus green alone; use safe palettes such as Seaborn's colorblind palette and add labels or markers.
4.4 Avoid clutter
•Remove what does not help: heavy gridlines, 3D effects, shadows, unnecessary borders.
•Keep the ratio of information to ink high: one main message per chart.
•Too many categories or lines make a chart unreadable; group small ones or split into several charts.
4.5 Avoid misleading graphics
•Start bar charts at zero. Bar length represents the value, so a truncated axis exaggerates differences (Figure 10).
•Do not change scales or intervals mid-chart, and keep the same scale when comparing charts.
•Do not use 3D or area effects that distort sizes; do not use a pie chart when the parts do not sum to a whole.
•Show the data source, the sample size and any data that was removed. Do not choose only the data that supports one story.
•Remember that correlation does not prove causation, even when a scatter plot shows a strong pattern.

Figure 10: The same data drawn with a truncated axis (left) and an honest zero baseline (right).
On the left the Software bar (50.5) looks almost nothing next to Cybersecurity (79.8), as if it were a small fraction of it. The honest chart on the right shows Software is about 63% of Cybersecurity.
5. Notebook Implementation
The accompanying Jupyter notebook (Data_Visualization_Notebook.ipynb) applies everything above. It is organised in numbered sections with comments in the code, and runs from top to bottom with no errors.
5.1 The sample dataset
The notebook uses the file trainees.xlsx, which holds results and training details for 12 IT trainees (four in each of three tracks, six female and six male). It is loaded with pandas.read_excel. If the file is not found, the notebook falls back to the same data typed in directly, so it always runs. The variables are listed in Table 3. With only 12 rows, our findings are illustrations of how each chart works and should be treated as tentative.
Variable	Type	Description
Trainee	Identifier	Name of the trainee
Track	Categorical	Cybersecurity, Networking or Software
Sex	Categorical	F or M
LabHours	Numerical	Hours spent in the lab
Attendance	Numerical	Attendance (%)
Score	Numerical	Assessment score (%)
Result	Categorical	Pass or Fail
Certified	Categorical	Yes or No
Table 3: Variables in the trainees dataset (12 rows, 8 columns).
import pandas as pd
 
df = pd.read_excel("trainees.xlsx")          # load the dataset
print(df.shape)                               # (12, 8)
df.head()                                     # first rows
df[["LabHours", "Attendance", "Score"]].describe()   # summary statistics
5.2 Structure of the notebook
Section	Content
1	Setup: importing pandas, numpy, matplotlib, seaborn and plotly
2	Anscombe's quartet – why we visualize
3	Loading and summarising the trainees dataset (head and describe)
4–8	Bar chart, line chart, histogram, scatter plot, box plot, pie chart, heatmap (Matplotlib and Seaborn)
9	Pandas plotting
10	Interactive Plotly charts (scatter, box, histogram, line)
11	Best practice: honest versus misleading chart
12–13	Dashboard of four charts and conclusions

5.3 Results and interpretation
The visualizations lead to the following observations. With only 12 trainees, these findings illustrate how to read each chart and should be treated as tentative.
•Distribution: scores have mean 65.5, median 65.5 and standard deviation 18.1 (range 41 to 93). The histogram shows a cluster of four low scores (41 to 49) and the rest spread evenly between about 54 and 93.
•Relationships: lab hours, attendance and score rise together almost perfectly: lab hours and score r = 0.99, attendance and score r ≈ 1.00, lab hours and attendance r ≈ 1.00. The line chart and scatter plot show this as an almost straight line. Correlation does not prove that more lab hours cause higher scores.
•Groups: Cybersecurity has the highest mean score (79.8), then Networking (66.2) and Software (50.5), although the box plots overlap a little. Female trainees average 76.8 and male trainees 54.2.
•Outcomes: 8 of 12 trainees passed and 5 of 12 (41.7%) are certified. All four who failed scored 49 or less, and every certified trainee scored 74 or above.

Figure 11: Dashboard combining four charts produced by the notebook.
6. Conclusion
Data visualization turns numbers into pictures that people can understand quickly, and it is an essential part of statistics: it reveals what summary statistics can hide (Anscombe, 1973) and makes findings easier to communicate. Python offers a complementary set of libraries: Matplotlib for control, Seaborn for statistical plots, Pandas for quick exploration and Plotly for interactivity. Each chart type answers a particular kind of question, and choosing the wrong one can confuse the reader. Finally, good practice (clear titles and labels, sensible colour, zero-based bars, minimal clutter and honest scales) ensures that a chart is not only attractive but also truthful. Our notebook demonstrates all of these ideas in working code.
