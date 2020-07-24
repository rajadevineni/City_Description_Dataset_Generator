# City_Description_Dataset_Generator
This kernal is created to collect data on many cities around the world to categorize them based on their descriptions. The list of cities are collected from [Simplemaps](https://simplemaps.com) as part of their free plan.


## Inroduction:

In this kernal, there were series of decisions that were made to collect the data on each city. Some cities are filetred out due to various reasons which will be discussed in coming sections. Data was collected on 4016 cities.


## Loading Source:
There are 15,000 cities(CSV file) in the source. The source file is available [here](), make sure you have both python file and source file in the same directory when you run the script.

## Cleaning and filtering data:

  1. There are some cities with same names which are be in different states or countries.
  1. I considered such cities as duplicates as I couldn't automate WIKI_Travel link for them.
  1. Removing cities with same name is done based on their population.
  1. The city with a common name but has greater population than the rest of the cities is kept and remaining are dropped. 
  1. After removing the cities with common name, columns "city_ascii" & "country" are kept in the dataframe dropping the unwanted columns like lattitude, longitude etc., 

## Fetching Article data of city:
City name has special characters so it is cleaned and a WikiTravel URL is generated for every city with the below code
'''
city = row['city_ascii'].replace(' ', '_')
# creating a URL with city name
URL = 'https://wikitravel.org/en/' + city 
'''


There are some cities with a dedicated webpage but has no information on it, there are some cities with very less information that would not be enough to make an analysis.
Such cities are dropped based on the size of article data fetched. The below code takes care of the filtering.
'''
if len_article >700:
    new_row = {'City':row['city_ascii'], 'Country': row['country'], 'Description':article_data}
    city_descriptions = city_descriptions.append(new_row, ignore_index=True)
    counter += 1
    print(counter, row['city_ascii'])
'''

## Saving Dataset:

* The dataframe finally consists of 4016 cities descriptions, all the data is stored in the form of "city_description.csv" and also "city_description.h5" file.
Both the files are uploaded in this repository. 

## End Note:
>This dataset is available under MIT Licence. Feel free to use this data to make clustering of cities based on their description. 