# Entrada i sortida de dades

* [Entrada per teclat](#entrada-per-teclat)
* [Sortida per pantalla](#sortida-per-pantalla)

### Entrada per teclat

La funció `input()` té com a paràmetre d'entrada el text a mostrar i retorna la cadena de caràcters 
introduïda per l'usuari fins al salt de línia.
```python
nom = input("Com et dius?")
```

Aquesta funció pot utilitzar-se sense cap paràmetre d'entrada.
```python
x = input()
```

Per llegir un enter cal transformar la cadena amb `int()`.
```python
edat = int(input("Quants anys tens?"))
```

## Sortida per pantalla

**Cadenes de text**

La funció `print()` mostra el contingut per pantalla.
```python
print("El meu nom és Víctor")  # El meu nom és Víctor
```

Aquesta funció admet tants paràmetres com necessitem, separats per comes.
Cada valor s'imprimirà separat per un espai en blanc (per defecte).
```python
print("El","meu","nom","és","Víctor")    # El meu nom és Víctor
```

Podem personalitzar el separador amb el paràmetre `sep`.
```python
print("El","meu","nom","és","Víctor", sep="-")    # El-meu-nom-és-Víctor
```

Si no indiquem cap paràmetre s'imprimirà un salt de línia.
Això succeeix perquè al final del text sempre s'afegeix un salt de línia (per defecte).
Podem modificar aquest valor amb el paràmetre `end`.
```python
print("El meu nom", end=" ")
print("és Víctor")
# El meu nom és Víctor
```

**Caràcter d'escapada**

Si volem imprimir caràcters especials podem utilitzar `\`.

* `\n` - salt de línia
* `\t` - tabulador
* `\"` - cometa doble
* `\\` - barra inversa

**Variables**

La funció `print` també permet mostrar el valor d'una variable.
```python
nom = "Víctor"
print("El meu nom és " + nom)   # El meu nom és Víctor
print("El meu nom és", nom)     # El meu nom és Víctor
```

Si la variable no és de tipus `string` també pot imprimir-se directament.
```python
resultat = 12
print("El resultat és", resultat)
```

Si volem imprimir un nombre concatenat amb una cadena de text caldrà convertir-lo a `string` amb la funció `str()`.
```python
resultat = 12
print("El resultat és " + str(resultat))
```

Si la variable és un array es mostraran tots els valors que conté, sense necessitat d'iterar-los.
```python
x = [1,2,3,4,5]
print(x)    # [1,2,3,4,5]
```

**Sortida amb format**

La sortida amb format permet personalitzar la manera com es mostra el valor d'una variable.
Per utilitzar-la cal indicar el lloc on es vol mostrar el valor de la variable a la cadena de text a través 
dels caràcters següents:

* `%s` - cadena de text
* `%d` - nombre enter
* `%f` - nombre real
* `%o` - nombre en octal
* `%x` - nombre en hexadecimal

A més, al final de la cadena de text cal indicar `%` i totes les variables que contenen els valors (entre parèntesis i 
separades per comes).
```python
nom = "Pau"
edat = 8
print("Em dic %s i tinc %d anys"%(nom, edat))   # Em dic Pau i tinc 8 anys
```

En variables numèriques, la manera com es representen els nombres es pot personalitzar de la següent manera:

* `%0nd` - enter de longitud `n` omplint de zeros a l'esquerra
* `%n.df` - nombre real amb `n` valors enters i `d` decimals

```python
print("El resultat és %04d", 12)    # 0012
pi = 3.141592
print("El resultat és %1.4f"%pi)    # 3.1416
```





