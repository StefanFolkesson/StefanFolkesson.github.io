
### Uppgift 1: Räkna upp talen
**Beskrivning:** Skriv ett program som frågar användaren efter ett tal. Programmet ska sedan skriva ut alla tal från 1 upp till det givna talet.

#### Lösning:
1. **Input:** Be användaren skriva in ett tal.
   ```python
   antal = int(input("Ange ett tal: "))
   ```

2. **Iteration:** Använd en `for`-slinga för att räkna upp från 1 till det givna talet.
   ```python
   for i in range(1, antal + 1):
       print(i)
   ```

   - `range(1, antal + 1)` skapar en sekvens från 1 till användarens tal.
   - `print(i)` skriver ut varje tal.

#### Sammanfattning:
- Eleverna får repetera hur man tar in användarinput och använder `for`-loopar.
- De lär sig hur `range()` fungerar och får en bättre förståelse för iteration.
