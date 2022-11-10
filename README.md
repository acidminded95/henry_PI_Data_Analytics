![HenryLogo](https://d31uz8lwfmyn8g.cloudfront.net/Assets/logo-henry-white-lg.png)

# Henry PI: Data Analytics
This repository contains my third individual project for Henry Data Science career.

The proyect development is contained mostly in the 'test.ipynb' notebook, where the original data was extracted, transformed and loaded into a MySQL database, from where it was imported into a Power BI dashboard.

Link to dashboard: 

https://app.powerbi.com/links/61fBVpWCEY?ctid=56503a93-5742-4785-b4de-a97190ae92b3&pbi_source=linkShare

## What was expected from the project?

This project consisted in the simulation of a contract between the ICAO (International Civil Aviation Organization) and a consulting agency where the task was to elaborate an investigation and analysis of a database containing data regarding aircraft accidents from 1908 to 2021 and present a report assisted by a dashboard that summarized the key points extracted from the provided data. The ICAO 'asked' from us to cross this information with some extra datasets that could complement the insights obtained from the original dataset.

The whole description (in spanish) can be found in the following link:

https://github.com/soyHenry/PI03-Analytics

## My approach to the problem

I began by doing some throughout data exploration, from which I decided which columns I was going to include in the report and which ones would I discard. From the initial 18 columns I ended up using only 7:
- 'date' (originally named 'fecha')
- 'operator'
- 'ac_type'
- 'total_aboard' (originally named 'all_aboard')
- 'total_fatalities' (originally named 'cantidad de fallecidos')
-  'accident_location' (originally named 'Ruta')
- 'summary'

Plus, I was able to create some extra columns with the help of API's that allowed me to better filter the information in the final dashboard.

- 'manufacturer'
- 'lat'
- 'lon'
- 'country_code_a2'
- 'postcode'

So the original dataset ended up being a 12 columns dataset. But I also added a couple datasets ('passengers_per_year' and 'country_dim') from the World Bank page (https://data.worldbank.org/indicator/IS.AIR.PSGR?end=2020&most_recent_value_desc=true&start=1970&view=chart&year=2020) that also gave me information about yearly flight passengers by country and further data about the countries such as their region or their income classification. 

Finally, I created a couple tables that helped the analysis. One ('countries') that directly related each country name to it's alpha2 code. A second one ('events') that contained registers about relevant events throughout the aviation history and their dates in order to complement the analysis.

## Quality Report

Most of the original 5008 registers of the dataset where used in the final report (5000), but some columns had a considerable amount of missing values (like 'flight_no' or 'HORA declarada'). For the purpose of the analysis, some values where imputed as needed and they are detailed in 'test.ipynb' along with the reasons leading to the selected imputation.
Overall, one could say the data quality was good and enough to extract interesting insights from it.

## Data dictionay:

The following are descriptions for each column of each of the final tables.

### • plane_accidents (the original dataset)
    
    - data: date of the accident
    - operator: the airline operator of the flight
    - ac_type: aircraft model
    - manufacturer: aircraft manufacturer
    - total_aboard: total number of people on the aircraft at the time of the accident.
    - total_fatalities: total number of people diseased in the accident (from the ones who where on board of the aircraft)
    - accident_location: approximate place where the accident took place.
    - lat: latitude of 'accident_location'
    - lon: longitude of 'accident_location'
    - country_code_a2: alpha 2 code of the country where the accident took place
    - postcode: zip code of 'accident_location' (if any)
    - summary: brief recunstruction of the evens leading to the accident

### • passengers_per_year

    - country: country from which flights took place
    - country_code_a2: alpha 2 code of 'country'
    - year: year of measure
    - value: amount of people travelling by aircraft within or from 'country' during 'year'

### • country_dim

    - TableName: name of country
    - Region: region of country (North America, Europe & Central Asia, etc.)
    - IncomeGroup: classification of the country by it's GDP (High income, upper middle income, etc.)
    - country_code_a2: alpha 2 code of the country

### • countries:

    - country_code_a2: alpha 2 code of country
    - name: name of country

### • events:
    - event: Foundation of ALPA (Air Line Pilot Association), invention of Black Boxes, Boeing737 went live, Navstar 1 system went online for free and invention of Humble Checklist.
    - year: the year when 'event' took place