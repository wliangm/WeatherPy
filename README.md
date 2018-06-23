
# WeatherPy - Lucas Liang


```python
#dependencies

import numpy as np
import matplotlib.pyplot as plt
import openweathermapy as owm
import pandas as pd
import json


from datetime import date
from random import randint
from citipy import citipy

#config
from config import api_key
```


```python
#create ramdon latitude through 6 set of latitude
#this is to cover the full range of latitude by every 30 degrees from north pole to south pole

x_latitude_1 = [randint(-90, -60) for p in range(0, 400)]
x_latitude_2 = [randint(-60, -30) for p in range(0, 400)]
x_latitude_3 = [randint(-30, 0) for p in range(0, 400)]
x_latitude_4 = [randint(0, 30) for p in range(0, 400)]
x_latitude_5 = [randint(30, 60) for p in range(0, 400)]
x_latitude_6 = [randint(60, 90) for p in range(0, 400)]

x_latitude = x_latitude_1 + x_latitude_2 + x_latitude_3 + x_latitude_4+ x_latitude_5+ x_latitude_6

#print(str(len(x_latitude)))
#print(x_latitude)
```


```python
#create ramdon longtitude through 6 set of longtitude
#this is to cover the full range of longtitude by every 60 degrees from west to east

x_longtitude_1 = [randint(-180, -120) for p in range(0, 400)]
x_longtitude_2 = [randint(-120, -60) for p in range(0, 400)]
x_longtitude_3 = [randint(-60, 0) for p in range(0, 400)]
x_longtitude_4 = [randint(0, 60) for p in range(0, 400)]
x_longtitude_5 = [randint(60, 120) for p in range(0, 400)]
x_longtitude_6 = [randint(120, 180) for p in range(0, 400)]

x_longtitude = x_longtitude_1 + x_longtitude_2 + x_longtitude_3 + x_longtitude_4 + x_longtitude_5 + x_longtitude_6

#print(str(len(x_longtitude)))
#print(x_longtitude)
```


```python
#get city based on random x_latitude and x_longtitude

#create a empty list to store city coordinate
city_list = []    

#store city coordinate via loop
for x_lat, x_lon in zip(x_latitude,x_longtitude):
    city_list.append(citipy.nearest_city(x_lat, x_lon))

#store city name via loop
city_name_list = []
for city in city_list:
    city_name_list.append(city.city_name)
    
#store unique city name
unique_city_name_list = list(set(city_name_list))

#check for number of unique city
#print(str(len(unique_city_name_list)))

#check for city name
#print(unique_city_name_list)
```


```python
#test weather set

#settings={'units':'imperial', 'appid':api_key}

#test_city_weather = owm.get_current(city = 'codrington', **settings)

#test_city_weather

#print(unique_city_name_list[0])
```


```python
#create variable/list and settings for owm

settings={'units':'imperial', 'appid':api_key}

city_clouds = []
city_lat = []
city_lng = []
city_hum = []
city_wind = []
city_temp_max = []
city_date = []
city_country = []
city_name = []
city_id = []
```


