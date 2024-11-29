Här kommer nästa tvåtimmarslektion, där vi tar vårt inventariesystem ett steg längre genom att lägga till **grafiska ikoner** för insamlade objekt, samt att utveckla systemet så att spelaren kan **använda eller interagera med objekt** i sitt inventory.

### Lektion 3: Visa objekt som ikoner i inventariet och interaktion med insamlade objekt

I denna lektion kommer vi att:
1. Lära oss att visa bilder (ikoner) i inventariet istället för text.
2. Utveckla en enkel logik för att interagera med objekt i inventariet, som att använda eller släppa dem.

---

### **Del 1: Visa insamlade objekt som ikoner (45 minuter)**

##### **Steg 1: Förbered dina ikoner**
1. **Skapa eller hämta bilder för objekt:**
   - Om du inte redan har bilder för dina insamlingsbara objekt, kan du skapa eller hämta några enkla ikoner (t.ex. en nyckel, ett mynt, etc.). Dessa ska representera objekten visuellt i inventariet.
   - Dra och släpp dessa bilder i **Assets**-mappen i Unity.

2. **Lägg till ikoner till insamlingsbara objekt:**
   - Gå till dina insamlingsbara objekt (t.ex. "Collectible"-objektet från tidigare lektioner) och lägg till en ny **public Sprite** i `Collectible.cs`-skriptet. Detta låter oss tilldela en bild för varje objekt.

```csharp
using UnityEngine;
public class Collectible : MonoBehaviour
{
    public Sprite itemIcon;  // Bild för objektet

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Inventory playerInventory = other.GetComponent<Inventory>();
            if (playerInventory != null)
            {
                playerInventory.AddItem(gameObject);  // Skickar hela Collectible-objektet
                gameObject.SetActive(false);
            }
        }
    }
}
```

3. **Tilldela ikoner i Unity:**
   - Gå tillbaka till Unity och markera varje insamlingsbart objekt. I **Inspector** för varje objekt kan du nu tilldela en bild till fältet **Item Icon** i `Collectible.cs`.

##### **Steg 2: Skapa en dynamisk UI-panel för att visa ikoner**
1. **Använd en UI Grid Layout:**
   - Markera din **InventoryPanel** och lägg till en **Grid Layout Group** i **Inspector**. Detta gör att ikonerna automatiskt placeras i ett rutnät.
   - Justera **Cell Size** för att passa storleken på dina objektikoner.

2. **Skapa en Prefab för inventarieobjekt:**
   - Skapa en ny UI-ikon: Högerklicka på **InventoryPanel** och välj **UI > Image**. Detta blir ett placeholder-element som representerar en insamlad ikon.
   - Justera bildstorleken och tilldela en bild (du kan tilldela en standardbild som ersätts senare när ett objekt plockas upp).
   - Dra denna **Image** från **Hierarchy** till **Assets**-mappen för att skapa en prefab. Namnge den "InventorySlot".

3. **Uppdatera Inventory Script:**
   - Vi ska nu uppdatera vårt `Inventory.cs`-skript för att skapa och lägga till ikoner i UI när spelaren plockar upp ett objekt. Lägg till följande kod i `Inventory.cs`:

```csharp
using System.Collections.Generic;
using UnityEngine;

public class Inventory : MonoBehaviour
{
    public List<GameObject> collectedItems = new List<GameObject>();
    public GameObject inventoryPanel;  // Panel där ikoner visas
    public GameObject inventorySlotPrefab;  // Prefab för ikoner

    public void AddItem(GameObject item)
    {
        collectedItems.Add(item);
        Debug.Log(item.name + " tillagd i inventariet.");

        // Skapa en ny ikon i UI
        GameObject newSlot = Instantiate(inventorySlotPrefab, inventoryPanel.transform);
        newSlot.GetComponent<UnityEngine.UI.Image>().sprite = item.GetComponent<Collectible>().itemIcon;  // Tilldela objektets bild
    }
}
```

4. **Koppla UI och prefabs i Unity:**
   - Gå tillbaka till Unity och markera **Player**. I **Inventory**-skriptet i **Inspector**, dra din **InventoryPanel** till fältet **Inventory Panel**, och dra **InventorySlot**-prefaben till **Inventory Slot Prefab**-fältet.
   - Nu ska det skapas en ikon i inventariet varje gång ett objekt plockas upp.

##### **Steg 3: Testa spelet**
- Starta spelet och plocka upp ett objekt. Nu ska en ikon för varje insamlat objekt dyka upp i inventariet på skärmen.

---

### **Del 2: Interaktion med objekt i inventariet (45 minuter)**

