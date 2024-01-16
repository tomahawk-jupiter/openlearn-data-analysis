# Data Analysis Notes

## Table of Contents

- [Presenting Your Analysis](#presenting-your-analysis)
- [Sharing Your Project](#sharing-your-project)
- [Combining Datasets](#combining-datasets)
- [Correlation: Spearman rank correlation coefficient](#correlation-spearman-rank-correlation-coefficient)
- [Vizualizations](#vizualizations)
- [Miscellaneous](#miscellaneous)

## Presenting Your Analysis

There is no right or wrong way to write up data analysis but the important thing is to present the answers to the questions you had. To keep things simple, I suggest the following structure:

1. A descriptive title
1. An introduction setting the context and stating what you want to find out with the data.
1. A section detailing the source(s) of the data, with the code to load it into the notebook.
1. One or more sections showing the processes (calculating statistics, sorting the data, etc.) necessary to address the questions.
1. A conclusion summarising your findings, with qualitative analysis of the quantitative results and critical reflection on any shortcomings in the data or analysis process.

Its good to write the text in a way where the reader doesn't need to understand the code.

## Sharing Your Project

One of the simplest is to create a zip archive, upload it to a cloud service like Dropbox or Google Drive, and publicise the download link.

You can also choose `File -> Download as` to export as a `PDF` or `HTML` file. In VSCode Click the dots for `More Actions`. Make sure you have run all the cells first and that there are no errors. Sharing these files means the recipient wont need to run any code and it'll be read only.

## Combining Datasets

You need a column of common values between the datasets you're combining. You need to take care that these common values really mean the same thing, that they were obtained in the same way when the data was collected.

Also consider the precision of your data and what level of unit to use. If the data isn't very precise, use a larger unit. Eg. the population data used 1000s as the unit. For a countries GDP millions of dollars might be best, especially as its been converted from the original currency and these can cause innaccuracies.

## Correlation: Spearman rank correlation coefficient

To see if life expectancy grows when the GDP increases I will use a statistical measure known as the **Spearman rank correlation coefficient**.

It’s a number between -1 and 1 that describes how well two indicators correlate, in the following sense.

- A value of 1 means that if I rank (sort) the data from smallest to largest value in one indicator, it will also be in ascending order according to the other indicator. In other words, if one indicator grows, so does the other.
- A value of -1 means a perfect inverse rank relation: if I sort the data from smallest to largest according to one indicator, I will see it is sorted from largest to smallest in the other indicator. When one indicator goes up, the other goes down.
- A value of 0 means there is no rank relation between the two indicators.

A positive value smaller than 1 (or a negative value larger than -1) means there is some direct (or inverse) correlation, but it is not systematic across the whole dataset.

The p-value indicates how significant the result is, in a particular technical sense. To say a correlation is statistically significant doesn’t necessarily mean it is important or strong in the real world, but only that there is reasonable statistical evidence that there is some kind of relationship. Typically, the obtained correlation coefficient is considered statistically significant if the p-value is below 0.05.

The pandas module doesn’t calculate complex statistics. There are other modules in the Anaconda distribution for that. In particular, scipy (Scientific Python) has a stats module that provides the spearmanr() function. The function takes as arguments the two columns of data to correlate. Contrary to the functions you’ve seen so far, it returns two values instead of one: the correlation and the p-value. To store both values, simply use a pair of variables, written in parenthesis.

Also remember, correlation is not causation.

## Vizualizations

### Scatterplot

Using a more qualitative view like a scatter plot helps to see relationships that the quantitative analysis might have missed.

**Logarithmic Scale** (multiplicative factor 10, 100, 1000, etc rather than a constant like 10, 20, 30, etc) can be useful for spreading out an axis if the data is too close together.

### Other kinds of viz's

- line graph
- pie chart
- geo data maps
- stem
- histograph
- bar chart

## Miscellaneous

- **heterogenous**: data that is mixed in some way
- **split apply combine pattern**
  - summary operation: a single row is returned for each group (`aggregate()`)
  - filtering or filtration operation: groups are retained or discarded based on a particular property of the group as a whole, Eg. the sum of the values in a group is above some threshold.
