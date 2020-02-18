# Col·leccions

* [Llistes i tuples](#llistes-i-tuples)
* [Diccionaris](#diccionaris)

### Llistes i tuples

**Definició**

Les **llistes** són variables que permeten emmagatzemar vàries dades de tipus diferents de manera ordenada.
Es declaren utilitzant `[]` i els seus valors se separen per `,`.
Per accedir a un valor s'utilitza la seva posició, començant per 0.

```python
llista = ['text', 15, 2.8, True]
llista[0]   # 'text'
llista[1]   # 15
```

La funció `print()` permet mostrar tots els valors de la llista sense necessitat d'iterar-la.

En una llista, la variable emmagatzema la posició de memòria on es troben els seus valors.
Això vol dir que les si assignem aquesta llista a una altra variable estarem copiant-li l'adreça on es troben els seus valors.
Per tant, qualsevol operació que efectuem sobre la nova variable es passaran per referència i afectarà sempre els valors 
de totes dues variables.

```python
a = [5]
b = a
a[0] = 2
print(b[0])     # 2
```

Les **tuples** també permeten emmagatzemar dades diferents de manera ordenada (com una llista) però no es poden modificar, són immutables.
Es declaren utilitzant `()`, però s'hi accedeix com a una llista.
Per crear una tupla buida podem utilitzar `()`, però per crear una llista d'un sol element hem de fer `(1,)` per 
indicar que no és un literal.

```python
tupla = ('text', 124, False, 5.9)
tupla[0]  # Primer element
```

**Creació de llistes**

La funció `list()` permet crear un llista a partir d'altres tipus de dades.
```python
list("text")        # ['t','e','x','t']
list(range(5))      # [0,1,2,3,4]
list(range(3,8))    # [3,4,5,6,7]
list(range(1,10,2)) # [1,3,5,7,9]
```

Les llistes poden multiplicar-se i concatenar-se.
```python
[1,2,3] * 2         # [1,2,3,1,2,3]
[1,2,3] + [4,5,6]   # [1,2,3,4,5,6]
```

Les **llistes per comprensió** permeten crear llistes a partir d'una definició abstracta.
```python
quadrats = [x**2 for x in range(6)]                 # [0,1,4,9,16,25]
senars = [x for x in range(1,10) if x%2!=0]         # [1,3,5,7,9]
parells = [1 if x%2==0 else 0 for x in range(6)]   # [1, 0, 1, 0, 1, 0] 
```

La funció `split()` crea una llista separant una cadena de text per un caràcter especificat.
La funció `join()` realitza l'operació inversa i permet unir els elements d'una llista en una cadena de text nova.
```python
cadena = "a-b-c"
llista = cadena.split('-')  # ["a","b","c"]
cadena = '-'.join(llista)   # "a-b-c"
```

**Funcions**

Avaluen un resultat a partir d'una llista.

* `len()` - avalua la longitud de la llista, el nombre d'elements
```python
len([1,2,3,4])    # 4
```

* `max()` - avalua el valor més alt de la llista
```python
max([5,8,13,9])    # 13
```

* `min()` - avalua el valor més baix de la llista
```python
min([5,8,13,9])    # 5
```

* `sorted()` - retorna la llista ordenada
```python
sorted([4,2,6,3])   # [2,3,4,6]
```

* `del` - elimina l'element indicat de la llista
```python
a = [1,2,3,4,5]
del a[1]        # [1,3,4,5]
```

**Mètodes**

Actuen sobre la llista modificant els seus valors o propietats.

* `append(x)` - afegeix un valor al final de la llista
```python
a = [1,2,3]
a.append(4)     # afegim 4 al final
print(a)        # [1,2,3,4]
```

* `insert(n,x)` - afegeix el valor x a la posició n
```python
a = [1,2,3]
a.insert(0,5)   # afegim 5 a la posició 0
print(a)        # [5,1,2,3,4]
```

* `remove(x)` - elimina l'element especificat pel valor
```python
a = [1,2,3]
a.remove(2)     # eliminem el valor 2
print(a)        # [1,3]
```

* `index(x)` - indica la posició on es troba el valor
```python
a = [1,2,3]
a.index(3)     # 2
```

* `sort()` - ordena la llista
```python
a = [4,7,2,5]
a.sort()
print(a)    # [2,4,5,7]
```

**Slice**

La tècnica del *slice* permet fer una còpia d'una llista o d'una part d'ella; 
això vol dir que quan s'assigna a una nova variable no es copia l'adreça de la llista sinó tot o part del seu contingut.

Característiques:

* La seva sintaxi més general és `llista[inici:final]`
* El valor final inicial s'inclou a la llista però el final sempre queda exclòs
* `llista[:]` fa una còpia de la llista sencera
* Els nombres negatius indiquen les posicions comptant des del final
* Quan s'omet una valor és té en compte des de l'inici o des del final
* Pot especificar-se l'increment entre valors `llista[inici:final:salt]`

```python
a = [0,1,2,3,4,5,6]
a[:]        # [0,1,2,3,4,5,6]
a[1:4]      # [1,2,3]
a[-1]       # [6]
a[3:]       # [3,4,5,6]
a[:3]       # [0,1,2]
a[0:6:2]    # [0,2,4]
a[::-1]     # [6,5,4,3,2,1,0]
```

La paraula `del` permet eliminar part d'una llista.
```python
a = [0,1,2,3,4,5,6]
del a[1:5]
print(a)    # [0,5,6]
```

**Operadors**

* `in` - Avalua si un element es troba a la llista. Retorna `True` si hi és i `False` si no hi és.
```python
llista = [3,8,5,10]
5 in llista         # True
```
* `not in` - Avalua si un element no es troba a la llista. Retorna `True` si no hi és i `False` si hi és.
```python
llista = [3,8,5,10]
5 not in llista         # False
```

**Matrius**

Una matriu és una llista de llistes i pot representar-se com una taula de dades.
Per obtenir una fila podem fer `matriu[fila]` i per accedir a un element `matriu[fila][columna]`.
```python
matriu = [[0,1,2],[3,4,5],[6,7,8]]
matriu[1]       # [3,4,5]
matriu[2][1]    # 7
```

Podem generar matrius utilitzant les llistes per comprensió.
```python
[[i+j for i in range(3)] for j in range(3)]
# [[0, 1, 2],
#  [1, 2, 3],
#  [2, 3, 4]]
```

## Diccionaris

**Definició**

Els diccionaris permeten emmagatzemar dades que es consulten a partir d'una clau.
Les claus han de ser totes del mateix tipus de dades i no es poden repetir.
A diferència de les llistes, les dades no s'emmagatzemen seguint un ordre.

Per definir un diccionari s'utilitza la sintaxi següent:
```python
# Definició
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
# Consulta
prefixos[93]    # Barcelona
```

Les dades es poden consultar indicant la clau entre `[]`.
Si es fa una assignació sobre una clau ja existent se substituirà el valor antic pel nou.
En canvi, si es fa una assignació sobre una clau que no existeix s'afegiran la clau i el valor.
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona'}
# consulta
prefixos[93]    # Barcelona
# canvi de valor
prefixos[977] = "Reus"
# nova clau
prefixos[973] = "Lleida"
```

Per eliminar una clau utilitzem la paraula `del`.
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona'}
del prefixos[977]
```

**Operadors**

Els operadors `in` i `not in` permeten saber si una clau es troba al diccionari.
```python
# Definició
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
# Consulta
93 in prefixos      # True
977 not in prefixos # False
```

**Iteració**

Si volem obttenir tots els valors d'un diccionari podem utilitzar el mètode `keys()`.
Aquest mètode retorna una llista amb totes les claus del diccionari i permet iterar sobre elles.
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
# iteració
for codi in prefixos.keys():
    print("codi: ", codi, " província: ", prefixos[codi])
```

Una altra possibilitat és utilitzar el mètode `items()`, que retorna una llista de tuples (clau, valor).
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
# iteració
for codi,prefix in prefixos.items():
    print("codi: ", codi, " província: ", prefix)
```

Finalment, disposem del mètode `values()` que retorna una llista de tots els valors del diccionari.
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
# iteració
for provincia in prefixos.values():
    print("província: ", provincia)
```

**Funcions**

* `len()` - retorna la longitud del diccionari, el nombre de claus
```python
prefixos = {93:'Barcelona', 972:'Girona', 977:'Tarragona', 973:'Lleida'}
len(prefixos)   # 4
```
