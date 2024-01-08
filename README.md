Deliverable 1: Scrape Titles and Preview Text from Mars News
# Import Splinter and BeautifulSoup. I removed the "for soup" section of the starting code because I kept getting errors with it there.
from splinter import Browser
from bs4 import BeautifulSoup
browser = Browser('chrome')
Step 1: Visit the Website
Use automated browsing to visit the Mars news site. Inspect the page to identify which elements to scrape.

Hint To identify which elements to scrape, you might want to inspect the page by using Chrome DevTools.

# Visit the Mars news site
url = 'https://static.bc-edx.com/data/web/mars_news/index.html'
browser.visit(url)
Step 2: Scrape the Website
Create a Beautiful Soup object and use it to extract text elements from the website.

html = browser.html
soup = BeautifulSoup(html, 'html.parser')
# Create a Beautiful Soup object
html = browser.html
soup = BeautifulSoup(html, 'html.parser')
all_text = soup.get_text()
# Extract all the text elements    Took this from other class content. 'Content_Title' is from the Inspect element of the website.
all_text = soup.get_text()
titles = soup.find_all('span', class_='content_title')
​
for title in titles:
    print(title.text)
# Extract all the text elements
all_text = soup.get_text()
# Find all title elements with class 'content_title'     Repeat from prior
title = soup.find_all('div', class_='content_title')
# Find all preview elements with class 'article_teaser_body'       'article_teaser_body' is from the Inspect element of the website.
preview = soup.find_all('div', class_='article_teaser_body')
Step 3: Store the Results
Extract the titles and preview text of the news articles that you scraped. Store the scraping results in Python data structures as follows:

Store each title-and-preview pair in a Python dictionary. And, give each dictionary two keys: title and preview. An example is the following:

{'title': "NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm", 
 'preview': "For the first time in its eight years orbiting Mars, NASA’s MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27."
}
Store all the dictionaries in a Python list.

Print the list in your notebook.

for titles in title:
    print(titles.text.strip())
NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm
NASA Prepares to Say 'Farewell' to InSight Spacecraft
NASA and ESA Agree on Next Steps to Return Mars Samples to Earth
NASA's InSight Lander Detects Stunning Meteoroid Impact on Mars
NASA To Host Briefing on InSight, Mars Reconnaissance Orbiter Findings
Why NASA Is Trying To Crash Land on Mars
Curiosity Mars Rover Reaches Long-Awaited Salty Region
Mars Mission Shields Up for Tests
NASA's InSight Waits Out Dust Storm
NASA's InSight 'Hears' Its First Meteoroid Impacts on Mars
NASA's Perseverance Rover Investigates Geologically Rich Mars Terrain
NASA to Host Briefing on Perseverance Mars Rover Mission Operations
NASA's Perseverance Makes New Discoveries in Mars' Jezero Crater
10 Years Since Landing, NASA's Curiosity Mars Rover Still Has Drive
SAM's Top 5 Discoveries Aboard NASA's Curiosity Rover at Mars
for previews in preview:
    print(previews.text.strip())
