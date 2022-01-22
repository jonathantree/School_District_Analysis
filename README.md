# School District Test Analysis with Pandas

## Project Overview
The school board has requested a summary of the standardized test scores from all the schools in the district. Given the datasets schools_complete.csv and students_complete.csv which contain data about each school's size and budget and each student at that schools reading and math grades, the task is to produce the following:

### District Summary

* Create a table showing a high level snapshot of the district's key metrics
 
### School Summary

* An overview table that summarizes key metrics about each school

### Top Performing Schools (By Passing Rate)

* A table that highlights the top 5 performing schools based on Overall Passing Rate.

### Bottom Performing Schools (By Passing Rate)

* A table that highlights the bottom 5 performing schools based on Overall Passing Rate.

### Math Scores by Grade

* A table that lists the average Math Score for students of each grade level at each school.

### Reading Scores by Grade

* A table that lists the average Reading Score for students of each grade level at each school.

### Scores by School Spending

* A table that breaks down school performances based on average Spending Ranges (Per Student). 


## Resources Used
- Data Sources: 
  - Resources/schools_complete.csv
  - Resources/students_complete.csv
- Software: Python 3.7.6, Pandas 1.3.5, NumPy 1.20.3


## Challenge Overview
The school board has notified us that the students_complete.csv file shows evidence of academic dishonesty. The reading and math grades for Thomas High School ninth graders appear to have been altered. Desiring to uphold state-testing standards this analysis was done by replacing the math and reading scores for Thomas High School with NaNs while keeping the rest of the data intact. 

## Results
### Replace the math and reading scores for Thomas High School with NaNs

```python
# Step 2. Use the loc method on the student_data_df to select all the reading scores 
#from the 9th grade at Thomas High School and replace them with NaN.

student_data_df.loc[
    (student_data_df.school_name == "Thomas High School") 
    & (student_data_df.grade == "9th"),
    ["reading_score"] 
    ] = np.nan

student_data_df
```
### Deliverable #1 result


```python
#  Step 4. Check the student data for NaN's. 
nan_df = student_data_df.loc[
    (student_data_df.school_name == "Thomas High School") 
    & (student_data_df.grade == "9th")
]

nan_df
```
### *DataFrame to check for NaN*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>37537</th>
      <td>37537</td>
      <td>Erik Snyder</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>37538</th>
      <td>37538</td>
      <td>Tanya Martinez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>37539</th>
      <td>37539</td>
      <td>Noah Erickson</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>37540</th>
      <td>37540</td>
      <td>Austin Meyer</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>37543</th>
      <td>37543</td>
      <td>Madison Hampton</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39152</th>
      <td>39152</td>
      <td>Lori Moore</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>39153</td>
      <td>William Hubbard</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>39157</th>
      <td>39157</td>
      <td>Kristen Gonzalez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>39164</th>
      <td>39164</td>
      <td>Joseph Anthony</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>461 rows × 7 columns</p>
</div>

## Deliverable 2 : Repeat the school district analysis

### District Summary

The total number of 9th grad students from Thomas High School is 461. The Total number of students is 39,170. This makes the new student count 38,709. Because the subtraction of the THS 9th graders is a small percentage of the total student count, the metrics at this level remain unaffected. No change was observed in the percentage of students passing math (74.8 %), passing reading (85.7%), and the overall passing rate (64.9%).

