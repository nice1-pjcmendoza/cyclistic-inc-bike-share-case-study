# Cyclistic Bike-Share Case Study

## Foreword from the Data Analyst

Welcome to my Google Data Analytics Capstone Project! In this case study, I will analyze Cyclistic’s dataset and offer recommendations, just like what a junior data analyst would do in his free time😊. To complete this task, I will perform the data analysis process: ask, prepare, process, analyze, share, and act. I will use the power of Power BI to complete this challenge.

Let's do this!

## Scenario

[Extracted from GDA Capstone CS1]

You are a junior data analyst working in the marketing analyst team at Cyclistic, a [fictional] bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations. 

## About Cyclistic

[Extracted from GDA Capstone CS1]

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends. 

Three questions will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes differently?

2. Why would casual riders buy Cyclistic annual memberships?

3. How can Cyclistic use digital media to influence casual riders to become members?

## Ask: State the Business Task

Determine how **MEMBERS** and **CASUAL** users use Cyclistic bikes differently. Specifically:
1. Analyze the data and identify trends and patterns,
2. Create visualizations, and
3. Provide key findings and recommendations. 

Let's ask the SMART questions.

**Specific**. Which bike type is the most preferred by MEMBERS and CASUAL users?

**Measurable**. What percentage of the total rides is made by the MEMBERS?

**Action-oriented**. How can we convince the CASUAL users to join the annual membership?

**Relevant**. What programs can we launch to attract more users to ride bikes?

**Time-bound**. What trends can we observe from different short-term time periods?


## Prepare: Do the Datasets ROCCC?

