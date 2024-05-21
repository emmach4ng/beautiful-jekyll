---
layout: post
title: Examining Local Investment in Flushing's Small Businesses in the Context of NYC
subtitle: Final Project
gh-repo:
gh-badge:
tags:
comments: true
---

## Why Flushing, Queens?

For my project, I wanted to hone in on the ways that NYC is supporting the Flushing neighborhood because I have a strong personal connection to its small businesses.

My father grew up in Flushing during his early childhood, and my grandparents currently live in Flushing. Even though my family lives in Manhattan, we often to go Flushing to visit Yeye and Nainai or eat our favorite Taiwanese hand-pulled beef noodle soup.

However, what stands out the most as one walks down Flushing's Main Street are the countless, small storefronts owned by local families. In fact, small businesses fuel Flushing's local economy. According to the US Census Bureau in 2020, small businesses with fewer than 10 employees, or microbusinesses, constituted nearly 90 percent of the neighborhood's businesses, which is a significantly higher rate than the nationwide average. Only 18 firms had more than 250 employees, including institutions like hospitals and nursing care facilities.

Evidently, small businesses are the backbone of local economic activity in Flushing. Fortunately, the New York State Comptroller found that between 2000 and 2019, the number of businesses in the Flushing area grew by 81.8%, exceeding the speed of growth in the broader Queens borough (44%) and Manhattan (29.6%), with the vast majority being microbusinesses.

Intrigued by Flushing's thriving ecosystem of small businesses, I wanted to explore one potential factor which may have contributed to this growth in my final project: government intervention and/or other sources of external investment. Through this project, I hoped to find whether the amount of government/external investment into small businesses in Flushing was positively correlated with its upward trend in business formation, and if the amount of investment matches the ratio between Flushing's business formation and the rest of NYC's business formation.

## The Data and Analysis

To observe potential trends in the amount of external investment in both Flushing and NYC as a whole, I utilized datasets from 2018, 2019, and 2020, which entailed financial information about NYC's various Business Improvement Districts (BIDs). BIDs are overseen by the NYC Department of Small Business Services, meant to catalyze small business formation and success. In the datasets I used for this project, the investment information was separated into distinct categories within the overall budget.

To examine Flushing specifically, I extracted the data from its BID, named the "Downtown Flushing Transit Hub."

Since each year (2018, 2019, 2020) was a separate CSV, I parsed through each year individually. For example, here's how I extracted Flushing's data for the year 2018 out of the rest of the BIDs:

~~~

flushing = {} # dictionary to store the data for each year in Flushing

# business improvement district expenditures in 2018
with open("finalproject/2018_BIDs.csv", "r") as f: 

    data = csv.DictReader(f)

    for row in data: # loop thru each district

        # organizes Flushing data only
        if row["BID Name:"].__contains__("Flushing"): # finds the row for Flushing's district
            
            budget = int(row["Assessment revenue"]) + int(row["Government grants"])

            flushing["2018"] = { # creates a nested dictionary for the year 2018 in Flushing
                # metrics of-interest
                "total budget": budget,
                "government grants": row["Government grants"],
                    # assessments + grants = BID budget
                "support and revenue": row["Total support and revenue"],
                "sanitation expenses": row["Sanitation expenses"],
                "marketing and event expenses": row["Marketing, holiday lighting, and special event expenses"],
                "public safety employees": row["Public Safety staff employed"],
                "businesses": row["Individual businesses (retail, restaurant, office, etc.)"]
            }
~~~

I repeated the same process for 2019 and 2020.

Then, to examine the investment for BIDs across NYC, I created variables to add the sum of each metric in each BID in a given year. For example, I used these for 2018:

~~~

budget_2018 = 0
supportrevenue_2018 = 0
sanitation_2018 = 0
marketing_2018 = 0
publicsafety_2018 = 0

~~~

Additionally, to ultimately find an average for each metric throughout 2018-2020, I initialized the following variables:

~~~

total_budget = 0
total_supportrevenue = 0
total_sanitation = 0
total_marketing = 0
total_publicsafety = 0
count_districts = 0

~~~

## Sources used

https://www.osc.ny.gov/files/reports/osdc/pdf/report-10-2012.pdf
https://www.osc.ny.gov/press/releases/2021/12/dinapoli-releases-economic-report-greater-flushing-area#:~:text=From%202000%20to%202019%2C%20total,with%20fewer%20than%2010%20employees.