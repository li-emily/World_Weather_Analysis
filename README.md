# World_Weather_Analysis

## Overview
### Purpose
> Jack loves the PlanMyTrip app. Beta testers love it too. And, as with any new product, they’ve recommended a few changes to take the app to the next level. Specifically, they recommend adding the weather description to the weather data you’ve already retrieved in this module. Then, you'll have the beta testers use input statements to filter the data for their weather preferences, which will be used to identify potential travel destinations and nearby hotels. From the list of potential travel destinations, the beta tester will choose four cities to create a travel itinerary. Finally, using the Google Maps Directions API, you will create a travel route between the four cities as well as a marker layer map.

### Resources
- Language: Python 3.7.10
- Interface: Jupyter Notebook
- Environment: Miniconda
- Packages: Pandas, Numpy, SciPy, Requests, Citipy
- APIs: OpenWeatherMap, Google Maps and Places, Google Search Nearby
- Further resources: [In Depth Input() Explanation](https://betterprogramming.pub/how-you-make-sure-input-is-the-type-you-want-it-to-be-in-python-521f3565a66d)

## Results
### Deliverable 1: Retrieve Weather Data
Created a random set of longtitudes and latitudes, used citipy to find nearby cities, then used OpenWeatherMap to find current weather descriptions. Combined this data together in a exportable DataFrame for further use (WeatherPy_database.csv).

![Deliverable 1](https://github.com/li-emily/World_Weather_Analysis/blob/main/Weather_Database/Weather_Data_Excerpt.png)

### Deliverable 2: Create a Customer Travel Destinations Map
Used the WeatherPy_database to find a subset of cities that had maximum and minimum temperatures suited to the beta tester's weather preferences. Dropped any empty rows in the DataFrame, created a new DataFrame including hotel information (WeatherPy_vacation.csv). Iterated through using Google Nearby Search API, and added the information to the map figure.

![Deliverable 2](https://github.com/li-emily/World_Weather_Analysis/blob/main/Vacation_Search/WeatherPy_vacation_map.png)

### Deliverable 3: Create a Travel Itinerary Map
Filter WeatherPy_vacation with the beta tester's country and city preferences. Created an itinerary of four cities that looped back to the starting city. The beta tester chose the travel mode between driving, bicycling, and walking. Using Google Maps API, outputted a map with directions between all four cities, and a marker map containing basic information including local weather and hotels. Notable code included the following, which helped check and confirm that inputted data was of the correct kind and could be properly analyzed.

```
# Create list of Japanese cities

japan_df = vacation_df.loc[(vacation_df.Country == country_choice)]
jp_cities = japan_df.City.tolist()

# Choose which cities to go to

# Def function to see if inputted city is in the list
def is_jp(check_input):
    if check_input in jp_cities:
        return True
    return False

# Create vacation stop list
vacation_stops = [] 
maxLengthList = 4

print (f'Choose a total of four cities.')
print(jp_cities)

while len(vacation_stops) < 4:
    user_input = input('Choose a City: ')

    # Make sure input is in the list
    while not is_jp(user_input):
        print (f'Please try again, city is required as input')
        user_input = input('Pick your item from the list above: ')

    # Add the choice to list
    vacation_stops.append(user_input)

print(f'Your chosen vacation stops are as follows: {vacation_stops[0]}, 
         {vacation_stops[1]}, {vacation_stops[2]}, {vacation_stops[3]}')

```
![Deliverable 3 directions](https://github.com/li-emily/World_Weather_Analysis/blob/main/Vacation_Itinerary/WeatherPy_travel_map.png)
![Deliverable 3 map markers](https://github.com/li-emily/World_Weather_Analysis/blob/main/Vacation_Itinerary/WeatherPy_travel_map_markers.png)

