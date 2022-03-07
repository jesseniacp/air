# Visualizacion de archivo netCDF - Temperatura de Aire
*ALUMNOS* |  
----------------------| 
CASAS POMACAJA JESSENIA | 
IIlan Prada Catheling Palmira |
Perez Rojas Naason |
Sangama López Sofia Samantha |
Zevallos Segura Percy Miguel |

-  Instalando libreria netCDF
```
!pip install netCDF4

Requirement already satisfied: netCDF4 in c:\users\armando\anaconda3\lib\site-packages (1.5.7)
Requirement already satisfied: cftime in c:\users\armando\anaconda3\lib\site-packages (from netCDF4) (1.5.0)
Requirement already satisfied: numpy>=1.9 in c:\users\armando\anaconda3\lib\site-packages (from netCDF4) (1.16.5)
```
- importar las librerias que se usaran 
```
from netCDF4 import Dataset 
import numpy as np 
import matplotlib.pyplot as plt
```
- leer el archivo netCDF4
``` 
ncFile =Dataset("C:\OpenGrADS\Z_DATOS PARA TRABAJO FINAL/airetemperatura.nc","r")
```
- para ver las propiedades del archivo
```
print(ncFile)
<class 'netCDF4._netCDF4.Dataset'>
root group (NETCDF4_CLASSIC data model, file format HDF5):
    Conventions: COARDS
    title: mean daily NMC reanalysis (2011)
    description: Data is from NMC initialized reanalysis
(4x/day).  These are the 0.9950 sigma level values.
    platform: Model
    history: Sat Mar  5 16:04:28 2022: ncrcat -O -d lat,-90.000000,90.000000 -d lon,0.000000,357.500000 -d time,2011-01-01T00:00:0.0,2020-01-01T00:00:0.0 -n 10,4,1 /Datasets/ncep.reanalysis.dailyavgs/surface/rhum.sig995.2011.nc /Public/www/X179.6.218.238.63.16.4.27.nc
created 2011/01 by Hoop (netCDF2.3)
Converted to chunked, deflated non-packed NetCDF4 2014/09
    dataset_title: NCEP-NCAR Reanalysis 1
    References: https://www.psl.noaa.gov/data/gridded/data.ncep.reanalysis.html 
    NCO: netCDF Operators version 4.8.1 (Homepage = http://nco.sf.net, Code = http://github.com/nco/nco)
    dimensions(sizes): lat(73), lon(144), time(3288)
    variables(dimensions): float32 lat(lat), float32 lon(lon), float64 time(time), float32 air(time,lat,lon)
    groups: 
```
- Ver las variables
```
{'level': <class 'netCDF4._netCDF4.Variable'>
 float32 level(level)
     units: millibar
     long_name: Level
     positive: down
     GRIB_id: 100
     GRIB_name: hPa
     axis: Z
     actual_range: [500. 500.]
 unlimited dimensions: 
 current shape = (1,)
 filling on, default _FillValue of 9.969209968386869e+36 used,
 'lat': <class 'netCDF4._netCDF4.Variable'>
 float32 lat(lat)
     units: degrees_north
     long_name: Latitude
     standard_name: latitude
     axis: Y
     actual_range: [ 10. -60.]
 unlimited dimensions: 
 current shape = (29,)
 filling on, default _FillValue of 9.969209968386869e+36 used,
 'lon': <class 'netCDF4._netCDF4.Variable'>
 float32 lon(lon)
     units: degrees_east
     long_name: Longitude
     standard_name: longitude
     axis: X
     actual_range: [270. 330.]
 unlimited dimensions: 
 current shape = (25,)
 filling on, default _FillValue of 9.969209968386869e+36 used,
 'time': <class 'netCDF4._netCDF4.Variable'>
 float64 time(time)
     long_name: Time
     delta_t: 0000-00-01 00:00:00
     avg_period: 0000-00-01 00:00:00
     standard_name: time
     axis: T
     units: hours since 1800-01-01 00:00:0.0
     actual_range: [1753152. 1849584.]
 unlimited dimensions: time
 current shape = (4019,)
 filling on, default _FillValue of 9.969209968386869e+36 used,
 'air': <class 'netCDF4._netCDF4.Variable'>
 float32 air(time, level, lat, lon)
     long_name: mean Daily Air temperature
     units: degK
     precision: 2
     least_significant_digit: 1
     GRIB_id: 11
     GRIB_name: TMP
     var_desc: Air temperature
     dataset: NCEP Reanalysis Daily Averages
     level_desc: Multiple levels
     statistic: Mean
     parent_stat: Individual Obs
     missing_value: -9.96921e+36
     valid_range: [150. 350.]
     actual_range: [240.87001 269.95   ]
 unlimited dimensions: time
 current shape = (4019, 1, 29, 25)
 filling on, default _FillValue of 9.969209968386869e+36 used}
 ```
 - Dimensiones
