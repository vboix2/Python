# Accés a fitxers

### Introducció

Per processar dades o guardar els resultats d'un programa de manera persistent necessitem accedir a fitxers del sistema operatiu.
La ruta d'un fitxer varia segons el sistema operatiu que s'utilitzi;
en Windows tenen aquest aspecte `C:\directori\fitxer`, mentre que en Linux tenim `/directori/fitxer`.
La diferència en el separador de directoris és important perquè `\` és el caràcter d'escapada en Python i, per tant, les
rutes en Windows s'hauran d'escriure com a `C:\\directori\\fitxer`.

Els llenguatges de programació no es comuniquen directament amb els fitxers del sistema operatiu, 
sinó que ho fan a través d'un flux de dades o `stream`.
Això vol dir que abans de realitzar qualsevol lectura o escriptura cal connectar el flux de dades amb el fitxer (obrir el fitxer),
i un cop finalitzades les operacions desconnectar-lo (tancar el fitxer).
El flux de dades permet dues operacions: llegir dades del fitxer i escriure dades al fitxer.
Això vol dir que tindrem tres modes d'operació amb un `stream`:

* `read` - només permet operacions de lectura
* `write` - només permet operacions d'escriptura
* `update` - permet operacions de lectura i escriptura

### Obrir i tancar fitxers

El mètode `open()` obre un fitxer del sistema operatiu i crea un stream que representa a aquest fitxer al programa.
El primer paràmetre indica el nom del fitxer associat a l'stream i el segon paràmetre (`mode`) indica el mode d'operació.
```python
stream = open(file, mode='r')
```

Els modes d'operació són:

* read: `r` - el fitxer associat ha d'existir i tenir permisos de lectura.
* write: `w` - si el fitxer no existeix es crearà i si existeix se sobreescriurà
* append: `a` - si el fitxer no existeix es crearà i si existeix s'escriurà al final del seu contingut
* read and update: `r+` - el fitxer ha d'existir i tenir permisos d'escriptura. L'stream podrà llegir i escriure.
* write and update: `w+` - i el fitxer no existeix es crearà i si existeix s'escriurà al final. L'stream podrà llegir i escriure.

A més, la lletra `b` indica que el fitxer s'obrirà en **mode binari** i la lletra `t` en **mode text**. 

Per tancar el fitxer utilitzem el mètode `close()`.

```python
try:
    stream = open("C:/users/user/Desktop/file.txt", "rt")
    # Processament de dades
    stream.close()
except Exception as exc:
    print("open failed", exc)
```

### Mòdul sys

Tots els programes disposen de tres fluxos de dades oberts el moment d'executar-los:

* `stdin` - Associat al teclat. S'hi accedeix amb el mètode `input()` que llegeix dades del teclat.
* `stdout` - Associat a la pantalla. S'hi accedeix amb el mètode `print()` que escriu dades per pantalla.
* `stderr` - Associat a la pantalla i destinat a enviar missatges d'error.

Si es volen utilitzar cal importar el mòdul `sys`.
```python
import sys
```

### Errors

Quan un stream de dades produeix un error llença una excepció de tipus `IOError`.
Aquesta excepció disposa d'un atribut `errno` que proporciona més informació sobre aquest error.
Els seus possible valor estan representats per diferents constants del mòdul `errno`.

* `errno.EACCESS` - Permission denied
* `errno.EBADF` - Bad file number
* `errno.EEXIST` - File exists
* `errno.EFBIG` - File too large
* `errno.EISDIR` - Is a directory
* `errno.EMFILE` - Too many open files
* `errno.ENOENT` - No such file or directory 
* `errno.ENOSPC` - No space left on device

```python
import errno

try:
    stream = open("C:/directory/file.txt", "rt")
    stream.close()
except Exception as exc:
    if exc.errno == errno.ENOENT:
        print("The file doesn't exist")
    elif exc.errno == errno.EMFILE:
        print("You've opened too many file")
    else:
        print("Error number", exc.errno)
```

Aquest codi es pot simplificar amb la funció `strerror`, que indica el missatge d'error a partir del seu codi.
```python
from os import strerror

try:
    stream = open("C:/directory/file.txt", "rt")
    stream.close()
except Exception as exc:
    print("File could not be opened: ", strerror(exc.errno))
```

### Lectura de fitxers de text

El mètode més senzill per llegir fitxers de text és `read()`.
Permet llegir del fitxer el nombre de caràcters especificat i tornar una cadena de text.
Quan ja no queda text per llegir retorna una cadena buida.
```python
from os import strerror

try:
    s = open("file.txt", "rt")
    ch = s.read(1)
    while ch!="":
        print(ch, end="")
        s.read(1)
    s.close()
except IOError as e:
    print("I/O error: ", strerror(e.errno))
```

Si es coneix la mida del fitxer, pot llegir-se tot de cop invocant al mètode `read()` sense cap paràmetre d'entrada.
```python
from os import strerror

try:
    s = open("file.txt", "rt")
    content = s.read()
    for ch in content:
        print(ch, end="")
    s.close()
except IOError as e:
    print("I/O error: ", strerror(e.errno))
```

Altres mètodes per llegir dades d'un fitxer de text:

* `readline()` - Permet llegir fins al següent salt de línia. 
Torna una cadena buida quan s'ha arribat al final del fitxer.
* `readlines()` - Llegeix tot el contingut del fitxer i retorna una llista de cadenes de text separades per un salt de línia.

El mètode `open()` també pot tractar-se com a un iterador.
```python
from os import strerror

try:
    for line in open("file.txt", "rt"):
        print(line)
except IOError as e:
    print("I/O error: ", strerror(e.errno))
```

### Escriptura de fitxers de text

Per escriure dades en un fitxer de text disposem del mètode `write()`.
Aquest mètode té un únic paràmetre d'entrada: el text que cal escriure al fitxer.

```python
from os import strerror

try:
    fo = open("file.txt", "wt")
    for i in range(10):
        fo.write("line #" + str(i+1) + "\n")
    fo.close()
except IOError as e:
    print("I/O error", strerror(e.errno))
```

### Lectura i escriptura de fitxers binaris

La funció `bytearray()` crea un objecte que permet emmagatzemar dades en binari.
El paràmetre d'entrada és un enter que indica el nombre de bytes que pot emmagatzemar.
Aquest objecte s'inicialitza amb tots els bytes a 0.
```python
data = bytearray(10)
```
Per escriure dades en un fitxer binari també utilitzem el mètode `write()`.

```python
from os import strerror

data = bytearray(10)
for i in range(len(data)):
    data[i] = 10 + i

try:
    bf = open("file.bin", "wb")
    bf.write(data)
    bf.close()
except IOError as e:
    print("I/O error", strerror(e.errno))
```

Per llegir dades d'un fitxer binari utilitzem el mètode `readinto()`.

```python
from os import strerror

data = bytearray(10)

try:
    bf = open("file.bin", "rb")
    bf.readinto(data)
    bf.close()
    
    for b in data:
        print(hex(b), end="")

except IOError as e:
    print("I/O error", strerror(e.errno))
```