Nu när vi kan visa ikoner i inventariet, ska vi utveckla systemet så att spelaren kan **använda** eller **släppa** objekt från inventariet.

##### **Steg 1: Skapa en interaktionsfunktion**
1. **Uppdatera InventorySlot-prefaben:**
   - Gå till din **InventorySlot**-prefab och lägg till en **Button**-komponent till den.
   - I **Inspector** kan du ställa in vad som händer när spelaren klickar på ikonen. Vi kommer att skriva ett skript som hanterar detta senare.

2. **Skapa ett nytt skript för interaktion:**
   - Skapa ett nytt skript och kalla det "InventorySlot". Detta skript kommer att ligga på varje ikon och hantera vad som händer när spelaren interagerar med objektet.
   - Skriv följande kod:

```csharp
using UnityEngine;
using UnityEngine.UI;

public class InventorySlot : MonoBehaviour
{
    public GameObject item;  // Objektet som ikonen representerar
    private Button button;

    void Start()
    {
        button = GetComponent<Button>();
        button.onClick.AddListener(OnItemClicked);  // Lyssna efter klick på ikonen
    }

    // När spelaren klickar på ikonen
    void OnItemClicked()
    {
        Debug.Log("Använder " + item.name);
        // Här kan du lägga till logik för att använda objektet
        UseItem();
    }

    void UseItem()
    {
        // Exempel: om objektet är en nyckel, öppna en dörr
        // Detta kan skräddarsys beroende på objektets funktion
        Debug.Log(item.name + " användes.");
        // När objektet har använts kan det tas bort från inventariet
        Destroy(gameObject);
    }
}
```

3. **Koppla Collectible till InventorySlot:**
   - När du skapar en ikon i inventariet måste vi se till att den kopplas till rätt objekt.
   - Uppdatera `Inventory.cs`-skriptet så att varje slot också får en referens till det insamlade objektet:

```csharp
GameObject newSlot = Instantiate(inventorySlotPrefab, inventoryPanel.transform);
InventorySlot slotScript = newSlot.GetComponent<InventorySlot>();
slotScript.item = item;  // Kopplar objektet till sloten
newSlot.GetComponent<UnityEngine.UI.Image>().sprite = item.GetComponent<Collectible>().itemIcon;  // Tilldela objektets bild
```

##### **Steg 2: Lägg till fler objekt och funktionalitet**
1. **Skapa flera insamlingsbara objekt:**
   - Skapa fler objekt i spelet (t.ex. olika nycklar, potions, eller andra föremål) och ge dem olika bilder och funktioner. Detta ger dig en känsla för hur olika objekt kan fungera i spelet.

2. **Skapa en funktion för att släppa objekt:**
   - I `InventorySlot.cs` kan du också lägga till en knapp eller tangentbindning som låter spelaren släppa objekt från sitt inventarium.

```csharp
void DropItem()
{
    Debug.Log("Släpper " + item.name);
    // Släpp objektet tillbaka i spelet (placera det vid spelarens position eller en viss plats)
    item.gameObject.SetActive(true);
    item.transform.position = GameObject.FindGameObjectWithTag("Player").transform.position;
    Destroy(gameObject);  // Ta bort ikonen från inventariet
}
```

##### **Steg 3: Testa interaktionen**
- Starta spelet och plocka upp objekt. När du klickar på ikonen ska du se ett meddelande om att objektet används, och objektet kan tas bort från inventariet eller aktiveras tillbaka i spelet beroende på vad du implementerar.

---

### **Del 3: Förberedelse för nästa lektion (30 minuter)**

Nu har vi ett grundläggande system där spelaren kan plocka upp objekt, visa dem som ikoner i ett inventory, och interagera med dem. Vi kan vidareutveckla detta system i nästa lektion, till exempel:
- **Uppdatera interaktioner:** Gör så att varje objekt har unika interaktioner (t.ex. en nyckel kan öppna dörrar).
- **Användarvänliga inventarier:** Lägg till funktioner som att

 dra och släppa objekt mellan olika platser i inventariet.

---

### Nästa steg:
I nästa lektion kommer vi att:
- Lägga till specifika funktioner för vissa objekt, t.ex. att en nyckel kan öppna dörrar eller att en potion kan återställa hälsa.
- Utforska mer avancerad UI-hantering, såsom att dra och släppa objekt inom inventariet.

---

### Hemuppgift:
- Skapa fler insamlingsbara objekt och anpassa deras funktioner.
- Experimentera med olika ikoner och inventarielayouter för att skapa ett mer attraktivt användargränssnitt.

Vi är snart klara med ett fullt fungerande system för insamling och interaktion, och vi kan sedan fortsätta med mer avancerade funktioner i spelet!

[Dag 4](unity4.md)