```
ncFile.dimensions
{'level': <class 'netCDF4._netCDF4.Dimension'>: name = 'level', size = 1,
 'lat': <class 'netCDF4._netCDF4.Dimension'>: name = 'lat', size = 29,
 'lon': <class 'netCDF4._netCDF4.Dimension'>: name = 'lon', size = 25,
 'time': <class 'netCDF4._netCDF4.Dimension'> (unlimited): name = 'time', size = 4019}
``` 
- Variable air
``` 
<class 'netCDF4._netCDF4.Variable'>
float32 air(time, lat, lon)
    long_name: mean Daily Air temperature at sigma level 995
    units: degK
    precision: 2
    least_significant_digit: 1
    GRIB_id: 11
    GRIB_name: TMP
    var_desc: Air temperature
    dataset: NCEP Reanalysis Daily Averages
    level_desc: Surface
    statistic: Mean
    parent_stat: Individual Obs
    missing_value: -9.96921e+36
    valid_range: [185.16 331.16]
    actual_range: [230.37 311.45]
unlimited dimensions: time
current shape = (3288, 73, 144)
filling on, default _FillValue of 9.969209968386869e+36 used
``` 
- Definimos las variables que vamos a trabajaar air(time, lat, lon)
```
#air(time, lat, lon)
air = ncFile.variables["air"][:]
lon = ncFile.variables["lon"][:]
lat = ncFile.variables["lat"][:]
t = ncFile.variables["time"][:]
```
- Llamamos a las variables 
```
lon
masked_array(data=[  0. ,   2.5,   5. ,   7.5,  10. ,  12.5,  15. ,  17.5,
                    20. ,  22.5,  25. ,  27.5,  30. ,  32.5,  35. ,  37.5,
                    40. ,  42.5,  45. ,  47.5,  50. ,  52.5,  55. ,  57.5,
                    60. ,  62.5,  65. ,  67.5,  70. ,  72.5,  75. ,  77.5,
                    80. ,  82.5,  85. ,  87.5,  90. ,  92.5,  95. ,  97.5,
                   100. , 102.5, 105. , 107.5, 110. , 112.5, 115. , 117.5,
                   120. , 122.5, 125. , 127.5, 130. , 132.5, 135. , 137.5,
                   140. , 142.5, 145. , 147.5, 150. , 152.5, 155. , 157.5,
                   160. , 162.5, 165. , 167.5, 170. , 172.5, 175. , 177.5,
                   180. , 182.5, 185. , 187.5, 190. , 192.5, 195. , 197.5,
                   200. , 202.5, 205. , 207.5, 210. , 212.5, 215. , 217.5,
                   220. , 222.5, 225. , 227.5, 230. , 232.5, 235. , 237.5,
                   240. , 242.5, 245. , 247.5, 250. , 252.5, 255. , 257.5,
                   260. , 262.5, 265. , 267.5, 270. , 272.5, 275. , 277.5,
                   280. , 282.5, 285. , 287.5, 290. , 292.5, 295. , 297.5,
                   300. , 302.5, 305. , 307.5, 310. , 312.5, 315. , 317.5,
                   320. , 322.5, 325. , 327.5, 330. , 332.5, 335. , 337.5,
                   340. , 342.5, 345. , 347.5, 350. , 352.5, 355. , 357.5],
             mask=False,
       fill_value=1e+20,
            dtype=float32)
lat
masked_array(data=[ 90. ,  87.5,  85. ,  82.5,  80. ,  77.5,  75. ,  72.5,
                    70. ,  67.5,  65. ,  62.5,  60. ,  57.5,  55. ,  52.5,
                    50. ,  47.5,  45. ,  42.5,  40. ,  37.5,  35. ,  32.5,
                    30. ,  27.5,  25. ,  22.5,  20. ,  17.5,  15. ,  12.5,
                    10. ,   7.5,   5. ,   2.5,   0. ,  -2.5,  -5. ,  -7.5,
                   -10. , -12.5, -15. , -17.5, -20. , -22.5, -25. , -27.5,
                   -30. , -32.5, -35. , -37.5, -40. , -42.5, -45. , -47.5,
                   -50. , -52.5, -55. , -57.5, -60. , -62.5, -65. , -67.5,
                   -70. , -72.5, -75. , -77.5, -80. , -82.5, -85. , -87.5,
                   -90. ],
             mask=False,
       fill_value=1e+20,
            dtype=float32)
t
masked_array(data=[1849584., 1849608., 1849632., ..., 1928424., 1928448.,
                   1928472.],
             mask=False,
       fill_value=1e+20)
air
masked_array(
  data=[[[241.76999, 241.76999, 241.76999, ..., 241.76999, 241.76999,
          241.76999],
         [242.1    , 242.15   , 242.20001, ..., 242.05002, 242.05002,
          242.1    ],
         [238.62   , 238.65   , 238.70001, ..., 239.1    , 238.85   ,
          238.70001],
         ...,
         [254.32   , 254.35   , 254.32   , ..., 254.28   , 254.26999,
          254.32   ],
         [250.32   , 250.20001, 250.15   , ..., 250.6    , 250.5    ,
          250.42001],
         [249.35   , 249.35   , 249.35   , ..., 249.35   , 249.35   ,
          249.35   ]],

        [[247.4    , 247.4    , 247.4    , ..., 247.4    , 247.4    ,
          247.4    ],
         [248.97   , 248.85   , 248.72   , ..., 249.22   , 249.15   ,
          249.05002],
         [248.17001, 247.76999, 247.37   , ..., 249.82   , 249.25   ,
          248.67001],
         ...,
         [253.4    , 253.47   , 253.55002, ..., 253.17001, 253.20001,
          253.28   ],
         [249.70001, 249.62   , 249.55002, ..., 250.01999, 249.92001,
          249.82   ],
         [250.32   , 250.32   , 250.32   , ..., 250.32   , 250.32   ,
          250.32   ]],

        [[249.47   , 249.47   , 249.47   , ..., 249.47   , 249.47   ,
          249.47   ],
         [247.1    , 247.25   , 247.35   , ..., 246.62   , 246.82   ,
          246.97   ],
         [249.95001, 249.97   , 249.97   , ..., 249.76999, 249.87   ,
          249.93   ],
         ...,
         [251.65   , 251.80002, 251.92001, ..., 251.07   , 251.22   ,
          251.42001],
         [247.05002, 246.97   , 246.92001, ..., 247.35   , 247.22   ,
          247.12   ],
         [248.75   , 248.75   , 248.75   , ..., 248.75   , 248.75   ,
          248.75   ]],

        ...,

        [[247.4    , 247.4    , 247.4    , ..., 247.4    , 247.4    ,
          247.4    ],
         [245.17499, 245.04999, 244.87498, ..., 245.52498, 245.42499,
          245.32498],
         [246.15   , 246.15   , 246.04999, ..., 245.87498, 246.     ,
          246.07498],
         ...,
         [255.99997, 256.05   , 256.1    , ..., 255.875  , 255.85   ,
          255.92499],
         [252.67499, 252.65   , 252.62498, ..., 252.82498, 252.77498,
          252.72499],
         [251.54999, 251.54999, 251.54999, ..., 251.54999, 251.54999,
          251.54999]],

        [[244.67499, 244.67499, 244.67499, ..., 244.67499, 244.67499,
          244.67499],
         [242.65   , 242.34999, 242.09998, ..., 243.42499, 243.17499,
          242.92499],
         [243.14998, 242.99998, 242.79999, ..., 243.4    , 243.34999,
          243.22499],
         ...,
         [254.14998, 254.22498, 254.275  , ..., 254.09998, 254.04999,
          254.09999],
         [250.07498, 250.04999, 250.04999, ..., 250.24998, 250.15   ,
          250.09998],
         [250.92499, 250.92499, 250.92499, ..., 250.92499, 250.92499,
          250.92499]],

        [[241.775  , 241.775  , 241.775  , ..., 241.775  , 241.775  ,
          241.775  ],
         [240.525  , 240.65   , 240.775  , ..., 240.125  , 240.275  ,
          240.425  ],
         [236.92499, 237.1    , 237.34999, ..., 236.275  , 236.49998,
          236.7    ],
         ...,
         [252.4    , 252.65   , 252.875  , ..., 251.79999, 251.94998,
          252.15   ],
         [248.72499, 248.74998, 248.79999, ..., 248.72499, 248.7    ,
          248.72499],
         [250.32498, 250.32498, 250.32498, ..., 250.32498, 250.32498,
          250.32498]]],
  mask=False,
  fill_value=1e+20,
  dtype=float32)
  ```
 - air(time, lat, lon)
 ```
data = air[3287,:,:]

x,y =np.meshgrid(lon,lat)
  ```
- Codigos para el grafico
```
fig = plt.figure()

ax = fig.add_axes([1,1,1.5,1.5])

cmap = plt.cm.get_cmap('jet')

ax.set_xlabel(r'LON', size=20)

ax.set_ylabel(r'LAT', size=20)

ax.grid(b=True, which='major', color='grey', linestyle='--',alpha= 0.5)

#####################################SUB REGIONES########

ax.grid(b=True, which='major', color='grey', linestyle='--',alpha= 0.5)

############variables con el ploteo del efecto shaded y contour################

mapaf = plt.contourf(x,y,data,30 ,alpha=0.95,cmap=cmap)

mapac = plt.contour(x,y,data,30,colors = 'g')

plt.clabel(mapaf,fontsize=8,inline=1,fmt= '%1.1f')

plt.colorbar(mapaf)

plt.title("TEMPERATURA DE VIENTO/ENERO 2020",size=20)

plt.show()
```
-Imagen
 ![Temperatura de Aire/Enero2020](https://github.com/jesseniacp/air/blob/main/temperaturaenero.jpeg)

