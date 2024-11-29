### Dag 3: Objektorienterad programmering i C#

Objektorienterad programmering (OOP) är ett programmeringsparadigm där program är strukturerade runt objekt och klasser snarare än procedurer och funktioner. OOP gör det lättare att strukturera och underhålla stora kodbaser genom att bryta ner program i självständiga komponenter som representerar olika verkliga eller abstrakta entiteter.

---

### 1. **Klasser och objekt**

#### **Klasser**
En klass är en mall eller en "blåkopi" som beskriver egenskaper och beteenden för en viss typ av objekt. Klasser i C# definierar data (fält) och funktioner (metoder) som hör ihop med objekten.

**Syntax för en klass:**
```csharp
public class Person {
    // Fält (attribut)
    public string name;
    public int age;

    // Metod (funktion)
    public void SayHello() {
        Console.WriteLine($"Hej, mitt namn är {name} och jag är {age} år gammal.");
    }
}
```

#### **Objekt**
Ett objekt är en instans av en klass. När en klass har definierats kan vi skapa objekt från den klassen, och varje objekt får sina egna kopior av de fält och metoder som definieras i klassen.

**Exempel på objektinstansiering:**
```csharp
Person person1 = new Person();
person1.name = "John";
person1.age = 30;
person1.SayHello(); // Utskriften blir: Hej, mitt namn är John och jag är 30 år gammal.
```

#### **Objekt och skillnader från Java och JavaScript:**
- I både C# och Java används klasser och objekt på ett liknande sätt, men C# har vissa syntaktiska skillnader (t.ex. användningen av `get` och `set`-egenskaper).
- I JavaScript används objekt oftast som löst typade "hashmaps" där du kan dynamiskt tilldela egenskaper och metoder. C# är mycket mer strikt och typad i sin användning av objekt och klasser.

---

### 2. **Inkapsling (Encapsulation)**

Inkapsling innebär att dölja en objekts inre tillstånd (fält) och endast exponera en begränsad uppsättning metoder för att interagera med objektet. Detta gör att vi kan skydda data från att ändras på felaktiga eller oönskade sätt. I C# uppnås inkapsling genom åtkomstmodifierare som `private`, `public`, `protected`, och `internal`.

**Exempel på inkapsling med `private` och `public`:**
```csharp
public class Person {
    // Fält är privata
    private string name;
    private int age;

    // Publika metoder som ger tillgång till de privata fälten
    public void SetName(string newName) {
        name = newName;
    }

    public string GetName() {
        return name;
    }
}
```

I exemplet ovan är fälten `name` och `age` privata, vilket innebär att de inte kan ändras direkt från utanför klassen. Användaren måste använda de publika metoderna `SetName` och `GetName` för att komma åt eller ändra dem.

C# har också en smidig mekanism som kallas **egenskaper (properties)**, som är en kombination av fält och metoder för att underlätta inkapsling.

**Exempel med egenskaper:**
```csharp
public class Person {
    private string name;

    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

I detta fall kan du läsa eller sätta `name`-fältet med enkel syntax, som om det vore ett publikt fält, men du behåller ändå kontroll över fältet via `get`- och `set`-blocken.

---

### 3. **Arv (Inheritance)**

Arv tillåter oss att skapa nya klasser som är baserade på befintliga klasser. Den nya klassen (subklass eller derived class) ärver alla fält och metoder från den gamla klassen (superklass eller base class), men kan även utöka eller ändra dem.

#### **Exempel på arv:**
```csharp
// Superklass
public class Animal {
    public string Name { get; set; }

    public void Speak() {
        Console.WriteLine($"{Name} makes a sound.");
    }
}

// Subklass
public class Dog : Animal {
    public void Bark() {
        Console.WriteLine($"{Name} barks.");
    }
}