For the first time in its eight years orbiting Mars, NASA’s MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27.
A closer look at what goes into wrapping up the mission as the spacecraft’s power supply continues to dwindle.
The agency’s Perseverance rover will establish the first sample depot on Mars.
The agency’s lander felt the ground shake during the impact while cameras aboard the Mars Reconnaissance Orbiter spotted the yawning new crater from space.
Scientists from two Mars missions will discuss how they combined images and data for a major finding on the Red Planet.
Like a car’s crumple zone, the experimental SHIELD lander is designed to absorb a hard impact.
After years of climbing, the Mars rover has arrived at a special region believed to have formed as Mars’ climate was drying.
Protecting Mars Sample Return spacecraft from micrometeorites requires high-caliber work.
InSight’s team is taking steps to help the solar-powered lander continue operating for as long as possible.
The Mars lander’s seismometer has picked up vibrations from four separate impacts in the past two years.
The latest findings provide greater detail on a region of the Red Planet that has a watery past and is yielding promising samples for the NASA-ESA Mars Sample Return campaign.
Members of the mission will discuss the rover’s activities as it gathers samples in an ancient river delta.
The rover found that Jezero Crater’s floor is made up of volcanic rocks that have interacted with water.
Despite signs of wear, the intrepid spacecraft is about to start an exciting new chapter of its mission as it climbs a Martian mountain.
“Selfie” of the Curiosity rover with inset showing the SAM instrument prior to installation on the rover.
# Create an empty list to store the dictionaries
news_articles = []
# Loop through the text elements
# Extract the title and preview text from the elements
article_elements = soup.find_all('div', class_='list_text')
​
for article_element in article_elements:
    title = article_element.find('div', class_='content_title').text.strip()
    preview = article_element.find('div', class_='article_teaser_body').text.strip()
​
    # Store each title and preview pair in a dictionary
    article_data = {'title': title, 'preview': preview}
​
    # Add the dictionary to the list
    news_articles.append(article_data)
    
    # Print the list to confirm success
    print(article_data)
{'title': "NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm", 'preview': 'For the first time in its eight years orbiting Mars, NASA’s MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27.'}
{'title': "NASA Prepares to Say 'Farewell' to InSight Spacecraft", 'preview': 'A closer look at what goes into wrapping up the mission as the spacecraft’s power supply continues to dwindle.'}
{'title': 'NASA and ESA Agree on Next Steps to Return Mars Samples to Earth', 'preview': 'The agency’s Perseverance rover will establish the first sample depot on Mars.'}
{'title': "NASA's InSight Lander Detects Stunning Meteoroid Impact on Mars", 'preview': 'The agency’s lander felt the ground shake during the impact while cameras aboard the Mars Reconnaissance Orbiter spotted the yawning new crater from space.'}
{'title': 'NASA To Host Briefing on InSight, Mars Reconnaissance Orbiter Findings', 'preview': 'Scientists from two Mars missions will discuss how they combined images and data for a major finding on the Red Planet.'}
{'title': 'Why NASA Is Trying To Crash Land on Mars', 'preview': 'Like a car’s crumple zone, the experimental SHIELD lander is designed to absorb a hard impact.'}
{'title': 'Curiosity Mars Rover Reaches Long-Awaited Salty Region', 'preview': 'After years of climbing, the Mars rover has arrived at a special region believed to have formed as Mars’ climate was drying.'}
{'title': 'Mars Mission Shields Up for Tests', 'preview': 'Protecting Mars Sample Return spacecraft from micrometeorites requires high-caliber work.'}
{'title': "NASA's InSight Waits Out Dust Storm", 'preview': 'InSight’s team is taking steps to help the solar-powered lander continue operating for as long as possible.'}
{'title': "NASA's InSight 'Hears' Its First Meteoroid Impacts on Mars", 'preview': 'The Mars lander’s seismometer has picked up vibrations from four separate impacts in the past two years.'}
{'title': "NASA's Perseverance Rover Investigates Geologically Rich Mars Terrain", 'preview': 'The latest findings provide greater detail on a region of the Red Planet that has a watery past and is yielding promising samples for the NASA-ESA Mars Sample Return campaign.'}
{'title': 'NASA to Host Briefing on Perseverance Mars Rover Mission Operations', 'preview': 'Members of the mission will discuss the rover’s activities as it gathers samples in an ancient river delta.'}
{'title': "NASA's Perseverance Makes New Discoveries in Mars' Jezero Crater", 'preview': 'The rover found that Jezero Crater’s floor is made up of volcanic rocks that have interacted with water.'}
{'title': "10 Years Since Landing, NASA's Curiosity Mars Rover Still Has Drive", 'preview': 'Despite signs of wear, the intrepid spacecraft is about to start an exciting new chapter of its mission as it climbs a Martian mountain.'}
{'title': "SAM's Top 5 Discoveries Aboard NASA's Curiosity Rover at Mars", 'preview': '“Selfie” of the Curiosity rover with inset showing the SAM instrument prior to installation on the rover.'}
# Print the list to confirm success     I printed it twice. This one in its own cell just prints the first one since its outside of the for loop.
print(article_data)
{'title': "SAM's Top 5 Discoveries Aboard NASA's Curiosity Rover at Mars", 'preview': '“Selfie” of the Curiosity rover with inset showing the SAM instrument prior to installation on the rover.'}
browser.quit()



