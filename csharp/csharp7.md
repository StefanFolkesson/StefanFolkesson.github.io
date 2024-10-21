Här kommer en djupare förklaring av de teoretiska delarna för Dag 7, där vi fokuserar på **asynkron programmering** i C#. Asynkron programmering är viktigt för att skriva effektiva och responsiva applikationer, särskilt när det gäller I/O-intensiva operationer som att läsa från en databas, kommunicera med en webbserver, eller bearbeta stora filer.
### Dag 7: Asynkron programmering och avslutande projekt

Asynkron programmering i C# gör det möjligt att hantera långsamma operationer utan att blockera huvudtråden i ditt program. Detta är särskilt viktigt i grafiska användargränssnitt (GUI) och webbapplikationer där man inte vill att användaren ska behöva vänta medan programmet utför tidskrävande uppgifter.

---

### 1. **Introduktion till `async` och `await`**

De viktigaste nyckelorden för asynkron programmering i C# är **`async`** och **`await`**. Med hjälp av dessa kan du skriva kod som ser ut som vanlig sekventiell kod, men som körs asynkront i bakgrunden.

#### **Grunderna i `async` och `await`:**

- **`async`**: När du deklarerar en metod med `async` betyder det att den kan innehålla asynkron kod. Det betyder dock inte att hela metoden körs asynkront – bara de delar som innehåller `await`.
- **`await`**: Nyckelordet `await` används för att invänta en asynkron operation utan att blockera huvudtråden. Medan programmet väntar på att en uppgift ska slutföras, kan det fortsätta med andra uppgifter under tiden.

**Exempel på en asynkron metod:**
```csharp
public async Task<int> GetNumberAsync() {
    await Task.Delay(2000);  // Simulerar en långsam operation (2 sekunder)
    return 42;
}

public async Task ExecuteAsync() {
    int result = await GetNumberAsync();
    Console.WriteLine($"Resultat: {result}");
}
```

I detta exempel gör `await Task.Delay(2000)` så att programmet väntar i 2 sekunder innan den återgår till att köra resten av koden, utan att blockera huvudtråden.

#### **Viktiga punkter om `async` och `await`:**
- En metod som deklareras med `async` måste returnera `Task` eller `Task<T>`. Om metoden inte returnerar något kan den deklareras som `async Task`.
- `await`-nyckelordet kan endast användas inom metoder som har markerats med `async`.
- `async`-metoder körs inte nödvändigtvis på en separat tråd; istället frigörs huvudtråden för att hantera andra uppgifter medan den väntar på att en uppgift ska slutföras.

---

### 2. **Task Parallel Library (TPL)** och parallell programmering

**Task Parallel Library (TPL)** är en kärnkomponent i .NET för att skapa och hantera asynkrona operationer och parallella uppgifter. TPL använder klassen **`Task`** för att representera asynkrona operationer. Det gör det enkelt att skapa parallella uppgifter och köra dem utan att explicit hantera trådar.

#### **Skapa och köra uppgifter (Tasks):**
Du kan skapa uppgifter manuellt och köra dem parallellt. Här är ett enkelt exempel på hur du skapar en parallell uppgift med hjälp av TPL:

```csharp
public async Task RunTasksAsync() {
    Task task1 = Task.Run(() => DoWork(1));
    Task task2 = Task.Run(() => DoWork(2));

    await Task.WhenAll(task1, task2);  // Väntar på att båda uppgifterna ska slutföras
}

public void DoWork(int taskNumber) {
    Console.WriteLine($"Uppgift {taskNumber} startar.");
    Thread.Sleep(1000);  // Simulerar arbete
    Console.WriteLine($"Uppgift {taskNumber} slutförd.");
}
```

I detta exempel kör vi två uppgifter parallellt med `Task.Run`, och vi väntar tills båda är färdiga med hjälp av `Task.WhenAll`.

#### **Vänta på flera uppgifter med `Task.WhenAll` och `Task.WhenAny`:**
- **`Task.WhenAll`**: Används för att vänta på att flera uppgifter ska slutföras.
- **`Task.WhenAny`**: Används för att vänta på att någon av uppgifterna ska slutföras.

---

### 3. **Hantera undantag i asynkrona operationer**