```python
# Create a DataFrame
district_summary_df = pd.DataFrame(
          [{"Total Schools": school_count, 
          "Total Students": student_count, 
          "Total Budget": total_budget,
          "Average Math Score": average_math_score, 
          "Average Reading Score": average_reading_score,
          "% Passing Math": passing_math_percentage,
         "% Passing Reading": passing_reading_percentage,
        "% Overall Passing": overall_passing_percentage}])



# Format the "Total Students" to have the comma for a thousands separator.
district_summary_df["Total Students"] = district_summary_df["Total Students"].map("{:,}".format)
# Format the "Total Budget" to have the comma for a thousands separator, a decimal separator and a "$".
district_summary_df["Total Budget"] = district_summary_df["Total Budget"].map("${:,.2f}".format)
# Format the columns.
district_summary_df["Average Math Score"] = district_summary_df["Average Math Score"].map("{:.1f}".format)
district_summary_df["Average Reading Score"] = district_summary_df["Average Reading Score"].map("{:.1f}".format)
district_summary_df["% Passing Math"] = district_summary_df["% Passing Math"].map("{:.1f}".format)
district_summary_df["% Passing Reading"] = district_summary_df["% Passing Reading"].map("{:.1f}".format)
district_summary_df["% Overall Passing"] = district_summary_df["% Overall Passing"].map("{:.1f}".format)

# Display the data frame
district_summary_df
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>38,709</td>
      <td>$24,649,428.00</td>
      <td>78.9</td>
      <td>81.9</td>
      <td>74.8</td>
      <td>85.7</td>
      <td>64.9</td>
    </tr>
  </tbody>
</table>
</div>



## School Summary
Changing the THS 9th graders tests scores to NaN and calculating the passing percentage with the 9th graders still in the calculations significantly affected the passing percentage for Thomas High School. When the 9th graders of THS are left unchanged, the percent passing math at THS was 93.3%. The percent of THS students passing math was 97.3%, and the percentage passing both subjects was 90.9%. When these calculations are made leaving the 9th graders in and setting their grades to NaN, the percentage passing is reduced to 66.9%, 69.7%, and 65.1% for math, reading, and passing both respectively. This reduction can be seen in the school summary dataframe below with the title "School Summary Including THS 9th Graders". Removing the THS 9th graders from the calculation returns the passing percentages near the values that they were in the calculations from the unaltered dataset. This change is reflected in the dataframe below titled "School Summary Excluding THS 9th Graders".  

### *School Summary Including THS 9th Graders*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>$628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>54.642283</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>91.334769</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>53.204476</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>54.289887</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>90.599455</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>53.527508</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>89.227166</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>53.513884</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>53.539172</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>90.540541</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>52.988247</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>89.892107</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>$638.00</td>
      <td>83.350937</td>
      <td>83.896082</td>
      <td>66.911315</td>
      <td>69.663609</td>
      <td>65.076453</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>90.582567</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>90.333333</td>
    </tr>
  </tbody>
</table>
</div>

- Get the number of the students from THS in grades 10th through 12th and redo the passing percentage calculations

### *School Summary Excluding THS 9th Graders*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>$628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>54.642283</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>91.334769</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>53.204476</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>54.289887</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>90.599455</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>53.527508</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>89.227166</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>53.513884</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>53.539172</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>90.540541</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>52.988247</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>89.892107</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>$638.00</td>
      <td>83.350937</td>
      <td>83.896082</td>
      <td>93.185690</td>
      <td>97.018739</td>
      <td>90.630324</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>90.582567</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>90.333333</td>
    </tr>
  </tbody>
</table>
</div>



## Math and Reading Scores by Grade 

- Because only the 9th graders of THS had their grades replaced by NaN, the only change in the Math and Reading Scores by Grade dataframe is that the indicie of these students show NaN. All other values are unchanged.


## Scores by School Spending, School Size, and School Type

- The new calculated passing percentages in the `per_school_summary_df` for students grades 10th through 12th replaced the previous percentages effected by the NaN. Th observed change was negligible from the calculations from the unaltered dataset. Thus, as discussed in prior explanation, little change in the THS passing percentages for the test scores is observed in any subsequent dataframes that pull data from the `per_school_summary_df` which was used in preparing the summaries of the school spending, size and type. 

```python
# Establish the spending bins and group names.
spending_bins = [0, 585, 630, 645, 675]
group_names = ["<$584", "$585-629", "$630-644", "$645-675"]

# Categorize spending based on the bins.
per_school_summary_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels=group_names)

per_school_summary_df

# Calculate averages for the desired columns. 
spending_math_scores = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["Average Math Score"]

spending_reading_scores = per_school_summary_df.groupby(
    ["Spending Ranges (Per Student)"]).mean()["Average Reading Score"]

spending_passing_math = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Math"]

spending_passing_reading = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Reading"]

overall_passing_spending = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Overall Passing"]

# Create the DataFrame
spending_summary_df = pd.DataFrame({
          "Average Math Score" : spending_math_scores,
          "Average Reading Score": spending_reading_scores,
          "% Passing Math": spending_passing_math,
          "% Passing Reading": spending_passing_reading,
          "% Overall Passing": overall_passing_spending})

spending_summary_df

# Format the DataFrame 
spending_summary_df["Average Math Score"] = spending_summary_df["Average Math Score"].map("{:.1f}".format)

spending_summary_df["Average Reading Score"] = spending_summary_df["Average Reading Score"].map("{:.1f}".format)

spending_summary_df["% Passing Math"] = spending_summary_df["% Passing Math"].map("{:.0f}".format)

spending_summary_df["% Passing Reading"] = spending_summary_df["% Passing Reading"].map("{:.0f}".format)

spending_summary_df["% Overall Passing"] = spending_summary_df["% Overall Passing"].map("{:.0f}".format)

spending_summary_df
```
### *Average scores and spending ranges DataFrame*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$584</th>
      <td>83.5</td>
      <td>83.9</td>
      <td>93</td>
      <td>97</td>
      <td>90</td>
    </tr>
    <tr>
      <th>$585-629</th>
      <td>81.9</td>
      <td>83.2</td>
      <td>87</td>
      <td>93</td>
      <td>81</td>
    </tr>
    <tr>
      <th>$630-644</th>
      <td>78.5</td>
      <td>81.6</td>
      <td>73</td>
      <td>84</td>
      <td>63</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>77.0</td>
      <td>81.0</td>
      <td>66</td>
      <td>81</td>
      <td>54</td>
    </tr>
  </tbody>
</table>
</div>



## Scores by School Size


```python
# Establish the bins.
size_bins = [0, 1000, 2000, 5000]
group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]
# Categorize spending based on the bins.
per_school_summary_df["School Size"] = pd.cut(per_school_summary_df["Total Students"], size_bins, labels=group_names)

per_school_summary_df.head()

