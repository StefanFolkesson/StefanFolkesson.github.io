Här kommer nästa tvåtimmarslektion, där vi fokuserar på att implementera **fiende-AI** och introducera **animationer** för att skapa ett mer dynamiskt och engagerande spel. Vi kommer även börja fundera på nivådesign och progression i spelet.

### Lektion 6: Fiende-AI, animationer och nivådesign

---

### **Del 1: Implementera fiende-AI (1 timme)**

Nu ska vi ge fienderna ett mer dynamiskt beteende genom att implementera AI, så att de kan följa och attackera spelaren. Vi kommer även att lägga till enkel "patrulleringslogik" där fienderna rör sig mellan olika punkter.

##### **Steg 1: Skapa grundläggande AI för fiender**

1. **Skapa ett EnemyAI-skript:**
   - Skapa ett nytt skript och kalla det `EnemyAI`. Detta skript kommer att hantera fiendens beteende, som att följa spelaren eller patrullera mellan punkter.

```csharp
using UnityEngine;

public class EnemyAI : MonoBehaviour
{
    public float speed = 2f;  // Fiendens hastighet
    public float detectionRange = 5f;  // Hur nära spelaren måste vara för att fienden ska börja följa
    private Transform player;  // Referens till spelarens position

    void Start()
    {
        // Hitta spelaren genom dess tagg
        player = GameObject.FindGameObjectWithTag("Player").transform;
    }

    void Update()
    {
        // Kolla avståndet mellan spelaren och fienden
        float distanceToPlayer = Vector2.Distance(transform.position, player.position);

        if (distanceToPlayer < detectionRange)
        {
            // Följ spelaren om den är inom räckhåll
            FollowPlayer();
        }
    }

    void FollowPlayer()
    {
        // Flytta fienden mot spelarens position
        Vector2 direction = (player.position - transform.position).normalized;
        transform.position = Vector2.MoveTowards(transform.position, player.position, speed * Time.deltaTime);
    }
}
```

2. **Lägg till EnemyAI-skriptet till fienderna:**
   - Gå tillbaka till Unity och markera dina fiender i **Hierarchy**.
   - Lägg till `EnemyAI`-skriptet till fienderna. Justera hastigheten och detectionRange i **Inspector** beroende på hur snabbt och aggressivt du vill att fienderna ska vara.

3. **Testa fiendernas rörelser:**
   - Starta spelet och se hur fienderna rör sig mot spelaren när du kommer inom räckhåll. Du kan justera hastigheten och räckvidden för olika fiendetyper för att skapa variation.

##### **Steg 2: Patrullerande fiender**

1. **Lägg till patrulleringspunkter:**
   - Om du vill att vissa fiender ska patrullera mellan punkter, kan du skapa ett system där fienderna rör sig mellan fördefinierade platser i spelvärlden.
   - Skapa två tomma objekt i **Hierarchy** och placera dem på de punkter där du vill att fienden ska patrullera. Namnge dessa "PatrolPoint1" och "PatrolPoint2".

2. **Uppdatera EnemyAI-skriptet för patrullering:**

```csharp
public class EnemyAI : MonoBehaviour
{
    public float speed = 2f;
    public float detectionRange = 5f;
    public Transform player;
    public Transform[] patrolPoints;  // Array för patrulleringspunkter
    private int currentPatrolIndex = 0;

    void Update()
    {
        float distanceToPlayer = Vector2.Distance(transform.position, player.position);

        if (distanceToPlayer < detectionRange)
        {
            FollowPlayer();
        }
        else
        {
            Patrol();
        }
    }

    void FollowPlayer()
    {
        Vector2 direction = (player.position - transform.position).normalized;
        transform.position = Vector2.MoveTowards(transform.position, player.position, speed * Time.deltaTime);
    }

    void Patrol()
    {
        if (Vector2.Distance(transform.position, patrolPoints[currentPatrolIndex].position) < 0.2f)
        {
            currentPatrolIndex = (currentPatrolIndex + 1) % patrolPoints.Length;
        }

        transform.position = Vector2.MoveTowards(transform.position, patrolPoints[currentPatrolIndex].position, speed * Time.deltaTime);
    }
}
```

3. **Tilldela patrullpunkter:**
   - Gå tillbaka till Unity och tilldela dina patrullpunkter till `EnemyAI`-skriptet genom att dra "PatrolPoint1" och "PatrolPoint2" till **Inspector** under fältet för patrulleringspunkter.

4. **Testa patrulleringen:**
   - Fienderna ska nu röra sig mellan patrullpunkterna tills spelaren kommer nära, då de börjar följa spelaren.

---

### **Del 2: Skapa animationer för spelaren och fiender (1 timme)**

Animationer är en viktig del för att skapa ett mer dynamiskt och levande spel. I denna del kommer vi att lägga till enkel animation för att visa när spelaren rör sig eller attackerar, samt ge fiender rörelseanimationer.

##### **Steg 1: Använda Unity's Animator**

