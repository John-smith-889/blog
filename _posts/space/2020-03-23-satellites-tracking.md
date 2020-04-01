---
layout: post
title: Satellites Tracking in Python
categories: [Space]
tags: ["#python &nbsp; #satellites &nbsp; #n2yo REST API &nbsp; "]
comments: true
---
<p align="left"> <span style="color:darkblue; font-family:Calibri; font-size: 110%;"> <em> #python &nbsp;  #satellites &nbsp; #n2yo REST API  </em></span> </p>

![background-picture]({{site.baseurl}}/assets/Sojuz-TMA.jpg)
<p align="right"> <span style="font-size: 85%; line-height: 4px; display:block"> <i> Sojuz-TMA on orbit, source: NASA </i> </span> </p>


Space industry is the one of the most exciting fields of data science application areas. Data related to space we may get from radio telescopes, sky cameras, 
or devices installed on satellites, such as cameras, and other sensors. One type of data is a location of satellites itself. While the sky 
is clear, it is even possible to spot some of them with a naked eye, especially while phenomenon like 
<a href="https://en.wikipedia.org/wiki/Satellite_flare" target="_blank" title="keyword">satellite flare</a>
occurs – one may see satellite passing through the sky with enhanced flash during a few seconds.   

Satellites and another objects on the Earth orbit are catalogued in Satellite Catalog Number, known also as NORAD Catalog Number. NORAD means
North American Aerospace Defense Command - organisation incorporating United States and Canada. Its purpose is to provide aerospace warning and air sovereignty
for North America.

For satellites tracking we may use N2YO.COM REST API. Detailed instructions are available at 
<a href="https://www.n2yo.com/api/" target="_blank" title="keyword">https://www.n2yo.com/api/</a>.
The current limit is 1000 transactions per hour. According to official documentation we may use the API 
to provide data for software/web applications involving satellite tracking 
or predicting their locations. In 
<a href="https://www.n2yo.com/about/?a=terms" target="_blank" title="keyword">Terms of Use</a>
section, we may discover the main source of data: 

  > The software used for tracking is using mainly space surveillance data provided by "Space Track", 
  > a website consisting of a partial catalog of observations collected by the US Space Surveillance Network, 
  > operated by US Air Force Space Command (AFSPC). AFSPC does not make any warranties as to the accuracy or completeness of the data provided (...)

<a href="https://www.space-track.org/" target="_blank" title="keyword">"Space Track"</a>
website has a limit of 200 requests per hour. So n2yo probably gets the data from space track, implement its own algorithms 
to predict information about satellites, and redistribute it for 5 times higher API requests limit for wider audience.

It is not the only one source of data. As we may see:

  > In special circumstances for a few satellites the traking data ("keplerian elements") 
  > are derived from public sources (monitoring or visual observation)

but there is not specified what sources are they exactly, and for which satellites. 
Let's look at main data source again. On
<a href="https://www.space-track.org/" target="_blank" title="keyword">space-track.org</a>
we may read that:

  > As the United States government agency responsible for Space Situational Awareness (SSA) 
  > information, United States Space Command (USSPACECOM), is committed to promoting a safe, 
  > stable, sustainable, and secure space environment through SSA information sharing. As more 
  > countries, companies, and non-governmental organizations field space capabilities and benefit 
  > from the use of space systems, it is in our collective interest to act responsibly and 
  > to enhance overall spaceflight safety. To achieve effective SSA, USSPACECOM seeks 
  > to increase cooperation and collaboration with partners and space-faring entities 
  > through the exchange of SSA data and provision of SSA services.

