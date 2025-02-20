1. **Hello World!**  
   Skriv ett program som skriver ut "Hello, World!" på skärmen.  
   *Mål: Bekanta dig med att köra ett enkelt Python-program och skriva ut text.*
   Exempelutskrift:
---
   Hello World!
---
2. **Enkel kalkylator**  
   Skriv ett program som frågar användaren efter två heltal. Programmet ska sedan beräkna och skriva ut:  
   - Summan  
   - Differensen  
   - Produkten  
   - Kvoten (se till att hantera division med noll)  
   *Mål: Träna på inmatning, konvertering av datatyper och grundläggande aritmetik.*
   Exempelutskrift:
---
   Mata in tal 1: `30`
   Mata in tal 2: `10`
   Summan är: 40
   Differensen är: 20
   Produkten är: 300
   Kvoten är: 3
---
3. **Temperaturomvandlare**  
   Skriv ett program som tar in en temperatur i Celsius från användaren, omvandlar den till Fahrenheit och skriver ut resultatet. Formeln är:  
   \[
   F = C \times \frac{9}{5} + 32
   \]  
   *Mål: Använd matematiska operationer och arbeta med flyttal.*
   Exempelutskrift:
---
Mata in ett tal i Celsius:`0`
Detta motsvarar:32^o^F
```
4. **Jämna och udda tal**  
   Skriv ett program som tar in ett heltal från användaren och avgör om talet är jämnt eller udda. Använd modulusoperatorn (%) för att lösa uppgiften.  
   *Mål: Förstå och använda villkorssatser (if/else).*
---
Mata in ett tal:`13`
13 är ett udda tal.
---
5. **Multiplikationstabell**  
   Skriv ett program som frågar användaren efter ett heltal och sedan skriver ut multiplikationstabellen för det talet, t.ex. från 1 till 10.  
   *Mål: Använd loopar (t.ex. for-loop) för att iterera genom en sekvens.*
---
Mata in ett tal:`6`
Multiplikationstabellen:
1 x 6 = 6
2 x 6 = 12
3 x 6 = 18
4 x 6 = 24
5 x 6 = 30
6 x 6 = 36
7 x 6 = 42
8 x 6 = 48
9 x 6 = 54
10 x 6 = 60
---
6. **Fibonacci-sekvensen**  
   Skriv ett program som tar in ett heltal n från användaren och genererar de första n talen i Fibonacci-sekvensen.  
   *Mål: Öva på loopar och variabelhantering genom att arbeta med en sekvens där varje tal beräknas utifrån de två föregående talen.*
---
Mata in ett tal:`7`
Fibonacci-sekvensens första 7 tal är:
1 1 2 3 5 8 13
---
7. **Fakultetsberäkning med rekursion**  
   Skriv en rekursiv funktion som beräknar fakulteten (n!) av ett givet tal n. Använd funktionen i ett program där användaren matar in ett tal.  
   *Mål: Förstå rekursion och funktioner i Python.*
---
Mata in ett tal:`7`
Fakulteten för 7! dvs(1*2*..*n-1*n)
Svar:5040
---
8. **Gissa talet**  
   Skriv ett program där datorn slumpmässigt väljer ett tal mellan 1 och 100. Användaren ska försöka gissa talet. Efter varje gissning ska programmet ge feedback om gissningen är för hög eller för låg och räkna antalet försök.  
   *Mål: Arbeta med slumpgenerering, loopar och villkorssatser.*
---
Gissa talet!
Gissa ett tal:`45`
Talet är för lågt.
Gissa ett tal:`60`
Talet är för lågt.
Gissa ett tal:`70`
Talet är lite för högt.
Gissa ett tal:`68`
Rätt gissning! Du gissade rätt på 4 gissningar. 
---
9. **Lista och sortering**  
   Skriv ett program som ber användaren mata in en rad med tal (separerade med mellanslag). Konvertera inmatningen till en lista med heltal, sortera listan i stigande ordning och skriv ut den sorterade listan.  
   *Mål: Hantera strängar, listor och inbyggda funktioner för sortering.*
---
Mata in flera tal med mellanslag mellan:`3 4 32 5 1`
Den sorterande ordningen är: 1 3 4 5 32
---
10. **Ordfrekvensanalys**  
    Skriv ett program som läser in en text från en fil. Programmet ska räkna antalet förekomster av varje ord och sedan skriva ut de fem vanligaste orden tillsammans med deras frekvens.  
    *Mål: Arbeta med filhantering, ordbibliotek (dictionaries) och strängmanipulation.*
---
Skriv in filens namn:`text.txt`
I filen text.txt
antal ord: 445
Vanligaste orden är:
är: 10
jag: 5
kan: 3
vill: 3
har: 2
---