Cyclistic’s datasets can be downloaded [here](https://divvy-tripdata.s3.amazonaws.com/index.html). This case study covers the latest 12-month data available in the repository, i.e., April 2022 to March 2023. The files are first-party datasets owned, prepared and shared by Cyclistic with file naming format ‘YYYYMM-divvy-tripdata.csv’. Once stored locally, all 12 files have a total size of 1.03 GB!

Let's be reminded that Cyclistic is a fictional company that represents a real-world organization. Its datasets are prepared to maintain anonymity. The data has been made available by Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement).

STEP 1: Download and Store the Datasets

1. Download 12 zip files from the repository

2. Extract the comma-separated values (CSV) files

3. Save all 12 CSV files in a folder preferably without any irrelevant files

4. Rename the CSV files to YYYYMM-divvy-tripdata.csv format for consistency


Before we analyze the datasets, we should ask ourselves this first: "Does this data ROCCC?" 

Reliable. Data is accurate, complete and unbiased. 

Original. The datasets are first-party data owned, prepared and shared by Cyclistic.

Comprehensive. Per case study guide, "... the datasets are appropriate and will enable to answer the business questions."

Current. The repository is regularly updated to maintain relevance.

Cited. The data has been made available by Motivate International Inc. under this license.

The answer is YES so we can be sure that our datasets are unbiased and are credible. 

And by that, we can now proceed with the next phase.

## Process: Clean and Manipulate the Data

My initial plan was to use SQL and Excel to extract, transform, load and visualize the datasets. I later opted to use Power BI instead because it can do all the steps (plus no need to import/export between software) and because I’m already proficient with it (at this point, Tableau is a no-go for me).

I’ll try other combinations of tools I learned from the GDA course (i.e., SQL, Excel, R and Tableau), but that’s for another post.

We start cleaning the data by merging the datasets into a single table first (as part of data wrangling). Since all 12 datasets have the same columns, this will be easy to execute.

STEP 2: Load Data in Power Query Editor (PQE)

     Open Power BI, then open the PQE by clicking the "Transform data" in the Home tab

     In the PQE, click "New Source" > click "More" > "All" tab > click "Folder" 

     Go to windows explorer > locate the CSV files you saved in STEP 1.3 > copy the directory

     Go back to PQE > paste the directory in the "Folder path" field > hit "OK"

     Check if all 12 CSV files are loaded > hit "Combine & Transform Data"

     "Combine Files" window will appear > hit "OK"

     All your data will now be loaded in the Power Query Editor.


STEP 3: Transform Data in Power Query Editor

         Remove the columns

                Source.Name, start_station_id, end_station_id, end_station_name, start_lat, start_lng, end_lat,  end_lng

         Rename the columns

                rideable_type > ride_type

                started_at > start_time

                ended_at > end_time

                member_casual > user_type

         Replace values on each column

                Column ride_type: right click column header > click "Replace Values..." > 

electric_bike > Electric

classic_bike > Classic

docked_type > Docked

                Column user_type: right click column header > click "Transform" > click "Capitalize Each Word"

         Check each column's datatype


STEP 4: Clean Data in Power Query Editor

     Check each column for inconsistencies (impossible values, wrong spelling, errors, etc.) and nulls

     Add custom columns

            trip_duration: "Add Column" tab > hit "Custom Column" > type in the formula "[end_time]-[start_time]"

> right click column header > click "Transform" > click "Total Minutes"

            start_date: right click start_time column header > click "Duplicate Column" > find the duplicate > click "Transform" > click "Date Only"

            start_hour: follow the previous step > click "Transform" > click "Hour" > hit "Hour"

            day_of_week: follow the previous step > click "Transform" > click "Day" > hit "Day of Week"

            day_SMTWTFS: follow the previous step > click "Transform" > click "Day" > hit "Name of Day"

     Filter out outliers

            Trip duration that are negative and less than 1 minute are physically impossible

            We'll filter out other outliers in the next phase

     Filter out empty observations/rows

            Some start station rows are empty probably because the GPS did not work


We removed several columns in STEP 3.1 because I preferred not to explore the geographical data at the moment. In Power BI, the latitude and longitude must be in decimal number format.

Once we're satisfied with cleaning and manipulating, we hit "Close and Apply" and we return to Power BI for data analysis.

### BEFORE

![Files Loaded in the Power Query Editor](Assets\process-1-after.png)
*This image...*

### AFTER
![Data Transformed in the Power Query Editor](Assets\process-1-after.png)
*This image...*

## Analyze: Find Insights, Trends and Patterns

We go back to our business task: Determine how MEMBERS and CASUAL users use Cyclistic bikes differently. Let's also use the SMART questions we formulated earlier as our guide.

STEP 5: Analyze using Power BI

These are my plans in analyzing our data:

     We use count of trip_id to get the total number of trips, which we'll later refer to as "Bike Activity"

     We use the average of trip_duration (instead of sum) to further differentiate the user_type

     We use ride_type or user_type as legends

     We use pie, bar and line charts (just the simple charts) since these are more preferred by the Executives, our stakeholders

     We use pie chart to find the value and percentage composition of each user_type

     We use bar chart to further split user_type by ride_type

     We also use bar chart and sort it in descending order to identify the top start_station_name

     We use line chart to get the daily and weekly trends

     We use shades of blue to differentiate user_type because I like blue


The good thing about Power BI is that analysis and visualization go simultaneously. Cards visual can be used to instantly determine the Bike Activity and Average Trip Duration. You can use the Matrix visual to simulate a pivot table, which can be formatted into a heatmap.

To be transparent, I also have other plans that I scrapped along the way because they're difficult to execute. For example, I tried plotting the start and end stations to visualize the routes majority of the users took, but I'm limited by what I currently know. I also drafted a heatmap for daily and weekly trends, but it ended up looking like an abstract art, and it did not show what I intend to emphasize.

After discovering several insights and trends, let's make visualizations to impress the Executives!

## Share: Create the Story

We use the 10-second rule to assess if our visualizations are effective in communicating the message. As we mentioned in STEP 5.4, we'll just use simple charts like pies, bars and lines. Subtitles are also included to give our insights. I used MS PowerPoint to create appealing underlays complete with the company logo, headers, white boxes, side tabs and background. 

Check out these screenshots from my Power BI output. 

![Introduction Slide](Assets\output-1-intro.png)

![Users Slide](Assets\output-2-users.png)

![Trips Slide](Assets\output-3-trips.png)

## Act: Give Actionable Insights & Recommendations

Finally, we end our case study by sharing our insights and recommendations. Our statements must be clear, concise and consistent.

Check out this screenshot from my Power BI output.

![Insights Slide](Assets\output-4-insights.png)

## Closing Remarks

And by that we finally finished our very first case study! It took me a week to finalize the Power BI output and setup an online portfolio. The contents, and its delivery, might not be as polished and as optimized as I envision it to be, but I hope I gave a satisfactory output at the very least.

The [Google Data Analytics](https://www.coursera.org/professional-certificates/google-data-analytics) course at Coursera is my entry point in the world of data analytics. There is so much more to learn and explore!

To anyone reading this, thank you.

## About the Data Analyst

Paul Mendoza is a career shifter from the power industry. He aspires to become a data analyst in the hopes of fulfilling his dream of setting up a glorious pc with wide monitors. As someone said, "data is the new oil." But just like crude oil, we should apply the distillation process to obtain quality information ready to combust!


``
Introduction
Background
Tools I Used
Analysis
What I Learned
Conclusions
``