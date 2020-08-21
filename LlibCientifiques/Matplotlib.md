# Matplotlib

### Introducció

Matplotlib és una llibreria que permet generar gràfiques a partir d'arrays.
Està escrita en Python, però utilitza `Numpy` i altres extensions per aconseguir gran eficiència en arrays grans.

Els seu codi es divideix en tres parts: pylab, matplotlib API i backends.
Pylab és la interfície que permet crear gràfiques amb un codi i funcionament semblants al de Matlab.

Importació
```python
import matplotlib                   # inicialitzem matplotlib
import numpy as np                  # importem Numpy
import matplotlib.pyplot as plt     # Importem la llibreria
```

En Jupyter, la instrucció `%matplotlib inline` permet que les gràfiques es representin al mateix notebook.

**Representació bàsica**

* `plt.plot(x,y)` - representa els punts formats pels arrays x i y
* `plt.plot(x)` - representa els punts formats per l'índex i l'array x
* `plt.show()` - mostra la gràfica

**Format de presentació**

Color i tipus de línia o punt

* `plt.plot(x,y, color="blue", linewidth=2.5, linestyle="-")`

Eixos

* `plt.xlim(x_min, x_max)` - límits per a l'eix x
* `plt.ylim(y.min()*1.1, y.max()*1.1)` - límits per a l'eix y
* `plt.xticks([p1,p2,p3])` - punts a indicar a l'eix x
* `plt.xticks([p1,p2,p3], ["A","B","C"])` - etiquetes per als punts de l'eix x
* `plt.xlabel('nom')` - nom per a l'eix x
* `plt.grid(True)` - reixeta

Llegenda

```python
plt.plot(x,y,color="blue",label="A")
plt.legend(loc="upper left")
```

Text

* `plt.title(u'Text en unicode')` - Títol
* `plt.text(x,y,"Text")` - Text a la posició x,y
* `plt.text(x,y,r"$\pi$"")` - Text amb una expressió LaTex
* `plt.annotate("Text",xy=(x,y), xytext=(x,y))` - text a la posició xytext amb una fletxa apuntant a xy

**Múltiples gràfiques**

Una figura és una finestra que pot contenir una o més gràfiques.
Podem especificar-ne la mida, color, resolució...

`plt.figure(num, figsize=(a,b))`

* num - número de figura
* figsize - mida en polsades (amplada, alçada)
* dpi - resolució (punt per polsada)
* facecolor - color de fons
* edgecolor - color dels marges

En una mateixa figura podem posar vàries subgràfiques

`plt.subplot(files, columnes, número)`

````python
plt.figure(1)
plt.subplot(211)
plt.plot(...)
plt.subplot(212)
plt.plot(...)
````

**Representacions**

Histograma: Distribució de freqüències basada en un diagrama de barres.

`plt.hist(x)` 

* x - array de valors
* bins - nombre de columnes
* normed - normalització [0,1]
* facecolor - color
* alpha - transparència


**Representació 3D**

L'eina `mplot3D` permet fer representacions en 3D

````python
# Importació
from mpl_toolkits.mplot3d import Axes3D

# Generem una finestra 3D
fig = plt.figure()
ax = fig.gca(projection="3d")

# Punts en 3D
ax.scatter(x,y,z)

# Línia en 3D
ax.plot(x,y,z)  # vectors formats pels valors dels punts que formen la línia

# Superfície 3D
x,y = np.meshgrid(x,y) # valors en forma de matrius bidimensionals
z = np.cos(x) - np.sin(y)
ax.plot_surface(x,y,z)
````