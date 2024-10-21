### Dag 4: Felhantering och undantag i C#

Felhantering i C# hanteras främst genom användningen av undantag (exceptions). Undantag är händelser som inträffar under programkörning och som bryter det normala exekveringsflödet. Genom att fånga och hantera undantag på rätt sätt kan du undvika att applikationen kraschar och istället hantera problemet på ett kontrollerat sätt.

---

### 1. **Exception-handling med `try`, `catch`, `finally`, och `throw`**

I C# används undantag främst genom följande strukturer:
- **`try`**: Innesluter den kod där ett undantag potentiellt kan uppstå.
- **`catch`**: Fångar och hanterar undantaget om det inträffar.
- **`finally`**: Innesluter kod som alltid ska köras, oavsett om ett undantag inträffar eller inte. Detta är användbart för att städa upp resurser som filer eller nätverksanslutningar.
- **`throw`**: Används för att manuellt kasta ett undantag, antingen inom en metod eller återkasta ett fångat undantag.

#### **Grundläggande syntax:**
```csharp
try {
    // Kod som kan orsaka ett undantag
    int[] numbers = { 1, 2, 3 };
    Console.WriteLine(numbers[5]);  // Detta orsakar ett undantag (index out of range)
} catch (IndexOutOfRangeException e) {
    // Hantering av undantaget
    Console.WriteLine("Ett undantag inträffade: " + e.Message);
} finally {
    // Kod som alltid körs
    Console.WriteLine("Rensning eller avslutande logik här.");
}
```

#### **Steg-för-steg genomgång:**
1. **`try`-blocket** körs, och om det inte uppstår något undantag, ignoreras `catch`-blocket.
2. Om det uppstår ett undantag inom `try`, hoppar exekveringen direkt till motsvarande `catch`-block.
3. **`finally`-blocket** körs oavsett om ett undantag inträffade eller inte. Detta är användbart för att frigöra resurser eller städa upp efter att programkoden har körts.

#### **Använda `throw`:**
Du kan kasta egna undantag med `throw`-nyckelordet.
```csharp
public void ValidateAge(int age) {
    if (age < 18) {
        throw new ArgumentException("Åldern måste vara minst 18.");
    }
}
```

När `throw` används i koden ovan, kommer ett undantag att kastas om åldern är mindre än 18. Om detta undantag inte fångas någonstans i applikationen, kommer programmet att krascha.

---

### 2. **Vanliga undantagstyper i C#**

C# har ett stort antal inbyggda undantagstyper som du kan fånga och hantera beroende på vilken typ av fel som uppstår. Här är några av de vanligaste:

#### **System.Exception**
- Detta är basklassen för alla undantag i C#. Om du fångar ett undantag av typen `Exception`, fångar du alla typer av undantag. Det är dock en god praxis att vara så specifik som möjligt när du fångar undantag, för att inte dölja felaktiga undantag.
  
#### **ArgumentException**
- Detta undantag kastas när ett ogiltigt argument skickas till en metod. Ett vanligt exempel är när du försöker skicka in en null-referens till en metod som inte tillåter det.
  
#### **IndexOutOfRangeException**
- Detta inträffar när du försöker komma åt ett element i en array eller lista med ett ogiltigt index, som i vårt tidigare exempel.

#### **NullReferenceException**
- Detta undantag uppstår när du försöker använda en objektreferens som inte har tilldelats ett faktiskt objekt (det vill säga, referensen är `null`).

#### **DivideByZeroException**
- Detta undantag uppstår när du försöker dela ett tal med noll.

#### **InvalidOperationException**
- Detta undantag kastas när ett objekt inte är i ett tillstånd där en viss operation kan utföras.

**Exempel på att fånga olika undantagstyper:**
```csharp
try {
    // Kod som kan orsaka flera typer av undantag
    int a = 10;
    int b = 0;
    int result = a / b;  // Orsakar DivideByZeroException
} catch (DivideByZeroException ex) {
    Console.WriteLine("Kan inte dela med noll: " + ex.Message);
} catch (Exception ex) {
    // Fångar alla andra typer av undantag
    Console.WriteLine("Ett annat undantag inträffade: " + ex.Message);
}
```

---

### 3. **Skillnad mellan fel och undantag**