This means that USSPACECOM encurages institutions to cooperation and releases data. Information about space
objects are available via API after estabilishing user account, but advanced access requires custom Orbital Data Request, or SSA Sharing Agreement.
What may be interesting for polish readers, according to official website of Polish Space Agency - 
<a href="https://polsa.gov.pl/en/events/events/15-latest/1012-polsa-has-signed-an-agreement-with-usstratcom-for-sharing-space-situational-awareness-ssa-data" target="_blank" title="keyword">polsa.gov.pl</a>, 
POLSA has signed such an agreement on April 10, 2019 with USSTRATCOM for sharing SSA information (USSPACECOM was merged with USSTRATCOM at the time and was not independent entity).

N2YO.COM API offers a few methods to get information about satellites. Below four methods are described, without "Get radio passes" method, 
which may be useful, when someone want to estabilish a direct connection with satellites, for example with 
<a href="https://en.wikipedia.org/wiki/Software-defined_radio" target="_blank" title="keyword">Software Defined Radio</a>. 
Due to presentation clarity some of the output responses below code snippets will be shown. 

<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
width: 60%;
"
> <strong>Contents:</strong> 
<br>
<strong>1.</strong> TLE method, 
<br> 
<strong>2. </strong> Positions method,
<br> 
<strong>3. </strong> Visualpasses method,
<br> 
<strong>4. </strong> Above method.
</p>

<div style="line-height:20%;"> <br> </div>
## 1. TLE method
<div style="line-height:60%;"> <br> </div>

TLE method is responsible for getting TLE - 
<a href="https://en.wikipedia.org/wiki/Two-line_element_set" target="_blank" title="keyword">"Two-line element set"</a>.
TLE is special data format which encodes information about 
certain object on the planet orbit, such as NORAD Catalog Number, satellite number, satellite classification, satellite launch year, 
launch number of the year, and more.  

To communicate with API we will use `get` method from `requests` package. To get apiKey necessary to estabilish connection we need to register an account at n2yo.com, and after login visit the profile page and push 
the button that creates the API key. 


```python
# Import requests library 
import requests

# Define satellite NORAD Catalog Number of choosen satellite
sat_id_01 = '13242'

# Define API KEY (your API key from n2yo.com)
apiKey = 'R4BXQP-LPVRES-2TJMDS-33P2'

# Use get method
r_01 = requests.get(url = "https://www.n2yo.com/rest/v1/satellite/tle/" \
	+ sat_id_01 + "&apiKey=" + apiKey) 

# Check response code, if response == 200, request was performed correctly
r_01
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    <Response [200]>

#### Data extraction

```python
# Extract data in JSON format 
data_01 = r_01.json() 
```

```python
# Print obtained data
import json
print(json.dumps(data_01, indent = 2))
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

```
{
  "info": {
    "satid": 13242,
    "satname": "SL-8 R/B",
    "transactionscount": 2
  },
  "tle": "1 13242U 82051B   20075.75668091 +.00000023 +00000-0 
  +16967-4 0 9992\r\n2 13242 074.0438 313.4556 0025991 267.9974 
  091.8203 14.35970955977236"
}
```

We may see above that response variable is just a dictionary, so we extract data with its keys.


```python
# Extract Satellite name
data_01['info']['satname']

# Extract transactions count in last 60 minutes
data_01['info']['transactionscount']
```

```python
# Extract "2-line" TLE informations
data_01['tle']

```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    '1 13242U 82051B   20075.75668091 +.00000023 +00000-0 +16967-4 0  
	9992\r\n2 13242 074.0438 313.4556 0025991 267.9974 091.8203 
	14.35970955977236'


<div style="line-height:20%;"> <br> </div>
## 2. Positions method
<div style="line-height:60%;"> <br> </div>

This method is used to predict future positions of given satellite. Request returns satellite's latitude, 
longitude as independent coordinates, and azimuth, elevation with respect to the observer location. 


Response array contains number of elements set by "seconds" parameter. If "seconds" parameter is set to '2',
as a result we get an array with first element for current UTC time, and second element for current UTC time + 1 second.
If we set this parameter to '3' we will get an array with data for current UTC time, current UTC time + 1 second, and current UTC time + 2 seconds, etc.

