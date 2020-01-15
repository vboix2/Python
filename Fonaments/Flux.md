# Flux de control

## Estructura seqüencial

Les instruccions se separen sempre amb un salt de línia.
Excepcionalment, poden posar-se dues instruccions en una mateixa línia separades per `;`.
```python
a = 1       # instrucció 1
b = 2       # instrucció 2
c = a + b   # instrucció 3
```
```python
a = 1; b = 2 # instruccions 1 i 2
c = a + b    # instrucció 3
```
L'agrupament d'instruccions es realitza amb la identació; això vol dir que les instruccions s'agrupen en funció de la seva
separació amb el marge esquerra.

## Comparadors

Permeten avaluar si una expressió és certa (`True`) o falsa (`False`).
Són els següents:

* Igual: `==`
* Diferent: `!=`
* Més gran que: `>`
* Més petit que `<`
* Més gran o igual que: `>=`
* Més petit o igual que: `<=`

Els operadors sempre tenen prioritat per sobre dels comparadors.

Per construir comparacions més complexes utilitzem els **operadors lògics** `and`, `or` i `not`.
```python
a = 4; b = 5; c = 6
a < b and b < c
c > b or a ==c
not a != b
```


## Condicionals: if, elif, else

Podem condicionar l'execució d'una instrucció al resultat d'una comparació utilitzant la paraula `if`.

```python
a = 5; b = 3
if a > b:
    # instruccions condicionades
    print("'a' és més gran que 'b'")
```

En cas que no es cumpleixi la condició podem afegir una instrucció alternativa amb la paraula `else`.

```python
a = 5; b = 3
if a > b:
    print("'a' és més gran que 'b'")
else:
    # instruccions alternatives
    print("'a' no és més gran que 'b'")
```

També podem afegir noves condicions que s'avaluaran en el cas que no es cumpleixi la primera.
Per fer-ho utilitzem la paraula `elif`.

```python
a = 5; b = 3
if a > b:
    print("'a' és més gran que 'b'")
elif a==b:
    # codi per a la nova condició
    print("'a' és igual que 'b'")
else:
    print("'a' és més petit que 'b'")
```

Quan els condicionals només inclouen una instrucció poden situar-se en una mateixa línia.
```python
a = 5; b = 3
if a > b: print("'a' és més gran que 'b'")
elif a==b: print("'a' és igual que 'b'")
else: print("'a' és més petit que 'b'")
```

La sentència switch no existeix en Python, s'implementa amb un diccionari.

## Repetició condicionada: while

Aquest tipus d'expressions també avaluen una condició, però repeteixen totes les instruccions que es troben al seu interior mentre es cumpleixi la condició. 
Per construir-les utilitzem la paraula `while`.
```python
i = 10
while i >= 0:
    print(i)
    i -= 1 
```

També pot construir-se una repetició infinita i sortir-ne amb la paraula `break` quan ens interessi.
```python
i = 0
while True:
    # instruccions
    i += 1
    if i == 10: break
```

La paraula `continue` també ens permet abandonar la iteració, però en aquest cas es tornarà a avaluar la condició i es 
tornaran a repetir les instruccions si el resultat és cert. 

```python
i = 0
while True:
    # instruccions
    i += 1
    if i == 5: continue
    print(i)
```

Finalment, podem afegir instruccions alternatives utilitzant `else`, que s'executaran únicament quan deixi de cumplir-se 
la condició inicial però no quan se surti amb `break`.
```python
i = 10
while i >= 0:
    print(i)
    i -= 1
else:
    print("else",i)
```

## Repetició controlada: for

Aquesta expressió permet repetir un conjunt d'instruccions per a tots els valors possibles d'una variable de control.

La sintaxi a utilitzar és: `for` + variable de control + `in` + iterador + `:`.

Podem iterar sobre els valors d'una llista:
```python
for i in (2,4,6,8):
    print(i)
```

També podem iterar sobre valors generats amb la funció `range()`.
Els seus paràmetres d'entrada són: (valor inicial,) valor final (i increment).
Cal tenir en compte que el valor final queda exclòs.
```python
range(5)        # (1,2,3,4)
range(5,10)     # (5,6,7,8,9)
range(5,0,-1)   # (5,4,3,2,1)
```

```python
for i in range(10):
    print(i)
```

Les paraules `break` i `continue` també ens permeten sortir de la repetició o passar a la següent iteració.

De la mateixa manera, la repetició controlada també disposa de la paraula `else`.


