# Funcions

### Definició

Les funcions permeten encapsular un conjunt d'instruccions i executar-les únicament a partir d'un nom, evitant 
repetir-les vàries vegades durant el codi. També permeten dividir un programa excessivament complex en diferents 
blocs més senzills i fàcils de comprendre. Això és la base de la **programació modular** i permet dividir
un programa en diferents blocs autònoms, que poden ser desenvolupats de manera independent per diferents persones.

Les funcions poden ser:

* pròpies del llenguatge python: `print`, `input`...
* de mòduls o llibreries externes
* definides pel programador

Per definir una funció utilitzem: `def ` + nom de la funció + `() :`.
El nom de la funció segueix les mateixes restriccions que una variable, a més, no pot haver-hi una variable i una
funció amb el mateix nom.
Les instruccions de la funció s'agrupen a través de la identació.
Per cridar una funció  n'hi ha prou amb utilitzar el seu nom, però cal tenir en compte que python és un llenguatge
interpretat i, per tant, sempre que es cridi una funció s'haurà d'haver definit abans.
```python
# definició de la funció
def nombres():
    for i in range(10):
        print(i)
# crida a la funció
nombres()
```

### Paràmetres d'entrada

Les funcions admeten paràmetres d'entrada (arguments) per afegir dades a la seva invocació.
Els paràmetres d'entrada s'indiquen com a variables al parèntesi de la declaració de la funció i només tenen 
validesa dins del context de la funció.
```python
# definició
def nombres(final):
    for i in range(final):
        print(i)
# invocació
nombres(10)
```

També podem indicar més d'un paràmetre d'entrada.
En aquest cas, si durnat la invocació de la funció només indiquem el valor dels paràmetres (els arguments) s'identificaran
per la seva posició a la declaració de la funció (*positional parameter passing*).
```python
def nombres(inici, final):
    for i in range(inici, final):
        print(i)
# pas de paràmetres posicionals
nombres(5,10)
```

Una altra opció és identificar-los pel nom de la variable que tenen assignat a la declaració (*keyword argument passing*).
```python
def nombres(inici, final):
    for i in range(inici, final):
        print(i)
# pas d'arguments per paraula clau
nombres(final=10, inici=5)
```

Alguns paràmetres d'entrada poden estar predefinits a la pròpia declaració.
En aquest cas, si no s'indica cap valor s'agafarà el valor per defecte indicat a la declaració.
```python
def nombres(final, inici=1):
    for i in range(inici, final):
        print(i)

nombres(10)
```

### Paràmetres de sortida

Els paràmetres de sortida permeten obtenir un valor com a resultat de l'execució de la funció.
Per fer-ho cal indicar un valor (literal, variable o expressió) després de la paraula `return` al final de la declaració de la funció.
El valor del paràmetre de sortida subsituirà a la funció allà on ha estat invocada i pot ser operat, assignat a una
variable o, fins i tot, utilitzar-se com a paràmetre d'entrada en una altra invocació. 
```python
# declaració
def suma(a,b):
    c = a + b
    return c
# invocació
x = suma(25,74)
```

La paraula `return`, sense cap valor a continuació, permet sortir de l'execució de la funció en qualsevol moment.
En aquest cas, la invocació de la funció obté el valor `None`.
```python
def funcio(sortir=True):
    print("inici")
    if sortir:
        return
    print("final")
```

El resultat d'una funció també pot ser una llista.
```python
def nombres(inici,final):
    llista = [i for i in range(inici, final)]
    return llista
```

### Abast de les variables

Les variables declarades dins d'una funció només tenen validesa dins d'aquesta funció.
En canvi, les variables declarades fora poden ser llegides dins de qualsevol funció,
excepte si ja hi ha una altra variable declarada dins de la funció amb el mateix nom;
no poden ser modificades perquè l'assignació obligaria a crear una nova variable dins de la funció.
```python
x = 100
def suma(y):
    return x + y
```

Per poder utilitzar una variable d'una funció fora d'aquesta l'hem de declarar com a `global`.
En aquest cas podem llegir i modificar la variable tant fora com dins de la funció. 
```python
def suma(x,y):
    global z
    z = x+y
print(z)
```