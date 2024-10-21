Här kommer nästa tvåtimmarslektion där vi tar vårt spel ett steg vidare. I denna lektion kommer vi att:
1. Lägga till specifika funktioner för vissa objekt, t.ex. en nyckel som kan öppna dörrar eller en potion som återställer hälsa.
2. Lägga till drag-och-släpp-funktionalitet i inventariet för att hantera objekt mer dynamiskt.

### Lektion 4: Objektinteraktion och drag-och-släpp i inventariet

---

### **Del 1: Lägga till objektinteraktion (1 timme)**

Nu ska vi göra så att insamlade objekt kan användas till specifika ändamål. Till exempel kan en nyckel användas för att öppna en dörr, eller en potion kan användas för att återställa spelarens hälsa.

##### **Steg 1: Skapa en dörr som kan öppnas med en nyckel**

1. **Skapa en dörr i spelet:**
   - Skapa en enkel sprite eller använd en fyrkant för att representera en dörr. Namnge objektet "Door".
   - Lägg till en **Box Collider 2D** till dörren och markera "Is Trigger" i **Inspector** så att spelaren kan interagera med dörren.

2. **Skapa ett Door-skript:**
   - Skapa ett nytt skript som heter `Door` och skriv följande kod för att låta spelaren öppna dörren när de har nyckeln:

```csharp
using UnityEngine;

public class Door : MonoBehaviour
{
    public bool isLocked = true;  // Dörren är låst tills spelaren använder en nyckel

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Inventory playerInventory = other.GetComponent<Inventory>();

            // Kolla om spelaren har en nyckel
            if (playerInventory != null)
            {
                foreach (var item in playerInventory.collectedItems)
                {
                    if (item.name == "Key")  // Kontrollera om det insamlade objektet är en nyckel
                    {
                        isLocked = false;  // Lås upp dörren
                        Debug.Log("Dörren är nu öppen!");
                        OpenDoor();
                        return;  // Sluta leta efter fler objekt efter att nyckeln har använts
                    }
                }
            }
        }
    }

    void OpenDoor()
    {
        // Här kan du lägga till animationer eller dölja dörren
        gameObject.SetActive(false);  // Dölj dörren för att simulera att den öppnas
    }
}
```

3. **Lägg till Door-skriptet på dörren:**
   - Gå tillbaka till Unity och lägg till `Door`-skriptet på din dörr i **Inspector**.

4. **Justera nyckelobjektet:**
   - Se till att nyckelobjektet i spelet har namnet "Key" så att det matchar i koden. Detta kan du justera i **Hierarchy** genom att klicka på nyckelobjektet och redigera dess namn.

##### **Steg 2: Skapa en potion som återställer hälsa**

1. **Skapa en hälsobar:**
   - I spelet kan du skapa en hälsobar som visuellt representerar spelarens hälsa. Gör så här:
     - Skapa en ny **Canvas** (om du inte redan har en) genom att högerklicka i **Hierarchy** och välja **UI > Canvas**.
     - Skapa ett nytt **UI > Slider**-element inuti Canvasen och placera det någonstans synligt på skärmen. Detta blir vår hälsobar.
     - Ställ in **Max Value** till 100 och **Current Value** till 100 (representerar fullt liv).

2. **Skapa ett HealthManager-skript:**
   - Skapa ett nytt skript som heter `HealthManager` och lägg till det till spelaren. Detta skript kommer att hantera spelarens hälsa:

```csharp
using UnityEngine;
using UnityEngine.UI;

public class HealthManager : MonoBehaviour
{
    public Slider healthBar;
    public int maxHealth = 100;
    public int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
        UpdateHealthBar();
    }

    public void TakeDamage(int amount)
    {
        currentHealth -= amount;
        if (currentHealth < 0)
            currentHealth = 0;

        UpdateHealthBar();
    }

    public void Heal(int amount)
    {
        currentHealth += amount;
        if (currentHealth > maxHealth)
            currentHealth = maxHealth;

        UpdateHealthBar();
    }

    void UpdateHealthBar()
    {
        healthBar.value = currentHealth;
    }
}
```

3. **Lägg till HealthManager till spelaren:**
   - Lägg till `HealthManager`-skriptet på din **Player** och dra din hälsobar (Slider) till skriptets **Health Bar**-fält i **Inspector**.

4. **Lägg till funktionalitet för att använda potion:**
   - Uppdatera ditt `InventorySlot.cs`-skript så att en potion kan återställa spelarens hälsa när den används:

```csharp
void UseItem()
{
    if (item.name == "Potion")  // Kontrollera om objektet är en potion
    {
        HealthManager healthManager = GameObject.FindGameObjectWithTag("Player").GetComponent<HealthManager>();
        if (healthManager != null)
        {
            healthManager.Heal(20);  // Återställ 20 enheter hälsa
            Debug.Log("Potion användes! Hälsa återställd.");
        }
    }

    // Ta bort objektet från inventariet efter användning
    Destroy(gameObject);
}
```

