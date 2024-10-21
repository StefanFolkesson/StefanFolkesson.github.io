### Dag 6: Avancerad OOP och designmönster

Nu när du har en grundläggande förståelse för objektorienterad programmering (OOP) i C#, är det dags att fördjupa sig i avancerade koncept som gränssnitt (interfaces), abstrakta klasser och vanliga designmönster. Dessa koncept hjälper dig att skapa mer modulära och lättunderhållna applikationer.

---

### 1. **Interface och abstrakta klasser**

Både interfaces och abstrakta klasser används för att skapa kontrakt och gemensamma gränssnitt mellan olika klasser, men de har några viktiga skillnader.

#### **Interface**

Ett interface är ett kontrakt som definierar ett antal metoder eller egenskaper som måste implementeras av en klass som "ärver" interfacet. Ett interface innehåller endast deklarationer – ingen implementation.

**Syntax för interface:**
```csharp
public interface IMovable {
    void Move();
}
```

När en klass implementerar ett interface, måste den definiera (implementera) alla metoder som interfacet specificerar.

**Exempel:**
```csharp
public interface IMovable {
    void Move();
}

public class Car : IMovable {
    public void Move() {
        Console.WriteLine("Bilen rör sig.");
    }
}
```

Du kan använda interfaces för att säkerställa att olika klasser som inte har en gemensam förfader ändå kan behandlas likadant om de implementerar samma interface.

#### **Abstrakta klasser**

En abstrakt klass är en klass som kan innehålla både fullständiga (implementerade) metoder och ofullständiga (abstrakta) metoder. Abstrakta klasser kan inte instansieras direkt; istället är deras syfte att fungera som bas för andra klasser.

**Syntax för en abstrakt klass:**
```csharp
public abstract class Animal {
    public abstract void MakeSound();  // Abstrakt metod utan implementation
    public void Sleep() {
        Console.WriteLine("Djur sover.");
    }
}
```

Abstrakta metoder måste implementeras i alla underklasser, medan icke-abstrakta metoder kan användas direkt av underklasserna.

**Exempel:**
```csharp
public abstract class Animal {
    public abstract void MakeSound();
    public void Sleep() {
        Console.WriteLine("Djur sover.");
    }
}

public class Dog : Animal {
    public override void MakeSound() {
        Console.WriteLine("Hunden skäller.");
    }
}
```

Här måste `Dog`-klassen implementera `MakeSound`, eftersom den är abstrakt i `Animal`. Däremot kan `Dog` direkt använda den implementerade `Sleep`-metoden.

---

### 2. **Designmönster**

Designmönster är beprövade lösningar på återkommande problem inom programvaruutveckling. De är inte färdiga lösningar, utan snarare generella mönster som kan användas i olika sammanhang för att skapa mer strukturerad och underhållbar kod. Låt oss titta på några av de vanligaste designmönstren.

#### **Singleton-mönstret**

Singleton-mönstret säkerställer att en klass bara har en enda instans, och tillhandahåller en global åtkomstpunkt till denna instans. Detta är användbart för resurser som endast ska existera en gång i applikationen, som en konfigurationsfil eller en anslutning till en databas.

**Exempel på Singleton:**
```csharp
public class Singleton {
    private static Singleton instance = null;

    // Privat konstruktor förhindrar instansiering utanför klassen
    private Singleton() { }

    public static Singleton GetInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

I detta exempel kan vi inte skapa fler än en instans av `Singleton` eftersom konstruktorerna är privata, och vi får alltid samma instans via `GetInstance`-metoden.

#### **Factory-mönstret**

Factory-mönstret används för att skapa objekt utan att specifikt ange den exakta klass som ska instansieras. Detta är användbart när vi vill abstrahera instansieringslogik och låta fabriksklassen hantera beslutet om vilken klass som ska instansieras.

**Exempel på Factory-mönster:**
```csharp
public interface IVehicle {
    void Drive();
}

public class Car : IVehicle {
    public void Drive() {
        Console.WriteLine("Bilen kör.");
    }
}