// Användning
Dog dog = new Dog();
dog.Name = "Buddy";
dog.Speak(); // Buddy makes a sound.
dog.Bark();  // Buddy barks.
```

I detta exempel är `Dog` en subklass av `Animal`. `Dog`-klassen ärver `Name`-egenskapen och `Speak`-metoden från `Animal`, och kan lägga till egna metoder som `Bark`.

---

### 4. **Polymorfism**

Polymorfism innebär att objekt av olika typer kan behandlas som om de vore av samma typ, vilket gör att vi kan skriva kod som fungerar på flera olika typer utan att behöva känna till exakt vilken typ objekten har. Polymorfism kan uppnås på två sätt i C#:
- **Metodöverskrivning (Method Overriding)**: En subklass kan åsidosätta en metod i sin superklass med hjälp av `override`-nyckelordet.
- **Gränssnitt (Interface)**: En klass kan implementera ett gränssnitt, vilket gör det möjligt för olika klasser att ha samma metodsignaturer men olika implementationer.

#### **Exempel på polymorfism med metodöverskrivning:**
```csharp
public class Animal {
    public virtual void Speak() {
        Console.WriteLine("The animal makes a sound.");
    }
}

public class Dog : Animal {
    public override void Speak() {
        Console.WriteLine("The dog barks.");
    }
}

// Användning
Animal myAnimal = new Dog();  // Polymorfism: en Dog behandlas som en Animal
myAnimal.Speak();  // Utskrift: The dog barks.
```

Här är `Speak`-metoden i `Dog` en överskrivning av `Speak` i `Animal`. Även om objektet deklareras som `Animal`, kommer den version av `Speak` som körs vara den som finns i `Dog`-klassen.

---

### 5. **Statisk vs instans-baserade medlemmar**

C# skiljer på instansmedlemmar och statiska medlemmar:
- **Instansmedlemmar** tillhör specifika objektinstanser. Varje objekt har sina egna kopior av dessa medlemmar.
- **Statiska medlemmar** tillhör själva klassen och delas av alla objekt.

#### **Exempel på statiska medlemmar:**
```csharp
public class MathHelper {
    public static int Add(int a, int b) {
        return a + b;
    }
}

// Användning utan att skapa en instans av klassen
int result = MathHelper.Add(5, 10);  // Utskrift: 15
```

I detta exempel är `Add` en statisk metod som kan anropas direkt på klassen `MathHelper` utan att behöva skapa ett objekt.

---

### 6. **Praktiska övningar för Dag 3**

För att omsätta dessa teorier i praktiken kan du göra följande övningar:

1. **Skapa en klass:**
   - Definiera en klass `Car` med attribut som `brand`, `model` och `year`. Skapa metoder som låter användaren köra och stanna bilen.
   `Du startar bilen`, `Bilen rör sig frammåt`, etc...

2. **Skapa en till klass**
    - Definera en motor som är en egen klass med attribut som `växel`,`varvtal`,`på`.
    - Motorn skall ha metoder som hanterar motorn och växlar.
    - Motorn skall ha metoder som visa status.
    `Motorn är på och växel 3 är i`,`Du växlar upp`,etc..
    - Motorn skall vara en del av bilen.

3. **Använd inkapsling:**
   - Modifiera din `Car` och `Motor`-klass genom att göra fälten privata och skapa egenskaper för att få och sätta värdena på dessa fält.

4. **Implementera arv och polymorfism:**
   - Skapa en superklass `Vehicle` och låt `Car` ärva från `Vehicle`. Skapa en metod i `Vehicle` som överskrivs i `Car`, t.ex. en metod som beskriver fordonets rörelse.

5. **Statisk medlem:**
   - Lägg till en statisk metod i `Car` som returnerar antalet bilar som har skapats.

---

Efter Dag 3 kommer du ha en djup förståelse för objektorienterad programmering i C#, inklusive hur du skapar och använder klasser och objekt, samt hur du implementerar arv, inkapsling och polymorfism. Detta kommer ge dig en kraftfull grund för att skriva välstrukturerade och skalbara program i C#.

[Dag 4](csharp4.md)
