# Case Study 1
[toc]
## Ask
### Guiding questions
* What is the problem you are trying to solve?
  * How annual members and casual riders use Cyclistic bikes differently.
* How can your insights drive business decisions?
  * By analyzing Cyclistic's historical data, data-driven decisions can be made to achieve the goal.
### Key tasks
1. Identify the business task
2. Consider key stakeholders
### Deliverable
- [x] A clear statement of the business task
## Prepare
### Guiding questions
* Where is your data located?
  * On my server storage.
* How is the data organized?
  * The data is organized in the form of .csv (comma-separated values), with 13 columns including ride_id, rideable_type, etc., to describe a single ride record.
* Are there issues with bias or credibility in this data? Does your data ROCCC?
  * Potential biases might occur. Some of the tripdata included Trips less than 1 minute or greater than 24 hours, while some tripdata did not have such constraint.
  * The data is not ROCCC:
    * Reliable:
      * The dataset comes from an interational Inc. with proper license (should be considered as reliable).
    * Original: 
      * The dataset is originally made available by Motivate International Inc. 
    * Comprehensive
      * The dataset is well organized in the .csv form.
    * Current:
      * The dataset includes the most recent data (2021/10 for now)
    * Cited
      * The dataset is originally made available by Motivate International Inc.
* How are you addressing licensing, privacy, security, and accessibility?
  * The entire dataset is under its own data license agreement, which describes privacy, security, and accrssibility to the dataset.
* How did you verify the data’s integrity?
  * I loaded and checked all the historical data by the corresponding columns in all the .csvs. Most of the data in the dataset comes with consist columns and data types. However, some of the data did not share all the columns, for instance, trips data before 2020, like "Divvy_Trips_2019_Q4.csv", did not have "rideable_type" column. To be mentioned, there are several file naming conventions existed. For instance, "Divvy_Trips_{Year}_{Q}.csv", "{Year}{Month}-divvy-tripdata.csv", and "Divvy_Stations_{Year}_{Q}.csv". To make sure the data's integrity, metadata recored in each README files within each .zip file should be carefully examined.
* How does it help you answer your question?
  * The historical data could be used to provide insights and capture different trends between members and casual users.
* Are there any problems with the data?
  * Null values detected in many data. For instance, "end_station_name", "end_station_id", and "end_lat" columns contained numerous NaNs in "202004-divvy-tripdata.csv".
  * For some of the .csv files, potential data imbablance problems could exist. For example, in "Divvy_Trips_2020_Q1.csv", the proportion of "member" and "casual" records for "member_casual" column is 0.8864 v.s 0.1136. To avoid potential biases, analysis should be conducted using muliple .csv files. 
  * Some of the .csv files do not have "member_casual" column, instead, they have a column named "usertype" with entities "Customer" and "Subscriber". However, these .csv files do not come with metadata, and therefore are hard to integrate (I personally suggested that "Subscriber" referred to "member" and "Customer" referred to "casual"). Also, for some .csv files, "usertype" column existed entity "Dependent", which I don't know the meaning of it.
  * "gender" and "birthday" information are missing for some of the .csv files.
  * For years after 2017, station data is missing.
  * "Divvy_Trips_2019_Q1.zip" and "Divvy_Trips_2019_Q2.zip" contained data with missing ".csv" suffix.

### Key tasks
1. Download data and store it appropriately.
2. Identify how it’s organized.
3. Sort and filter the data.
4. Determine the credibility of the data.
### Deliverable
* A description of all data sources used
## Process
### Guiding questions
* What tools are you choosing and why?
  * I use python language with pandas library for data analysis. Pandas (python data analysis library) is an easy and powerful library for data analysis.
* Have you ensured your data’s integrity?
  * Yes, I removed records with Nans, and concatenated all collected .csv files (incompatiable columns were removed). Also, "Divvy_Trips_2018_Q1.csv" has different feature naming convention comparing to others and are therefore renamed. 
