## PyDataPeek 

![](https://github.com/UBC-MDS/pydatapeek/workflows/build/badge.svg) [![codecov](https://codecov.io/gh/UBC-MDS/pydatapeek/branch/master/graph/badge.svg)](https://codecov.io/gh/UBC-MDS/pydatapeek) ![Release](https://github.com/UBC-MDS/pydatapeek/workflows/Release/badge.svg)

[![Documentation Status](https://readthedocs.org/projects/pydatapeek/badge/?version=latest)](https://pydatapeek.readthedocs.io/en/latest/?badge=latest)

### Project Proposal
Data scientists are expected to orient business users to the datasets by analyzing in a way that is accessible and easy to understand. This process is the first step to building trust in the analysis.

PyDataPeek is a package that enables data scientists to efficiently generate a visual summary of a dataset. This package includes functions that show the size of the dataset, a visual summary of missing data, a sample of the dataset showing the data types as well as exploratory visualizations for quantitative and qualitative data.

This package is also useful for business users who have to interact with data and want to begin exploring the data without using too much code or having to open a potentially large dataset on Excel. 

### Functions in this package
All functions take in csv or Excel files as inputs to generate user-friendly summaries of the ingested dataset.
1. **missing_data_overview**: Returns a visualization of the data where missing values are highlighted and the number of rows and columns are visually displayed. A heatmap will be used here to highlight the missing values so it's easy for users to have an overview of which part is missing in the data.
2. **sample_data**: Returns a dataframe that displays the column names as rows, an example of one row, the data type of each column and summary statistics for each column depending on the data type. Integer data is summarized with number of unique values, text data is summarized with average length of string and float data is summarized with the median of the values.
3. **explore_with_histograms**: Returns saved png files of histograms that shows the distribution of responses for given columns. The given list of numerical columns can be chosen by user.
4. **explore_with_word_bubble**: Returns a saved word bubble visualization for text data given column name. This would allow users to know what are the most frequently used words for each column in a short time.

### How this fits in the Python ecosystem
Several Python packages are available that support exploratory data analysis but none are specific to the targeted use cases here - a simple and technologically friendly way of summarizing data. 
- [Pandas Profiling](https://pandas-profiling.github.io/pandas-profiling/docs/): This package generates a report of a dataframe that has some of the features in the proposal. Our package will differ from this by offering the user simpler summaries that are friendlier to a non-technical audience.
- [Python Pandas](https://pandas.pydata.org): Our package will leverage `pandas` functionality to manipulate dataframes. Our package functionality overlaps with some functions such as [`pd.describe`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html) which computes summary statistics for dataframes. The package differs in that it aims to offer summary statistics dependent on data type, including long form text data. 
- [Python Altair](https://altair-viz.github.io), [Python Seaborn](https://seaborn.pydata.org) and [Python WordCloud](https://github.com/amueller/word_cloud): These visualization packages will be used to create visualizations that summarize the dataset as well as user-defined features in the dataset. 

### Installation:
This project is under development! Upon it's first release, it can be installed with the following instructions.

```
pip install pydatapeek --extra-index-url=https://test.pypi.org/simple/
```

### Dependencies:
Note that `selenium` and `chromedriver` are needed to save Altair charts. More information on installation can be found [here](https://altair-viz.github.io/user_guide/saving_charts.html).

### Usage:
We detail an example usage of our function below. The sample data file that we have used below can be found [here](https://github.com/UBC-MDS/PyDataPeek/blob/master/usage/example.csv). The following example assumes that the file has been downloaded as `example.csv` in the root of your working directory. 

#### Setup

```
from PyDataPeek import PyDataPeek as pdp
```

#### Check for missing data
**Input**
```
pdp.missing_data_overview('example.csv')
```
**Output**
A `.png` file in your working directory named `0_heatmap.png`:

![](usage/0_heatmap.png)

#### View summary statistics of data
**Input**
```
pdp.sample_data('example.csv`)
```
**Output**
|            | sample_record                                              | data_type | summary                          | 
|------------|------------------------------------------------------------|-----------|----------------------------------| 
| Unnamed: 0 | 1                                                          | int64     | unique values: 4                 | 
| A          | 1.0                                                        | float64   | median value: 1.0                | 
| B          | 2013-01-02                                                 | object    | average length of string: 10.0   | 
| C          | 0.5049417                                                  | float64   | median value: 0.34510475         | 
| D          | 3                                                          | int64     | unique values: 1                 | 
| E          | train                                                      | object    | average length of string: 4.2    | 
| F          | foo                                                        | object    | average length of string: 3.0    | 
| movies     | "Young couple on the road, minding their own business ..." | object    | average length of string: 1336.2 | 

...

#### View histogram of a numerical column of the data
**Input**
```
pdp.explore_w_histograms('example.csv', columns_list=['C'])
```
**Output**

A `.png` file in your working directory named `C_chart.png`:

![](usage/C_chart.png)

#### View wordcloud of a text column of the data
**Input**
```
pdp.word_bubble('example.csv', column="movies")
```
**Output**

A `.png` file in your working directory named `0_wordcloud.png`:

![](usage/0_wordcloud.png)



### Documentation
The official documentation is hosted on Read the Docs: <https://PyDataPeek.readthedocs.io/en/latest/>

### Credits
This package was created with Cookiecutter and the UBC-MDS/cookiecutter-ubc-mds project template, modified from the [pyOpenSci/cookiecutter-pyopensci](https://github.com/pyOpenSci/cookiecutter-pyopensci) project template and the [audreyr/cookiecutter-pypackage](https://github.com/audreyr/cookiecutter-pypackage).