Deliverable 2: Scrape and Analyze Mars Weather Data
# Import relevant libraries
from splinter import Browser
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
import pandas as pd
browser = Browser('chrome')
Step 1: Visit the Website
Use automated browsing to visit the Mars Temperature Data Site. Inspect the page to identify which elements to scrape.

Hint To identify which elements to scrape, you might want to inspect the page by using Chrome DevTools to discover whether the table contains usable classes.

https://static.bc-edx.com/data/web/mars_facts/temperature.htm
# Visit the website
# https://static.bc-edx.com/data/web/mars_facts/temperature.html
url = "https://static.bc-edx.com/data/web/mars_facts/temperature.html"
browser.visit(url)
Step 2: Scrape the Table
Create a Beautiful Soup object and use it to scrape the data in the HTML table.

Note that this can also be achieved by using the Pandas read_html function. However, use Beautiful Soup here to continue sharpening your web scraping skills.

# Create a Beautiful Soup Object
html = browser.html
soup = BeautifulSoup(html, 'html.parser')
# Create a Beautiful Soup Object
html = browser.html
soup = BeautifulSoup(html, 'html.parser')
# Extract all rows of data
table = soup.find('table', class_='table')
Step 3: Store the Data
Assemble the scraped data into a Pandas DataFrame. The columns should have the same headings as the table on the website. Here’s an explanation of the column headings:

id: the identification number of a single transmission from the Curiosity rover
terrestrial_date: the date on Earth
sol: the number of elapsed sols (Martian days) since Curiosity landed on Mars
ls: the solar longitude
month: the Martian month
min_temp: the minimum temperature, in Celsius, of a single Martian day (sol)
pressure: The atmospheric pressure at Curiosity's location
# Create an empty list
table_data = []
​
# Loop through the scraped data to create a list of rows
for row in table.find_all('tr'):
    # Extract all cells within each row
    cells = row.find_all(['td', 'tr'])
​
    # Skip the header row
    if not cells:
        continue
​
    # Create a dictionary for each row using header names
    row_data = {
        'id': cells[0].text.strip(),
        'terrestrial_date': cells[1].text.strip(),
        'sol': cells[2].text.strip(),
        'ls': cells[3].text.strip(),
        'month': cells[4].text.strip(),
        'min_temp': cells[5].text.strip(),
        'pressure': cells[6].text.strip()
    }
​
    table_data.append(row_data)
# Create a Pandas DataFrame
weather_df = pd.DataFrame(table_data)
weather_df
# Confirm DataFrame was created successfully
# Display the DataFrame
weather_df.head()
id	terrestrial_date	sol	ls	month	min_temp	pressure
0	2	2012-08-16	10	155	6	-75.0	739.0
1	13	2012-08-17	11	156	6	-76.0	740.0
2	24	2012-08-18	12	156	6	-76.0	741.0
3	35	2012-08-19	13	157	6	-74.0	732.0
4	46	2012-08-20	14	157	6	-74.0	740.0
Step 4: Prepare Data for Analysis
Examine the data types that are currently associated with each column. If necessary, cast (or convert) the data to the appropriate datetime, int, or float data types.

Hint You can use the Pandas astype and to_datetime methods to accomplish this task.