* What steps have you taken to ensure that your data is clean?
  * Records with Nan values were removed.
  * ID columns were removed.
  * Station related columns were removed (since no available station information after 2017).
  * Add "tripduration" column to .csv files without this column (calculated by "ended_at"-"started_at").
  * Add "Season", "Weekday", "Start_hour" and "End_hour" columns. 
  * commas in "tripduration" were removed (such as "1,783.0") and converted to numbers.
* How can you verify that your data is clean and ready to analyze?
  * No Nan values existed in the cleaned dataset.
  * The data type of "tripduration" is now float64, meaning all the values are consistent.
  * "usertype" now containes only two possible values: "Customer", and "Subscriber".
* Have you documented your cleaning process so you can review and share those results?
  * Yes, the cleaning process is written in the markdown cells or comments.
### Key tasks
1. Check the data for errors.
2. Choose your tools.
3. Transform the data so you can work with it effectively.
4. Document the cleaning process
### Deliverable
- [x] Documentation of any cleaning or manipulation of data
## Analyze
### Guiding questions
* How should you organize your data to perform analysis on it?
  * I integrated all entire historical data into a single integrated dataset.
* Has your data been properly formatted?
  * Yes, the "tripduration" column now has the type of float (rather than a mixture of strings and numbers).
* What surprises did you discover in the data?
  * As a whole:
    * Subscriber records are around two times more than customer records (20722460 v.s. 9049927). 
    * The mean trip duration of customers (2167.102 secs) is higher than subscribers (822.2 secs).
    * The standard deviation of customer records is higher than that of subscribers (26440.44 v.s. 9585.859).
  * In the view of 7 days of a week:
    * Subscribers' records mainly focused on Monday to Friday, while Cutomers' records mainly focused on weekends, implying that the main population of subscribers is consist of workers.
  * In the view of 24 hours in a day:
    * The peaks of subscribers records are 8:00 AM and 17:00 PM, reassuring that the main population of subscribers is consist of workers.
* What trends or relationships did you find in the data?
  * Subscribers utilize the bike service more often, and the trip durations are relatively short. This might suggest that subscribers take short and regular bike rides.
* How will these insights help answer your business questions?
  * We can design a discount strategy especially for customers. For example, 30% discounts on weekends for subscribers will encourage customers to subcribe, as they often rent bikes on weekends, or discounts for long-term rental.
### Key tasks
1. Aggregate your data so it’s useful and accessible.
2. Organize and format your data.
3. Perform calculations.
4. Identify trends and relationships
### Deliverable
* A summary of your analysis
## Share
### Guiding questions
* Were you able to answer the question of how annual members and casual riders use Cyclistic bikes differently?
  * As described in above.
* What story does your data tell?
  * As described in above.
* How do your findings relate to your original question?
  * Trends captured from data can be used to distinguish customers and subscribers, and further design custom stragies.
* Who is your audience? What is the best way to communicate with them?
  * Stakeholders of the company. Making a professional data anaylsis report will be great and convincing.
* Can data visualization help you share your findings?
  * Sure, graphs are more visually pleasent then numbers.
* Is your presentation accessible to your audience?
  * Yes if it is open-sourced or open-accessed.
### Key tasks
1. Determine the best way to share your findings.
2. Create effective data visualizations.
3. Present your findings.
4. Ensure your work is accessible.
### Deliverable
Supporting visualizations and key findings
## Act
### Guiding questions
* What is your final conclusion based on your analysis?
  * Design a discount strategy especially for customers based on the characteristics of customers' habits.
* How could your team and business apply your insights?
  * They could draw up a discount plain based on the insight.
* What next steps would you or your stakeholders take based on your findings?
  * We could try to implement the plain and see if the plain works.
* Is there additional data you could use to expand on your findings?
  * With station information, more insights moght be found. For instance, we can find out stations with more customers' records, and arrange more sales on these stations to promote subscriptions.
### Key tasks
1. Create your portfolio.
2. Add your case study.
3. Practice presenting your case study to a friend or family member.
### Deliverable
Your top three recommendations based on your analysis