public class Bike : IVehicle {
    public void Drive() {
        Console.WriteLine("Cykeln kör.");
    }
}

public class VehicleFactory {
    public IVehicle GetVehicle(string vehicleType) {
        if (vehicleType == "Car") {
            return new Car();
        } else if (vehicleType == "Bike") {
            return new Bike();
        } else {
            return null;
        }
    }
}
```

I detta exempel skapar `VehicleFactory` objekt av olika typer beroende på den parameter som skickas in till `GetVehicle`-metoden.

#### **Observer-mönstret**

Observer-mönstret används när du har ett objekt (subject) som behöver notifiera flera andra objekt (observers) om förändringar i sitt tillstånd. Detta är ett vanligt mönster i händelsedrivna system, som GUI-applikationer.

**Exempel på Observer-mönster:**
```csharp
public interface IObserver {
    void Update(string message);
}

public class Subject {
    private List<IObserver> observers = new List<IObserver>();

    public void Attach(IObserver observer) {
        observers.Add(observer);
    }

    public void Notify(string message) {
        foreach (var observer in observers) {
            observer.Update(message);
        }
    }
}

public class ConcreteObserver : IObserver {
    public void Update(string message) {
        Console.WriteLine("Observer fick meddelande: " + message);
    }
}

// Användning
var subject = new Subject();
var observer1 = new ConcreteObserver();
var observer2 = new ConcreteObserver();

subject.Attach(observer1);
subject.Attach(observer2);

subject.Notify("Ändring har skett!");  // Notifierar alla observers
```

Observer-mönstret möjliggör att flera objekt kan reagera på förändringar i ett centralt objekt utan att det centrala objektet behöver känna till alla observers i detalj.

---

### 3. **Dependency Injection (DI)**

Dependency Injection är ett designmönster där ett objekts beroenden (andra objekt som det behöver för att fungera) tillhandahålls utifrån, snarare än att objektet själv skapar dem. Detta mönster är centralt för att skriva testbar och löst kopplad kod, särskilt i stora applikationer.

DI kan implementeras manuellt eller via ramverk som `Microsoft.Extensions.DependencyInjection`.

**Exempel på Dependency Injection:**
```csharp
public interface IService {
    void Serve();
}

public class Service : IService {
    public void Serve() {
        Console.WriteLine("Service fungerar.");
    }
}

public class Client {
    private IService _service;

    // Beroendet injiceras via konstruktorn
    public Client(IService service) {
        _service = service;
    }

    public void Start() {
        _service.Serve();
    }
}

// Användning
IService service = new Service();
Client client = new Client(service);
client.Start();
```

Här injicerar vi beroendet (`Service`) i `Client`-klassen istället för att skapa det inuti `Client`. Detta gör `Client` lättare att testa och underhålla, eftersom vi enkelt kan byta ut beroendet vid behov.

---

### 4. **Praktiska övningar för Dag 6**

För att praktisera dagens teori, rekommenderas följande övningar:

1. **Skapa ett interface:**
   - Definiera ett interface `IShape` med en metod `GetArea`. Skapa sedan två klasser `Circle` och `Rectangle` som implementerar detta interface och beräknar arean på respektive form.

2. **Använd en abstrakt klass:**
   - Definiera en abstrakt klass `Employee` med en abstrakt metod `CalculateSalary`. Skapa underklasser `FullTimeEmployee` och `PartTimeEmployee` som implementerar `CalculateSalary` på olika sätt.

3. **Implementera Singleton-mönster:**
   - Skapa en klass som representerar en logg (logger) och implementera den som en Singleton. Loggern ska ha en metod `Log` som skriver ett meddelande till konsolen.

4. **Bygg en enkel fabrik (Factory):**
   - Skapa en fabrik som producerar olika typer av geometriska former baserat på användarens input.

5. **Observer-mönster:**
   - Implementera ett observer-mönster där flera "lyssnare" (observers) får veta när ett värde ändras i ett subjekt. Demonstrera detta med ett exempel där observatörerna reagerar på en förändring av
   