1. **Skapa en Animator Controller:**
   - Högerklicka i **Assets** och välj **Create > Animator Controller**. Namnge det "PlayerAnimator".
   - Gör samma sak för fiender och skapa en "EnemyAnimator".

2. **Lägg till animationer:**
   - Importera några sprite-animationer för både spelaren och fiender (t.ex. en gå-animation för spelaren och en attack-animation).
   - Dra varje sprite-sekvens till **Animator Controller** för att skapa en animation. Namnge animationerna "Walk", "Idle", "Attack", etc.

3. **Tilldela animationerna:**
   - Markera spelaren och lägg till en **Animator**-komponent. Dra din "PlayerAnimator" till **Controller**-fältet.
   - Gör samma sak för fienderna och tilldela "EnemyAnimator" till deras **Animator**-komponent.

##### **Steg 2: Skapa animationstriggers**

1. **Skapa parametrar för animationer:**
   - Öppna **Animator**-fönstret och skapa nya **parameters** genom att klicka på + och välja "Bool" eller "Trigger".
   - Skapa t.ex. en **Bool** som heter "isWalking" för att växla mellan gå-animationen och idle-animationen.

2. **Använd Animation Triggers i koden:**
   - I spelarens rörelseskript, uppdatera koden så att animationen triggas när spelaren rör sig:

```csharp
public Animator animator;

void Update()
{
    float moveX = Input.GetAxisRaw("Horizontal");
    float moveY = Input.GetAxisRaw("Vertical");

    if (moveX != 0 || moveY != 0)
    {
        animator.SetBool("isWalking", true);  // Spelaren rör sig
    }
    else
    {
        animator.SetBool("isWalking", false);  // Spelaren står still
    }
}
```

3. **Testa animationerna:**
   - Kör spelet och se hur spelarens och fiendernas animationer triggas när de rör sig eller attackerar.

##### **Steg 3: Lägga till attackanimation**

1. **Skapa en attackanimation för spelaren:**
   - Lägg till en "Attack"-animation i spelarens **Animator Controller**.
   - I ditt **PlayerMovement**-skript kan du lägga till en trigger som aktiverar attacken när spelaren trycker på en tangent:

```csharp
if (Input.GetKeyDown(KeyCode.Space))  // Om spelaren trycker på mellanslag
{
    animator.SetTrigger("Attack");  // Spelaren utför en attack
}
```

2. **Synka attacken med vapnet:**
   - Du kan synkronisera spelarens attack med vapnet genom att aktivera vapnets kolliderare (för att skada fiender) endast under attackanimationen.

```csharp
void EnableWeaponCollider()
{
    // Aktivera vapnet när attacken startar
    weaponCollider.enabled = true;
}

void DisableWeaponCollider()
{
    // Stäng av vapnet när attacken slutar
    weaponCollider.enabled = false;
}
```

---

### **Del 3: Nivådesign och progression (30 minuter)**

För att göra spelet mer intressant kan vi börja fundera på nivådesign och progression. Vi kan skapa enkla nivåer med olika utmaningar, och när spelaren besegrar fiender eller klarar specifika mål, kan de avancera till nästa nivå.

##### **Steg 1: Skapa flera nivåer**

1. **Skapa nya scener:**
   - Högerklicka i **Assets** och välj **Create > Scene**. Namnge scenerna "Level1", "Level2", etc.
   - Designa varje scen genom att lägga till olika fiender, hinder och föremål.

2. **Ladda nästa nivå:**
   - När spelaren når ett visst mål (t.ex.

 besegrar en boss eller plockar upp ett objekt), kan du ladda nästa nivå:

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

void OnTriggerEnter2D(Collider2D other)
{
    if (other.CompareTag("Player"))
    {
        // När spelaren når slutet av nivån, ladda nästa scen
        SceneManager.LoadScene("Level2");
    }
}
```

##### **Steg 2: Progression och svårighetsgrad**

1. **Skapa progression genom svårare fiender:**
   - För varje nivå kan du lägga till starkare fiender, fler hinder eller ge spelaren färre resurser (som hälsopotions) för att öka svårighetsgraden.

2. **Lägg till bossar:**
   - Skapa en starkare fiende eller "boss" som spelaren måste besegra för att avancera till nästa nivå. Ge bossen unika attacker och mer hälsa för att göra kampen mer utmanande.

---

### Nästa lektion:
I nästa lektion kommer vi att:
- Implementera mer avancerade spelmekaniker som power-ups, fällor och olika typer av utmaningar för att ge spelet mer djup.
- Lära oss att hantera spelstatistik, som poäng och högsta poäng, samt spara spelarens framsteg.

---

### Hemuppgift:
- Designa några nivåer med varierande utmaningar och se till att spelaren kan avancera genom dem.
- Experimentera med olika AI-mönster för fiender och lägg till fler animationer för karaktären och fienderna.

Vi börjar närma oss ett spel med full funktionalitet, och snart kan vi fokusera på att förfina och utöka spelet ytterligare med fler funktioner och detaljer!
