Här kommer nästa tvåtimmarslektion, där vi fokuserar på att implementera **mer avancerade spelmekaniker** som **power-ups**, **fällor** och olika typer av utmaningar för att skapa mer djup i spelet. Vi kommer även börja titta på hur vi kan **spara spelarens framsteg** och hantera **spelstatistik** som poäng och högsta poäng.

### Lektion 7: Power-ups, fällor och spelstatistik

---

### **Del 1: Implementera power-ups (1 timme)**

Power-ups är objekt som ger spelaren speciella förmågor eller bonusar under spelets gång, som ökad hälsa, hastighet eller styrka. Vi kommer nu att skapa några enkla power-ups och se till att de påverkar spelaren när de plockas upp.

##### **Steg 1: Skapa ett Power-up-objekt**

1. **Skapa en power-up sprite:**
   - Skapa eller hämta en enkel sprite för en power-up (t.ex. en hastighetssko, en sköld eller ett hjärta).
   - Dra in bilden till **Assets** och skapa ett nytt GameObject i scenen, namnge det "PowerUp".

2. **Lägg till en Collider och Trigger:**
   - Lägg till en **Box Collider 2D** eller **Circle Collider 2D** på PowerUp-objektet och markera "Is Trigger" i **Inspector** så att spelaren kan plocka upp power-upen när de kolliderar med den.

##### **Steg 2: Skapa PowerUp-skript**

1. **Skapa ett PowerUp-skript:**
   - Skapa ett nytt skript som heter `PowerUp`. Detta skript kommer att definiera hur power-ups fungerar och vad de gör för spelaren:

```csharp
using UnityEngine;

public class PowerUp : MonoBehaviour
{
    public enum PowerUpType { Health, Speed, Strength }
    public PowerUpType powerUpType;  // Typ av power-up
    public float powerUpDuration = 5f;  // Hur länge power-upen varar (om tillämpligt)

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            PlayerController player = other.GetComponent<PlayerController>();  // Referens till spelarens skript

            if (player != null)
            {
                ApplyPowerUp(player);
                Destroy(gameObject);  // Ta bort power-upen efter att den plockats upp
            }
        }
    }

    void ApplyPowerUp(PlayerController player)
    {
        switch (powerUpType)
        {
            case PowerUpType.Health:
                player.IncreaseHealth(20);  // Öka spelarens hälsa med 20
                break;
            case PowerUpType.Speed:
                StartCoroutine(player.IncreaseSpeed(powerUpDuration));  // Öka spelarens hastighet tillfälligt
                break;
            case PowerUpType.Strength:
                StartCoroutine(player.IncreaseStrength(powerUpDuration));  // Öka spelarens skada tillfälligt
                break;
        }
    }
}
```

2. **Tilldela PowerUp-skriptet till PowerUp-objektet:**
   - Gå tillbaka till Unity och tilldela `PowerUp`-skriptet till ditt PowerUp-objekt. I **Inspector** kan du nu välja vilken typ av power-up det är (Health, Speed eller Strength).

##### **Steg 3: Hantera Power-ups i PlayerController**

1. **Uppdatera spelarens skript:**
   - Öppna ditt **PlayerController**-skript och lägg till funktioner för att hantera olika power-ups:

```csharp
public class PlayerController : MonoBehaviour
{
    public float speed = 5f;
    public int maxHealth = 100;
    private int currentHealth;
    public int damage = 10;

    void Start()
    {
        currentHealth = maxHealth;
    }

    public void IncreaseHealth(int amount)
    {
        currentHealth += amount;
        if (currentHealth > maxHealth)
        {
            currentHealth = maxHealth;
        }
        Debug.Log("Hälsan ökade med " + amount);
    }

    public IEnumerator IncreaseSpeed(float duration)
    {
        speed *= 2;  // Fördubbla hastigheten
        Debug.Log("Hastigheten ökade!");
        yield return new WaitForSeconds(duration);  // Vänta tills power-upen tar slut
        speed /= 2;  // Återställ hastigheten
        Debug.Log("Hastigheten återställd.");
    }

    public IEnumerator IncreaseStrength(float duration)
    {
        damage *= 2;  // Fördubbla spelarens skada
        Debug.Log("Skadan ökade!");
        yield return new WaitForSeconds(duration);
        damage /= 2;  // Återställ skadan
        Debug.Log("Skadan återställd.");
    }
}
```

2. **Testa power-ups:**
   - Placera PowerUp-objekt i scenen och testa att spelaren kan plocka upp dem. När spelaren plockar upp power-ups ska deras effekt aktiveras (t.ex. ökad hastighet eller hälsa).

---

### **Del 2: Skapa fällor och utmaningar (1 timme)**

Fällor och utmaningar gör spelet mer spännande genom att sätta hinder i spelarens väg. Vi kommer nu att skapa några enkla fällor som minskar spelarens hälsa eller orsakar andra problem när de aktiveras.

##### **Steg 1: Skapa en fälla**

1. **Skapa en fällesprite:**
   - Skapa en enkel sprite som representerar en fälla (t.ex. en spikmatta eller en fallande sten).
   - Dra in bilden till **Assets** och skapa ett nytt GameObject, namnge det "Trap".

2. **Lägg till en Collider och Trigger:**
   - Lägg till en **Box Collider 2D** på fällan och markera "Is Trigger" så att fällan aktiveras när spelaren går över den.

##### **Steg 2: Skapa ett Trap-skript**

1. **Skapa ett Trap-skript:**
   - Skapa ett nytt skript som heter `Trap`. Detta skript kommer att hantera vad som händer när spelaren aktiverar fällan.