```python
#set counter to zero
counter = 0

print('Beginning Data Retrieval')
print('------------------------')

for city in unique_city_name_list:
        
    try:
        #query weather data via api
        city_weather = owm.get_current(city = city, **settings)
        
        #print header and url per city
        counter += 1
        print('Processing Record ' + str(counter) + ' | ' + city)
        print(owm.BASE_URL + "appid=" + api_key + "&q=" + city)
        
        #append data into each variable/list per city
        city_clouds.append(city_weather('clouds.all'))
        city_lat.append(city_weather('coord.lat'))
        city_lng.append(city_weather('coord.lon'))
        city_hum.append(city_weather('main.humidity'))
        city_wind.append(city_weather('wind.speed'))
        city_temp_max.append(city_weather('main.temp_max'))
        city_date.append(city_weather('dt'))
        city_country.append(city_weather('sys.country'))
        city_name.append(city_weather('name'))
        city_id.append(city_weather('id'))
        
    except:
        pass
    #if counter == 500:
     #   break

print('------------------------')
print('Data Retrieval Complete')
print('------------------------')
```

    Beginning Data Retrieval
    ------------------------
    Processing Record 1 | kutum
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kutum
    Processing Record 2 | katakwi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=katakwi
    Processing Record 3 | liliani
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=liliani
    Processing Record 4 | vilyuysk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vilyuysk
    Processing Record 5 | deputatskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=deputatskiy
    Processing Record 6 | chunian
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chunian
    Processing Record 7 | mumford
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mumford
    Processing Record 8 | beidao
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=beidao
    Processing Record 9 | uruzgan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=uruzgan
    Processing Record 10 | ati
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ati
    Processing Record 11 | nedjo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nedjo
    Processing Record 12 | ayorou
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ayorou
    Processing Record 13 | santa vitoria
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=santa vitoria
    Processing Record 14 | jiexiu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jiexiu
    Processing Record 15 | kamuli
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kamuli
    Processing Record 16 | moroto
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=moroto
    Processing Record 17 | sokode
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sokode
    Processing Record 18 | wana
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wana
    Processing Record 19 | tandalti
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tandalti
    Processing Record 20 | gewane
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gewane
    Processing Record 21 | polovinnoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=polovinnoye
    Processing Record 22 | balakhta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=balakhta
    Processing Record 23 | mitha tiwana
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mitha tiwana
    Processing Record 24 | yagodnoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yagodnoye
    Processing Record 25 | berdigestyakh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=berdigestyakh
    Processing Record 26 | rosario
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rosario
    Processing Record 27 | suhbaatar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=suhbaatar
    Processing Record 28 | ushuaia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ushuaia
    Processing Record 29 | yasnyy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yasnyy
    Processing Record 30 | jos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jos
    Processing Record 31 | zhezkazgan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhezkazgan
    Processing Record 32 | bam
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bam
    Processing Record 33 | venado tuerto
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=venado tuerto
    Processing Record 34 | poltavka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=poltavka
    Processing Record 35 | sohag
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sohag
    Processing Record 36 | orlovskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=orlovskiy
    Processing Record 37 | bayan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bayan
    Processing Record 38 | mogzon
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mogzon
    Processing Record 39 | churapcha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=churapcha
    Processing Record 40 | campina grande do sul
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=campina grande do sul
    Processing Record 41 | shar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shar
    Processing Record 42 | pingliang
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pingliang
    Processing Record 43 | yumen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yumen
    Processing Record 44 | parana
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=parana
    Processing Record 45 | aswan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aswan
    Processing Record 46 | baiyin
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=baiyin
    Processing Record 47 | leningradskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=leningradskiy
    Processing Record 48 | hobyo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hobyo
    Processing Record 49 | wajir
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wajir
    Processing Record 50 | avarua
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=avarua
    Processing Record 51 | baoying
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=baoying
    Processing Record 52 | dabat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dabat
    Processing Record 53 | nikki
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nikki
    Processing Record 54 | bayangol
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bayangol
    Processing Record 55 | sao jose da coroa grande
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sao jose da coroa grande
    Processing Record 56 | ust-kuyga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ust-kuyga
    Processing Record 57 | bella union
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bella union
    Processing Record 58 | qandala
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=qandala
    Processing Record 59 | kassala
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kassala
    Processing Record 60 | puerto madryn
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=puerto madryn
    Processing Record 61 | ishim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ishim
    Processing Record 62 | muromtsevo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=muromtsevo
    Processing Record 63 | lichuan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lichuan
    Processing Record 64 | mingaora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mingaora
    Processing Record 65 | kaura namoda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kaura namoda
    Processing Record 66 | ust-kut
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ust-kut
    Processing Record 67 | videira
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=videira
    Processing Record 68 | georgetown
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=georgetown
    Processing Record 69 | kaka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kaka
    Processing Record 70 | san francisco
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=san francisco
    Processing Record 71 | toktogul
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=toktogul
    Processing Record 72 | juba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=juba
    Processing Record 73 | carnot
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=carnot
    Processing Record 74 | bahia blanca
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bahia blanca
    Processing Record 75 | kamoke
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kamoke
    Processing Record 76 | duldurga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=duldurga
    Processing Record 77 | petukhovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=petukhovo
    Processing Record 78 | mulchen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mulchen
    Processing Record 79 | castro
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=castro
    Processing Record 80 | okoneshnikovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=okoneshnikovo
    Processing Record 81 | marzuq
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=marzuq
    Processing Record 82 | pevek
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pevek
    Processing Record 83 | kidal
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kidal
    Processing Record 84 | buta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=buta
    Processing Record 85 | sergeyevka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sergeyevka
    Processing Record 86 | watsa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=watsa
    Processing Record 87 | diamantino
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=diamantino
    Processing Record 88 | linhares
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=linhares
    Processing Record 89 | dir
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dir
    Processing Record 90 | dukat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dukat
    Processing Record 91 | vikhorevka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vikhorevka
    Processing Record 92 | comodoro rivadavia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=comodoro rivadavia
    Processing Record 93 | porciuncula
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=porciuncula
    Processing Record 94 | alvinopolis
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=alvinopolis
    Processing Record 95 | belaya gora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=belaya gora
    Processing Record 96 | dauriya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dauriya
    Processing Record 97 | constitucion
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=constitucion
    Processing Record 98 | martyush
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=martyush
    Processing Record 99 | paracuru
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=paracuru
    Processing Record 100 | asyut
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=asyut
    Processing Record 101 | adrar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=adrar
    Processing Record 102 | jalu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jalu
    Processing Record 103 | kysyl-syr
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kysyl-syr
    Processing Record 104 | borogontsy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=borogontsy
    Processing Record 105 | chokurdakh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chokurdakh
    Processing Record 106 | yinchuan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yinchuan
    Processing Record 107 | plast
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=plast
    Processing Record 108 | nizhnevartovsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nizhnevartovsk
    Processing Record 109 | dori
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dori
    Processing Record 110 | arraial do cabo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=arraial do cabo
    Processing Record 111 | hun
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hun
    Processing Record 112 | tengzhou
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tengzhou
    Processing Record 113 | talcahuano
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=talcahuano
    Processing Record 114 | sur
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sur
    Processing Record 115 | butajira
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=butajira
    Processing Record 116 | okhotsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=okhotsk
    Processing Record 117 | kontagora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kontagora
    Processing Record 118 | guarapari
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=guarapari
    Processing Record 119 | pozo colorado
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pozo colorado
    Processing Record 120 | tevriz
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tevriz
    Processing Record 121 | birnin kebbi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=birnin kebbi
    Processing Record 122 | moreira sales
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=moreira sales
    Processing Record 123 | markova
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=markova
    Processing Record 124 | zaton
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zaton
    Processing Record 125 | arlit
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=arlit
    Processing Record 126 | belyy yar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=belyy yar
    Processing Record 127 | ust-koksa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ust-koksa
    Processing Record 128 | itapeva
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itapeva
    Processing Record 129 | chivilcoy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chivilcoy
    Processing Record 130 | kalga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kalga
    Processing Record 131 | nisia floresta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nisia floresta
    Processing Record 132 | wanlaweyn
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wanlaweyn
    Processing Record 133 | zhanakorgan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhanakorgan
    Processing Record 134 | tabuk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tabuk
    Processing Record 135 | sabha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sabha
    Processing Record 136 | chik
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chik
    Processing Record 137 | taksimo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=taksimo
    Processing Record 138 | hargeysa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hargeysa
    Processing Record 139 | lyantonde
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lyantonde
    Processing Record 140 | hailar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hailar
    Processing Record 141 | ibra
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ibra
    Processing Record 142 | goure
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=goure
    Processing Record 143 | jacareacanga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jacareacanga
    Processing Record 144 | kalanwali
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kalanwali
    Processing Record 145 | aracati
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aracati
    Processing Record 146 | cotonou
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cotonou
    Processing Record 147 | tessalit
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tessalit
    Processing Record 148 | tigil
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tigil
    Processing Record 149 | itarema
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itarema
    Processing Record 150 | san rafael
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=san rafael
    Processing Record 151 | seydi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=seydi
    Processing Record 152 | matinha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=matinha
    Processing Record 153 | manaus
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=manaus
    Processing Record 154 | garowe
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=garowe
    Processing Record 155 | atbasar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=atbasar
    Processing Record 156 | bagdarin
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bagdarin
    Processing Record 157 | volchansk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=volchansk
    Processing Record 158 | erenhot
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=erenhot
    Processing Record 159 | aksu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aksu
    Processing Record 160 | fasa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=fasa
    Processing Record 161 | tezu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tezu
    Processing Record 162 | salym
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=salym
    Processing Record 163 | bilibino
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bilibino
    Processing Record 164 | garoua
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=garoua
    Processing Record 165 | nioaque
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nioaque
    Processing Record 166 | tinskoy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tinskoy
    Processing Record 167 | axim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=axim
    Processing Record 168 | warri
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=warri
    Processing Record 169 | carutapera
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=carutapera
    Processing Record 170 | heze
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=heze
    Processing Record 171 | chara
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chara
    Processing Record 172 | beringovskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=beringovskiy
    Processing Record 173 | bolshoy lug
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bolshoy lug
    Processing Record 174 | calbuco
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=calbuco
    Processing Record 175 | kolosovka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kolosovka
    Processing Record 176 | linxia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=linxia
    Processing Record 177 | beba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=beba
    Processing Record 178 | selenduma
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=selenduma
    Processing Record 179 | xiaolingwei
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=xiaolingwei
    Processing Record 180 | yeniseysk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yeniseysk
    Processing Record 181 | bulgan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bulgan
    Processing Record 182 | tupik
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tupik
    Processing Record 183 | novobirilyussy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=novobirilyussy
    Processing Record 184 | dzhebariki-khaya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dzhebariki-khaya
    Processing Record 185 | bayir
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bayir
    Processing Record 186 | buraydah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=buraydah
    Processing Record 187 | ulaangom
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ulaangom
    Processing Record 188 | stepnogorsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=stepnogorsk
    Processing Record 189 | lukaya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lukaya
    Processing Record 190 | lebu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lebu
    Processing Record 191 | malumfashi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=malumfashi
    Processing Record 192 | sherlovaya gora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sherlovaya gora
    Processing Record 193 | bumba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bumba
    Processing Record 194 | mecca
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mecca
    Processing Record 195 | alta floresta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=alta floresta
    Processing Record 196 | ossora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ossora
    Processing Record 197 | oeiras
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=oeiras
    Processing Record 198 | yendi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yendi
    Processing Record 199 | megion
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=megion
    Processing Record 200 | aguai
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aguai
    Processing Record 201 | trairi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=trairi
    Processing Record 202 | jega
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jega
    Processing Record 203 | kyzyl-suu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kyzyl-suu
    Processing Record 204 | maragogi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=maragogi
    Processing Record 205 | trelew
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=trelew
    Processing Record 206 | abha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abha
    Processing Record 207 | komsomolskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=komsomolskiy
    Processing Record 208 | pospelikha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pospelikha
    Processing Record 209 | sitrah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sitrah
    Processing Record 210 | vanavara
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vanavara
    Processing Record 211 | jacobina
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jacobina
    Processing Record 212 | verkhoturye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=verkhoturye
    Processing Record 213 | xinyang
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=xinyang
    Processing Record 214 | epe
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=epe
    Processing Record 215 | cherskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cherskiy
    Processing Record 216 | gbadolite
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gbadolite
    Processing Record 217 | jiuquan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jiuquan
    Processing Record 218 | ouallam
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ouallam
    Processing Record 219 | ginda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ginda
    Processing Record 220 | kropotkin
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kropotkin
    Processing Record 221 | zyryanka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zyryanka
    Processing Record 222 | buchanan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=buchanan
    Processing Record 223 | kedrovyy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kedrovyy
    Processing Record 224 | puerto montt
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=puerto montt
    Processing Record 225 | graneros
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=graneros
    Processing Record 226 | adre
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=adre
    Processing Record 227 | zyryanskoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zyryanskoye
    Processing Record 228 | ust-nera
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ust-nera
    Processing Record 229 | camapua
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=camapua
    Processing Record 230 | sao joao da barra
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sao joao da barra
    Processing Record 231 | port-gentil
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=port-gentil
    Processing Record 232 | sayat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sayat
    Processing Record 233 | navoi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=navoi
    Processing Record 234 | yantal
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yantal
    Processing Record 235 | taguatinga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=taguatinga
    Processing Record 236 | mercedes
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mercedes
    Processing Record 237 | yerbogachen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yerbogachen
    Processing Record 238 | abu zabad
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abu zabad
    Processing Record 239 | ancud
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ancud
    Processing Record 240 | talaya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=talaya
    Processing Record 241 | ibirite
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ibirite
    Processing Record 242 | hovd
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hovd
    Processing Record 243 | goiatuba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=goiatuba
    Processing Record 244 | tommot
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tommot
    Processing Record 245 | rafai
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rafai
    Processing Record 246 | najran
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=najran
    Processing Record 247 | tyubuk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tyubuk
    Processing Record 248 | mirandopolis
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mirandopolis
    Processing Record 249 | mayor pablo lagerenza
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mayor pablo lagerenza
    Processing Record 250 | itapora
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itapora
    Processing Record 251 | san juan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=san juan
    Processing Record 252 | sangmelima
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sangmelima
    Processing Record 253 | cururupu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cururupu
    Processing Record 254 | tokmak
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tokmak
    Processing Record 255 | mogadishu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mogadishu
    Processing Record 256 | bom jardim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bom jardim
    Processing Record 257 | zhicheng
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhicheng
    Processing Record 258 | zhigalovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhigalovo
    Processing Record 259 | touros
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=touros
    Processing Record 260 | mangaratiba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mangaratiba
    Processing Record 261 | xuanwu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=xuanwu
    Processing Record 262 | jumla
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jumla
    Processing Record 263 | jinan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jinan
    Processing Record 264 | staropyshminsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=staropyshminsk
    Processing Record 265 | coihaique
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=coihaique
    Processing Record 266 | khor
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=khor
    Processing Record 267 | moron
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=moron
    Processing Record 268 | arinos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=arinos
    Processing Record 269 | serra
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=serra
    Processing Record 270 | kirensk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kirensk
    Processing Record 271 | awjilah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=awjilah
    Processing Record 272 | bosobolo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bosobolo
    Processing Record 273 | lagos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lagos
    Processing Record 274 | salvador
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=salvador
    Processing Record 275 | horqueta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=horqueta
    Processing Record 276 | mao
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mao
    Processing Record 277 | coxim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=coxim
    Processing Record 278 | aden
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aden
    Processing Record 279 | ribas do rio pardo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ribas do rio pardo
    Processing Record 280 | gao
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gao
    Processing Record 281 | cavalcante
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cavalcante
    Processing Record 282 | peruibe
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=peruibe
    Processing Record 283 | dongkan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dongkan
    Processing Record 284 | bitam
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bitam
    Processing Record 285 | vagay
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vagay
    Processing Record 286 | aracaju
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aracaju
    Processing Record 287 | vila velha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vila velha
    Processing Record 288 | guanambi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=guanambi
    Processing Record 289 | minab
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=minab
    Processing Record 290 | chengde
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chengde
    Processing Record 291 | khuzhir
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=khuzhir
    Processing Record 292 | maine-soroa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=maine-soroa
    Processing Record 293 | simoes
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=simoes
    Processing Record 294 | leh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=leh
    Processing Record 295 | kachiry
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kachiry
    Processing Record 296 | mega
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mega
    Processing Record 297 | itarantim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itarantim
    Processing Record 298 | puerto quijarro
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=puerto quijarro
    Processing Record 299 | umm lajj
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=umm lajj
    Processing Record 300 | xining
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=xining
    Processing Record 301 | camacari
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=camacari
    Processing Record 302 | kazerun
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kazerun
    Processing Record 303 | ola
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ola
    Processing Record 304 | armizonskoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=armizonskoye
    Processing Record 305 | itupiranga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itupiranga
    Processing Record 306 | cordoba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cordoba
    Processing Record 307 | jijiga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jijiga
    Processing Record 308 | victoria
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=victoria
    Processing Record 309 | vitim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vitim
    Processing Record 310 | huangmei
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=huangmei
    Processing Record 311 | korem
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=korem
    Processing Record 312 | tilichiki
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tilichiki
    Processing Record 313 | lasa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lasa
    Processing Record 314 | darhan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=darhan
    Processing Record 315 | marsa matruh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=marsa matruh
    Processing Record 316 | gambela
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gambela
    Processing Record 317 | bogandinskiy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bogandinskiy
    Processing Record 318 | ler
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ler
    Processing Record 319 | coruripe
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=coruripe
    Processing Record 320 | vaini
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vaini
    Processing Record 321 | esna
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=esna
    Processing Record 322 | jaicos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jaicos
    Processing Record 323 | massakory
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=massakory
    Processing Record 324 | batagay-alyta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=batagay-alyta
    Processing Record 325 | kungurtug
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kungurtug
    Processing Record 326 | biltine
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=biltine
    Processing Record 327 | novo aripuana
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=novo aripuana
    Processing Record 328 | caxambu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=caxambu
    Processing Record 329 | bilma
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bilma
    Processing Record 330 | lensk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lensk
    Processing Record 331 | turinsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=turinsk
    Processing Record 332 | tabory
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tabory
    Processing Record 333 | orlik
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=orlik
    Processing Record 334 | kaz
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kaz
    Processing Record 335 | ulety
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ulety
    Processing Record 336 | pitimbu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pitimbu
    Processing Record 337 | wuwei
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wuwei
    Processing Record 338 | moissala
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=moissala
    Processing Record 339 | at-bashi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=at-bashi
    Processing Record 340 | khandyga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=khandyga
    Processing Record 341 | sangar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sangar
    Processing Record 342 | altay
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=altay
    Processing Record 343 | puyang
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=puyang
    Processing Record 344 | bayanday
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bayanday
    Processing Record 345 | edd
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=edd
    Processing Record 346 | seymchan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=seymchan
    Processing Record 347 | palana
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=palana
    Processing Record 348 | kosh-agach
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kosh-agach
    Processing Record 349 | yining
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yining
    Processing Record 350 | general pico
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=general pico
    Processing Record 351 | makurdi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=makurdi
    Processing Record 352 | sao felix do xingu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sao felix do xingu
    Processing Record 353 | zhangye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhangye
    Processing Record 354 | luba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=luba
    Processing Record 355 | villa maria
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=villa maria
    Processing Record 356 | jaciara
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jaciara
    Processing Record 357 | kolpashevo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kolpashevo
    Processing Record 358 | hazorasp
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hazorasp
    Processing Record 359 | riyadh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=riyadh
    Processing Record 360 | guozhen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=guozhen
    Processing Record 361 | jardim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jardim
    Processing Record 362 | sarakhs
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sarakhs
    Processing Record 363 | nizhniy ufaley
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nizhniy ufaley
    Processing Record 364 | neuquen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=neuquen
    Processing Record 365 | olinda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=olinda
    Processing Record 366 | conde
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=conde
    Processing Record 367 | guaruja
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=guaruja
    Processing Record 368 | mitzic
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mitzic
    Processing Record 369 | ouricuri
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ouricuri
    Processing Record 370 | klyuchi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=klyuchi
    Processing Record 371 | rikitea
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rikitea
    Processing Record 372 | mandalgovi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mandalgovi
    Processing Record 373 | crixas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=crixas
    Processing Record 374 | abu samrah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abu samrah
    Processing Record 375 | tamandare
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tamandare
    Processing Record 376 | umm kaddadah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=umm kaddadah
    Processing Record 377 | mujiayingzi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mujiayingzi
    Processing Record 378 | kurchum
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kurchum
    Processing Record 379 | jinchang
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jinchang
    Processing Record 380 | imbituba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=imbituba
    Processing Record 381 | zaria
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zaria
    Processing Record 382 | priiskovyy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=priiskovyy
    Processing Record 383 | eyl
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=eyl
    Processing Record 384 | shihezi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shihezi
    Processing Record 385 | abai
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abai
    Processing Record 386 | maceio
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=maceio
    Processing Record 387 | abu dhabi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abu dhabi
    Processing Record 388 | gazojak
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gazojak
    Processing Record 389 | krasnoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=krasnoye
    Processing Record 390 | chulym
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chulym
    Processing Record 391 | evensk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=evensk
    Processing Record 392 | yuanping
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yuanping
    Processing Record 393 | lugovoy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lugovoy
    Processing Record 394 | livramento
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=livramento
    Processing Record 395 | zakamensk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zakamensk
    Processing Record 396 | bocaiuva
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bocaiuva
    Processing Record 397 | prado
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=prado
    Processing Record 398 | ginir
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ginir
    Processing Record 399 | tanhacu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tanhacu
    Processing Record 400 | portel
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=portel
    Processing Record 401 | joao pinheiro
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=joao pinheiro
    Processing Record 402 | general roca
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=general roca
    Processing Record 403 | santa ines
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=santa ines
    Processing Record 404 | miguelopolis
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=miguelopolis
    Processing Record 405 | rio gallegos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rio gallegos
    Processing Record 406 | chabahar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chabahar
    Processing Record 407 | lisakovsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lisakovsk
    Processing Record 408 | hohhot
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hohhot
    Processing Record 409 | alta gracia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=alta gracia
    Processing Record 410 | wanxian
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wanxian
    Processing Record 411 | say
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=say
    Processing Record 412 | podgornoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=podgornoye
    Processing Record 413 | awbari
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=awbari
    Processing Record 414 | lenger
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=lenger
    Processing Record 415 | rebrikha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rebrikha
    Processing Record 416 | ayagoz
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ayagoz
    Processing Record 417 | zalesovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zalesovo
    Processing Record 418 | verkhoyansk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=verkhoyansk
    Processing Record 419 | kachug
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kachug
    Processing Record 420 | monte alegre
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=monte alegre
    Processing Record 421 | barao de melgaco
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=barao de melgaco
    Processing Record 422 | birao
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=birao
    Processing Record 423 | kathmandu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kathmandu
    Processing Record 424 | changji
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=changji
    Processing Record 425 | caravelas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=caravelas
    Processing Record 426 | gat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gat
    Processing Record 427 | mokhsogollokh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mokhsogollokh
    Processing Record 428 | santo antonio do sudoeste
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=santo antonio do sudoeste
    Processing Record 429 | sao miguel do araguaia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sao miguel do araguaia
    Processing Record 430 | srednekolymsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=srednekolymsk
    Processing Record 431 | estrela
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=estrela
    Processing Record 432 | pocone
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pocone
    Processing Record 433 | gazli
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gazli
    Processing Record 434 | concordia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=concordia
    Processing Record 435 | amga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=amga
    Processing Record 436 | sar-e pul
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sar-e pul
    Processing Record 437 | gari
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gari
    Processing Record 438 | viedma
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=viedma
    Processing Record 439 | ilhabela
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ilhabela
    Processing Record 440 | adet
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=adet
    Processing Record 441 | san joaquin
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=san joaquin
    Processing Record 442 | zhigansk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zhigansk
    Processing Record 443 | ziarat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ziarat
    Processing Record 444 | tres arroyos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tres arroyos
    Processing Record 445 | yaan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yaan
    Processing Record 446 | cachoeira do sul
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cachoeira do sul
    Processing Record 447 | muscat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=muscat
    Processing Record 448 | kaabong
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kaabong
    Processing Record 449 | shitanjing
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shitanjing
    Processing Record 450 | anloga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=anloga
    Processing Record 451 | aguas belas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aguas belas
    Processing Record 452 | mizan teferi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mizan teferi
    Processing Record 453 | diapaga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=diapaga
    Processing Record 454 | kholodnyy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kholodnyy
    Processing Record 455 | boguchany
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=boguchany
    Processing Record 456 | oskemen
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=oskemen
    Processing Record 457 | rawson
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rawson
    Processing Record 458 | barreirinha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=barreirinha
    Processing Record 459 | natal
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=natal
    Processing Record 460 | boda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=boda
    Processing Record 461 | belmonte
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=belmonte
    Processing Record 462 | jamestown
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jamestown
    Processing Record 463 | nizwa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nizwa
    Processing Record 464 | faya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=faya
    Processing Record 465 | laguna
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=laguna
    Processing Record 466 | boa viagem
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=boa viagem
    Processing Record 467 | camocim
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=camocim
    Processing Record 468 | taywarah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=taywarah
    Processing Record 469 | hami
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=hami
    Processing Record 470 | waddan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=waddan
    Processing Record 471 | macheng
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=macheng
    Processing Record 472 | malanville
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=malanville
    Processing Record 473 | araguaina
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=araguaina
    Processing Record 474 | goya
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=goya
    Processing Record 475 | saskylakh
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=saskylakh
    Processing Record 476 | valdivia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=valdivia
    Processing Record 477 | porangatu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=porangatu
    Processing Record 478 | teguldet
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=teguldet
    Processing Record 479 | khani
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=khani
    Processing Record 480 | panjab
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=panjab
    Processing Record 481 | shu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shu
    Processing Record 482 | sao raimundo das mangabeiras
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sao raimundo das mangabeiras
    Processing Record 483 | umarizal
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=umarizal
    Processing Record 484 | caceres
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=caceres
    Processing Record 485 | shache
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shache
    Processing Record 486 | mangan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mangan
    Processing Record 487 | rongai
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rongai
    Processing Record 488 | bell ville
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bell ville
    Processing Record 489 | jiaozuo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jiaozuo
    Processing Record 490 | emba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=emba
    Processing Record 491 | vilhena
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vilhena
    Processing Record 492 | nalut
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=nalut
    Processing Record 493 | ereymentau
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ereymentau
    Processing Record 494 | chifeng
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chifeng
    Processing Record 495 | coquimbo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=coquimbo
    Processing Record 496 | jizan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=jizan
    Processing Record 497 | tabou
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tabou
    Processing Record 498 | ouadda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ouadda
    Processing Record 499 | obo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=obo
    Processing Record 500 | carambei
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=carambei
    Processing Record 501 | chapada dos guimaraes
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chapada dos guimaraes
    Processing Record 502 | along
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=along
    Processing Record 503 | barra do bugres
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=barra do bugres
    Processing Record 504 | quetta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=quetta
    Processing Record 505 | krasnoarmeysk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=krasnoarmeysk
    Processing Record 506 | san carlos
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=san carlos
    Processing Record 507 | tiksi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tiksi
    Processing Record 508 | pindi gheb
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pindi gheb
    Processing Record 509 | cabedelo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=cabedelo
    Processing Record 510 | batagay
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=batagay
    Processing Record 511 | kodinsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kodinsk
    Processing Record 512 | rio do sul
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rio do sul
    Processing Record 513 | atagay
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=atagay
    Processing Record 514 | vengerovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=vengerovo
    Processing Record 515 | salalah
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=salalah
    Processing Record 516 | shieli
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shieli
    Processing Record 517 | iranshahr
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=iranshahr
    Processing Record 518 | terra santa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=terra santa
    Processing Record 519 | surt
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=surt
    Processing Record 520 | pontes e lacerda
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pontes e lacerda
    Processing Record 521 | bouca
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bouca
    Processing Record 522 | bakchar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bakchar
    Processing Record 523 | aguas formosas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aguas formosas
    Processing Record 524 | punta arenas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=punta arenas
    Processing Record 525 | asosa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=asosa
    Processing Record 526 | samarkand
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=samarkand
    Processing Record 527 | valparaiso
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=valparaiso
    Processing Record 528 | zemio
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zemio
    Processing Record 529 | santa rosa
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=santa rosa
    Processing Record 530 | wagar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=wagar
    Processing Record 531 | abonnema
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abonnema
    Processing Record 532 | entre rios
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=entre rios
    Processing Record 533 | ganganagar
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ganganagar
    Processing Record 534 | barra do garcas
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=barra do garcas
    Processing Record 535 | rafaela
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=rafaela
    Processing Record 536 | pasighat
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=pasighat
    Processing Record 537 | kyzyl-mazhalyk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kyzyl-mazhalyk
    Processing Record 538 | chishtian mandi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=chishtian mandi
    Processing Record 539 | tapiramuta
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tapiramuta
    Processing Record 540 | sayyan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sayyan
    Processing Record 541 | ouesso
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=ouesso
    Processing Record 542 | numan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=numan
    Processing Record 543 | yuncheng
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=yuncheng
    Processing Record 544 | morros
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=morros
    Processing Record 545 | batalha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=batalha
    Processing Record 546 | takoradi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=takoradi
    Processing Record 547 | aksha
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=aksha
    Processing Record 548 | tyup
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=tyup
    Processing Record 549 | carahue
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=carahue
    Processing Record 550 | koshurnikovo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=koshurnikovo
    Processing Record 551 | toritama
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=toritama
    Processing Record 552 | makushino
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=makushino
    Processing Record 553 | businga
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=businga
    Processing Record 554 | kichera
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=kichera
    Processing Record 555 | semey
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=semey
    Processing Record 556 | owando
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=owando
    Processing Record 557 | baoro
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=baoro
    Processing Record 558 | arua
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=arua
    Processing Record 559 | alekseyevsk
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=alekseyevsk
    Processing Record 560 | camaragibe
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=camaragibe
    Processing Record 561 | weinan
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=weinan
    Processing Record 562 | anadyr
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=anadyr
    Processing Record 563 | mataura
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mataura
    Processing Record 564 | conceicao do araguaia
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=conceicao do araguaia
    Processing Record 565 | bondo
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bondo
    Processing Record 566 | isiro
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=isiro
    Processing Record 567 | xuddur
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=xuddur
    Processing Record 568 | mikhaylovka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=mikhaylovka
    Processing Record 569 | makokou
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=makokou
    Processing Record 570 | bandarbeyla
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=bandarbeyla
    Processing Record 571 | petropavlovka
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=petropavlovka
    Processing Record 572 | sertanopolis
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=sertanopolis
    Processing Record 573 | piacabucu
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=piacabucu
    Processing Record 574 | abong mbang
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=abong mbang
    Processing Record 575 | namtsy
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=namtsy
    Processing Record 576 | marawi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=marawi
    Processing Record 577 | shushenskoye
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=shushenskoye
    Processing Record 578 | baruun-urt
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=baruun-urt
    Processing Record 579 | amambai
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=amambai
    Processing Record 580 | dosso
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=dosso
    Processing Record 581 | itaituba
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=itaituba
    Processing Record 582 | esperantinopolis
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=esperantinopolis
    Processing Record 583 | erzin
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=erzin
    Processing Record 584 | zabol
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=zabol
    Processing Record 585 | gurupi
    http://api.openweathermap.org/data/2.5/appid=ada32f6f2c68d7b9107ab5982777180d&q=gurupi
    ------------------------
    Data Retrieval Complete
    ------------------------
    