# Calculate averages for the desired columns.
size_math_scores = per_school_summary_df.groupby(["School Size"]).mean()["Average Math Score"]

size_reading_scores = per_school_summary_df.groupby(["School Size"]).mean()["Average Reading Score"]

size_passing_math = per_school_summary_df.groupby(["School Size"]).mean()["% Passing Math"]

size_passing_reading = per_school_summary_df.groupby(["School Size"]).mean()["% Passing Reading"]

size_overall_passing = per_school_summary_df.groupby(["School Size"]).mean()["% Overall Passing"]

# Assemble into DataFrame. 
size_summary_df = pd.DataFrame({
          "Average Math Score" : size_math_scores,
          "Average Reading Score": size_reading_scores,
          "% Passing Math": size_passing_math,
          "% Passing Reading": size_passing_reading,
          "% Overall Passing": size_overall_passing})

size_summary_df

# Format the DataFrame 
size_summary_df["Average Math Score"] = size_summary_df["Average Math Score"].map("{:.1f}".format)

size_summary_df["Average Reading Score"] = size_summary_df["Average Reading Score"].map("{:.1f}".format)

size_summary_df["% Passing Math"] = size_summary_df["% Passing Math"].map("{:.0f}".format)

size_summary_df["% Passing Reading"] = size_summary_df["% Passing Reading"].map("{:.0f}".format)

size_summary_df["% Overall Passing"] = size_summary_df["% Overall Passing"].map("{:.0f}".format)

size_summary_df
```
### *Average scores based on the sizes of schools DataFrame*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.8</td>
      <td>83.9</td>
      <td>94</td>
      <td>96</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.4</td>
      <td>83.9</td>
      <td>94</td>
      <td>97</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.7</td>
      <td>81.3</td>
      <td>70</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



## Scores by School Type


```python
# Calculate averages for the desired columns. 
type_math_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Math Score"]

type_reading_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Reading Score"]

type_passing_math = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Math"]

type_passing_reading = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Reading"]

type_overall_passing = per_school_summary_df.groupby(["School Type"]).mean()["% Overall Passing"]

# Assemble into DataFrame. 
type_summary_df = pd.DataFrame({
          "Average Math Score" : type_math_scores,
          "Average Reading Score": type_reading_scores,
          "% Passing Math": type_passing_math,
          "% Passing Reading": type_passing_reading,
          "% Overall Passing": type_overall_passing})

type_summary_df

# Format the DataFrame 
type_summary_df["Average Math Score"] = type_summary_df["Average Math Score"].map("{:.1f}".format)

type_summary_df["Average Reading Score"] = type_summary_df["Average Reading Score"].map("{:.1f}".format)

type_summary_df["% Passing Math"] = type_summary_df["% Passing Math"].map("{:.0f}".format)

type_summary_df["% Passing Reading"] = type_summary_df["% Passing Reading"].map("{:.0f}".format)

type_summary_df["% Overall Passing"] = type_summary_df["% Overall Passing"].map("{:.0f}".format)

type_summary_df
```
### *Average Scores based on the School Type DataFrame*
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.5</td>
      <td>83.9</td>
      <td>94</td>
      <td>97</td>
      <td>90</td>
    </tr>
    <tr>
      <th>District</th>
      <td>77.0</td>
      <td>81.0</td>
      <td>67</td>
      <td>81</td>
      <td>54</td>
    </tr>
  </tbody>
</table>
</div>

## Summary
In conclusion, after revising the dataset by replacing NaN for test scores of 9th graders at THS and removing them from the THS student count in average test score calculations, five main conclusions are drawn from the summary metrics that were calculated. They are:

1. The 5 highest performing schools are all charter schools while the lowest performing 5 schools are all district schools.
2. The range of average scores for all student's math scores was 75.91 to 85.00. The range of average test scores for all student's reading score was 80.31 to 84.70. These ranges in average scores are broken down by grade levels here:

- Math:
  - The minimum and maximum average math scores for 9th graders are: 76.40, 83.79
  - The minimum and maximum average math scores for 10th graders are: 75.91, 84.23
  - The minimum and maximum average math scores for 11th graders are: 76.40, 85.00
  - The minimum and maximum average math scores for 12th graders are: 76.18, 84.12

- Reading:
  - The minimum and maximum average reading scores for 9th graders are: 80.63, 84.12
  - The minimum and maximum average reading scores for 10th graders are: 80.63, 84.25
  - The minimum and maximum average reading scores for 11th graders are: 80.40, 84.37
  - The minimum and maximum average reading scores for 12th graders are: 80.31, 84.70

3. The amount of money spent per student is negatively correlated with the percentage of the student that passed. This trend can be observed in the *Average scores and spending ranges DataFrame*. Oddly, the smallest per student budget of <$584 resulted in the highest percentage of students passing math, reading, or both.
4. Both small and medium sized schools performed better than their larger counterparts. This observation can be seen in the *Average scores based on the sizes of schools DataFrame*.
5.  Overall, Charter schools largely outperform District schools with a percentage of overall passing rates of 90% at Charter schools vs 54% at District schools. This observation can be seen in the *Average Scores based on the School Type DataFrame*.
