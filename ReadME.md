# Wikipedia Article View Traffic Analysis (2015-2024)

### DATA-512

### Homework 1

### Title: Professionalism & Reproducibility

## Goal

This project aims to construct and analyze a dataset of monthly article traffic for selected Wikipedia pages from July 1, 2015, to September 30, 2024. The dataset provides insights into page view trends, enabling the analysis of article popularity and traffic patterns for both desktop and mobile devices.

The motivation is to gain practical experience in open scientific research, emphasizing reproducibility through accessible data, transparent documentation, and adherence to licensing standards.

## Licenses

### Source Data

The data is sourced from the Wikimedia Foundation via their publicly available [Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). According to the Wikimedia Foundation's [Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), users may freely utilize the content with proper attribution, preservation of open licenses, and respect for copyright. Appropriate attribution is provided to ensure compliance with these terms.

### Data Acquisition Code

Code snippets in Wikipedia_article_analysis.ipynb are adapted from examples developed by Dr. David W. McDonald for DATA 512 at the University of Washington. This code is licensed under Creative Commons CC-BY.

## Documentation

### API

1. Pageviews API: Provides page view analytics for Wikimedia projects, starting from July 1, 2015.

### Packages

1. urllib: Used for fetching data from the Pageviews API.
2. pandas: Employed for processing time series data.
3. matplotlib: Used for visualizations summarizing the analysis.

## Generated Files

Executing Wikipedia_article_analysis.ipynb generates multiple time series datasets reflecting monthly activity for articles in rare-disease_cleaned.AUG.2024.csv, focusing on user page views. Each file is of JSON type. The data is structured into three files names as follows:

1. rare-disease_monthly_cumulative_201501-202409.json: Contains total page view activity (desktop + mobile) for each article.
2. rare-disease_monthly_desktop_201501-202409.json: Contains monthly desktop page view activity.
3. rare-disease_monthly_mobile_201501-202409.json: Contains monthly mobile page view activity.

Each of the above file contain a dictionary with the disease as the key and a list of JSONs as the value. Each element in the JSON list has the below schema:

```Text
{
    string: [                         #Page title
        {
            "project": string,        #Wikimedia domain and subdomain
            "article": string,        #Page title
            "granularity": string,    #Time interval between datapoints
            "timestamp": string,      #Timestamp in YYYYMMDDHH format
            "agent": string,          #Type of user agent
            "views": integer          #Number of page views
        }
  ]
}
```

## Plots

1. max_min_avg_plot.png: Graph showing articles with the highest and lowest average page requests for both desktop and mobile access.
2. top10_viewed_articles.png: Graph displaying the top 10 articles with the highest peak page views for desktop and mobile access types.
3. least_months_of_data.png: Graph illustrating the 10 articles with the fewest months of available data for both desktop and mobile access.

## Issues faced/Special considerations

1. The API calls take quite sometime to run (around 30 minutes on a mac m1 with 8gb RAM). So patiently wait for it to be completed.
2. The original data acquisition code from Dr. McDonald failed to encode '/' in article titles (e.g., 'Sulfadoxine/pyrimethamine'). I needed to add a safe parameter to the urllib.parse.quote method.The safe='' parameter ensures all characters, including '/', are encoded properly.
3. API documentation changes many times with updates. In case of any issues, check the [Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html) documentation for more details.