```python
#test and check for number of city from sucessed api call
#print(city_clouds)
#print(city_coord)
#print(city_hum)
#print(city_wind)
#print(city_temp_max)
#print(str(len(city_clouds)))
```


```python
#create dataframe for city weather data
weather_city_df = pd.DataFrame({'City ID': city_id,'City': city_name, 'Cloudiness': city_clouds,'Country':city_country,'Date':city_date,
                               'Humidity':city_hum,'Latitude':city_lat,'Longtitude': city_lng,'Max Temp':city_temp_max,
                               'Wind Speed':city_wind})

#reset index
#weather_city_df = weather_city_df.reset_index()

#weather_city_df.head()

#save df into csv file
weather_city_df.to_csv("C:/Users/LENOVO USER/Desktop/USC Data Bootcamp/5-HW, Python API/weather_city_api_file.csv",encoding='utf-8',index=False)
```


```python
#create x and y axis for scatter plot 1

x_lat = weather_city_df['Latitude']
y_max_temp = weather_city_df['Max Temp']

#scatter plot for Temperature (F) vs. Latitude

plt.figure(1)

plt.scatter(x_lat, y_max_temp, marker="o", facecolors="blue", edgecolors="black",
                         s=40, alpha=0.75)

plt.title("City Latitude vs. Max Temperature " + "(" + str(date.today()) + ")")
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")

plt.grid()
plt.savefig("C:/Users/LENOVO USER/Desktop/USC Data Bootcamp/5-HW, Python API/temp_vs_lat.png")
```


