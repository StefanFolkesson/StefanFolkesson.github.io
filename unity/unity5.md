Här kommer nästa tvåtimmarslektion, där vi tar vårt projekt vidare genom att lägga till **mer avancerad interaktion mellan objekt**, exempelvis att kombinera objekt eller använda dem för att påverka spelvärlden (t.ex. vapen och fiender). Vi kommer också att förbättra vår **UI-upplevelse** och lägga till visuella effekter för att ge spelaren bättre feedback.

### Lektion 5: Avancerad interaktion och dynamiskt användargränssnitt

---

### **Del 1: Skapa vapen och fiender för interaktion (1 timme)**

I denna del kommer vi att skapa ett vapen som spelaren kan använda för att attackera fiender. Vi kommer även att implementera grundläggande fiendelogik där fiender tar skada och till slut försvinner när de blir besegrade.

##### **Steg 1: Skapa en fiende**

1. **Skapa en fiendesprite:**
   - Skapa en enkel sprite för din fiende (t.ex. en cirkel eller en figur) och dra in den i Unity.
   - Högerklicka i **Hierarchy** och välj **Create Empty** för att skapa en GameObject för fienden. Namnge det "Enemy".
   - Dra din fiendesprite till detta objekt så att det representerar fienden visuellt.

2. **Lägg till en Collider och Rigidbody2D:**
   - Lägg till en **Box Collider 2D** eller **Circle Collider 2D** på fienden så att den kan kollidera med spelaren eller andra objekt.
   - Lägg också till en **Rigidbody2D** och ställ in **Gravity Scale** till 0 så att fienden inte påverkas av gravitationen.

3. **Skapa ett skript för fiendens hälsa och logik:**
   - Skapa ett nytt skript som heter `Enemy` och skriv följande kod för att hantera fiendens hälsa och hur den reagerar på attacker:

```csharp
using UnityEngine;

public class Enemy : MonoBehaviour
{
    public int maxHealth = 50;
    private int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
    }

    // Denna metod kallas när fienden tar skada
    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        if (currentHealth <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log("Fienden är besegrad!");
        // Lägg till effekter här (t.ex. explosioner, ljud)
        Destroy(gameObject);  // Ta bort fienden från scenen
    }
}
```

##### **Steg 2: Skapa ett vapen**

1. **Skapa ett vapenobjekt:**
   - Skapa en sprite för ditt vapen (t.ex. ett svärd eller en annan ikon).
   - Dra den in i **Assets** och skapa ett nytt GameObject i scenen, namnge det "Weapon".
   - Lägg till en **Box Collider 2D** för att hantera kollisioner och markera "Is Trigger".

2. **Lägg till vapenlogik:**
   - Skapa ett nytt skript som heter `Weapon` och lägg till det på vapnet:

```csharp
using UnityEngine;

public class Weapon : MonoBehaviour
{
    public int damage = 20;  // Skadan som vapnet gör

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Enemy"))
        {
            Enemy enemy = other.GetComponent<Enemy>();
            if (enemy != null)
            {
                enemy.TakeDamage(damage);  // Applicera skada på fienden
                Debug.Log("Fienden tog skada!");
            }
        }
    }
}
```

##### **Steg 3: Ge spelaren möjlighet att använda vapnet**

1. **Använda vapnet från inventariet:**
   - Uppdatera ditt `InventorySlot.cs`-skript så att spelaren kan använda vapnet på fiender. Lägg till en logik där vapnet aktiveras när spelaren klickar på det i inventariet.

```csharp
void UseItem()
{
    if (item.name == "Sword")  // Om objektet är ett svärd
    {
        Debug.Log("Vapnet har aktiverats!");
        // Här kan du aktivera vapnet för att kunna attackera fiender
        GameObject weapon = GameObject.Find("Weapon");
        if (weapon != null)
        {
            weapon.SetActive(true);  // Aktivera vapnet i spelet
        }
    }
    // Om vapnet används, kan vi behålla det eller ta bort det från inventariet beroende på spelets regler
}
```

2. **Placera vapnet nära spelaren:**
   - Placera vapnet i scenen nära spelaren och se till att det är osynligt från början genom att markera det som inaktivt i **Inspector** (avmarkera "Active" vid start).

3. **Testa vapnet:**
   - Starta spelet, plocka upp vapnet i inventariet och använd det för att attackera fiender när du går i närheten av dem.

---

### **Del 2: Förbättra UI och ge feedback till spelaren (1 timme)**

Nu när vi har grundläggande funktioner för fiender och vapen ska vi lägga till bättre visuella och användarmässiga feedbacksystem, så att spelaren får bättre information om vad som händer.