weather_df.dtypes
# Examine data type of each column
weather_df.dtypes
id                  object
terrestrial_date    object
sol                 object
ls                  object
month               object
min_temp            object
pressure            object
dtype: object
# Change data types for data analysis      astype changes dtype: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html
weather_df['id'] = weather_df['id'].astype(int)
weather_df['terrestrial_date'] = pd.to_datetime(weather_df['terrestrial_date'])
weather_df['sol'] = weather_df['sol'].astype(int)
weather_df['ls'] = weather_df['ls'].astype(float)
weather_df['month'] = weather_df['month'].astype(int)
weather_df['min_temp'] = weather_df['min_temp'].astype(float)
weather_df['pressure'] = weather_df['pressure'].astype(float)
# Confirm type changes were successful by examining data types again
weather_df.dtypes
id                           int32
terrestrial_date    datetime64[ns]
sol                          int32
ls                         float64
month                        int32
min_temp                   float64
pressure                   float64
dtype: object
Step 5: Analyze the Data
Analyze your dataset by using Pandas functions to answer the following questions:

How many months exist on Mars?
How many Martian (and not Earth) days worth of data exist in the scraped dataset?
What are the coldest and the warmest months on Mars (at the location of Curiosity)? To answer this question:
Find the average the minimum daily temperature for all of the months.
Plot the results as a bar chart.
Which months have the lowest and the highest atmospheric pressure on Mars? To answer this question:
Find the average the daily atmospheric pressure of all the months.
Plot the results as a bar chart.
About how many terrestrial (Earth) days exist in a Martian year? To answer this question:
Consider how many days elapse on Earth in the time that Mars circles the Sun once.
Visually estimate the result by plotting the daily minimum temperature.
num_months = weather_df['month'].nunique()
num_months
# 1. How many months are there on Mars?     So originally I just did a nunique for this answer. But in the original answer supplied in the file I saw it was a table, so I switched to making it counts for each month.
month_counts = weather_df['month'].value_counts().sort_index()
​
print(f'The number of days for each month on Mars is:\n{month_counts}')
The number of days for each month on Mars is:
month
1     174
2     178
3     192
4     194
5     149
6     147
7     142
8     141
9     134
10    112
11    138
12    166
Name: count, dtype: int64
# 2. How many Martian days' worth of data are there?
num_sols = weather_df['sol'].nunique()
print(f"There are {num_sols} days on Mars.")
There are 1867 days on Mars.
average_low_temp_by_month = weather_df.groupby('month')['min_temp'].mean()

# Print the result
print(average_low_temp_by_month)
# 3. What is the average low temperature by month?
average_low_temp_by_month = weather_df.groupby('month')['min_temp'].mean()
​
# Print the result
print(average_low_temp_by_month)
month
1    -77.160920
2    -79.932584
3    -83.307292
4    -82.747423
5    -79.308725
6    -75.299320
7    -72.281690
8    -68.382979
9    -69.171642
10   -71.982143
11   -71.985507
12   -74.451807
Name: min_temp, dtype: float64
average_low_temp_by_month.plot(kind='bar', xlabel='Month', ylabel='Temperature in Celsius', title='Average Low Temperature on Mars')
# Plot the average temperature by month
average_low_temp_by_month.plot(kind='bar', xlabel='Month', ylabel='Temperature in Celsius', title='Average Low Temperature on Mars')
<Axes: title={'center': 'Average Low Temperature on Mars'}, xlabel='Month', ylabel='Temperature in Celsius'>

.sort_values()
# Identify the coldest and hottest months in Curiosity's location     Here I sorted it by values of the 'min_temp' so that it would be ordered by coldest to warmest.
average_low_temp_by_month2 = weather_df.groupby('month')['min_temp'].mean().sort_values()
​
# Print the result
print(average_low_temp_by_month2)
month
3    -83.307292
4    -82.747423
2    -79.932584
5    -79.308725
1    -77.160920
6    -75.299320
12   -74.451807
7    -72.281690
11   -71.985507
10   -71.982143
9    -69.171642
8    -68.382979
Name: min_temp, dtype: float64
average_low_temp_by_month2.plot(kind='bar', xlabel='Month', ylabel='Temperature in Celsius', title='Average Low Temperature on Mars in Order of Month')
average_low_temp_by_month2.plot(kind='bar', xlabel='Month', ylabel='Temperature in Celsius', title='Average Low Temperature on Mars in Order of Month')
<Axes: title={'center': 'Average Low Temperature on Mars in Order of Month'}, xlabel='Month', ylabel='Temperature in Celsius'>