#### At first we need to set parameters of the request

```python
# Satellite id (there in an example for International Space Station)
sat_id_02 = '25544'
```

#### There we set location parameters for Warsaw, Poland

```python
# Observer's latitide in decimal degrees
lat_02 = '52.237049'

# Observer's longitude in decimal degrees
lng_02 = '21.017532'

# Observer's altitude above sea level in meters
alt_02 = '100'

# Number of satellite positions to return 
#(each position for each further second with limit 300 seconds)
sec_02 = '2' # return positions for current time, and current time + 1 second
```


#### Send a request

```python
r_02 = requests.get(url = "https://www.n2yo.com/rest/v1/satellite/positions/" 
                 + sat_id_02+ '/' + lat_02 + '/' + lng_02 + '/' + alt_02 + '/' 
                 + sec_02 + '/' + "&apiKey=" + apiKey) 
```

```python
# Check request message
r_02
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    <Response [200]>


#### Extract data
```python
# Extract data in JSON format 
data_02 = r_02.json() 
```

```python
# Print obtained data
import json
print(json.dumps(data_02, indent = 2))
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

```
{
  "info": {
    "satname": "SPACE STATION",
    "satid": 25544,
    "transactionscount": 0
  },
  "positions": [
    {
      "satlatitude": 19.04015824,
      "satlongitude": 99.09844139,
      "sataltitude": 421.38,
      "azimuth": 87.08,
      "elevation": -31.16,
      "ra": 283.11435926,
      "dec": -22.47502746,
      "timestamp": 1584397228
    },
    {
      "satlatitude": 18.9911662,
      "satlongitude": 99.13901737,
      "sataltitude": 421.38,
      "azimuth": 87.08,
      "elevation": -31.19,
      "ra": 283.1412382,
      "dec": -22.50212702,
      "timestamp": 1584397229
    }
  ]
}
```


```python
# Show data with key "info"
data_02['info']

# Show NORAD Catalog Number used in input
data_02['info']['satid']

# Satellite name
data_02['info']['satname']

# Count of transactions in last 60 minutes for present API key
data_02['info']['transactionscount']
```


#### Show coordinates of satellite in present time
```python
# Satellite footprint latitude in decimal degrees
data_02['positions'][0]['satlatitude']

# Satellite footprint longitude in decimal degrees
data_02['positions'][0]['satlongitude']

# Satellite footprint altitude in kilometers
data_02['positions'][0]['sataltitude']

## Location with respect to the observer

# Satellite azimuth with respect to observer's location in degrees
data_02['positions'][0]['azimuth']

# Satellite elevation with respect to observer's location in degrees
data_02['positions'][0]['elevation']

## Location with respect to the earth 

# Satellite right ascension in degrees
data_02['positions'][0]['ra']

# Satellite declination in degrees
data_02['positions'][0]['dec']
```

```python
# Get Unix timestamp in seconds for this position
data_02['positions'][0]['timestamp']

# Convert Unix timestamp value to observer's UTC time 
from datetime import datetime
print(datetime.fromtimestamp(data_02['positions'][0]['timestamp']).strftime('%Y-%m-%d %H:%M:%S'))

```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1584397228
	2020-03-16 23:20:28

To show coordinates of satellite in present time + 1 second, 
we need to relate to second element of a list with [1] 
instead of [0].



<div style="line-height:20%;"> <br> </div>
## 3. Visualpasses method
<div style="line-height:60%;"> <br> </div>

Visualpasses method is used to get information about consecutive visual passes of choosen satellite
indicated by NORAD Catalog Number, from given place on the earth.
To spot the satellite it should be above the horizon, illuminated, and the sky should be dark enough.
Firstly, to perform the query, we need to set request parameters such as observer's coordinates. 

#### Parameters setting 

