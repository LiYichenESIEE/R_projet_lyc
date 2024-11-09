# Analysis of 2020 Election Results, Median Income, and Education in New York State

## Table of Contents

-   [Project Overview](#project-overview)
-   [User Guide](#user-guide)
    -   [Prerequisites](#prerequisites)
    -   [Installation](#installation)
    -   [Running the Dashboard](#running-the-dashboard)
-   [Data](#data)
    -   [Data Sources](#data-sources)
    -   [Data Access](#data-access)
-   [Developer Guide](#developer-guide)
    -   [Project Structure](#project-structure)
    -   [Code Architecture](#code-architecture)
    -   [Adding New Features](#adding-new-features)
-   [Rapport d'Analyse](#rapport-danalyse)
-   [Copyright](#copyright)
-   [License](#license)

## Project Overview {#project-overview}

The **Analysis of 2020 Election Results, Median Income, and Education in New York State** is a Shiny dashboard developed in R that provides an interactive exploration of the relationships between median household income, education levels, and voting patterns in the 2020 U.S. General Election within New York's congressional districts. Utilizing publicly available Open Data, the dashboard offers various visualizations, including histograms, geolocated maps, scatter plots, and bar charts to illuminate key i...

## User Guide {#user-guide}

### Prerequisites {#prerequisites}

Before running the dashboard, ensure that you have the following installed on your machine:

-   **R** (version 4.0 or higher)
-   **RStudio** (optional but recommended)
-   **Git** (for cloning the repository)

### Installation {#installation}

1.  **Clone the Repository**

    Open your terminal or Git Bash and run:

    ``` bash
    git clone https://github.com/yourusername/my_shiny_app.git
    ```

2.  **Navigate to the Project Directory**

    ``` bash
    cd my_shiny_app
    ```

3.  **Install Required R Packages**

    Open R or RStudio and install the necessary packages by running the following command:

    ``` r
    source("install_packages.R")
    ```

    Alternatively, you can manually install the packages listed in the `requirements.txt` by executing:

    ``` r
    install.packages(c(
      "tidycensus", "tidyverse", "shinydashboard", "sf",
      "tmap", "tigris", "ggplot2", "ggthemes", "dplyr",
      "broom", "ggrepel", "viridis", "plotly", "shiny"
    ))
    ```

### Running the Dashboard {#running-the-dashboard}

1.  **Open the Project in RStudio**

    Open `my_shiny_app.Rproj` in RStudio.

2.  **Launch the Shiny App**

    In the R console, run:

    ``` r
    source("app.R")
    ```

    The dashboard should launch in your default web browser, accessible at `http://localhost:8080`.

## Data {#data}

## Data Sources {#data-sources}

1.  **2020 General Election Results Disaggregated to 2020 Census Blocks**
    -   **Description:** Election results for the 2020 U.S. General Election at the census block level in New York.
    -   **Format:** Shapefile (`.shp` along with accompanying files)
    -   **Source:** [Redistricting Data Hub](https://redistrictingdatahub.org/state/new-york/)
2.  **New York Congressional Districts**
    -   **Description:** Geospatial data for New York's congressional districts.
    -   **Format:** RDS file (`.rds`)
    -   **Source:** Data downloaded using the `tidycensus` R package, based on the 2020 American Community Survey (ACS).
3.  **New York Income and Education Data**
    -   **Description:** Median household income and education statistics, including the number of people with a bachelor's degree or higher, at the census tract level in New York.
    -   **Format:** RDS file (`.rds`)
    -   **Source:** Data downloaded using the `tidycensus` R package, based on the 2020 American Community Survey (ACS).

### Data Access {#data-access}

All datasets used in this project are publicly accessible and can be retrieved using the provided scripts in the `R/helpers.R` file. The raw data files are stored locally in the `data/raw/` directory, and processed data is saved in the `data/processed/` directory.

-   **Raw Data Directory:** `data/raw/`
-   **Processed Data Directory:** `data/processed/`

## Developer Guide {#developer-guide}

### Project Structure {#project-structure}

```         
my_shiny_app/
├── R/
│   ├── global.R
│   ├── helpers.R
│   ├── server.R
│   └── ui.R
├── data/
│   ├── processed/
│   │   └── merged_data_sf.rds
│   └── raw/
│       ├── 2020 General Election Results Disaggregated to 2020 Census Blocks/
│       │   ├── README.txt
│       │   ├── ny_2020_gen_2020_blocks.cpg
│       │   ├── ny_2020_gen_2020_blocks.dbf
│       │   ├── ny_2020_gen_2020_blocks.prj
│       │   ├── ny_2020_gen_2020_blocks.shp
│       │   └── ny_2020_gen_2020_blocks.shx
│       ├── ny_congressional_districts.rds
│       └── ny_income_data.rds
├── app.R
├── README.md
├── requirements.txt
└── my_shiny_app.Rproj
```

### Code Architecture {#code-architecture}

The application follows a modular structure using Shiny's server and UI scripts. Below is a visual representation of the code architecture:

``` mermaid
graph LR
    app.R --> global.R
    app.R --> ui.R
    app.R --> server.R
    global.R --> helpers.R
    server.R --> plotly
    ui.R --> shinydashboard
```

### Adding New Features {#adding-new-features}

To add a new page or graph to the dashboard:

1.  **Update `ui.R`**

    Add a new `menuItem` in the sidebar and a corresponding `tabItem` in the `dashboardBody`.

2.  **Update `server.R`**

    Implement the server-side logic for the new visualization, ensuring it follows the reactive programming paradigm.

3.  **Modify `helpers.R` or `global.R` if Necessary**

    Add any new data processing functions or load additional data as required.

4.  **Document Your Changes**

    Ensure that all new functions and components are well-documented with comments explaining their purpose and functionality.

## Analysis Findings

### Income and Voting Patterns

-   **Lack of Significant Correlation:** The regression analysis indicates that there is no statistically significant linear relationship between median income and the vote shares for either Biden or Trump in New York State's congressional districts. The p-values for median income in both the Biden and Trump vote share models are greater than 0.5, suggesting that median income is not a significant predictor of voting preference.

-   **Diverse Income Levels Among Voters:** High median income districts do not consistently favor one candidate over the other. For instance, **Congressional District 1** has a high median income of **\$106,318** but shows a slight preference for Trump with a **52%** vote share. Conversely, **Congressional District 12**, with an even higher median income of **\$120,837**, overwhelmingly supports Biden with an **85%** vote share.

### Education Levels

-   **No Significant Predictive Power:** Similar to income, education levels---as measured by the percentage of residents holding a bachelor's degree or higher---do not significantly predict vote shares for Biden or Trump. The p-values in the regression models are around 0.18, indicating a lack of statistical significance.

-   **Inconsistent Patterns:** Districts with both high and low education shares exhibit strong support for Biden. **Congressional District 12** has a high education share of **36.77%** and a high Biden vote share of **85%**, while **Congressional District 15** has a low education share of **10.54%** but still shows strong support for Biden with an **87%** vote share.

### Urban vs. Rural Divide

-   **Urban Districts Favor Biden:** The data reveals a pronounced urban-rural divide in voting patterns. Urban districts, particularly those in New York City (e.g., Districts 5, 6, 7, 8, 9, 10, 12, 13, 14, and 15), show significantly higher vote shares for Biden, often exceeding **80%**.

-   **Rural Districts Favor Trump:** Rural districts tend to favor Trump. For example, **Congressional Districts 21, 22, and 23** are rural areas where Trump receives approximately **55%** of the vote share.

### Spatial Distribution

-   **Geographic Clustering:** There is a clear spatial clustering of voting patterns, with urban areas leaning Democratic and rural areas leaning Republican. This suggests that geographic location and the associated lifestyle factors may play a more critical role in voting behavior than income or education alone.

### Notable Trends and Anomalies

-   **Exception to Expected Correlations:** Contrary to common assumptions, higher median income and education levels do not correlate strongly with increased support for Biden in this dataset.

-   **Influence of Other Factors:** The lack of significant correlation between income, education, and voting patterns suggests that other variables---such as urbanization, demographic composition, and cultural factors---may have a more substantial impact on voter preferences in New York State.

### Regression Analysis Summary

-   **Median Income Models:** The regression models for both Biden and Trump vote shares with median income yield low R-squared values (adjusted R-squared around **-0.02401**), indicating that median income explains very little of the variance in vote shares.

-   **Education Share Models:** Similarly, the models using education share have low explanatory power, with adjusted R-squared values around **0.03256**. The coefficients for education share are not statistically significant predictors of vote share.

-   **Implications:** These results imply that neither median income nor education share is a strong predictor of voting behavior in New York State's congressional districts during the 2020 election.

------------------------------------------------------------------------

*Overall, the analysis suggests that in New York State, particularly in the context of the 2020 election, factors other than median income and education levels---such as urbanization and demographic characteristics---play a more significant role in shaping voting patterns across congressional districts.*

## Copyright {#copyright}

I hereby declare that the code provided in this project is my own work(YICHEN_LI), except for the lines or sections explicitly acknowledged below:

-   Any external code snippets or functions used from third-party sources are properly cited within the codebase.
-   For each line or block of code borrowed from external resources, the source is referenced, and the syntax is explained.

Any code not explicitly cited above is deemed to be original work by the author(s). Failure to declare external sources constitutes plagiarism.

## License {#license}

This project is licensed under the [MIT License](LICENSE).