![png](output_10_0.png)



```python
#create x and y axis for scatter plot 2

x_lat = weather_city_df['Latitude']
y_huminity = weather_city_df['Humidity']

#scatter plot for Latitude vs. Humidity Plot

plt.figure(2)

plt.scatter(x_lat, y_huminity, marker="o", facecolors="blue", edgecolors="black",
                         s=40, alpha=0.75)

plt.title("City Latitude vs. Humidity " + "(" + str(date.today()) + ")")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")

plt.grid()
plt.savefig("C:/Users/LENOVO USER/Desktop/USC Data Bootcamp/5-HW, Python API/humidity_vs_lat.png")
```


![png](output_11_0.png)



```python
#create x and y axis for scatter plot 3

x_lat = weather_city_df['Latitude']
y_clouds = weather_city_df['Cloudiness']

#scatter plot for Latitude vs. Cloudiness Plot 

plt.figure(3)

plt.scatter(x_lat, y_clouds, marker="o", facecolors="blue", edgecolors="black",
                         s=40, alpha=0.75)

plt.title("City Latitude vs. Cloudiness " + "(" + str(date.today()) + ")")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")

plt.grid()
plt.savefig("C:/Users/LENOVO USER/Desktop/USC Data Bootcamp/5-HW, Python API/clouds_vs_lat.png")
```


