# Pandas Notes

## Table of Contents

- [Selection](#selection)
- [Methods and Attributes](#methods-and-attributes)
- [Cleaning Data](#cleaning-data)
- [Dtypes](#dtypes)
- [Transorm Data](#transorm-data)
- [Grouping](#grouping)
- [Save DataFrame](#save-dataframe)
- [Suppress Warnings](#suppress-warnings)
- [Pivot Table JavaScript Library](#pivot-table-javascript-library)
- [Visualisations](#visualisations)

## Selection

- `df['column name']` Select a column. Returns a Pandas Series, a 1D labeled array
- `df[['column1', 'column2']]` Select multiple columns
- ` new_column = df['column name1'] * df['column name2']` perform an operation on two columns, in this case multiply.
- `df.iloc[0]` select row by index, first row in this case
- `df.head(10)` and `df.tail(10)` see first or last rows, default will be 5
- `pd.concat([df.head(2), df.tail(3)])` get the first and last few rows
- `df.head(5).tail(5-2)` you can combine, this example returns index 2,3,4, index 0,1 are sliced off
- `df[0:3]` slice rows, `df[0]` won't work, it must be a range/slice
- `df['column name'].iloc[0]` choose a row from a single (or multiple) column
- `df[df['Population (1000s)'] > 80000]` return rows where population (in 1000s) is greater than 80000
- `&` and `|` or can be used to match multiple conditions, use brackets around each condition
- `df.index = df['col_name']` change index column, default is 0 indexed integers
- `df.loc[index_value]` select a row by named index
- `df.sort_index()` put the new index in order
- `df.loc[datetime(2014,12,8) : datetime(2014,12,12)]` select slice
- `df[df['Country'].str.startswith('P')]` filter by what first letter

## Methods and Attributes

- `column.sum()` sum of a column
- `.min()` and `.max()` of a column. If used on a dataFrame will return for first column (I think)
- `.mean()` and `.median()`
- `df.sort_values('col_name')` does not modify original
- `df.columns` gives all column names
- `df_copy = df.copy()` create a copy, otherwise the variable points to the same thing

## Cleaning Data

- `pd.read_csv(csv_data, skipinitialspace=True)` remove leading space, ie. space before comma in csv
- `df.rename(columns={'Original name':'New name'})` rename column
- `df['col_name'] = df['col_name'].str.rstrip(' ')` remove trailing space from values in column
- `df['col_name'] = df['col_name'].str.replace('<br />', '')` replace substring from values in column
- `df['col_name'].isnull()` gives a series of boolean values, True means no data ie. is null
- `.isna()` same as `.isnull`
- `df[df['col_name'].isnull()]` use the boolean series to get only rows that have missing data for given column
- `df.dropna()` drop rows that contain a null value in any column
- `df.fillna('')` replace null with a fixed value, in this case an empty string
- Pandas will ignore null values when computing numeric statistics eg. `sum()`, `median()`, etc.
- `df = df.dropna(subset=['NY.GDP.MKTP.CD'])` remove rows that contain null values in the given column
- `df.dropna(subset=['NY.GDP.MKTP.CD'], inplace=True)` like above but modifies original
- `df = df.drop('column_name', axis=1)` remove a column, `axis=1` means a column (not a row)
- `df['column'].combine_first(df['column_dup'])` replace null values in one column with values in the other column

## Dtypes

- `df.dtypes` see datatypes of all columns
- `int64` is the pandas data type for whole numbers such as 55 or 2356
- `float64` is the pandas data type for decimal numbers such as 55.25 or 2356.00
- `object` is the pandas data type for strings such as 'hello world' or 'rain'
- `df['col_name'] = df['col_name'].astype('int64')` change dtype of column
- `datetime64`
- `import datetime from datetime` import datetime class from the datetime python module
- `df['Date_col'] = pd.to_datetime(df['Date_col'])`
- `df[df['Date'] == datetime(2014, 6, 4)]` use datetime create a datetime value and use it to query

## Transorm Data

- `column.apply(my_function).apply(function_two)` apply a function to each value in a column, can be chained
- `pd.merge(gdp_df, life_df, on='Country', how='right')` use merge to join tables. There are fours kinds:
  - `left` keeps all rows in left table, if they aren't in right table values are set as `NaN`
  - `right` keeps rows in right table
  - `outer` keeps all rows
  - `inner` keeps only rows common to both
- `df.style.format('{:,.2f}')` format so its not in scientific notation
- `my_pandas_series.apply(lambda x: '{:,.2f}'.format(x))` format so its not in scientific notation
- `df.groupby('col1')['col2'].sum().apply(lambda x: f"{x / 1_000_000:.2f}")` get the anser in units of one million
- Pivot Table

  ```py
  report = pd.pivot_table(
    df,
    index=['Col1'],
    columns=['Col2'],
    values='Col3',
    aggfunc=sum,
    margins=True,
    margins_name='Total'
  )
  ```

## Grouping

- `gdp.groupby('column1')['column2'].aggregate(sum)`
  - `groupby` will group values that are the same in the given column together.
  - `aggregate(sum)` is used to do something to a given column in the grouped data. In this case, add the values together.
  - `apply(my_func)` you can also use apply on groups, you can pass your own functions
- `grouped.groups.keys()` see the group names
- `grouped.keys` see the column that it was grouped on?
- `grouped.get_group('group_name')` get a table containing just rows from the given group
- `df.groupby(['Commodity', 'Year'])` group by two columns
- `grouped.get_group(('A', 2020))`
- `df.groupby(['Col1', 'Col2']).agg(my_custom_name=pd.NamedAgg(column='Col3', aggfunc='sum'))` you can give the agg column a name
- `pd.pivot_table(df, index=['Col1','Col2'], values='Col3', aggfunc=sum)` creates a table just like the one above, ie. double grouped and aggregated
- Add a column to the grouped data with the row count of each group

  ```py
  aggregated_group = df.groupby('Coutnry')['PrimaryValue'].agg([sum])
  row_count_each_group = df.groupby('Country').size()

  aggregated_group['RowsInGroup'] = row_count_each_group
  ```

- `grouped.filter(myFilterFunction)` will apply a user defined filtration function to each group in a set of grouped items that tests each group and returns a Boolean True or False value to say whether each group has passed the filter test. The .filter() function then returns a single dataframe that contains the combined rows from groups that the user defined filter function let through.

## Save DataFrame

- `df.to_csv('filename.csv', index=False)` save dataframe in csv file, don't include default index pandas adds.
- `pd.read_csv(LOCATION, encoding='ISO-8859-1')` I had to pass the encoding, aparently this encoding is common for csv with special characters.

## Suppress Warnings

This will suppress warnings about future pandas changes.

```py
import warnings
warnings.simplefilter('ignore', FutureWarning)
```

## Pivot Table JavaScript Library

Can be used to create interactive pivot tables. Can be used in notebook with python. It creates an html file that can also be opened directly in the browser. Theres also a javascript package.

- [Python package pivottablejs](https://pypi.org/project/pivottablejs/)

```py
from pivottablejs import pivot_ui
pivot_ui(dataFrame)
```

NOTE: doesn't work in vscode.

## Visualisations

### Create a bar chart where sub-categories have their own bars side by side

```py
import pandas as pd
import matplotlib.pyplot as plt

# Sample DataFrame
data = {'Category': ['A', 'A', 'B', 'B', 'A', 'A', 'B', 'B'],
        'Subcategory': ['X', 'Y', 'X', 'Y', 'X', 'Y', 'X', 'Y'],
        'Value': [10, 15, 20, 25, 12, 18, 22, 27]}

df = pd.DataFrame(data)

grouped_df = df.groupby(['Category', 'Subcategory']).sum().unstack()

# ax = grouped_df.plot(kind='bar', stacked=True) # stack the bars for the subcategories
ax = grouped_df.plot(kind='bar')

plt.xlabel('Category')
plt.ylabel('Value')
plt.title('Double Grouped Bar Chart')
plt.show()
```

### Kinds

- `.plot()` default line graph?
- `scatter`
- `stem`
- `.plot(kind='barh')` bar histogram?
- `maps` name?

### Logarithmic Scale

- `.plot(kind='barh', logx=True)` use to spread out the data, eg. 10x, 100x, 1000x, rather than 10, 20, 30.

### Hover Tooltip on charts

`mplcursors` is more hover tooltips for data plots. I couldn't get it working. There is another library called `plotly`.

NOTE: The `%matplotlib notebook` magic command apparently should get it working, it might just be my environment (VSCode).

```python
# %matplotlib inline
%matplotlib notebook
import matplotlib.pyplot as plt
import mplcursors

# Assuming 'all' is your DataFrame and COUNTRY, GDP, LIFE are column names
headers = [COUNTRY, GDP, LIFE]
gdp_vs_life = all[headers]

# Create a scatter plot
fig, ax = plt.subplots()
scatter = ax.scatter(gdp_vs_life[GDP], gdp_vs_life[LIFE])

# Add labels and title
ax.set_xlabel('GDP')
ax.set_ylabel('Life Expectancy')
ax.set_title('GDP vs Life Expectancy')

# Add tooltips using mplcursors
mplcursors.cursor(hover=True).connect("add", lambda sel: sel.annotation.set_text(gdp_vs_life[COUNTRY][sel.target.index]))

# Show the plot
plt.show()
```
