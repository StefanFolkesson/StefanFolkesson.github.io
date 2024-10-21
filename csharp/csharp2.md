Självklart! Här kommer en djupare förklaring av de teoretiska delarna för Dag 2.

### Dag 2: Grunder i C#-syntax

Under dag 2 fokuserar vi på att lära oss grunderna i C#-syntax och hur det skiljer sig från andra språk som Java och JavaScript. Målet är att förstå hur C# hanterar variabler, datatyper och kontrollstrukturer. Låt oss bryta ner dessa områden.

---

### 1. **Datatyper i C# (värdetyper vs referenstyper)**

C# är ett starkt typat språk, vilket betyder att varje variabel måste deklareras med en specifik datatyp. C# har två huvudkategorier av datatyper: värdetyper och referenstyper.

#### **Värdetyper (Value Types)**
Värdetyper lagrar sina data direkt i minnet där de deklareras. När du tilldelar en variabel med en värdetyp kopieras värdet, vilket innebär att varje variabel har sin egen kopia av data.
- Exempel på värdetyper: `int`, `double`, `bool`, `char`, `struct`.
  
**Exempel:**
```csharp
int a = 5;
int b = a;  // b får en kopia av värdet i a
a = 10;     // Ändrar inte värdet på b
Console.WriteLine(b); // Utskriften är 5
```

#### **Referenstyper (Reference Types)**
Referenstyper lagrar en pekare till den plats i minnet där datan lagras. När du tilldelar en referenstyp till en annan variabel delar de båda samma pekare, vilket innebär att om en variabel ändras så ändras även den andra.
- Exempel på referenstyper: `object`, `string`, `arrays`, `class`.

**Exempel:**
```csharp
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;   // arr2 pekar på samma array som arr1
arr1[0] = 10;        // Ändring i arr1 påverkar arr2
Console.WriteLine(arr2[0]); // Utskriften är 10
```

### 2. **Variabler, operatorer och uttryck**

#### **Variabler och deklaration**
I C# måste alla variabler deklareras med en typ innan de används. Här är några vanliga datatyper och hur de används:
- **int**: Heltal
- **double**: Flyttal
- **bool**: Boolean (sant/falskt)
- **string**: Textsträng
- **char**: Enskild karaktär

**Exempel:**
```csharp
int number = 10;
double pi = 3.14;
bool isTrue = true;
string name = "John";
char letter = 'A';
```

#### **Operatorer**
C# har flera typer av operatorer, inklusive:
- **Aritmetiska operatorer**: `+`, `-`, `*`, `/`, `%`
  - Exempel: `int sum = 5 + 10; // 15`
  
- **Jämförelseoperatorer**: `==`, `!=`, `>`, `<`, `>=`, `<=`
  - Exempel: `bool isEqual = (5 == 10); // false`
  
- **Logiska operatorer**: `&&` (och), `||` (eller), `!` (inte)
  - Exempel: `bool result = (true && false); // false`

#### **Uttryck**
Ett uttryck är en kombination av variabler, operatorer och värden som evalueras till ett resultat. Du kan skapa komplexa uttryck med både aritmetiska och logiska operatorer.
  
**Exempel:**
```csharp
int a = 5;
int b = 10;
int result = (a + b) * 2; // Resultatet blir 30
bool isGreater = (a > b); // false
```

### 3. **Kontrollstrukturer (if, else, switch, loops)**

Kontrollstrukturer låter dig styra flödet i ditt program baserat på vissa villkor eller genom att repetera en viss sekvens av kod.

#### **If-Else**
Den enklaste kontrollstrukturen i C# är `if-else`. Den används för att köra viss kod om ett villkor är sant, och eventuellt annan kod om villkoret är falskt.

**Exempel:**
```csharp
int number = 10;
if (number > 5) {
    Console.WriteLine("Numret är större än 5");
} else {
    Console.WriteLine("Numret är 5 eller mindre");
}
```

#### **Switch**
`switch` är användbart när du har flera möjliga fall att testa och vill undvika långa `if-else`-kedjor. Det jämför ett uttryck med flera värden och kör motsvarande kodblock.

**Exempel:**
```csharp
int day = 3;
switch (day) {
    case 1:
        Console.WriteLine("Måndag");
        break;
    case 2:
        Console.WriteLine("Tisdag");
        break;
    case 3:
        Console.WriteLine("Onsdag");
        break;
    default:
        Console.WriteLine("Okänd dag");
        break;
}
```

#### **Loops (for, while, do-while)**
Loops används för att repetera kodblock flera gånger baserat på ett villkor.

- **For-loop**: Används när du vet hur många gånger du vill upprepa något.
  ```csharp
  for (int i = 0; i < 5; i++) {
      Console.WriteLine(i);  // Skriver ut 0 till 4
  }
  ```

- **While-loop**: Körs så länge ett villkor är sant.
  ```csharp
  int j = 0;
  while (j < 5) {
      Console.WriteLine(j);
      j++;
  }
  ```

- **Do-while-loop**: Körs minst en gång innan villkoret testas.
  ```csharp
  int k = 0;
  do {
      Console.WriteLine(k);
      k++;
  } while (k < 5);
  ```

### 4. **Praktiska övningar för Dag 2**

För att praktisera dagens teori, rekommenderas att du implementerar små program där du övar på variabelhantering, kontrollstrukturer och loops. Här är några förslag:

1. **Program 1: Villkorsstyrd inmatning**
   - Skriv ett program där användaren matar in ett tal, och programmet skriver ut om talet är positivt, negativt eller noll.
   - Använd `if-else`-struktur för att testa villkoren.
  
   **Exempel:**
   ```csharp
   Console.WriteLine("Mata in ett tal:");
   int number = int.Parse(Console.ReadLine());
   if (number > 0) {
       Console.WriteLine("Talet är positivt");
   } else if (number < 0) {
       Console.WriteLine("Talet är negativt");
   } else {
       Console.WriteLine("Talet är noll");
   }
   ```

2. **Program 2: Enkel miniräknare med switch**
   - Skriv ett program där användaren kan mata in två tal och välja en operation (addition, subtraktion, multiplikation, division) med hjälp av en meny. Använd `switch` för att implementera de olika operationerna.

3. **Program 3: Loopar och array-manipulering**
   - Skapa ett program som använder en for-loop för att fylla en array med värden. Skriv sedan ut alla värden i arrayen med hjälp av en while-loop.

---

Efter denna dag kommer du att ha en stabil förståelse för hur du kan deklarera variabler, använda operatorer och kontrollstrukturer samt repetera kod med loopar i C#. Detta ger dig grunden för att kunna bygga mer komplexa program i de kommande dagarna!
