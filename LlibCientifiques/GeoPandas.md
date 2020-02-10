# GeoPandas

[Exemples](GeoPandas.ipynb)

## Introducció

GeoPandas és un projecte de codi obert per treballar amb dades geoespacials en Python.
Es tracta d'una extensió de les estructures de dades de Pandas per poder representar dades geomètriques i efectuar operacions espaials.

GeoPandas depèn de les llibreries: numpy, pandas, shapely, fiona, pyproj i six.
A més, per a la representació gràfica requereix matplotlib, descartes i mapclassify.

La importació acostuma a fer-se amb l'àlies `gpd`.
```python
import geopandas as gpd
```

Les opcions de la llibreria poden consultar-se amb l'atribut `options`.

```python
import geopandas
geopandas.options
```

## Estructures de dades

GeoPandas utilitza tres tipus d'objectes geomètrics o vectors:

* punts: Point / MultiPoint
* línies: Line / MultiLine
* polígons: Polygon / MultiPolygon

Aquests objectes d'implementen a través de dues estructures de dades: `GeoSeries`, que és una subclasse de `Series`,
i `GeoDataFrame`, que és una extensió de `DataFrame`.

### GeoSeries

Es tracta d'un vector que conté un conjunt d'objectes geomètrics del mateix tipus (punt, línia o polígon).

Atributs:

* `area` - area de la forma en les unitats de la projecció
* `bounds` - coordenades màximes i mínimes de cada eix per cada element
* `total_bounds` - coordenades màximes i mínimes de cada eix per a tota la sèrie
* `geom_type` - tipus de geometria
* `is_valid` - avalua si les coordenades generen una forma raonablement geomètrica d'acord amb certes condicions

Mètodes:

* `distance()` - distància mínima a un altre objecte
* `centroid()` - retorna el centroide
* `representative_point()` - torna un punt situat dins de cada objecte
* `to_crs()` - canvia el sistema de coordenades de referència
* `plot()` - representa tots els objectes en un mapa
* `contains()` - avalua si una forma conté una altra
* `intersects()` - avalua si una forma talla una altra

### GeoDataFrame

Estructura en forma de taula que conté un objecte `GeoSeries` en una columna, generalment anomenada *geometry*.
Aquesta columna pot ser consultada a través l'atribut `geometry`. 
Quan se li aplica un mètode espaial a un GeoDataFrame només actua sobre aquesta columna.

Podem modificar el nom de la columna geomètrica amb `gdf.geometry.name`.
També podem canviar la columna que conté les dades geomètriques amb el mètode `set_geometry()`.
La columna que conté les dades geomètriques s'identifica pel nom, per tant, si canvia el seu nom cal reassignar-la com a columna geomètrica.

```python
gdf.geometry.name   # 'geometry
gdf = gdf.rename(columns={'geometry': 'formes'}).set_geometry('formes')
gdf.geometry.name   # 'formes'
``` 

```python
gdf['centroid_column'] = gdf.centroid
gdf = gdf.set_geometry('centroid_column')
gdf.plot()
```

Els atributs i mètodes descrits per a les `GeoSeries` també funcionen per als `GeoDataFrame`, 
únicament sobre la columna *geometry*.

## Entrada i sortida de dades

### Llegint dades de fitxers

GeoPandas pot llegir dades vectorials de fitxers amb formats *ESRI shapefile*, *GeoJSON* i altres amb la funció `read_file()`.
Aquesta funció retorna un objecte `GeoDataFrame`.
```python
gdf = gpd.read_file('dades.shp')
```

Aquesta lectura de dades es basa en la llibreria **fiona** i utilitza la instrucció `fiona.open`.
Això vol dir que tots els paràmetres de *fiona* poden utilitzar-se també darrera del nom del fitxer.
La documentació d'aquesta llibreria pot aconseguir-se fent:
```python
import fiona
help(fiona.open)
```

La lectura de dades pot fer-se també de fitxers remots a través de la URL.
```python
world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
```

El paràmetre `layer` permet obtenir una cap concreta d'un fitxer multi-capa.
```python
gdf = gpd.read_file('package.gpkg', layer='capa')
```

Finalment, poden obtenir-se data d'una base de dades **PostGIS** amb la funció `read_postgis()`.

### Escriptura de dades en fitxers

Els objectes `GeoDataFrame` poden exportar-se a diferents formats de fitxers utilitzant la funció `to_file()`.
La llista de formats suportats pot consultar-se a `fiona.supported_drivers`.

```python
# Guarden a Shapefile
gdf.to_file("nom.shp")

# Guardant a GeoJSON
gdf.to_file("nom.geojson", driver='GeoJSON')

# Guardant a GeoPackage
gdf.to_file("package.gpkg", layer='capa', driver='GPKG')
``` 

## Selecció de dades

GeoPandas permet seleccionar dades utilitzant elsmètodes habituals de pandas: `.loc[]` per filtrar a través del nom 
de les etiquetes, i `.iloc[]` per filtrar per posició.
A més, proporciona un mètode per `cx` filtrar a partir de les dades geoespacials.
Aquest mètode utilitza les coordenades geogràfiques per seleccionar les dades que tallen amb l'àrea indicada.

```python
hemisferi_sud = world.cx[:, :0]
```  

## Visualització de dades

GeoPandas proporciona una interfície d'alt nivell per crear mapes utilitzant la llibreria **matplotlib**.
Invocant el mètode `plot()` des de qualsevol objecte `GeoSeries` o `GeoDataFrame` es representa gràficament tota la informació en un mapa.
En general, totes les opcions de **pyplot** poden passar-se al mètode `plot()`.
```python
gdf.plot()
```

