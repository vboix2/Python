# Pandas

* [Series](#series)
* [DataFrame](#dataframe)

### Introducció

Llibreria per a la manipulació i anàlisi de dades.

Generalment s'importa amb l'àlies `pd`.
```python
import pandas as pd
```

**Estructures de dades**

Pandas utilitza tres estructures de dades:

* *Series* - vector unidimensional de dades homogènies amb etiquetes
* *DataFrame* - matriu bidimensional de dades heterogènies amb etiquetes
* *Panel* - estructura tridimensional de dades heterogènies amb etiquetes

**Tipus de dades**


### Series

Permet representar un conjunt de dades unidimensional (enters, reals o cadenes de caràcters).
Si es barregen tipus de dades es crearà la sèrie amb el tipus més general.

Per crear una sèrie utilitzem el constructor `Series()`.
Per defecte s'utilitzen com a índex nombres enters començant pel 0.
```python
pd.Series([3,5,8])
# 0     3
# 1     5
# 2     8
# dtype: int64
```

Si volem especificar les etiquetes podem crear una sèrie a partir d'un diccionari o indicar els índexs en un array.
```python
pd.Series({"a":3, "b":5, "c":8})
pd.Series([3,5,8], index=["a","b","c"])
# a     3
# b     5
# c     8
# dtype: int64
```

### DataFrame

**Definició**

El `DataFrame` és l'estructura principal de Pandas.
Es tracta d'una matriu bidimensional de dades amb etiquetes.
Cada columna ha de tenir el mateix tipus de dada, però columnes diferents poden tenir un tipus de dades diferents.
Podem crear etiquetes per files i per columnes.

Per crear un DataFrame utilitzem el seu constructor `DataFrame()`.
Es pot crear a partir d'un diccionari de llistes i una llista d'etiquetes.
```python
dicc = {"columna1":[1,3,5], "columna2":[2,4,6]}
pd.DataFrame(dicc, index=["fila1","fila2","fila3"])
#       columna1    columna2
# fila1     1           2
# fila2     3           4
# fila3     5           6
```

També és possible crear-lo a partir d'una matriu i dues llistes d'etiquetes.
```python
m = [[1,2],[3,4],[5,6]]
pd.DataFrame(m, columns=["columna1","columna2"], index=["fila1","fila2"])
#       columna1    columna2
# fila1     1           2
# fila2     3           4
# fila3     5           6
```

Si no s'especifica `index` (etiquetes per a les files) s'utilitzen nombres enters començant per 0.

**Importació i exportació de dades**

La funció `read_csv()` permet crear un DataFrame a partir d'un fitxer CSV.
```python
df = pd.read_csv('fitxer.csv')
```
Paràmetres:

* `sep` - personalitza el separador
* `encoding` - codificació de caràcters (`utf8`,`latin1`...)
* `index_col` - tria la columna que actuarà d'índex

La funció `to_csv()` permet generar un fitxer CSV a partir d'un dataframe
```python
df.to_csv('fitxer.csv', header=True, index=False)
```

**Obtenció de dades**

* `df.index` - mostra l'índex
* `df.columns` - mostra el nom de les columnes
* `df.values` - mostra la matriu de valors
* `len(df)` - mostra la quantitat de registres
* `list(df)` - llistat d'atributs
* `df.head(n)` - mostra les n primeres files (per defecte 5)
* `df.tail(n)` - mostra les n últimes files (per defecte 5)
* `df.describe()` - mostra dades estadístiques de les columnes numèriques
* `df.info()` - mostra informació sobre el tipus de dades i el nombre de valors nuls

**Selecció de dades**

* `df[col]` - obtenim una sèrie amb tots els valors d'una columna
* `df[inici:final]` - seleccionem diverses files per slicing
* `df[col][fila]` - obtenim el valor d'una cel·la
* `df[col][inici:final]` - obtenim una sèrie amb una part dels valors d'una columna

L'operador `loc[]` permet consultar registres per etiqueta.

* `df.loc[[fila1,fila2..],[col1,col2...]]` - accés a valors concrets per etiqueta
* `df.loc[fila1:fila2, col1:col2]` - slicing per etiquetes
* `df.loc[df.columna==valor, columna]` - selecció per condicions booleanes

L'operador `iloc[]` permet seleccionar per posició

* `df.iloc[n]` - dades de la columna n
* `df.iloc[i,j]` - dades de la fila i columna j
* `df.iloc[a:b, c:d]` - dades de les files a:b, columnes c:d (slicing)
* `df.iloc[[a,b,c], [d,e]]` - dades de les files a,b,c i columnes d,e

**Valors nuls**

Els valors nuls es representen amb el tipus `np.nan`

* `df.isna()` - indica les posicions amb NaN
* `df.dropna(how='any')` - elimina les files amb algun valor nul
* `df.fillna(value=x)` - omple els NaN amb el valor especificat

**Operacions**

Les funcions min, max, sum, mean, median permeten obtenir valors estadístics de les files o columnes.
```python
df.mean()  # mitjana de les columnes
df.mean(1)  # mitjana de les files
```

La funció `apply()` aplica una funció a les dades
```python
df.apply(function)
df.apply(lambda x: np.sqrt(x))
``` 

**Agrupació**

Permet crear grups de dades i operar sobre els grups creats (min,max,sum,mean,count)

* `df.groupby(col).sum()`
* `df.groupby([col1, col2]).mean()`
* `df.groupby(col).agg({'col':fun, 'col2':fun})`


**Manipulació de dataframes**

Concatenació:

* `pd.concat([df1, df2])` - afegeix files
* `pd.concat([df1, df2], axis=1)` - afegeix columnes

Afegir columnes:

* `df.assign(nom = lambda x: expressió)`