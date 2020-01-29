# Mòdul random

## Introducció

El mòdul `random` permet treballar amb nombres pseudoaleatoris,
que semblen aleatoris però són calculats a través d'un algorisme.
Això és així perquè un ordinador és una màquina determinística i no pot generar
nombres completament aleatoris.

Els nombres aleatoris es generen a partir d'un valor anomenat `seed`.
Aquest valor s'utilitza per generar tots els nombres aleatoris seguint un cicle molt llarg però finit.
El valor `seed` s'estableix aleatòriament durant la inicialització del programa a partir de l'hora actual,
però també es pot fixar per permetre la repetibilitat de determinats càlculs.

Per importar aquest mòdul utilitzem
```python
import random
```

## Decimals aleatoris

* `random()` - produeix un nombre aleatori dins de l'interval [0,1)

## seed

La funció `seed()` permet fixar el valor generador de nombre aleatoris.

```python
from random import random, seed
seed(0)
random()    # 0.8444218515250481
```

## Enters aleatoris

* `randrange(n)` - produeix un enter aleatori des de 0 fins a n-1 [0,n)
* `randrange(m,n)` - produeix un enter aleatori des de m fins n-1 [m,n)
* `randint(m,n)` - produeix un enter aleatori des de m fins a n [m,n]
* `randrange(m,n,s)` - produeix un enter aleatori des de m fins a n-1 amb un salt s, tria un nombre de la llista range(m,n,s)

## Enters sense reemplaçament

* `choice(seq)` - Tria un element de la llista de manera aleatòria
* `sample(seq, n)` - Crea una llista aleatòria de n elements a partir de l'especificada

```python
from random import choice, sample
lst = [1,2,3,4,5,6,7,8,9,10]
choice(lst)     # 7
sample(lst, 3)  # [1,5,8]
sample(lst, 10) # [7, 5, 8, 3, 9, 2, 6, 4, 1, 10]
```