### Mapes de color

Per crear mapes de color, on la tonalitat de cada forma es basa en un valor associat, 
cal utilitzar el mètode `plot()` amb el paràmetre `column`.
```python
gdf.plot(column='columna_dades')
```

El paràmetre `cmap` permet escollir un mapa de color.
La llista completa es troba a la pàgina de [matplotlib](https://matplotlib.org/users/colormaps.html).
```python
gdf.plot(column='dades', cmap='RdPu')
```

Per afegir la llegenda podem utilitzar el paràmetre `legend=True`.

### Mapes amb capes

Abans de combinar mapes cal assegurar-se que comparteixen el sistema de coordenades.

Per utilitzar un mapa com a base d'una altra capa cal passar-lo a través del paràmetre `ax`.
```python
base = gdf.plot(color='white', edgecolor='black')
capa.plot(ax=base, color='red')
```

Una altra possibilitat, més flexible, consisteix a utilitzar els objectes de la llibreria matplotlib.
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()

gdf1.plot(ax=ax, color='white', edgecolor='black')
gdf2.plot(ax=ax, color='red')

plt.show()
```

## Sistemes de referència de coordenades

Els Sistemes de Referència de Coordenades (SRC) indiquen a quina posició de la Terra es troben les formes geomètriques.
Els SRC es referencien utilitzant codis anomenats **proj4 strings**; a més, les projeccions més habituals també poden ser 
referenciades utilitzant els codis EPSG.

Les dades importades d'un fitxer inclouen la informació de la projecció.
Podem obtenir-la amb l'atribut `crs`.

```python
gdf.crs     
```

Establir una projecció és necessari quan les dades tenen unes coordenades però no estan referenciada la seva posició a la Terra.
Per fer-ho cal indicar un valor a l'atribut `crs`.

```python
gdf.crs = {'init': 'epsg:4326'}
```

La funció `to_crs()` permet canviar el sistema de coordenades d'unes dades.

```python
gdf.crs     # {'init': 'epsg:4326'}
gdf = gdf.to_crs({'init': 'epsg:3395'})
```

## Manipulacions geomètriques

GeoPandas permet utilitzar totes les eines per a les manipulacions geomètriques de la llibreria **shapely**.

**Mètodes constructors**.

Generen un objecte `GeoSeries` a partir dels objectes geomètrics d'un altra `GeoSeries`: 

* `buffer()` - punts dins d'una determinada distància a l'objecte inicial
* `boundary` - objecte de dimensió inferior que representa el límit teòric de cada geometria (el contorn)
* `centroid` - punt centroide de cada geometria
* `convex_hull` - polígon convex més petit que conté tots els punts de cada geometria
* `envelope` - polígon rectangular més petit que conté cada objecte
* `simplify()` - representació simplificada de cada objecte

Genera una geometria:

* `unary_union` - unió de tots els elements de la `GeoSeries`   

**Transformacions afins**

* `affine_transform()` - transforma les geometries utilitzant una matriu de transformacions
* `rotate()` - rotació de l'objecte el nombre de graus especificat
* `scale()` - modifica l'escala al llarg de qualsevol eix
* `skew()` - deforma les geometries per angles al llarg de les dimensions x i y
* `translate()` - canvia les coordenades

## Operacions entre conjunts sobreposats

Es tracta de les operacions habituals entre geometries que se sobreposen:

* `intersection` - intersecció, punts en comú
* `union` - unió, tots els punts
* `difference` - diferència, punts d'una geometria no sobreposats a l'altra
* `symetrical difference` - diferència simètrica, punts no sobreposats, inversa de la intersecció

Aquestes operacions s'implementen a través de la funció `overlay()` i el paràmetre `how`.
Només funcionen sobre objectes `GeoDataFrame`.

```python
geopandas.overlay(df1, df2, how='intersection')
```

## Agregació

Per agregar dades a partir de la informació geomètrica utilitzem la funció `dissolve`.
Aquesta funció realitza tres tasques:

* Uneix totes les geometries en un únic objecte utilitzant el mètode `unary_union`
* Agrega totes les files en un registre utilitzant `groupby.aggregate()`
* Combina els dos resultats en un nou `GeoDataFrame`

El paràmetre `aggfunc` permet especificar la funció d'agregació utilitzada. Els seus valors poden ser: *first, last, min, max, sum, mean* i *median*.
```
world.dissolve(by='continent', aggfunc='sum')
```

## Combinació de dades

La combinació de diferents estructures de dades pot fer-se de dues maneres:

**Attribute joins**

Les estructures de dades es combinen a partir del valor d'un atribut. Es tracta de l'operació de `join` habitual amb el mètode `merge()` de Pandas. El `GeoDataFrame` ha de situar-se a l'esquerra i el `DataFrame` a la dreta.

**Spatial joins**

Els registres es combinen a partir de les seves relacions a l'espai. S'utilitza el mètode `sjoin()` amb els paràmetres `how` i `op`.

* `op`: intersects, within, contains
* `how`: left, right, inner


## Geocoding

GeoPandas suporta el **geocoding** a través de [GeoPy](https://geopy.readthedocs.io/en/stable/).
Aquesta eina permet situar en un mapa adreces, ciutats, països... 

Aquesta funció es troba a `gpd.tools.geocode()` i el paràmetre `provider` permet especificar el servei de geocoding utilitzat.

## Referències

* [geopandas.org](http://geopandas.org/)
* [Documentació oficial](http://geopandas.org/reference.html)
* [shapely](https://shapely.readthedocs.io/en/latest/manual.html)

