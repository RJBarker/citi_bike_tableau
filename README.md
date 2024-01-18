# citi_bike_tableau

### Tableau Public File

[Ryan Barker - citi_bike_v3](https://public.tableau.com/views/citi_bike_v3/CitiBike_Analysis?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)

------

### Scenario

Congratulations on your new job! As the new lead analyst for the [New York Citi Bike](https://en.wikipedia.org/wiki/Citi_Bike) program, you are now responsible for overseeing the largest bike-sharing program in the United States. In your new role, you will be expected to generate regular reports for city officials looking to publicize and improve the city program.

Since 2013, the Citi Bike program has implemented a robust infrastructure for collecting data on the program's utilization. Each month, bike data is collected, organized, and made public on the [Citi Bike Data](https://www.citibikenyc.com/system-data) webpage.

However, while the data has been regularly updated, the team has yet to implement a dashboard or sophisticated reporting process. City officials have questions about the program, so your first task on the job is to build a set of data reports to provide the answers.

------

### Instructions

Your task in this assignment is to aggregate the data found in the Citi Bike Trip History Logs and find two unexpected phenomena.

- Design 2–5 visualizations for each discovered phenomenon (4–10 total). You may work with a timespan of your choosing. Optionally, you can also merge multiple datasets from different periods.
- Use your visualizations (not necessarily all of them) to design a dashboard for each phenomenon. The dashboards should be accompanied by an analysis explaining why the phenomenon may be occurring.
- Create one of the following visualizations for city officials:
    - Basic: A static map that plots all bike stations with a visual indication of the most popular locations to start and end a journey, with zip code data overlaid on top.
    - Advanced: A dynamic map that shows how each station's popularity changes over time (by month and year). Again, with zip code data overlaid on the map.
    - The map you choose should also be accompanied by a write-up describing any trends that were noticed during your analysis.
- Create your final presentation:
    - Create a Tableau story that brings together the visualizations, requested maps, and dashboards.
    - Ensure your presentation is professional, logical, and visually appealing.

------

### Data Retrieval

#### Citi Bike

- I opted to retrieve data for Jersey City from the range of data available from the Citi Bike service
- I found that the datasets here were much more manageable in terms of size compared to the data for whole service
- My interest was to look at how the weather affects the service usage levels, particularly for the Summer and Winter months.
- For the summer months:
    - I obtained the data files for June, July and August
- For the winter months:
    - I obtained the data files for November, December and January

#### Weather Data

- As previously mentioned, I was keen to look at the trends which occur due to weather variances
- Some question's I wanted to look at:
    - How does peak usage hours compare between summer and winter months?
        - Do weekday usage vary greatly to weekend usage?
    - Does the temperature play a role on the number of rides occurring?
        - What temperature's saw the most usage in Summer?
        - How does that compare to the Winter?
    - Does the temperature cause average trip times to increase/decrease?
- To obtain the weather data for both Summer and Winter months, I used the API from [Open-Meteo.com](https://www.open-meteo.com/).
- This service offers historical hourly weather data, which was ideal for my analysis, among many other weather data services.
- My code to retrieve this data can be found:
    - Summer Months [Click Here](Data_Handling/Weather_Extract/summer_weather.ipynb)
    - Winter Months [Click Here](Data_Handling/Weather_Extract/winter_weather.ipynb)

#### Data Cleaning

**Citi Bike**
- *Full Code Can be found Here: [Concat Notebook](Data_Handling/Concat_CSV_Files.ipynb)*
- The Citi Bike data is broken down by month, and as I was using six documents (three for summer and three for winter), I wanted to condense these down into just two seperate files.
- I created a for loop which looped through the Resources directory to obtain the filename month to determine if it was a Winter or Summer month
- ![CitiBike - For Loop](Assets/CitiBike_ForLoop.png)
- With this determined I created a DataFrame and added it to a list, either winter_dfs or summer_dfs.
- These lists would then be used with the `pandas.concat()` function to concatenate the DataFrames together.
- ![CitiBike - Summer Concat](Assets/CitiBike_ConcatSummer.png)
- To join the CitiBike data with the Weather data obtained from open-meteo.com, I created a helper column for the join. This would be the `started_at` column datetime converted to the format: "YYYY-MM-DD HH:00:00"
- ![CitiBike - Helper Columns](Assets/CitiBike_HelperColumns.png)
- With this completed, the DataFrames were output to new CSV's within the `Outputs` directory
    - `summer_df.csv`
    - `winter_df.csv`
    - *Note: Due to the size of these files, they may not show within this GitHub repo*

**Open-Meteo.com Weather**
- *Full Code can be found here: [Weather Extract Folder](Data_Handling/Weather_Extract/)*
- I first obtained the `min` and `max` dates of the `started_at` column to idenitfy the date period required.
- ![OpenMeteo - Min/Max Dates](Assets/OpenMeteo_DatePeriod.png)
- I then created a frequency DataFrame for each hour I required from the Open-Meteo service. This would be used in the API request
- ![]()
- A request was then made with the results being passed into another DataFrame.
- ![]()
- Additional mapping tasks were conducted on some of the values
- ![]()
- Once completed, the DataFrame was then output as:
    - `summer_weather.csv`
    - `winter_weather.csv`


--------

## References

| Reference Name | Description |
|----------------|-------------|
| | |