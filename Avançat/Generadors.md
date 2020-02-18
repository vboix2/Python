# Iteradors, generadors i funcions lambda

* [Iteradors](#iteradors)
* [Generadors](#generadors)
* [Funcions lambda](#funcions-lambda)

## Iteradors

Un **iterador** és un objecte que s'ajusta al protocol que imposa el context de les sentències `for` i `in`.
Els iteradors han de disposar de dos mètodes:

* `__iter__()` - que retorna el propi objecte, s'invoca una sola vegada i és necessari per iniciar la iteració
* `__next__()` - que retorna el proper valor de la sèrie i serà invocat abans de passar a la següent iteració.
Si no hi ha més valors haurà de llençar l'excepció `StopIteration`.

```python
# Sèrie de Fibonacci
class Fib:
    def __init__(self, n):
        self.__n = n
        self.__i = 0
        self.__f1 = self.__f2 = 1
    
    def __iter__(self):
         return self

    def __next__(self):
        self.__i += 1
        if self.__i > self.__n:
            raise StopIteration
        if self.__i in [1,2]:
            return 1
        ret = self.__f1 + self.__f2
        self.__f1, self.__f2 = self.__f2, ret
        return ret

for i in Fib(10):
    print(i)
```

## Generadors

Un **generador** és un fragment de codi que permet produir sèries de valors i
controlar el procés d'iteració.

Una funció és invocada una sola vegada i retorna un únic valor ben definit; en canvi, un generador s'invoca, de manera implícita,
múltiples vegades i retorna una sèrie de valors. 

Un exemple de generador és la funció `range`.
```python
for i in range(5):
    print(i)
```

Una manera més senzilla de construir un iterador consisteix en utilitzar la sentència `yield`.
Un generador és una funció on hem substituït la sentència `return` per `yield`,
això permet invocar-la múltiples vegades a través d'un context `for-in`, de tal manera que, a cada invocació, 
les variables es guarden per a la propera iteració.
```python
def parells(n):
    for i in range(n):
        yield 2 * i

for v in parells(5):
    print(v)
```

Els generadors també poden utilitzar-se a les llistes per comprensió.
```python
llista = [x for x in parells(n)]
```

La funció `list()` permet crear una llista a partir de les diferents invocacions d'un generador.
```python
def Fib(n):
    p1 = p2 = 1
    for i in range(n):
        if i in [0,1]:
            yield 1
        else:
            r = p1 + p2
            p1, p2 = p2, r
            yield r

serie = list(Fib(10))
```

A més, podem utilitzar els valors del generador dins de l'operador `in`.
```python
for i in range(20):
    if i in Fib(20):
        print(i)
```

Una altra manera de crear un generador és utilitzant una **llista per comprensió** entre parèntesis.
```python
generador = (1 if x%2==0 else 0 for x in range(10))

for v in generador:
    print(v, end=" ")   # 1 0 1 0 1 0...
```

## Funcions lambda

Les funcions lambda permeten simplificar el codi i fer-lo més clar i senzill.
Una **funció lambda** és una funció sense nom, que es declara directament allà on es vol utilitzar;
tot i que també pot ser assignada a una variable.

La seva sintaxi és: `lambda` + paràmetres d'entrada + `:` + definició.
```python
lambda: 0
lambda x: x**2 + 1
lambda x,y: x + y
```

Generalment s'utilitzen en altres funcions que requereixen un funció com a paràmetre d'entrada.
D'aquesta manera, s'evita definir una funció que només caldrà utilitzar una vegada.
Per exemple, la funció `map()` requereix una funció i una llista i retorna un iterador amb el resultat d'aplicar
la funció a cada valor de la llista.
```python
llista1 = [x for x in range(5)]
llista2 = list(map(lambda x: x**2, llista1))    # [0, 1, 4, 9, 16]
```