```python
# Satellite id (there is International Space Station as an example)
sat_id_03 = '25544'

# Observer's latitide in decimal degrees (for Warsaw)
lat_03 = '52.237049'

# Observer's longitude in decimal degrees
lng_03 = '21.017532'

# Observer's altitude above sea level in meters
alt_03 = '100'

# Number of days of prediction (max 10)
days_03 = '5'

# Minimal time of satellite visibility in seconds to be considered 
# in the request
min_visibility_03 = '5'
```

#### Send a request
```python
r_03 = requests.get(url = "https://www.n2yo.com/rest/v1/satellite/visualpasses/" 
                 + sat_id_03+ '/' + lat_03 + '/' + lng_03 + '/' + alt_03 + '/' 
                 + days_03 + '/' + min_visibility_03 + "&apiKey=" + apiKey) 

# Check request message
r_03
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

	<Response [200]>


	
	
#### Data extraction

```python
# Extract data in JSON format 
data_03 = r_03.json() 

# Print obtained data
print(json.dumps(data_03, indent = 2))
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>
```
{
  "info": {
    "satid": 25544,
    "satname": "SPACE STATION",
    "transactionscount": 1,
    "passescount": 4
  },
  "passes": [
    {
      "startAz": 197.46,
      "startAzCompass": "SSW",
      "startEl": 0.02,
      "startUTC": 1584640715,
      "maxAz": 140.58,
      "maxAzCompass": "SE",
      "maxEl": 13.02,
      "maxUTC": 1584640985,
      "endAz": 82.75,
      "endAzCompass": "E",
      "endEl": 12.83,
      "endUTC": 1584641255,
      "mag": 0.1,
      "duration": 250
    },
    {
      "startAz": 228.93,
      "startAzCompass": "SW",
      "startEl": 0.08,
      "startUTC": 1584729990,
      "maxAz": 152.23,
      "maxAzCompass": "SSE",
      "maxEl": 34.07,
      "maxUTC": 1584730305,
      "endAz": 78.4,
      "endAzCompass": "E",
      "endEl": 27.74,
      "endUTC": 1584730610,
      "mag": -0.9,
      "duration": 255
    },
    {
      "startAz": 219.26,
      "startAzCompass": "SW",
      "startEl": 0.06,
      "startUTC": 1584813545,
      "maxAz": 148.7,
      "maxAzCompass": "SE",
      "maxEl": 25.27,
      "maxUTC": 1584813850,
      "endAz": 78.71,
      "endAzCompass": "E",
      "endEl": 19.46,
      "endUTC": 1584814150,
      "mag": -0.8,
      "duration": 385
    },
    {
      "startAz": 253.27,
      "startAzCompass": "WSW",
      "startEl": 0.13,
      "startUTC": 1584819315,
      "maxAz": 162.78,
      "maxAzCompass": "SSE",
      "maxEl": 69.02,
      "maxUTC": 1584819640,
      "endAz": 82.8,
      "endAzCompass": "E",
      "endEl": 20.33,
      "endUTC": 1584819955,
      "mag": -0.4,
      "duration": 195
    }
  ]
}
```

```python
# Show general information about passes
data_03['info']
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

```
{'satid': 25544,
 'satname': 'SPACE STATION',
 'transactionscount': 1,
 'passescount': 4}
```



#### First pass

```python
# Satellite azimuth for the start of this pass 
# (relative to the observer, in degrees)
data_03['passes'][0]['startAz']

# Satellite elevation for the start of this pass 
# (relative to the observer, in degrees)
data_03['passes'][0]['startEl']

# get Unix timestamp for the start of this pass 
data_03['passes'][0]['startUTC']
```

```python
# convert Unix timestamp value to observer's UTC time 
from datetime import datetime
print(datetime.fromtimestamp(data_03['passes'][0]['startUTC']).strftime('%Y-%m-%d %H:%M:%S'))
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1584640715
	2020-03-19 18:58:35