![png](output_12_0.png)



```python
#create x and y axis for scatter plot 4

x_lat = weather_city_df['Latitude']
y_wind = weather_city_df['Wind Speed']

#scatter plot for Latitude vs. Wind Speed Plot 

plt.figure(4)

plt.scatter(x_lat, y_wind, marker="o", facecolors="blue", edgecolors="black",
                         s=40, alpha=0.75)

plt.title("City Latitude vs. Wind Speed " + "(" + str(date.today()) + ")")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")

plt.grid()
plt.savefig("C:/Users/LENOVO USER/Desktop/USC Data Bootcamp/5-HW, Python API/wind_vs_lat.png")
```


![png](output_13_0.png)


# WeatherPy Analysis:

based on above scatter plots, there's three noticeble trends:

1 - Counties located between 0 and 40 degrees latitude have the higher temperature. As shown from the first scatter plot, the father from the equator, the colder it gets; or vice versa it gets warmer near the equator.

2 - Humidity get very high when it gets closer to the equator as well. The south part of the earth or between -40 and 0 degrees latitude, humidity are high compared to the north part of the earth and humidity on the north are more evenly distributed.

3 - Based on the last two scatter plots, cloudiness and winds don't have much of relationship with latitude. Cloudiness are evenly distributed across full range of latitude and winds are mostly low across and concentrated between 0 and 60 degrees latitude.
