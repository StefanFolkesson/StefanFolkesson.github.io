Här är en annan mer avancerad uppgift som använder iteration, listor och stränghantering, vilket kan ge dina elever en bra utmaning.

### Uppgift 3: Palindromdetektor
**Beskrivning:** Skriv ett program som ber användaren att mata in en sträng och sedan kontrollerar om strängen är ett palindrom. Ett palindrom är ett ord, en fras eller en sekvens som läses likadant framifrån som bakifrån (t.ex. "radar", "level").

#### Lösning:

1. **Be användaren mata in en sträng:**
   - Vi börjar med att ta en sträng från användaren.
   ```python
   text = input("Skriv in en sträng: ")
   ```

2. **Bearbeta strängen:**
   - Eftersom vi vill ignorera stora/små bokstäver och mellanslag, gör vi om strängen till små bokstäver och tar bort alla mellanslag.
   ```python
   text = text.lower().replace(" ", "")
   ```

3. **Kontrollera om strängen är ett palindrom:**
   - Vi kan använda en loop eller Python-funktioner för att kontrollera om strängen är samma framifrån och bakifrån.
   - En enkel metod är att jämföra strängen med sin omvända version.
   ```python
   if text == text[::-1]:
       print("Strängen är ett palindrom!")
   else:
       print("Strängen är inte ett palindrom.")
   ```

   - `text[::-1]` skapar en omvänd version av strängen.

#### Sammanfattning av koden:
Här är den kompletta lösningen:
```python
text = input("Skriv in en sträng: ")

# Gör om till små bokstäver och ta bort mellanslag
text = text.lower().replace(" ", "")

# Kontrollera om det är ett palindrom
if text == text[::-1]:
    print("Strängen är ett palindrom!")
else:
    print("Strängen är inte ett palindrom.")
```

#### Utmaning:
1. **Hantera fler tecken:** Låt eleverna utvidga programmet så att det ignorerar andra icke-bokstäver som punkter, kommatecken och utropstecken (t.ex. "A man, a plan, a canal, Panama!" är ett palindrom).
   - Detta kan göras med en extra bearbetning som filtrerar bort alla icke-bokstavliga tecken.
   ```python
   import string
   text = ''.join([char for char in text if char in string.ascii_letters])
   ```

2. **Längre texter:** Testa programmet med längre meningar eller fraser för att se om det fortfarande fungerar korrekt.

#### Sammanfattning:
- Eleverna får träna på stränghantering och iteration genom att bearbeta och omvandla texten.
- De introduceras till mer avancerad användning av listor och strängoperationer som slicing och filtrering.
- Utmaningen hjälper dem att hantera text mer effektivt och tänka på hur man optimerar kod för olika scenarier.