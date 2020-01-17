# Tipus de dades

* [Literals](#literals)
* [Operadors](#operadors)
* [Variables](#variables)
* [Comentaris](#comentaris)

## Literals

**Nombres enters**

Tots els enters (`int`) s'implementen amb el tipus `long` per defecte, que permet emmagatzemar nombres de qualsevol precisió.

```python
35  # enter long
```

També es poden especificar enters en octal ('0o') i en hexadecimal ('0x')
```python
0o43  # enter octal
0x23  # enter hexadecimal
```

**Nombres reals**

S'expressen amb el tipus `float` que utilitza 64 bits (equivalent al `double` de C).
Per representar un nombre real s'utilitza un punt.
El zero es pot ometre tant a l'esquerra (`.4`) com a la dreta del punt (`4.`).

```python
24.3        # real
0.2e-3      # notació científica
2.1 + 4.3j  # nombres complexos
```

**Booleans**

Només poden tenir dos valors: `True` o `False`.


**Cadenes de text**

Una cadena de text (`string`) pot indicar-se amb cometes simples o dobles, però sempre s'inicia i acaba amb el mateix caràcter.
```python
'text'
"text"
'I like "Monty Python"'
```

Tres cometes dobles permeten definir cadenes multilínia.
```python
cadena_multilinia = """cadena
que ocupa
vàries línes"""
``` 

Caràcters d'escapada:

* \n - salt de línia
* \t - tabulació
* \\" - cometes

Abans de la cadena de text podem especificar el tipus de codificació per al text.
```python
u"Cadena en unicode"
r"Cadena en text cru"  # Evita els caràcters d'escapada 
```

**None**

El literal `None` representa l'absència de valor.

**Conversió de tipus**

Disposem de diferents mètodes per avaluar o modificar el tipus de dades.

La funció `type()` indica el tipus de dades.
```python
type('text')
```

Funcions per a convertir tipus de dades:
```python
int("35")       # Converteix a tipus enter
float("4.6")    # Converteix a tipus float
str(25)         # Converteix a string
```

Codificació de caràcters:
```python
ord("a")    # Obté el codi ASCII
chr(55)     # Obté el caràcter del codi
```

## Operadors

**Signe**

Operadors unaris.
L'operador `+` manté el signe del nombre que té a la dreta, mentre que l'operador `-` el canvia.
```python
+ 5     # 5
- 5     # -5
- - 5   # 5
```

**Suma, resta i multiplicació**

Es representen amb els caràcters `+`, `-` i `*`.
Permeten operar nombres de tipus `int` i `float`.
Quan els dos nombres són enters el resultat és enter, però si un dels dos nombres és decimal el resultat serà decimal.
```python
2 + 5       # 7
2 + 5.      # 7.0
5.4 - 2.2   # 3.2
8 * 4       # 32
8. * 4      # 32.0
```

**Potència**

Es representa amb el signe `**`.
Quan els dos nombres són enters el resultat és enter, però si un dels dos nombres és decimal el resultat serà decimal.
Si hi ha més d'un operador s'avalua de dreta a esquerra.
```python
2 ** 3       # 8
2 ** 2 ** 3  # 256 (right-sided binding)
```
 

**Divisió decimal**

Es representa amb el signe `/`. Sempre dóna com a resultat un `float`.

```python
6 / 4   # 1.5 
```

**Divisió entera**

Es representa amb el signe `//`.
Si els dos valors són enters el resultat és enter, la divisió entera.
Si un valor és decimal retorna la divisió entera en tipus `float`.
```python
6 // 4      # 1
6. // 4     # 1.0
```

**Mòdul**

Es representa amb el signe `%` i retorna el residu de la divisió.
Quan hi ha més d'un operador s'avaluen d'esquerra a dreta.
```python
6 % 4       # 2
9 % 6 % 2   # 1 (left-sided binding)
```

**Prioritat dels operadors**

El parèntesi sempre té prioritat màxima.
Els operadors (de més a menys prioritat):

* Signe (+ - unari)
* Potència (**)
* multiplicació (*), divisió (/), divisió entera (//) i mòdul (%)
* suma (+) i resta (-)

**Operadors de text**

L'operador concatenació `+` s'aplica a dues cadenes de text i les uneix en un únic valor.
L'operador replicació `*` s'aplica a una cadena de text i un nombre enter, retorna la concatenació del text repetida tantes vegades com s'indiqui.

```python
"a" + "b"   # ab
"a" * 3     # aaa
```

**Operadors de bits**

Existeixen quatre operadors que permeten manipular bits d'informació (*bitwise operators*).

* `&` - conjunció (AND)
* `|` - disjunció (OR)
* `~` - negació (NOT)
* `^` - disjunció exclusiva (XOR)

Aquests operadors només poden treballar amb enters i actuen sobre cada bit de manera independent.
Això vol dir que el resultat de l'operació entre dos enters serà l'enter que correspon a la seqüència de bits obtinguda
en aplicar l'operador sobre cada parella de bits situats a la mateixa posició.

```python
i = 15  # 00000000000000000000000000001111
j = 22  # 00000000000000000000000000010110
i & j   # 00000000000000000000000000000110  (6)
i | j   # 00000000000000000000000000011111  (31)
~ i     # 11111111111111111111111111110000  (-16)
i ^ j   # 00000000000000000000000000011001  (25)
```

Una altra possible operació a nivell de bits és el desplaçament de bit (*shifting).
L'operador `>>` desplaça els bits a la dreta i `<<` desplaça els bits a l'esquerra.
```python
n = 8   # 000000000000000000000000000001000
n >> 1  # 000000000000000000000000000000100 (4)
n << 2  # 000000000000000000000000000100000 (32)
```

## Variables

Per crear una variable només cal assignar-li un valor amb l'operador `=`.

```python
text = "cadena de text"
nombre_enter = 15
nombre_decimal = 5.7
binari = True
```
El nom de la variable només pot contenir lletres majúscules, minúscules, nombres i '_', no pot començar amb un nombre i 
tampoc no pot utilitzar les paraules reservades `False`, `True`, `None`, `and`, `del`,
`from`, `not`, `while`, `as`, `elif`, `global`, `or`, `with`, `assert`, `else`, `if`, `pass`, `yield`, `break`, 
`except`, `import`, `print`, `class`, `exec`, `in`, `raise`, `continue`, `finally`, `is`, `return`, `def`, `for`,
`lambda` i `try`.

Podem fer múltiples assignacions en una sola línia.
```python
a,b,c = 'text', 15, True
``` 

També podem intercanviar el valor de dues variables en una sola línia.
```python
a = 1; b = 2;
a, b = b, a     # a = 2 i b = 1
```

L'assignació d'un valor a una variable pot fer-se a partir del valor anterior de la pròpia variable.
Per fer aquesta reassignació poden utilitzar-se els *shortcut operators*:
```python
x = 0
x += 2  # x = x + 2
x -= 2  # x = x - 2
x *= 2  # x = x * 2
x /= 2  # x = x / 2
x %= 2  # x = x % 2
x **= 2 # x = x ** 2
```

Els operadors de bits també admeten la representació abreviada: `&=`, `|=`, `~=` i `^=`.

Una variable només pot utilitzar-se dins del context on s'ha declarat.
Si volem utilitzar-la a qualsevol lloc del codi hem de declarar-la com a global utilitzant la paraula `global`.
```python
global c
c = 3e8
```

Podem declarar més d'una variable global separant-les per `,`.
```python
global a, b, c
```

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
