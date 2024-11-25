### Övning 2: Summera tal i en lista
**Beskrivning:** Skriv ett program som tar en lista av tal och beräknar summan av alla tal i listan.

#### Lösning:
1. **Lista:** Skapa en lista med några tal.
   ```python
   tal_lista = [3, 7, 2, 8, 10]
   ```

2. **Iteration:** Använd en `for`-loop för att summera alla tal i listan.
   ```python
   summa = 0
   for tal in tal_lista:
       summa += tal
   ```

   - Vi initierar variabeln `summa` till 0 för att hålla koll på summan.
   - `for tal in tal_lista` går igenom varje tal i listan.
   - `summa += tal` adderar varje tal till den totala summan.

3. **Output:** Skriv ut summan.
   ```python
   print("Summan av talen i listan är:", summa)
   ```

#### Sammanfattning:
- Eleverna får repetera listor och loopar.
- De övar på att iterera över en lista och använda en ackumulator (i detta fall `summa`).