```csharp
using UnityEngine;

public class Trap : MonoBehaviour
{
    public int damage = 20;  // Hur mycket skada fällan gör

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            PlayerController player = other.GetComponent<PlayerController>();
            if (player != null)
            {
                player.TakeDamage(damage);  // Spelaren tar skada från fällan
                Debug.Log("Spelaren träffades av en fälla och tog " + damage + " skada!");
            }
        }
    }
}
```

2. **Uppdatera spelarens skript för att hantera skada:**

```csharp
public void TakeDamage(int amount)
{
    currentHealth -= amount;
    if (currentHealth <= 0)
    {
        currentHealth = 0;
        Die();  // Hantera spelarens död
    }
    Debug.Log("Spelaren tog " + amount + " skada. Nuvarande hälsa: " + currentHealth);
}

void Die()
{
    Debug.Log("Spelaren dog!");
    // Här kan du lägga till logik för att återställa spelet eller gå tillbaka till huvudmenyn
}
```

3. **Testa fällan:**
   - Placera fällor i din scen och testa hur spelaren tar skada när de går över fällorna. Lägg till flera olika typer av fällor för att skapa varierade utmaningar.

##### **Steg 3: Skapa dynamiska fällor**

1. **Skapa en fälla som rör sig:**
   - Du kan skapa fällor som rör sig fram och tillbaka, eller faller ner på spelaren. Uppdatera fällans logik för att göra den mer dynamisk:

```csharp
public class MovingTrap : MonoBehaviour
{
    public Transform pointA;  // Startpunkt
    public Transform pointB;  // Slutpunkt
    public float speed = 2f;
    private bool movingToB = true;

    void Update()
    {
        if (movingToB)
        {
            transform.position = Vector2.MoveTowards(transform.position, pointB.position, speed * Time.deltaTime);
            if (Vector2.Distance(transform.position, pointB.position) < 0.1f)
            {
                movingToB = false;
            }
        }
        else
        {
            transform.position = Vector2.MoveTowards(transform.position, pointA.position, speed * Time.deltaTime);
            if (Vector2.Distance(transform.position, pointA.position) < 0.1f)
            {
                movingToB = true;
            }
        }
    }
}
```

2. **Testa dynamiska fällor:**
   - Placera fällor som rör sig i scenen och testa hur spelaren kan undvika dem genom att röra sig taktiskt.

---

### **Del 3: Hantera spelstatistik och spara spelarens framsteg (30 minuter)**



Nu ska vi lägga till funktioner för att **spara spelarens framsteg** och hantera statistik, som poäng och högsta poäng. Detta gör spelet mer engagerande och ger spelaren mål att sträva mot.

##### **Steg 1: Spara och ladda spelarens poäng**

1. **Skapa ett ScoreManager-skript:**
   - Skapa ett nytt skript som heter `ScoreManager`. Detta skript kommer att hantera spelarens poäng och spara dem mellan olika spelsessioner:

```csharp
using UnityEngine;

public class ScoreManager : MonoBehaviour
{
    public int score = 0;
    public int highScore = 0;

    void Start()
    {
        // Ladda högsta poängen från tidigare sessioner
        highScore = PlayerPrefs.GetInt("HighScore", 0);
    }

    public void AddScore(int points)
    {
        score += points;
        if (score > highScore)
        {
            highScore = score;
            PlayerPrefs.SetInt("HighScore", highScore);  // Spara högsta poängen
        }
        Debug.Log("Nuvarande poäng: " + score + ", Högsta poäng: " + highScore);
    }

    void OnApplicationQuit()
    {
        PlayerPrefs.Save();  // Se till att poängen sparas när spelet avslutas
    }
}
```

2. **Anropa ScoreManager i spelet:**
   - När spelaren besegrar fiender eller klarar utmaningar, kan du använda `ScoreManager` för att öka spelarens poäng:

```csharp
public class Enemy : MonoBehaviour
{
    public int scoreValue = 100;  // Poängen som spelaren får när fienden besegras

    void Die()
    {
        ScoreManager scoreManager = FindObjectOfType<ScoreManager>();
        if (scoreManager != null)
        {
            scoreManager.AddScore(scoreValue);  // Öka spelarens poäng
        }
        Destroy(gameObject);
    }
}
```

##### **Steg 2: Spara och ladda spelarens framsteg**

1. **Spara spelarens nivå:**
   - När spelaren når en ny nivå kan vi spara den i **PlayerPrefs**:

```csharp
public void SaveProgress(int currentLevel)
{
    PlayerPrefs.SetInt("CurrentLevel", currentLevel);  // Spara aktuell nivå
    PlayerPrefs.Save();
}

public int LoadProgress()
{
    return PlayerPrefs.GetInt("CurrentLevel", 1);  // Ladda aktuell nivå (standard 1 om inget sparat)
}
```

2. **Ladda nästa nivå:**
   - När spelaren når en viss nivå eller klarar ett mål kan vi ladda nästa nivå och spara framstegen:

```csharp
void OnLevelComplete()
{
    SaveProgress(currentLevel + 1);
    SceneManager.LoadScene("Level" + (currentLevel + 1));
}
```

---

### Nästa lektion:
I nästa lektion kommer vi att:
- Implementera ett system för **att återuppta spelet från där spelaren senast slutade**.
- Utveckla **power-up-systemet** vidare och lägga till mer komplexa spelfunktioner.
- Fortsätta arbeta med att balansera svårighetsgrad och skapa fler nivåer.

---

### Hemuppgift:
- Experimentera med att skapa fler power-ups och fällor för att lägga till mer variation i spelet.
- Fortsätt arbeta med spelets progression och testa olika poängsystem.

Vi bygger nu upp ett spel med fler interaktiva element och ett mer engagerande spelupplägg!

[Dag 8](unity8.md)