weather_df
# 4. Average pressure by Martian month
average_pressure_by_month = weather_df.groupby('month')['pressure'].mean().sort_values()
​
# Print the result       Here I sorted it by values of the 'pressure' so that it would be ordered by coldest to warmest.
print(average_pressure_by_month)
month
6     745.054422
5     748.557047
7     795.105634
4     806.329897
12    842.156627
11    857.014493
1     862.488506
8     873.829787
3     877.322917
10    887.312500
2     889.455056
9     913.305970
Name: pressure, dtype: float64
# Plot the average pressure by month
average_pressure_by_month.plot(kind='bar', xlabel='Month', ylabel='Atmospheric Pressure', title='Average Pressure on Mars')
<Axes: title={'center': 'Average Pressure on Mars'}, xlabel='Month', ylabel='Atmospheric Pressure'>

# 5. How many terrestrial (earth) days are there in a Martian year?
date_min_temp = weather_df[['terrestrial_date', 'min_temp']]
​
# Plot of daily minimum temperature
plt.figure(figsize=(12, 6))
plt.plot(date_min_temp['terrestrial_date'], date_min_temp['min_temp'], label='Daily Min Temperature')
plt.xlabel('Number of Terrestrial Days')
plt.ylabel('Min Temperature')
plt.title('Mars days vs Earth Days')
plt.legend()
plt.show()

max Earth dates in the dataset.
# Trying to get Earth Days per Mars Year in a different way. Here I am getting min and max Earth dates in the dataset.
min_terrestrial_date = weather_df['terrestrial_date'].min()
max_terrestrial_date = weather_df['terrestrial_date'].max()
​
print(f'Minimum Terrestrial Date: {min_terrestrial_date}')
print(f'Maximum Terrestrial Date: {max_terrestrial_date}')
Minimum Terrestrial Date: 2012-08-16 00:00:00
Maximum Terrestrial Date: 2018-02-27 00:00:00
.
# Trying to get Earth Days per Mars Year in a different way. Here I am getting the amonut of Earth years in the dataset.
min_terrestrial_date = weather_df['terrestrial_date'].min()
max_terrestrial_date = weather_df['terrestrial_date'].max()
​
# Calculate the number of days between the two dates
days_between_dates = (max_terrestrial_date - min_terrestrial_date).days
​
earth_years = days_between_dates / 365
​
earth_years
5.536986301369863
. Here I am getting the amount of Mars years in the dataset.
# Trying to get Earth Days per Mars Year in a different way. Here I am getting the amount of Mars years in the dataset.
mars_years = days_between_dates / 687
mars_years
2.9417758369723437
per Mars year.
# Trying to get Earth Days per Mars Year in a different way. Here I am getting the amount of Earth years per Mars year.
mars_earth_year = earth_years / mars_years
mars_earth_year
1.8821917808219177
On average, the third month has the coldest minimum temperature on Mars, and the eighth month is the warmest. But it is always very cold there in human terms!

Atmospheric pressure is, on average, lowest in the sixth month and highest in the ninth.

The distance from peak to peak is roughly 1425-750, or 675 days. A year on Mars appears to be about 675 days from the plot. Internet search confirms that a Mars year is equivalent to 687 earth days.

Step 6: Save the Data
Export the DataFrame to a CSV file.

# Write the data to a CSV
weather_df.to_csv('mars_weather_data.csv', index=False)
browser.quit()
