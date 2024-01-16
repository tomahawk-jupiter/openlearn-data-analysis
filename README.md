# Notes from OpenLearn Data Analysis free course

My work from the free [OpenLearn data analysis](https://www.open.edu/openlearn/digital-computing/learn-code-data-analysis/content-section-overview?active-tab=description-tab) course.

I made notes/reference sheet in `PANDAS_NOTES.md` and general data analysis notes in `DATA_ANALYSIS_NOTES.md`.

## Table of Contents

- [Dataset Sources](#dataset-sources)
- [Notebooks in this repo](#notebooks-in-this-repo)
- [How to run `.ipynb` files](#how-to-run-ipynb-files)
- [How to open in Anaconda](#how-to-open-in-anaconda)
- [VSCode extension](#vscode-extension)
- [Pivot Table JavaScript Library](#pivot-table-javascript-library)

## Dataset Sources

Used in course:

- [wolrdbank.org](https://data.worldbank.org/)
  - [GDP](https://data.worldbank.org/indicator/NY.GDP.MKTP.CD?end=2022&start=1960&view=chart)
  - [Life Expectency](https://data.worldbank.org/indicator/SP.DYN.LE00.IN)
  - [Total Population](https://data.worldbank.org/indicator/SP.POP.TOTL?end=2022&start=1960&view=chart)
- [UN Comtrade - trade data](https://comtradeplus.un.org/) API available. Be sure to read codes into pandas as strings not integers or you'll lose leading zeroes.

Other sources:

- [UK government open data site](https://www.data.gov.uk/) – a directory of UK public datasets
- [US government open data site](https://data.gov/) – the home of the US Government’s open data
- [Open Knowledge Global Open Data Index](http://index.okfn.org/dataset/) – a comprehensive directory of national open data initiatives
- [Open Data Inception](https://opendatainception.io/) – a geographic list of over 1500 data portals around the world
- [Google Public Data Explorer](https://www.google.com/publicdata/directory) – a further list of data providers, with charts for some datasets
- Many towns and cities also have their own data sites: search for the name of your town and the keywords ‘open data store’
- Open data published by government departments and agencies such as [performance of UK schools](https://www.compare-school-performance.service.gov.uk/) or [prices paid for house sales in the UK](https://landregistry.data.gov.uk/app/ppd)
- The pandas library supports a growing number of external data sources such as **Google Analytics**.

## Notebooks in this repo

- `part1/pop_tb.ipynb` contains some examples & exercises for using pandas
- `part2/weather.ipynb` more examples & exercises. Cleaning & visualising data
- `part2/weather_project.ipynb` is my first data analysis report/project
- `part3/part3.ipynb` applying functions to columns, joining tables, correlation with scipy (spearmanr)
- `part3/gdp_life_expectency_project.ipynb` answering more questions using the data from `part3.ipynb`
- `part4/tutorial_notes.ipynb` grouping, aggregating, pivot tables
- `part4/milk_project.ipynb` has examples of groups and pivot tables

## How to run `.ipynb` files

You run `.ipynb` files in Jupyter Notebook which comes with Anaconda (which you can install for free). You can also use google colab which you can add to your google dashboard/account for free which lets you open notebooks without installing anything on your machine.

## How to open in Anaconda

Anaconda lets you setup different python environments so that you can install different packages/versions in self contained environments. It comes with a `base` environment:

Activate base environment

```sh
conda activate base
```

Then you can start jupyter notebook which opens a GUI in your browser where you can open/create/edit the `.ipynb` files:

```sh
jupyter notebook
```

Alternatively you can open Anaconda Navigator (GUI) and navigate to jupyter notebook or jupyterLab from there.

```sh
anaconda-navigator
```

## VSCode extension

There is a VSCode extension that will let you open notebooks in vscode. When you open a `.ipynb` file you will have to choose an interpreter. It should open by itelf, or you can press `Ctrl + Shift + P` and go to `Python: Select Interpreter` to change it.

My base environment was `~/Anaconda3/bin/python`.

## Pivot Table JavaScript Library

Can be used to create interactive pivot tables. Can be used in notebook with python.

- [pivottable.js](https://pivottable.js.org/examples/)
- [Python package pivottablejs](https://pypi.org/project/pivottablejs/)

```py
from pivottablejs import pivot_ui

pivot_ui(dataFrame)
```

NOTE: the interactive pivot table didn't work in VSCode but did when running in the browswer, ie. start jupyter notebook from the command line in the conda env. I just noticed that `pivottablejs.html` has been created, you can open this file in the browswer without using jupyter notebook.
