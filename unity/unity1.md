Här kommer en första tvåtimmarslektion som introducerar dig till Unity och hur du kan börja skapa ett enkelt spel där en bild (karaktär) rör sig i två dimensioner och kan plocka upp ett objekt. Vi kommer också att gå igenom grunderna i Unitys användargränssnitt och hur du hanterar rörelser.

### Lektion 1: Introduktion till Unity och grundläggande rörelse i 2D

#### **Del 1: Introduktion till Unity-gränssnittet (30 minuter)**

1. **Öppna Unity och skapa ett nytt projekt:**
   - Öppna Unity Hub och skapa ett nytt 2D-projekt. Ge projektet ett namn (t.ex. "2D Collectible Game") och välj platsen där du vill spara det.
   - Se till att projektet är inställt på "2D" eftersom vi ska arbeta med tvådimensionella spelmekaniker.

2. **Utforska Unity-gränssnittet:**
   - **Scene View**: Här skapar du och ser ditt spel. Detta är arbetsområdet där du placerar dina objekt (sprites, karaktärer, bakgrunder, etc.).
   - **Game View**: Här ser du hur spelet kommer att se ut när det spelas.
   - **Hierarchy**: Visar alla objekt (GameObjects) i din scen.
   - **Inspector**: Visar egenskaperna för det valda objektet. Här kan du justera position, storlek, material, och lägga till komponenter.
   - **Project**: Här finns alla filer och resurser i ditt projekt (bilder, ljud, skript, etc.).

#### **Del 2: Skapa en enkel sprite och röra den i två dimensioner (1 timme)**

##### **Steg 1: Importera en sprite**
1. **Importera bilder:**
   - Hämta eller skapa en enkel bild (sprite) för din spelkaraktär. Du kan använda en kvadrat eller en cirkel för enkelhets skull.
   - Dra och släpp bilden från din dator till **Assets**-mappen i Unity.

2. **Skapa en GameObject för din karaktär:**
   - Högerklicka i **Hierarchy** och välj **Create Empty**.
   - Namnge det nya objektet till "Player".
   - Dra och släpp din sprite till **Player**-objektet i **Inspector** under **Sprite Renderer**.

##### **Steg 2: Lägg till en Rigidbody2D**
1. **Komponenter för fysisk simulation:**
   - Markera din karaktär i **Hierarchy** och klicka på **Add Component** i **Inspector**.
   - Sök efter **Rigidbody2D** och lägg till det. Detta gör att din karaktär får fysik i två dimensioner, vilket betyder att den påverkas av gravitation och kan kollidera med andra objekt.

2. **Justera Rigidbody2D:**
   - I **Inspector**, under **Rigidbody2D**, ändra **Gravity Scale** till 0. Vi vill inte att karaktären ska falla neråt, utan bara röra sig horisontellt och vertikalt.

##### **Steg 3: Skript för att röra karaktären**
1. **Skapa ett nytt skript:**
   - Högerklicka på **Assets**-mappen och välj **Create > C# Script**. Namnge skriptet "PlayerMovement".
   - Dubbelklicka på skriptet för att öppna det i din valda kodredigerare (Visual Studio eller Visual Studio Code).

2. **Skriv ett enkelt skript för rörelse:**
   - I `PlayerMovement`-skriptet, skriv följande kod för att få din karaktär att röra sig:

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float moveSpeed = 5f;
    public Rigidbody2D rb;

    Vector2 movement;

    // Update körs en gång per bildruta (frame)
    void Update()
    {
        // Få input från användaren (piltangenter eller WASD)
        movement.x = Input.GetAxisRaw("Horizontal"); // Rörelse längs X-axeln
        movement.y = Input.GetAxisRaw("Vertical");   // Rörelse längs Y-axeln
    }

    // FixedUpdate körs en gång per fast tidsintervall, perfekt för fysik
    void FixedUpdate()
    {
        // Flytta spelaren med hjälp av Rigidbody2D
        rb.MovePosition(rb.position + movement * moveSpeed * Time.fixedDeltaTime);
    }
}
```

3. **Lägg till skriptet till din spelare:**
   - Gå tillbaka till Unity och dra skriptet till din **Player** i **Inspector**.
   - Dra också din `Rigidbody2D`-komponent till skriptets **Rigidbody2D**-fält i **Inspector**.

4. **Testa spelet:**
   - Tryck på **Play** och använd piltangenterna eller WASD för att röra karaktären i två dimensioner.

#### **Del 3: Förberedelse för att plocka upp objekt (30 minuter)**

##### **Steg 1: Skapa ett objekt att plocka upp**
1. **Importera en sprite för ett objekt:**
   - Hämta eller skapa en sprite för ett objekt som din karaktär ska plocka upp (t.ex. en nyckel eller ett mynt).
   - Dra in bilden i **Assets**-mappen.

2. **Skapa en GameObject för objektet:**
   - I **Hierarchy**, högerklicka och välj **Create Empty**.
   - Namnge det till "Collectible".
   - Lägg till en **Sprite Renderer** och dra din nyckel- eller myntbild till den.

3. **Lägg till en Collider2D:**
   - Klicka på **Add Component** i **Inspector** för objektet och lägg till en **Circle Collider 2D** (eller en annan form som passar objektet). Detta låter Unity upptäcka när din karaktär kolliderar med objektet.

##### **Steg 2: Förbered pickup-mekanism**
1. **Lägg till ett tagg för spelaren:**
   - Markera **Player**-objektet, och i **Inspector**, välj **Tag > Player** eller skapa en ny tagg om det inte finns.
   - Detta gör att vi kan känna igen karaktären i koden.

2. **Lägg till ett skript för att plocka upp objektet:**
   - Skapa ett nytt skript och kalla det för "Collectible". Lägg till det till objektet och skriv följande kod:

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            // För närvarande, när spelaren plockar upp objektet, förstör vi det
            Destroy(gameObject);
        }
    }
}
```

3. **Justera Collider2D för trigger:**
   - Se till att "Is Trigger" är markerat i din **Collider2D**-komponent så att objektet registrerar kollisionen utan att stoppa karaktärens rörelse.

---

### Nästa steg:
Under nästa lektion kommer vi att:
- Lära oss att hantera ett enkelt inventariesystem där objekt som plockas upp visas i ett UI-element.
- Utveckla vidare vår pickup-mekanism så att objektet inte förstörs, utan istället lagras i ett inventory.

---

### Hemuppgift:
- Experimentera med att lägga till flera objekt i scenen som kan plockas upp.
- Justera karaktärens hastighet i **Inspector** för att känna hur spelet reagerar.

Lektionerna kommer stegvis att bygga upp spelet. Fortsätt träna på det vi gått igenom, så är du redo för nästa steg!

[Dag 2](unity2.md)