##### **Steg 1: Lägg till feedback för hälsa och skada**

1. **Använd visuell feedback för att visa när fiender tar skada:**
   - Du kan använda Unitys färgförändringssystem för att kort ändra fiendens färg när den tar skada. Uppdatera `Enemy`-skriptet så här:

```csharp
IEnumerator FlashRed()
{
    SpriteRenderer renderer = GetComponent<SpriteRenderer>();
    if (renderer != null)
    {
        renderer.color = Color.red;  // Ändra färg till röd
        yield return new WaitForSeconds(0.1f);  // Vänta en kort stund
        renderer.color = Color.white;  // Återställ till ursprungsfärgen
    }
}

public void TakeDamage(int damage)
{
    currentHealth -= damage;
    StartCoroutine(FlashRed());  // Lägg till visuell feedback när fienden tar skada

    if (currentHealth <= 0)
    {
        Die();
    }
}
```

2. **Lägg till ljudfeedback vid skada:**
   - Du kan också lägga till ljudklipp som spelas när fienden tar skada eller när den besegras. Skapa en **AudioSource** på fienden och lägg till ljudfiler i **Assets**.

##### **Steg 2: Förbättra UI för inventariet**

1. **Lägg till hover-effekter på inventarieobjekten:**
   - Uppdatera dina **InventorySlot**-prefabs för att inkludera hover-effekter, så att spelaren ser tydligt vilket objekt som är valt. Du kan göra detta genom att lägga till en färgändring eller en liten skaländring när muspekaren är över objektet.

```csharp
void OnMouseEnter()
{
    transform.localScale = new Vector3(1.1f, 1.1f, 1.1f);  // Förstora något när muspekaren är över objektet
}

void OnMouseExit()
{
    transform.localScale = Vector3.one;  // Återställ till ursprunglig storlek
}
```

2. **Visa objektbeskrivningar:**
   - Skapa ett UI-textfält under din inventariepanel som kan visa en kort beskrivning av varje objekt när muspekaren svävar över dem.

```csharp
void OnMouseEnter()
{
    // Visa en kort beskrivning av objektet
    descriptionText.text = "Detta är ett " + item.name;
}

void OnMouseExit()
{
    descriptionText.text = "";  // Töm texten när muspekaren lämnar objektet
}
```

##### **Steg 3: Lägg till feedback för när spelaren tar skada**

1. **Spelaren tar skada när den träffas av fiender:**
   - Du kan göra så att spelaren tar skada när den kolliderar med en fiende. Uppdatera `Player`- eller `HealthManager`-skriptet för att minska hälsan när en fiende rör spelaren:

```csharp
void OnTriggerEnter2D(Collider2D other)
{
    if (other.CompareTag("Enemy"))
    {
        // Spelaren tar skada när fienden kolliderar
        TakeDamage(10);  // Minska hälsan med 10
    }
}
```

2. **Lägg till en skärmeffekt vid skada:**
   - Du kan lägga till en enkel visuell effekt där skärmen kort blir röd för att indikera att spelaren har tagit skada. Skapa ett UI-element som täcker hela skärmen, och ändra dess transparens när spelaren tar skada.

```csharp
public Image damageOverlay;
public void FlashDamageOverlay()
{
    StartCoroutine(ShowDamageOverlay());
}

IEnumerator ShowDamageOverlay()
{
    damage

Overlay.color = new Color(1, 0, 0, 0.5f);  // Halvtransparent röd
    yield return new WaitForSeconds(0.2f);  // Visa i 0.2 sekunder
    damageOverlay.color = new Color(1, 0, 0, 0);  // Återställ transparens
}
```

---

### **Del 3: Förberedelse för nästa lektion (30 minuter)**

Nästa lektion kan vi utveckla spelet vidare genom att lägga till mer avancerad fiende-AI, samt kanske även implementera nivåsystem eller utmaningar. Vi kan också fortsätta arbeta med animationer och förbättring av spelupplevelsen.

---

### Nästa steg:
I nästa lektion kommer vi att:
- Implementera ett system för fiende-AI och utmana spelaren med mer komplexa fiender.
- Lära oss att skapa animationer för karaktärer och fiender.
- Introducera nivådesign och progression, så att spelaren kan avancera genom olika nivåer i spelet.

---

### Hemuppgift:
- Experimentera med att skapa olika fiendetyper och se till att de interagerar med spelaren och vapnen på olika sätt.
- Förbättra spelets UI och visuell feedback för att göra spelet mer engagerande och responsivt.

Vi är på god väg att skapa ett komplett spel med interaktiva objekt, fiender och ett funktionellt inventariesystem!

[Dag 6](unity6.md)
