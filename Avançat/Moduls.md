# Mòduls i paquets

* [Utilització de mòduls](#utilitzaci-de-mduls)
* [Creació de mòduls](#creaci-de-mduls)
* [Paquets](#paquets)

## Introducció

Els mòduls permeten dividir un programa en blocs de codi independents que funcionen conjuntament; 
a la vegada, cada mòdul es pot dividir en blocs més petits successivament.
Aquest sistema de desenvolupament s'anomena **programació modular** i permet que diferents
desenvolupadors treballin a la vegada en un mateix projecte, facilita la detecció i correció d'errors, 
i permet la reutilització de codi en diferents mòduls o en altres projectes.

Els mòduls poden ser creats pel mateix programador,
però també poden aprofitar-se mòduls creats per altres usuaris.

## Utilització de mòduls

### Importació: import

Cada mòdul està format per un conjunt d'entitats (funcions, variables, constants, classes i objectes) i s'identifica per un nom.
Per utilitzar un mòdul cal importar-lo amb la instrucció `import`, i una vegada importat podrem utilitzar totes les entitats que conté.
La manera com caldrà cridar les diferents entitats dependrà de com s'ha fet la importació.

La instrucció `import` s'ha de situar sempre abans d'utilitzar qualsevol entitat del mòdul, 
generalment totes les importacions necessàries se situen a la part superior del codi.
Si es vol importar més d'un mòdul pot fer-se a la mateixa instrucció separats per comes.
```python
import math, sys
```

Quan s'importa un mòdul d'aquesta manera totes les entitats que conté són accessibles però no s'afegeixen a l'espai de noms
per defecte del codi, per tant, caldrà cridar-los indicant sempre el nom del mòdul.
```python
import math
print(math.sin(math.pi/2))
```

### Entitats: from

Utilitzant la sentència `from ... import ...` podem especificar quines entitats volem importar d'un mòdul.
En aquest cas, les entitats s'afegeixen a l'espai de noms per defecte i no cal utilitzar el nom del mòdul per cridar-les.

```python
from math import pi, sin
print(sin(pi/2))
``` 

Utilitzant la sentència `from ... import *` importarem totes les entitats del mòdul i les afegirem a l'espai de noms per defecte.
Aquesta instrucció no és aconsellable perquè pot provocar conflictes de noms amb les variables o altres mòduls del codi.
```python
from math import *
print(sin(pi/2))
```

### Àlies: as

Una altra opció consisteix a substituir el nom del mòdul a tot el nostre codi utilitzant un àlies.
Per fer-ho cal indicar l'àlies del nou espai de noms amb la paraula `as`.
```python
import math as m
print(m.sin(m.pi/2))
```

La paraula clau `as` també permet modificar el nom de les entitats quan s'importen utilitzant `from`.
```python
from math import pi as P
from math import sin as sinus, cos as cosinus
print(sinus(P/2))
```

Sempre que s'utiltiza un àlies, el nom original esdevé inaccessible i no s'ha d'utilitzar.

### Llistat d'entitats: dir

La funció `dir()` mostra un llistat alfabètic de totes les entitats contingudes en un mòdul.
Per poder utilitzar-la cal que el mòdul s'hagi importat completament.
```python
import math
for name in dir(math):
    print(name, end=" ")
# __doc__ __file__ __loader__ ...
```

## Creació de mòduls

### Variable \_\_name\_\_

Quan importem un mòdul, Python realitza diverses accions:

* s'executa tot el seu codi
* es crea un fitxer PYC amb el codi del mòdul compilat
* es crea una variable anomenada `__name__` que pot prendre dos valors:
    - `__main__` quan s'executa el mòdul directament val 
    - el nom del mòdul quan s'executa en ser importat per un altre codi

Per exemple, si creem aquests dos fitxers en una mateixa carpeta:

**modul.py**
```python
print("__name__")
```

**main.py**
```python
import modul
```
En executar *modul.py* obtindrem `__main__`.
En canvi, en executar *main.py* obtindrem `modul`; a més, es crearà una carpeta `__pycache__` amb un fitxer `modul.cpython-36.pyc`
que contindrà el codi de *modul.py* compilat.

A l'hora de crear un mòdul, per tal de tenir en compte en quin context s'està executant, utilitzarem l'estructura següent:
```python
if __name__ == "__main__":
    # Codi per inicialitzar el mòdul o realitzar tests
```

### Variables privades

A diferència d'altres llenguatges de programació, Python no permet ocultar les variables als usuaris d'un mòdul.
Per aquest motiu, les variables envoltades per '__' només s'han de llegir però no s'han de modificar.
Aquesta notació és només una convenció, però no impedeix que aquestes variables es modifiquin.

### Estructura del mòdul

L'estructura general d'un mòdul és:

* *shabang*: `#!/usr/bin/env python3` - indica al sistema operatiu com ha d'executar el fitxer (per Python és només un comentari)
* *doc-string*: ```""" descripció del mòdul """"``` - explicació de l'objectiu i contingut del mòdul
* definicions - definició de les entitats del mòdul (variables, constants, funcions, classes...)
* inicialització: `if __name__ == "__main__":` -  codi per proves o per inicialitzar el mòdul

### Variable path

Quan el fitxer principal i el mòdul a importar es trobin en carpetes diferents utilitzarem la variable `path`.
Aquesta variable conté una llista amb totes les ubicacions on es buscarà el mòdul.
Python cercarà el mòdul a totes les carpetes de la llista i utilitzarà el primer que trobi que coincideixi amb el nom sol·licitat;
si no en troba cap, la importació fallarà.

La variable `path` forma part del mòdul `sys`, per tant la importarem utilitzant `from sys import path`.
A continuació, afegirem la ruta a la llista la carpeta on es troba el mòdul utilitzant el mètode `append()`.
La doble barra inversa és necessària per escapar aquest caràcter.

```python
from sys import path
path.append("..\\moduls")
import modul
```

## Paquets

Els paquets permeten agrupar mòduls semblants o relacionats en una estructura jeràrquica de carpetes i subcarpetes.

Per crear un paquet només cal:
 
* Crear un directori que contingui tots els mòduls que en formen part
* Afegir un fitxer anomenat `__init__.py` que s'encarregarà d'inicialitzar el paquet.
Aquest fitxer només cal situar-lo a al directori arrel de tota l'estructura de carpetes i pot deixar-se en blanc.
S'executarà sempre que s'importi algun mòdul del paquet.

Per accedir a un mòdul concret de dins del paquet indicarem el nom de les carpetes separades per `.`.

```python
# Importació de tot el paquet
import paquet.subpaquet.modul
paquet.subpaquet.modul.funcio()

# Importació d'una funció
from paquet.subpaquet.modul import funcio
funcio()

# Utilitzacio d'un àlies
import paquet.subpaquet.modul as alias
alias.funcio()
```