Det är viktigt att förstå skillnaden mellan fel (errors) och undantag (exceptions):
- **Fel** är vanligen problem som uppstår på en systemnivå eller hårdvarunivå, såsom ett strömavbrott eller en krasad hårddisk. Dessa kan vara svårare att hantera eftersom de kan ligga utanför applikationens kontroll.
- **Undantag** är mjukvaruproblem som kan uppstå under körning och som ofta kan hanteras av programmet genom korrekt undantagshantering.

En annan viktig skillnad är att undantag är en kontrollerad mekanism som gör att du kan hantera fel på ett systematiskt sätt, medan fel ofta är okontrollerade och kan leda till att hela applikationen kraschar utan möjlighet till återhämtning.

---

### 4. **Bästa praxis för undantagshantering**

Att hantera undantag på rätt sätt är viktigt för att skapa stabila och användarvänliga program. Här är några riktlinjer:

#### **1. Fånga bara undantag som du kan hantera**
Fånga aldrig undantag bara för sakens skull. Om du inte kan göra något användbart för att hantera ett undantag, låt det bubbla upp till en högre nivå där det kan hanteras på ett meningsfullt sätt.

```csharp
try {
    // Kod som kan orsaka undantag
} catch (FileNotFoundException e) {
    // Hantera specifikt fall
} catch (Exception e) {
    // Återkasta om det inte går att hantera undantaget här
    throw;
}
```

#### **2. Använd alltid `finally` för att städa upp resurser**
Om ditt program använder resurser som filer, databaskopplingar eller nätverksanslutningar, se till att dessa resurser alltid frigörs oavsett om ett undantag inträffar eller inte.

```csharp
StreamReader reader = null;
try {
    reader = new StreamReader("data.txt");
    // Läs data från filen
} catch (FileNotFoundException e) {
    Console.WriteLine("Filen hittades inte.");
} finally {
    if (reader != null) {
        reader.Close();  // Stäng filen, oavsett om ett undantag inträffade
    }
}
```

#### **3. Använd egna undantag (custom exceptions) vid behov**
Ibland kan det vara meningsfullt att skapa egna undantag om du stöter på specifika fel i ditt program som inte täcks av de inbyggda undantagstyperna. Detta gör det enklare att identifiera och hantera specifika situationer.

```csharp
public class InvalidAgeException : Exception {
    public InvalidAgeException(string message) : base(message) {}
}

public void CheckAge(int age) {
    if (age < 18) {
        throw new InvalidAgeException("Åldern är för låg.");
    }
}
```

---

### 5. **Praktiska övningar för Dag 4**

Här är några förslag på övningar för att praktisera undantagshantering:

1. **Fångning av inmatningsfel:**
   - Skapa ett program som ber användaren mata in ett heltal och försök sedan att dela det med ett annat heltal som användaren matar in. Hantera undantag som kan uppstå om användaren matar in ogiltiga data (t.ex. `FormatException` när ett tal förväntas men användaren skriver in en sträng) eller försöker dela med noll.

   **Exempel:**
   ```csharp
   try {
       Console.WriteLine("Mata in ett tal:");
       int num1 = int.Parse(Console.ReadLine());
       Console.WriteLine("

Mata in ett annat tal:");
       int num2 = int.Parse(Console.ReadLine());

       int result = num1 / num2;
       Console.WriteLine($"Resultatet är: {result}");
   } catch (FormatException e) {
       Console.WriteLine("Felaktig inmatning, vänligen mata in ett heltal.");
   } catch (DivideByZeroException e) {
       Console.WriteLine("Kan inte dela med noll.");
   } catch (Exception e) {
       Console.WriteLine("Ett oväntat fel inträffade: " + e.Message);
   }
   ```

2. **Användning av `finally`:**
   - Skriv ett program som öppnar en fil och läser dess innehåll. Se till att filen alltid stängs, oavsett om ett undantag inträffar eller inte, genom att använda `finally`.

3. **Skapa egna undantag:**
   - Implementera ett eget undantag, t.ex. för ett bankkonto som inte tillåter uttag över en viss gräns. Om användaren försöker ta ut för mycket pengar, kasta ett anpassat undantag som `OverdraftException`.

---

Efter Dag 4 kommer du ha en djup förståelse för hur undantag fungerar i C#, och du kommer att kunna skriva robust kod som kan hantera fel och undantag på ett kontrollerat sätt. Detta är en avgörande färdighet för att skapa applikationer som inte kraschar vid oväntade problem och som kan ge användaren informativa och användbara felmeddelanden.

