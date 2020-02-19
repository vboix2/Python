# Numpy

### Introducció

Numpy és una llibreria que proporciona eines per a treballar amb array multidimensionals.

NumPy permet escriure operacions vectorials amb molt poc codi, de manera molt concisa, fàcil de llegir i amb una notació semblant a la de les matemàtiques.
També proporciona un codi molt més eficient perquè utilitza llibreries precompilades en C.

Per utilitzar NumPy cal importar la llibreria a l'inici del codi, generalment s'utilitza l'abreviatura `np`.
```python
import numpy as np
```

### Objectes ndarray

L'objecte bàsic de Numpy, anomenat `ndarray`, és una llista multidimensional de nombres del mateix tipus.
Aquests objectes, a diferència dels arrays convencionals: 

* tenen mida fixa, no poden créixer dinàmicament
* han de contenir objectes del mateix tipus
* realitzen les operacions de manera molt més eficient

Els atributs d'un objecte `ndarray` són:

* **ndarray.ndim** -  dimensions (eixos)
* **ndarray.shape** -  longitud de cada dimensió
* **ndarray.size** -  nombre total d'elements
* **ndarray.dtype** - tipus de dades

Les assignacions i les funcions no copien els arrays, els passen per referència.

### Creació d'arrays

* **np.array([...])** - permet construir un ndarray a partir d'un array de python.
```python
np.array([1,2,3])
np.array([1,2,3], dtype=float)  # especificant el tipus de dades
```

* **np.zeros(n)** - genera un array de zeros de la mida especificada
```python
np.zeros(2)
# [0 0]
np.zeros((2,2))
# [[0 0],
# [0 0]]
```


* **np.ones(n)** - genera un array d'uns de la mida especificada
```python
np.ones(3)
# [1 1 1]
np.ones((2,3))
# [[1 1 1],
# [1 1 1]]
```

* **np.diag(valor, k)** - crea una matriu diagonal de mida k i valor especificat
```python
np.diag(1,2)
# [[1 0],
#  [0 2]]
```

* **np.eye(n)** - crea una matriu identitat n x n
```python
np.eye(3)
# [[1 0 0],
#  [0 1 0]
#  [0 0 1]]
```

* **np.arange(inici,final,pas=1)** - permet construir un array de nombres seqüencials
```python
np.arange(1,6)  # [1 2 3 4 5]
np.arange(0,10,2)  # [0 2 4 6 8]
```

* **np.linspace(inici,final,n_elements)** - genera un array de nombres seqüencials
```python
np.linspace(1, 2, 5)  # [1 1.25 1.5 1.75 2]
np.linspace(1, 2, 4, endpoint=False)  # [1 1.25 1.5 1.75] interval obert
```

* **np.random.random(dim)** - crea una matriu de nombres aleatoris
```python
np.random.random((2,2))  # matriu 2x2 de nombres aleatoris entre 0 i 1
```

### Operacions

Les operacions aritmètiques s'apliquen element per element:

* entre dos arrays s'operen els valors d'índexs iguals
* entre un array i un nombre s'opera el valor sobre tots els índexs de l'array

En tots dos casos s'obté un aray de la mateixa mida amb tots els resultats.
Quan s'operen arrays de diferents tipus de dades s'obté un array amb el tipus de dades més precís. 

Operacions unàries

* **sum()** - suma tots els valors de l'array
```python
a = np.array([2,8,5,3,6])
a.sum()     # 24
```
* **prod()** - producte de tots els valors de l'array `a.prod()`
* **max()** - valor màxim de l'array `a.max()`
* **min()** - valor mínim de l'array `a.min()`

Cal tenir en compte que el producte de dues matrius també es realitza element per element.
Si es vol calcular el producte matemàtic de matrius s'ha de fer amb el mètode `dot`.

```python
# producte de matrius a * b
a.dot(b)
np.dot(a,b)
```

### Comparació

La comparació de dos arrays `a == b` crea un nou array de tipus boolean que indica el resultat de comparar els valors element per element.

Per comparar dos arrays cal utilitzar el mètode `array_equal`.
```python
# comparació de dos arrays
np.array_equal(a,b) 
```

### Manipulació d'arrays

* **reshape(n.m)** - dóna forma a una llista especificant les dimensions
```python
a = np.array([1,2,3,4,])
a.reshape(2,2)
# [[1 2],
#  [3,4]]
```

* **ravel()** - aplana un array a una sola dimensió
```python
a = np.ones(2,2)
a.ravel()
# [1 1 1 1]
```

* **copy()** - fa una còpia de l'array
```python
d = a.copy()
```

* **np.vstack((a,b))** - apila verticalment
```python
a = np.ones(2)
b = np.zeros(2)
np.vstack((a,b))
# [[1., 1.],
# [0., 0.]])
```

* **np.hstack((a,b))** - apila horitzontalment
```python
a = np.ones(2)
b = np.zeros(2)
np.hstack((a,b))
# [1., 1., 0., 0.]
```

### Slicing

La tècnica del slicing permet accedir a una part dels valors d'un array utilitzant la sintaxi `a[inici:final]`.

```python
a = np.arange(6)
# [0 1 2 3 4 5]
a[2:5]  # elements 2-4
a[2:]  # elements 2-5
a[:-2]  # elements fins al penúltim
```

En arrays multidimensionals utilitzem `a[i:f, i:f]`.

També es pot indicar un valor per al pas `a[inici:final:pas]`.

```python
a[::-1]  # elements en ordre invers
a[::2]  # elements parells
```

### Iteració

Podem iterar sobre:

* els valors d'un array: `for i in vector:`
* les files d'una matriu: `for row in matriu:`
* tots els elements de l'array: `for i in array.flat:`

### Ordenació

El mètode `sort` permet ordenar un array. Els seus paràmetres són:

* axis - eix en què s'ordenen els valors (0 columnes, 1 files, None ordenació aplanada)
* kind - algorisme d'ordenació
* order - llista de strings per a l'ordenació

```python
np.sort(m, axis=1)  # ordenació d'un matriu per files
```

### Funcions matemàtiques

Poden aplicar-se sobre un nombre o sobre tots els valors d'un array. Retornen un array:

* **np.add(a, x)** - suma
* **np.exp(a)** - exponencial
* **np.sqrt(a)** - arrel quadrada
* **np.sin(a)** - sinus
* **np.cos(a)** - cosinus

Funcions d'estadística descriptiva. S'apliquen sobre un array i retornen un únic valor:

* **np.average(a)** - mitjana
* **np.median(a)** - mediana
* **np.std(a)** - desviació estàndard


### Àlgebra linial

* **T** o **transpose()** - transposició d'una matriu o vector
```python
a = np.arange(6).reshape((2,3))
a.T
a.transpose()
```
* **np.inv(a)** - inversa d'una matriu
* **np.linalg.solve(A,y)** - resol el sistema d'equacions
* **np.linalg.det(A)** - calcula el determinant d'una matriu

## Referències

* [Documentació de NumPy](https://numpy.org/devdocs/reference/index.html)