##### **Steg 3: Testa interaktionerna**

- **Testa dörren:** När spelaren har plockat upp nyckeln ska de kunna öppna dörren.
- **Testa potion:** När spelaren använder en potion ska deras hälsa återställas.

---

### **Del 2: Drag-och-släpp i inventariet (1 timme)**

Nu ska vi lägga till möjligheten för spelaren att flytta objekt runt i sitt inventory med en **drag-och-släpp**-funktion. Detta gör att vi kan hantera objekt mer dynamiskt och ordna dem i olika slots.

##### **Steg 1: Förbered inventariet för drag-och-släpp**

1. **Lägg till en ny panel för att visa slots:**
   - I din **InventoryPanel**, se till att du har flera slots (t.ex. genom att duplicera din **InventorySlot**-prefab). Varje slot ska kunna fyllas med ett objekt när spelaren släpper ett objekt på det.

2. **Skapa ett DragHandler-skript:**
   - Skapa ett nytt skript som heter `DragHandler`. Detta skript kommer att hantera drag-och-släpp av objekt i UI:

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

public class DragHandler : MonoBehaviour, IBeginDragHandler, IDragHandler, IEndDragHandler
{
    private RectTransform rectTransform;
    private CanvasGroup canvasGroup;

    void Awake()
    {
        rectTransform = GetComponent<RectTransform>();
        canvasGroup = GetComponent<CanvasGroup>();
    }

    public void OnBeginDrag(PointerEventData eventData)
    {
        canvasGroup.alpha = 0.6f;  // Gör ikonen halvtransparent under drag
        canvasGroup.blocksRaycasts = false;  // Låt ikonen ignoreras under drag
    }

    public void OnDrag(PointerEventData eventData)
    {
        rectTransform.anchoredPosition += eventData.delta / transform.lossyScale;
    }

    public void OnEndDrag(PointerEventData eventData)
    {
        canvasGroup.alpha = 1f;
        canvasGroup.blocksRaycasts = true;  // Återställ efter släpp
    }
}
```

3. **Lägg till `DragHandler` till dina inventoryslots:**
   - Gå till din **InventorySlot**-prefab och lägg till `DragHandler` som komponent.
   - För att detta ska fungera korrekt behöver varje slot en **CanvasGroup** och en **RectTransform**, så se till att dessa komponenter är tillagda (Unity lägger till dem automatiskt om de saknas).

##### **Steg 2: Släppa objekt på andra slots**

1. **Skapa ett DropHandler-skript:**
   - För att kunna släppa objekt i andra slots, behöver vi ett nytt skript som heter `DropHandler`:

```csharp
using UnityEngine;
using UnityEngine.EventSystems;

public class DropHandler : MonoBehaviour, IDropHandler
{
    public void OnDrop(PointerEventData eventData)
    {
        // Detta kallas när ett objekt släpps på en annan slot
        Debug.Log("Objekt släppt i slotten.");

        if (eventData.pointerDrag != null)
        {
            // Flytta det dragna objektet till denna slots position
            eventData.pointerDrag.GetComponent<RectTransform>().anchoredPosition = GetComponent<RectTransform>().anchoredPosition;
        }
    }
}
```

2

. **Lägg till `DropHandler` till varje slot:**
   - Gå tillbaka till Unity och lägg till `DropHandler`-skriptet till alla dina **InventorySlot**-prefabs.

##### **Steg 3: Testa drag-och-släpp**

- **Starta spelet** och plocka upp några objekt.
- Du ska nu kunna klicka på objekt i inventariet, dra dem och släppa dem på olika slots i ditt inventariesystem.

---

### **Del 3: Förberedelse för nästa lektion (30 minuter)**

I nästa lektion kan vi bygga vidare på systemet genom att:
- Skapa olika typer av objekt med mer komplexa interaktioner (t.ex. vapen som kan användas för att attackera fiender).
- Utveckla ett system där objekt kan ha olika statusar (t.ex. slitage, användningsbegränsningar).
- Lägga till feedback och animationer för mer dynamiska interaktioner.

---

### Nästa steg:
I nästa lektion kommer vi att:
- Implementera mer avancerad interaktion mellan objekt, som att kombinera objekt eller använda dem för att påverka omgivningen (t.ex. vapen och fiender).
- Fortsätta förbättra vårt UI för en mer användarvänlig upplevelse.

---

### Hemuppgift:
- Skapa fler typer av objekt (nycklar, potions, etc.) med olika funktioner och logik för att interagera med spelet.
- Förbättra drag-och-släpp-funktionaliteten genom att anpassa slots och inventarielayout.

Vi fortsätter att bygga upp spelet med fler funktioner och interaktionsmöjligheter, vilket gör det både mer komplext och intressant!
