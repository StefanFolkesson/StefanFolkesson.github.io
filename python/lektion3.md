
# L3: Gissa spel
Jag tänkte göra ett enklare gissa mitt tal i python där användaren ska gissa ett tal mellan 1 och 100. Om användaren gissar rätt ska programmet skriva ut att användaren gissade rätt och hur många försök det tog. Om användaren gissar fel ska programmet skriva ut om användaren gissade för högt eller för lågt. Programmet ska även skriva ut om användaren gissade utanför intervallet 1-100. Programmet ska även skriva ut om användaren skriver in något annat än ett heltal. För att göra det enklare att spela ska programmet skriva ut om användaren gissade väldigt nära det rätta talet.
## Steg 1
Vi börjar med att få programmet att slumpa fram ett tal mellan 1 och 100. Vi kan använda oss av random.randint() funktionen för att göra detta.
```python
import random
rätt_tal = random.randint(1, 100)
```
## Steg 2
Nästa steg är att få programmet att fråga användaren efter ett tal och sedan jämföra användarens gissning med det rätta talet.
```python
import random
rätt_tal = random.randint(1, 100)
gissning = input("Gissa ett tal mellan 1 och 100: ")

if gissning == rätt_tal:
    print("Grattis! Du gissade rätt.")
else:
    print("Tyvärr, du gissade fel.")
```
## Steg 3
Vi behöver nu lägga till en loop så att användaren kan fortsätta gissa tills hen gissar rätt.
Då använder vi en variabel som innehåller antal försök
```python
import random
rätt_tal = random.randint(1, 100)
försök = 0
gissning = None

while gissning != rätt_tal:
    gissning = input("Gissa ett tal mellan 1 och 100: ")

    försök += 1
    if gissning == rätt_tal:
        print(f"Grattis! Du gissade rätt på {försök} försök.")
    else:
        print("Tyvärr, du gissade fel.")
```
## Steg 4
Vi behöver nu lägga till en kontroll så att användaren inte kan gissa utanför intervallet 1-100.
```python
import random
rätt_tal = random.randint(1, 100)
försök = 0
gissning = None

while gissning != rätt_tal:
    gissning = input("Gissa ett tal mellan 1 och 100: ")

    try:
        gissning = int(gissning)
    except ValueError:
        print("Du måste skriva in ett heltal.")
        continue

    if gissning < 1 or gissning > 100:
        print("Du måste gissa ett tal mellan 1 och 100.")
        continue   

    försök += 1

    if gissning == rätt_tal:
        print(f"Grattis! Du gissade rätt på {försök} försök.")
    else:
        print("Tyvärr, du gissade fel.")
```
## Steg 5
Nu skall vi ge respons om användaren gissade för högt eller för lågt.
```python
import random

rätt_tal = random.randint(1, 100)
försök = 0
gissning = None

while gissning != rätt_tal:
    gissning = input("Gissa ett tal mellan 1 och 100: ")

    try:
        gissning = int(gissning)
    except ValueError:
        print("Du måste skriva in ett heltal.")
        continue

    if gissning < 1 or gissning > 100:
        print("Du måste gissa ett tal mellan 1 och 100.")
        continue

    försök += 1

    if gissning == rätt_tal:
        print(f"Grattis! Du gissade rätt på {försök} försök.")
    elif abs(gissning - rätt_tal) < 5:
        print("Du gissade väldigt nära det rätta talet.")
    elif gissning < rätt_tal:
        print("Du gissade för lågt.")
    else:
        print("Du gissade för högt.")
```
## Exempel på körning
```
Gissa ett tal mellan 1 och 100: 50
Du gissade för högt.
Gissa ett tal mellan 1 och 100: 25
Du gissade för lågt.
Gissa ett tal mellan 1 och 100: 35
Du gissade väldigt nära det rätta talet.
Gissa ett tal mellan 1 och 100: 30
Grattis! Du gissade rätt på 4 försök.
```
</body>
</html>