```python
# Satellite azimuth for the max elevation of this pass 
# (relative to the observer, in degrees)
data_03['passes'][0]['maxAz']

# Satellite max elevation for this pass 
# (relative to the observer, in degrees)
data_03['passes'][0]['maxEl']

# Unix time for the max elevation of this pass. 
# We should convert this UTC value to observer's time zone
data_03['passes'][0]['maxUTC']

# Max visual magnitude of the pass, same scale as star brightness. 
# If magnitude cannot be determined, the value is 100000
data_03['passes'][0]['mag']

# Total visible duration of this pass in seconds
data_03['passes'][0]['duration']
```


To show the second (and further) satellite pass if predicted, we need to relate to second element of the list with [1] instead of [0].

<div style="line-height:20%;"> <br> </div>
## 4. Above method
<div style="line-height:60%;"> <br> </div>

This method is used to get the information about objects in given radius related to the observer.
Radius parameter is expressed in range from 0 to 90 degrees. If radius is larger, more space for search is used.
This is very interesting method for people who want to spot some satellites during the night from certain place on the earth.


#### Parameters setting

```python
# Observer's latitide in decimal degrees (for Warsaw)
observer_lat_05 = '52.237049'

# Observer's longitude in decimal degrees
observer_lng_05 = '21.017532'

# Observer's altitude above sea level in meters
observer_alt_05 = '100'

# Search radius (range from 0 to 90)
search_radius_05 = '3'

# Category id 
category_id_05 = '0'
# Category id == 0 means search in all categories
```


#### Send a request

```python
r_05 = requests.get(url = "https://www.n2yo.com/rest/v1/satellite/above/" 
                 + observer_lat_05 + '/' + observer_lng_05 + '/' 
                 + observer_alt_05 + '/' + search_radius_05 + '/' 
                 + category_id_05 + "&apiKey=" + apiKey) 

# Check request message
r_05
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

	<Response [200]>

#### Data extraction

```python
# Extracting data in JSON format 
data_05 = r_05.json() 

# Print obtained data
import json
print(json.dumps(data_05, indent = 2))
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

```
{
  "info": {
    "category": "ANY",
    "transactionscount": 0,
    "satcount": 2
  },
  "above": [
    {
      "satid": 36549,
      "satname": "COSMOS 2251 DEB",
      "intDesignator": "1993-036BDK",
      "launchDate": "1993-06-16",
      "satlat": 50.4823,
      "satlng": 23.4983,
      "satalt": 5.2306528291122e+19
    },
    {
      "satid": 38203,
      "satname": "COSMOS 2251 DEB",
      "intDesignator": "1993-036BST",
      "launchDate": "1993-06-16",
      "satlat": 51.9402,
      "satlng": 22.982,
      "satalt": 6.0611831651699e+16
    }
  ]
}
```

```python
# Category name (ANY if category id requested was 0)
data_05['info']['category']

# Count of transactions performed with this API key in last 60 minutes
data_05['info']['transactionscount']

# Count of satellites returned
data_05['info']['satcount']

# Satellite NORAD Catalog Number
data_05['above'][0]['satid']

# Satellite name
data_05['above'][0]['satname']

# Satellite launch date (YYYY-MM-DD)
data_05['above'][0]['launchDate']

# Satellite footprint latitude in decimal degrees
data_05['above'][0]['satlat']

# Satellite footprint longitude in decimal degrees
data_05['above'][0]['satlng']

# Satellite altitude in kilometers
data_05['above'][0]['satalt']
```
	
	

To sum up, we described shortly and ilustrated usage of four methods to identify location of satellites used in n2yo REST API: *TLE* method, 
*positions* method, *visualpasses* method, and *above* method. There is also one more method called *radiopasses*, which may be used to get
information about passes of certain satellites with which radio contact is possible from a given place on the earth.


	

<br>
### Annotation
<div class="message">
Instructions are dedicated for Windows 10 <br>
Anaconda release: 2019.03 <br>
Python version: 3.7.3

</div>






