# Tipus de dades

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

### Conversió de tipus

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

## Variables

Per crear una variable només cal assignar-li un valor amb l'operador `=`.
El nom de la variable ha de desriure el seu contingut i només pot contenir lletres, nombres i '_'; a més,
no pot començar amb un nombre i diferencia majúscules de minúscules.
```python
text = "cadena de text"
nombre_enter = 15
nombre_decimal = 5.7
binari = True
```

El nom de la variable tampoc no pot utilitzar les paraules reservades `False`, `True`, `None`, `and`, `del`,
`from`, `not`, `while`, `as`, `elif`, `global`, `or`, `with`, `assert`, `else`, `if`, `pass`, `yield`, `break`, 
`except`, `import`, `print`, `class`, `exec`, `in`, `raise`, `continue`, `finally`, `is`, `return`, `def`, `for`,
`lambda` i `try`.

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
