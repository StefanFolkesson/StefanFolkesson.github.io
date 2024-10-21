### Dag 1: Introduktion till C# och .NET
Få en förståelse för C# som språk och dess ekosystem.

### 1. **Vad är C#? Introduktion till språket**

C# (uttalas "C-sharp") är ett objektorienterat, typsäkert programmeringsspråk som utvecklades av Microsoft och lanserades år 2000 som en del av deras .NET-ramverk. C# är inspirerat av många språk, bland annat C++, Java och även några koncept från funktionella språk som F#. Språket har utvecklats för att vara enkelt att använda, samtidigt som det är kraftfullt nog att skapa allt från enkla program till stora applikationer, inklusive webb-, mobil- och desktopapplikationer.

**Jämförelse med JavaScript och Java:**
- **C# och Java**: C# och Java är båda objektorienterade språk med liknande syntax. Båda använder klasser och objekt för att strukturera kod. Dock är C# mer bundet till Microsofts .NET-plattform, medan Java är plattformsoberoende med sin JVM (Java Virtual Machine). Både C# och Java har stark typning, men C# har fler funktioner som generics och LINQ som gör det mer flexibelt i vissa avseenden.
- **C# och JavaScript**: Till skillnad från JavaScript, som är ett dynamiskt skriptspråk, är C# ett kompilat språk med stark typning. Medan JavaScript främst används för webbutveckling i klientmiljöer, används C# i mer varierade miljöer, inklusive server, desktop och även spelutveckling (med Unity).

### 2. **Vad är .NET-plattformen och dess betydelse**

.NET är ett omfattande ramverk som tillhandahåller verktyg, bibliotek och runtime-miljöer för att utveckla applikationer. Det fungerar som grunden för många typer av applikationer, inklusive webb-, mobil- och desktopapplikationer, samt API-tjänster.

Några viktiga komponenter i .NET-plattformen är:
- **Common Language Runtime (CLR)**: CLR är den del av .NET som hanterar exekvering av C#-program. Det fungerar som en virtuell maskin, liknande JVM för Java. CLR tar hand om saker som minneshantering, trådhantering, och felhantering.
- **Base Class Library (BCL)**: BCL är en samling standardbibliotek som tillhandahåller vanliga funktioner såsom I/O, stränghantering, och datastrukturer som listor och arrayer. Denna bibliotekssamling gör det enkelt att hantera vanliga programmeringsuppgifter utan att behöva skriva mycket kod från grunden.

.NET har också utvecklats till **.NET Core**, vilket är en modern och plattformsoberoende version av .NET som gör det möjligt att utveckla och köra applikationer på Windows, Linux och macOS.

**Varför är .NET viktigt för C#?**
C# är nära kopplat till .NET-plattformen, eftersom det ger dig tillgång till alla verktyg och bibliotek som behövs för att utveckla kraftfulla applikationer. Genom .NET får du även stöd för asynkron programmering, säkerhet, och hantering av stora datastrukturer på ett effektivt sätt.

### 3. **Jämförelse mellan C# och Java/JavaScript (syntax, typning)**

**Syntax och struktur:**
- Både C# och Java har liknande syntax med blockstrukturer, klasser, metoder och attribut.
- JavaScript är mer löst typat än både Java och C#. Medan JavaScript tillåter att en variabel kan anta vilken typ av värde som helst, så kräver både C# och Java att du anger vilken typ en variabel ska ha från början.

**Typning:**
- **JavaScript**: Dynamiskt typat, vilket betyder att typer inte anges när en variabel deklareras. JavaScript försöker att inferera typen utifrån värdet som tilldelas.
  ```javascript
  let x = 5; // JavaScript tilldelar automatiskt typen "Number"
  ```
- **C# och Java**: Statiskt typat, vilket innebär att typer måste anges vid deklaration, och en variabel kan inte byta typ under körning.
  ```csharp
  int x = 5; // Typen måste anges i C#
  ```

**Funktionshantering:**
- JavaScript tillåter att du definierar och skickar funktioner som första-klassiga objekt, medan C# och Java hanterar funktioner genom metoder inom klasser. Dock stödjer både Java och C# anonyma metoder och lambda-uttryck, vilket gör dem mer flexibla i detta avseende.

### 4. **Installera Visual Studio eller Visual Studio Code med .NET SDK**

**Visual Studio** och **Visual Studio Code** är två populära utvecklingsmiljöer som stöder C#. Här är en kort översikt:

- **Visual Studio** (VS): Ett kraftfullt IDE som innehåller allt du behöver för att utveckla i C#. Visual Studio har integrerat stöd för debugging, versionhantering, och projektmallar för olika typer av applikationer (konsol, webb, mobil etc.). Det är det mest använda verktyget för professionell utveckling med C#.
  
- **Visual Studio Code** (VS Code): En lättviktig textredigerare som med tillägg kan göras kraftfull nog att utveckla i C#. Den används ofta för snabba projekt eller enklare utveckling och erbjuder integration med .NET SDK via tillägg.

**.NET SDK**: Detta är utvecklingsverktyget som gör det möjligt för dig att kompilera och köra C#-applikationer. Det inkluderar verktyg för att skapa, bygga och köra C#-projekt från kommandoraden.

För att komma igång:
1. **Ladda ner och installera Visual Studio eller Visual Studio Code.**
2. **Installera .NET SDK**, om det inte är inkluderat.
3. Skapa ett nytt projekt med en konsolapplikation:
   - Visual Studio: Skapa ett nytt projekt -> Välj "Console App (.NET)".
   - Visual Studio Code: Öppna terminalen och kör följande kommando:
     ```bash
     dotnet new console -o MyFirstApp
     cd MyFirstApp
     dotnet run
     ```
4. Detta skapar och kör en enkel "Hello World"-applikation.

### 5. **Utforska Visual Studios och dess funktioner för debugging**

Visual Studio erbjuder ett av de mest omfattande debugger-verktygen för C#-utveckling. Här är några viktiga funktioner att känna till:
- **Breakpoint**: Du kan sätta "breakpoints" för att pausa körningen av din kod vid specifika ställen. Detta är ovärderligt för att hitta buggar eller förstå programflödet.
- **Step Into/Over**: När du kör din kod med breakpoints, kan du använda dessa verktyg för att gå igenom kodrad för kodrad, eller hoppa över vissa delar om du bara vill följa en viss metod.
- **Locals och Watch**: Med "Locals"-fönstret kan du se värdena på dina variabler under körningen, medan du med "Watch" kan övervaka specifika uttryck eller variabler.

Efter denna introduktionsdag kommer du ha en grundläggande förståelse för vad C# är, dess förhållande till .NET, och hur du kan sätta upp en utvecklingsmiljö för att börja koda.

[Dag 2](csharp2.md)
