# Programació orientada a objectes

### Introducció

La orientació a objectes és un paradigma de programació basat en la encapsulació d'un grup de variables i funcions en una
estructura anomenada **classe**.
Aquesta estructura actua com un nou tipus de dades complexe i protegeix les dades de modificacions no volgudes.

Les variables declarades dins d'una classe s'anomenen **atributs** i s'interpreten com propietats de la classe.
Les funcions declarades dins d'una classe s'anomenen **mètodes** i actuen sobre les seves variables.
Quan definim uns valors concrets per a les variables d'una classe estem creant (instanciant) un objecte. 
La programació orientada a objectes permet crear tants objectes d'una classe com sigui necessari i tots compartiran 
la mateix estructura. A més, permet crear noves classes més específiques que heretin els atributs i mètodes de la classe
superior.


### Classes i objectes

La definició d'una **classe** comença amb la paraula `class` seguida del nom de la classe.
```python
class Classe:
    pass    # La instrucció pass no fa res
```

Per crear objectes d'una classe utilitzem una funció específica anomenada **constructor**.
El constructor s'ha d'anomenar `__init__` però s'invoca a través del nom de la classe.
Com a mínim, ha de tenir un paràmetre d'entrada (generalment anomenat `self`) que representa l'objecte creat.
Per crear un **objecte** assignem el resultat del constructor a una variable.

```python
# Definició de la classe
class Classe:
    def __init__(self):
        print("Objecte creat")

# Creació d'un objecte
objecte = Classe()
```

Atributs útils de les classes:

* `__name__` - conté el nom de la classe
* `__module__` - conté el nom del mòdul on s'ha declarat la classe
* `__dict__` - conté un diccionari amb el nom i el valor de tots els atributs d'un objecte
* `__bases__` - conté una llista amb el nom de les superclasses

Quan s'imprimeix un objecte es fa una crida al mètode `__str__()`. 
Si es vol modificar el resultat d'aquest mètode pot sobreescriure's definint novament el mètode a la classe.
```python
class Classe:
    def __init__(self, var):
        self.var = var
    def __str__(self):
        return "var: " + self.var
objecte = Classe(2)
print(objecte)      # var: 2
```

El mètode `isinstance()` avalua si un objecte és una instància d'una classe.

### Atributs

Els **atributs** o propietats són variables que s'emmagatzemen dins de l'objecte i es mantenen fins que s'elimini.
Per declarar, definir i accedir a un atribut s'ha d'indicar el nom de l'objecte (o `self` quan es fa dins de la classe), 
seguit d'un punt `.` i el nom de la variable.
```python
def Classe:
    def __init__(self):
        # Definició de l'atribut
        self.atribut = "valor"

objecte = Classe()

# Accés al valor de l'atribut
objecte.atribut
```

Quan un atribut té dues barres baixes davant del nom (`__nom`) esdevé **privat** i no pot ser accedit des de fora de la classe.
```python
class Classe:
    def __init__(self):
        self.__atribut_privat = "privat"
ob = Classe()
```

Tots els objectes tenen un atribut `__dict__` que conté un diccionari amb el nom i el valor de tots els atributs.
```python
objecte = Classe()
objecte.__dict__
```

Tipus d'atributs:

* Una **variable d'instància** és un atribut o propietat d'un objecte que es troba aïllada de la resta d'objectes.
* Una **variable de classe** és una propietat que existeix en un una sola còpia, val el mateix per a tots els objectes.
El seu valor s'emmagatzema fora de qualsevol objecte i existeix encara que no s'hagi creat cap objecte.
Per declarar una variable de classe cal assignar-li un valor fora de qualsevol mètode. 
Les variables de classe no apareixen al llistat de la variable `__dict__`.

```python
class Classe:
    # Variable de classe
    variable1 = 0
    def __init__(self, val=1):
        # Variable d'instància
        self.variable2 = val
objecte = Classe(2)
print(objecte.__dict__)     # {'variable2': 2}
print(objecte.variable1)    # 0
```

En Python, els atributs no cal declarar-los prèviament i, per tant, dos objectes d'una mateixa classe poden tenit atributs
diferents. Si intentem accedir a un atribut que no existeix es produirà una excepció `AttributeError`.
Per evitar-ho podem utilitzar una estructura `try-except` o bé el mètode `hasattr()`, que permet comprovar si un objecte
conté un atribut concret. 
Aquest mètode també permet comprovar l'existència de variables de classe.
```python
class Classe:
    c = 0
    def __init__(self, val):
        if val%2 == 0: self.a = val
        else: self.b = val
objecte = Classe(2)
if hasattr(objecte, 'b'):
    print (objecte.b)
hasattr(Classe, 'c')    # True
```


### Mètodes

Els **mètodes** són funcions que actuen sobre les propietats de l'objecte.
Per definir un mètode hem de definir una funció dins de la classe utilitzant `def`;
a més, cal que tots els mètodes tinguin com a mínim el paràmetre d'entrada `self` per poder accedir als atributs de la classe.
La resta de paràmetres d'entrada cal indicar-los després de `self`.
Per invocar un mètode utiltizem el nom de l'objecte i el nom del mètode separats per un punt.
```python
class Classe:
    # Declaració d'un mètode
    def metode(self):
        print("mètode")

objecte = Classe()

# Invocació del mètode
objecte.metode()
```

La paraula clau `self` dóna accés tant a l'objecte instanciat com a les variables de classe i també permet cridar 
altres mètodes dins de la classe.

Quan un mètode té dues barres baixes davant del nom (`__nom`) esdevé **privat** i no pot ser accedit des de fora de la classe.
```python
class Classe:
    def metode_public(self):
        print("públic")
    def __metode_privat(self):
        print("privat")
```

### Herència

L'herència permet crear noves classes aprofitant atributs i mètodes d'altres classes ja definides.
La classe que hereda ha d'indicar el nom de la seva superclasse entre parèntesis.
La subclasse pot definir nous atributs o mètodes, però també pot sobreescriure els heretats de la seva superclasse.
```python
class SuperClasse:
    def metode1:
        print("mètode 1")
    def metode2:
        print("mètode 2")
class SubClasse(SuperClasse):
    def metode2:
        print("mètode sobreescrit")

objecte1 = SuperClasse()
objecte1.metode1()  # mètode 1
objecte1.metode2()  # mètode 2

objecte2 = SubClasse()
objecte2.metode1()  # mètode 1
objecte2.metode2()  # mètode sobreescrit
```

Si utilitzem el nom de la superclasse dins de la subclasse podem accedir als seus mètodes i atributs.
La funció `super()` també ens permet accedir a la superclasse i sense necessitat de saber el seu nom.
```python
class SuperClasse:
    def __init__(self):
        print("objecte creat")
    def metode(self, var):
        print(var)

class SubClasse(SuperClasse):
    def __init__(self):
        SuperClasse.__init__()
    def metode(self, var):
        super().metode(var)

objecte = SubClasse()   # objecte creat
objecte.metode(2)       # 2
``` 

El mètode `issubclass()` permet saber si una classe hereta d'una altra.