# Floating-population

To investigate the impact of commuting population flows on housing prices in Busan, we collected commuting population data by district in Busan. 
This data was then merged with our existing hedonic dataset based on date and location to create an aggregated hedonic dataset.

(Aggregation process?) 

Data in this repository consists of Excel and CSV files:

- *Busan Commuting Population.xlsx*: Raw data of commuting population by district in Busan.
- *Hedonic data.csv*: Aggregated hedonic dataset of 53,458 observations with 26 variables


## Plotting commuting population and price


In order to easily visualize the distribution of commuting population, housing prices, and their relationship, it is crucial to plot the data for a clear overview. 



The following code performs the above step. (Note: Our code is written based on Google Colab.):
```python
!pip install pydeck
import pydeck
pydeck.__version__
mapbox_key =   # Write your mapbox key of pydeck library
import mapboxgl
print(f"Mapboxgl Version: {mapboxgl.__version__}")
from google.colab import drive
import pandas as pd
drive.mount('/content/drive')
directory = "/content/drive/MyDrive/"
import csv
import json

with open(street_path, 'r') as f:
    reader = csv.reader(f)
    next(reader)

    data = []
    for line in reader:
        d = {
            'latitude': line[0],
            'longitude': line[1],
        }
        data.append(d)

json_string = json.dumps(data, ensure_ascii=False, indent=2)

# print(json_string)

txt_file_path = directory + 'data.txt'

with open(txt_file_path, 'w', encoding='utf-8') as f:
    f.write(json_string)
busan_latlong = directory + 'data.txt'
with open(busan_latlong, "r") as f:
  geo_latlong = json.load(f)
busan_path = directory + 'Hedonic data.csv'
busan = pd.read_csv(busan_path)
import csv
import json

with open(busan_path, 'r') as f:
    reader = csv.reader(f)
    next(reader)

    data = []
    for line in reader:
        d = {
            'latitude': line[5],
            'longitude': line[4],
            'properties': {
                'price': line[1],
                'commute': line[25],
                }
        }
        data.append(d)

json_string = json.dumps(data, ensure_ascii=False, indent=2)

# print(json_string)

txt_file_path = directory + 'busan_data.txt'

with open(txt_file_path, 'w', encoding='utf-8') as f:
    f.write(json_string)data_path = directory + 'busan_data.txt'
with open(data_path, "r") as f:
  geo = json.load(f)
```







Figure 1 illustrates the visualization results, presenting a plot where housing prices are shown as height and commuting population is represented by color—darker blue shades indicate lower values, while brighter colors represent higher values.


<p align="center">
  <img src = "Visualization.png" width = "70%"> <br>
  Figure 1. Visualization of commuting population and apartment prices in Busan.
</p>