När du arbetar med asynkron kod kan undantag uppstå precis som i synkron kod. Dessa undantag kan fångas och hanteras med `try-catch`, men eftersom metoden returnerar en `Task`, måste du vänta på att uppgiften ska slutföras innan undantaget kastas.

**Exempel på undantagshantering i asynkron kod:**
```csharp
public async Task ExecuteWithErrorHandlingAsync() {
    try {
        await FailingTask();
    } catch (Exception ex) {
        Console.WriteLine($"Ett undantag inträffade: {ex.Message}");
    }
}

public async Task FailingTask() {
    await Task.Delay(1000);
    throw new InvalidOperationException("Ett fel inträffade.");
}
```

I detta exempel kommer ett undantag att kastas i `FailingTask`, men eftersom vi använder `try-catch` kan vi hantera det utan att programmet kraschar.

---

### 4. **Praktisk användning av asynkron programmering**

Asynkron programmering är särskilt användbar när du arbetar med långsamma operationer, såsom:
- **Fjärrtjänstanrop (API-anrop)**: Hämta eller skicka data från/till en server utan att blockera användargränssnittet.
- **Filhantering**: Läs eller skriv stora filer utan att låsa användargränssnittet.
- **Databasoperationer**: Utför långa databasoperationer asynkront för att bibehålla en responsiv applikation.

**Exempel på ett asynkront API-anrop:**
```csharp
public async Task<string> FetchDataFromApiAsync() {
    using (HttpClient client = new HttpClient()) {
        HttpResponseMessage response = await client.GetAsync("https://api.example.com/data");
        response.EnsureSuccessStatusCode();
        return await response.Content.ReadAsStringAsync();
    }
}
```

I detta exempel anropar vi ett API asynkront med hjälp av `HttpClient` och `await` för att vänta på att data ska hämtas utan att blockera programmet.

---

### 5. **Avslutande projekt**

För att tillämpa all kunskap från veckan rekommenderas att du avslutar med ett litet projekt där du kombinerar objektorienterad programmering, LINQ, felhantering och asynkron programmering.

#### **Förslag på avslutande projekt:**

1. **Asynkron API-konsument:**
   - Skapa en konsolapplikation som hämtar data från ett API, bearbetar datan med hjälp av LINQ och skriver ut ett filtrerat resultat till användaren. Implementera felhantering om något går fel under API-anropet.

   **Exempel:**
   - Hämta en lista med användare från ett API och använd LINQ för att filtrera ut alla användare som bor i en specifik stad.

2. **Filhanteringsprogram:**
   - Bygg en asynkron applikation som läser in stora textfiler, bearbetar innehållet (t.ex. räknar ord eller söker efter specifika mönster) och skriver resultatet till en ny fil. Implementera korrekt felhantering om filen inte kan hittas eller om det uppstår något annat problem.

3. **Parallell beräkning:**
   - Implementera en applikation som kör parallella beräkningar, t.ex. beräkning av stora primtal eller sortering av stora datasamlingar, med hjälp av TPL och `Task.WhenAll`.

---

### 6. **Rekommendationer för vidare utveckling**

Efter denna vecka har du fått en bra grund i C# och några av de viktigaste koncepten och mönstren inom programmering. Här är några rekommendationer för vad du kan fokusera på framöver:

- **Fördjupa dig i ASP.NET Core** om du är intresserad av webbutveckling med C#. ASP.NET Core är Microsofts kraftfulla ramverk för att bygga moderna webbapplikationer.
- **Utforska fler designmönster**, som Strategy, Adapter, och Decorator, för att förbättra dina färdigheter inom programdesign.
- **Arbeta med databaser och Entity Framework** för att lära dig hur man interagerar med databaser på ett effektivt sätt med hjälp av C#.
- **Bygg fullskaliga projekt**

 som inkluderar användning av asynkron programmering, LINQ, OOP, och designmönster för att stärka dina kunskaper.

---

Efter Dag 7 kommer du att ha en god förståelse för hur asynkron programmering fungerar i C# och vara väl förberedd för att hantera långsamma operationer på ett effektivt sätt. Dessutom kommer du ha avslutat ett praktiskt projekt som sammanför alla koncept du har lärt dig under veckan.
