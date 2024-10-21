Här kommer nästa lektion, där vi bygger vidare på det vi gjort genom att skapa ett **enkelt inventariesystem** och visa objekt som karaktären plockar upp i spelet.

### Lektion 2: Skapa ett inventariesystem och visa objekt i UI

I denna lektion kommer vi att:
1. Implementera ett enkelt inventariesystem där spelaren kan samla objekt.
2. Lära oss grunderna i Unity UI och skapa ett UI-element för att visa de insamlade objekten.
3. Justera spelmekaniken för att objektet läggs till i inventariet istället för att försvinna.

---

### **Del 1: Skapa ett enkelt inventariesystem (45 minuter)**

Ett inventariesystem lagrar objekt som spelaren plockar upp och kan visa dessa objekt på skärmen.

##### **Steg 1: Skapa en Inventory Script**
1. **Skapa ett nytt skript:**
   - Högerklicka i **Assets**-mappen och skapa ett nytt skript som heter "Inventory".
   - Detta skript kommer att hantera lagringen av objekt som spelaren plockar upp.

2. **Kod för Inventory Script:**
   - I `Inventory.cs`-skriptet kan du börja med en enkel lista som lagrar insamlade objekt. Lägg till följande kod:

```csharp
using System.Collections.Generic;
using UnityEngine;

public class Inventory : MonoBehaviour
{
    // Lista som lagrar insamlade objekt
    public List<GameObject> collectedItems = new List<GameObject>();

    // Funktion för att lägga till ett objekt i inventariet
    public void AddItem(GameObject item)
    {
        collectedItems.Add(item);
        Debug.Log(item.name + " tillagd i inventariet.");
    }
}
```

##### **Steg 2: Knyt inventariet till spelaren**
1. **Lägg till Inventory till Player:**
   - Markera **Player** i **Hierarchy** och lägg till **Inventory**-skriptet som en komponent.

2. **Uppdatera Collectible-skriptet:**
   - Nu ska vi ändra `Collectible.cs` så att när ett objekt plockas upp, läggs det till i inventariet istället för att bara förstöras.
   - Ändra koden i `Collectible.cs` så här:

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Inventory playerInventory = other.GetComponent<Inventory>();
            if (playerInventory != null)
            {
                playerInventory.AddItem(gameObject);  // Lägg till objektet i inventariet
                gameObject.SetActive(false);  // Döljer objektet istället för att förstöra det
            }
        }
    }
}
```

I denna kod döljer vi objektet (`gameObject.SetActive(false)`) istället för att förstöra det. Det lagras nu i spelarens inventarium.

---

### **Del 2: Skapa ett användargränssnitt (UI) för att visa insamlade objekt (45 minuter)**

Unitys UI-system låter dig skapa användargränssnitt som visar information till spelaren, som t.ex. vilka objekt de har plockat upp. Vi ska nu skapa en enkel visning av objekt som spelaren har plockat upp i ett inventarie.

##### **Steg 1: Skapa ett UI Canvas**
1. **Skapa en Canvas:**
   - Högerklicka i **Hierarchy** och välj **UI > Canvas**.
   - Detta skapar en **Canvas** där alla UI-element placeras.
   - Ändra Canvasens **Render Mode** till "Screen Space - Overlay" i **Inspector**.

2. **Skapa en Panel för inventariet:**
   - Inuti Canvasen, högerklicka och välj **UI > Panel**. Detta blir vår inventariepanel.
   - Namnge panelen "InventoryPanel" och justera storleken så att den passar bra i ena hörnet av skärmen.
   - Ändra panelens bakgrundsfärg till något neutralt eller transparent i **Inspector** om du vill.

##### **Steg 2: Skapa Text-UI för att visa objekt**
1. **Lägg till en Text för objekt:**
   - Inuti **InventoryPanel**, högerklicka och välj **UI > Text**.
   - Namnge detta textfält "ItemText".
   - Justera positionen och storleken på texten så att det ser bra ut i panelen.

2. **Anslut Text-UI till ett nytt skript:**
   - Skapa ett nytt skript som heter `InventoryUI`.
   - Detta skript ansvarar för att uppdatera textfältet med de objekt som spelaren har samlat. Skriv följande kod i `InventoryUI.cs`:

```csharp
using UnityEngine;
using UnityEngine.UI;

public class InventoryUI : MonoBehaviour
{
    public Inventory playerInventory;
    public Text itemText;

    void Update()
    {
        itemText.text = "Collected Items:\n";
        foreach (var item in playerInventory.collectedItems)
        {
            itemText.text += item.name + "\n";
        }
    }
}
```

3. **Lägg till InventoryUI till Canvas:**
   - Gå tillbaka till Unity och lägg till **InventoryUI**-skriptet som en komponent på **InventoryPanel**.
   - Dra din **Player**-karaktär till skriptets **Player Inventory**-fält i **Inspector**.
   - Dra även **ItemText**-Text-fältet till **InventoryUI**-komponenten.

##### **Steg 3: Testa ditt inventariesystem**
1. **Kör spelet:**
   - Tryck på **Play** och rör din karaktär över objektet. Det borde nu försvinna från scenen och dyka upp i inventariet i UI.
   - Alla objekt som spelaren samlar ska nu visas i panelen.

---

### **Del 3: Justering och förberedelse för nästa lektion (30 minuter)**

Nu när vi har ett grundläggande inventariesystem, kan vi lägga till fler funktioner i spelet. Här är några idéer som vi kan utveckla i kommande lektioner:
- **Grafiska ikoner i inventariet:** Vi kan visa bilder på insamlade objekt istället för bara text.
- **Flera objekt:** Skapa flera olika objekt som kan plockas upp och visa dem i inventariet.
- **Använda objekt:** Lägg till en funktion där spelaren kan använda eller släppa objekt från inventariet.

---

### Nästa steg:
I nästa lektion ska vi:
- Lära oss att visa objekt i inventariet med hjälp av ikoner (bilder) istället för text.
- Utveckla logiken för att använda eller interagera med objekt i inventariet.

---

### Hemuppgift:
- Skapa fler objekt att plocka upp och testa att de visas korrekt i inventariet.
- Experimentera med att ändra designen på UI-elementen (textstorlek, färger, placering) för att förbättra spelupplevelsen.

Vi bygger vidare på detta steg för steg, så se till att du känner dig bekväm med grunderna innan vi går vidare. Lycka till!

[Dag 3](unity3.md)
