# Strings i comentaris

* [Strings](#strings)
* [Comentaris](#comentaris)

## Strings

Les variables de tipus `String` són seqüències immutables.
Això vol dir que podem efectuar-hi determinades operacions com si es tractés d'una llista:

* Podem accedir a un caràcter a partir de la seva posició o utilitzar el *slicing*
```python
text = "Hola món!"
text[3]     # a
text[5:8]   # món
```

* Podem calcular-ne la longitud
```python
text = "Hola món!"
len(text)   # 9
```

* Podem iterar-les
```python
text = "Hola món!"
for c in text:
    print(c, end=".")
# H.o.l.a. .m.ó.n.!.
```

* Utilitzar els operadors `in` i `not in`
```python
text = "Hola món!"
"m" in text     # True
" " not in text # False
```

* Crear una llista utilitzant la funció `list()`
```python
text = "Hola món!"
list(text)  # ['H', 'o', 'l', 'a', ' ', 'm', 'ó', 'n', '!']
```

D'altra banda, en ser objectes immutables no podem aplicar-hi mètodes com `append()`, `insert()` o `del`.
Per modificar una cadena de text cal crear una nova còpia cada vegada.

**Comparadors**

Les cadenes de text poden comparar-se utilitzant el símbols habituals `==` i `!=`.
Dues cadenes de text són iguals si tenen els mateixos caràcters en el mateix ordre.
```python
"world"=="world"    # True
"World"!="world"    # True
```

Les comparacions de quantitat `>`, `<`, `>=` i `<=` tenen en compte la codificació ASCII.
Cal tenir en compte que les majúscules tenen un codi inferior a les minúscules;
a més, els nombres es compararan tenint en compte el seu codi, no el seu valor. 
```python
"world">"World"    # True
"10"<"8"            # True
```

Aquests resultats són els que es tindran en compte en ordenar una llista de text.
```python
text = ["omega","alpha","gamma","delta"]
sorted(text)    # ['alpha', 'delta', 'gamma', 'omega']
text.sort()     # ['alpha', 'delta', 'gamma', 'omega']
```

**Funcions i mètodes** 

* `join()` - Uneix els caràcters de la llista interposant el caràcter especificat
```python
"-".join(['H','e','l','l','o'])     # 'H-e-l-l-o'
```

* `split()` - Separa una cadena en una llista de cadenes a partir del caràcter especificat
```python
text = "Hola, com estàs?"
text.split(" ")     # ['Hola,', 'com', 'estàs?']
```

* `index()`, `find()`  - Troba la posició del caràcter o cadena especificats
```python
text = "Hola món!"
text.index('o')     # 1
text.find('món')      # 5
```

* `replace()` - reemplaça el primer paràmetre pel segon
```python
text = "Hola Paula"
text.replace("LA","la")    # HoLA PauLA
```

* `count()`  - Compta el nombre d'aparicions del caràcter especificat
```python
text = "Hola món!"
text.count('a')     # 1
```

* `capitalize()` - Crea una nova cadena amb la primera lletra majúscula i la resta minúscules
* `lower()` - Crea una nova cadena amb les lletres en minúscules
* `upper()` - Crea una nova cadena amb les lletres en majúscules
* `swapcase()` - Intercanvia majúscules i minúscules
* `title()` - Posa en majúscula la primera lletra després de cada espai i la resta en minúscula
```python
text = "aBc.DeF!"
text.capitalize()   # 'Abc.def!'
text.lower()        # 'abc.def!'
text.upper()        # 'ABC.DEF!'
text.swapcase()     # 'AbC.dEf!'
```

* `center()` - Crea una nova cadena amb el nombre de caràcters especificats el text centrat.
També pot especificar-se un caràcter diferent a l'espai per afegir als extrems
```python
text = "abcd"
text.center(8)          # '  abcd  '
text.center(10,"*")     # '***abcd***'
```

* `endswith()` - Indica amb un boolean si la cadena acaba amb el text especificat
```python
text = "abcd"
text.endswith("cd")     # True
```

* `min()`,`max()` -  Troben el caràcter mínim o màxim seguint la codificació ASCII.
```python
text = "Hola món!"
min(text)   # ' '
max(text)   # 'ó'
```

* `isalnum()` - Indica si la cadena només conté caràcters alfanumèrics (lletres i dígits)
* `isalpha()` - Indica si la cadena només conté lletres
* `isdigit()` - Indica si la cadena només conté dígits
* `islower()` - Indica si la cadena només conté lletres minúscules
* `isupper()` - Indica si la cadena només conté lletres majúscules
* `isspace()` - Indica si la cadena només conté espais

[Métodes per manipular cadenes de text](https://docs.python.org/3.4/library/stdtypes.html#string-methods)


## Comentaris

Els comentaris permeten escriure text descriptiu que no serà interpretat.

```python
# Comentari d'una línia

"""
Comentari
de vàries
línies
"""
```