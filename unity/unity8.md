Här kommer nästa lektion, där vi fortsätter att utveckla spelet genom att implementera ett system för att **återuppta spelet från där spelaren senast slutade**, vidareutveckla **power-up-systemet** och lägga till mer komplexa spelfunktioner. Vi kommer också att arbeta med att **balansera svårighetsgrad** och skapa fler nivåer.

### Lektion 8: Återuppta spelet, komplexa power-ups och nivåbalansering

---

### **Del 1: Återuppta spelet från där spelaren senast slutade (1 timme)**

För att spelare ska kunna fortsätta spela där de senast slutade, behöver vi spara spelarens position, hälsa och aktuella nivå. Detta gör vi genom att spara datan till **PlayerPrefs**, som lagrar information lokalt på användarens dator.

##### **Steg 1: Spara spelarens position och hälsa**

1. **Spara spelarens position:**
   - Öppna **PlayerController**-skriptet och lägg till en funktion för att spara spelarens position:

```csharp
public void SavePlayerProgress()
{
    PlayerPrefs.SetFloat("PlayerPosX", transform.position.x);
    PlayerPrefs.SetFloat("PlayerPosY", transform.position.y);
    PlayerPrefs.SetInt("PlayerHealth", currentHealth);  // Spara hälsa
    PlayerPrefs.Save();
    Debug.Log("Spelarens framsteg har sparats.");
}
```

2. **Ladda spelarens position:**
   - Skapa en funktion för att ladda spelarens tidigare position och hälsa när spelet startar:

```csharp
public void LoadPlayerProgress()
{
    if (PlayerPrefs.HasKey("PlayerPosX"))
    {
        float x = PlayerPrefs.GetFloat("PlayerPosX");
        float y = PlayerPrefs.GetFloat("PlayerPosY");
        transform.position = new Vector2(x, y);

        currentHealth = PlayerPrefs.GetInt("PlayerHealth", maxHealth);  // Ladda hälsa, eller sätt till max om inget är sparat
        Debug.Log("Spelarens framsteg har laddats.");
    }
}
```

3. **Anropa dessa funktioner:**
   - Anropa `SavePlayerProgress()` när spelaren når en specifik punkt (t.ex. när de klarar en nivå).
   - Anropa `LoadPlayerProgress()` i `Start()`-metoden i spelarens skript när spelet startar.

##### **Steg 2: Spara och ladda nivåprogression**

1. **Spara aktuell nivå:**
   - När spelaren klarar en nivå, spara vilken nivå de befinner sig på:

```csharp
public void SaveLevelProgress(int currentLevel)
{
    PlayerPrefs.SetInt("CurrentLevel", currentLevel);
    PlayerPrefs.Save();
    Debug.Log("Nivå " + currentLevel + " har sparats.");
}
```

2. **Ladda aktuell nivå:**
   - När spelet startar, ladda vilken nivå spelaren senast var på:

```csharp
public int LoadLevelProgress()
{
    return PlayerPrefs.GetInt("CurrentLevel", 1);  // Ladda aktuell nivå, eller starta på nivå 1 om inget är sparat
}
```

3. **Anropa dessa funktioner:**
   - Anropa `SaveLevelProgress()` när spelaren klarar en nivå, och `LoadLevelProgress()` när spelet startar för att återgå till rätt nivå.

---

### **Del 2: Vidareutveckla power-up-systemet (45 minuter)**

Nu ska vi skapa mer komplexa power-ups, som till exempel kombinationer av power-ups eller power-ups som har mer avancerad logik, t.ex. att påverka andra fiender eller hela spelvärlden.

##### **Steg 1: Kombinerade power-ups**

1. **Skapa en power-up som kombinerar effekter:**
   - Uppdatera `PowerUp.cs` för att skapa en power-up som kombinerar två eller fler effekter. Exempelvis kan vi skapa en power-up som både ökar spelarens hastighet och styrka:

```csharp
void ApplyPowerUp(PlayerController player)
{
    switch (powerUpType)
    {
        case PowerUpType.Health:
            player.IncreaseHealth(20);
            break;
        case PowerUpType.SpeedAndStrength:
            StartCoroutine(player.IncreaseSpeed(powerUpDuration));
            StartCoroutine(player.IncreaseStrength(powerUpDuration));
            break;
    }
}
```

2. **Skapa nya power-ups:**
   - Skapa nya power-up-objekt i scenen som använder denna kombinerade effekt. Du kan experimentera med olika kombinationer av effekter.

##### **Steg 2: Power-ups som påverkar fiender eller spelvärlden**

1. **Power-ups som påverkar fiender:**
   - Skapa en power-up som påverkar alla fiender i scenen, t.ex. att sakta ner dem under en viss tid. Lägg till en ny typ av power-up som påverkar fienderna:

```csharp
public void SlowDownEnemies(float duration)
{
    Enemy[] enemies = FindObjectsOfType<Enemy>();
    foreach (Enemy enemy in enemies)
    {
        enemy.speed /= 2;  // Halvera fiendernas hastighet
    }

    StartCoroutine(ResetEnemySpeedAfterDuration(duration, enemies));
}

IEnumerator ResetEnemySpeedAfterDuration(float duration, Enemy[] enemies)
{
    yield return new WaitForSeconds(duration);
    foreach (Enemy enemy in enemies)
    {
        enemy.speed *= 2;  // Återställ hastigheten
    }
}
```

2. **Power-ups som påverkar spelvärlden:**
   - Du kan skapa power-ups som ändrar spelets miljö, som att öka gravitationen eller förändra belysningen.

```csharp
public void ChangeWorldGravity(float newGravity, float duration)
{
    Physics2D.gravity = new Vector2(0, newGravity);  // Ändra gravitationen i spelvärlden

    StartCoroutine(ResetGravityAfterDuration(duration));
}

IEnumerator ResetGravityAfterDuration(float duration)
{
    yield return new WaitForSeconds(duration);
    Physics2D.gravity = new Vector2(0, -9.81f);  // Återställ standardgravitationen
}
```

---

### **Del 3: Balansera svårighetsgrad och skapa fler nivåer (45 minuter)**

Att balansera spelet är viktigt för att hålla det utmanande men rättvist. Vi ska nu gå igenom några sätt att balansera svårighetsgraden och designa nivåer som passar spelets progression.

##### **Steg 1: Justera fiendernas svårighetsgrad**

1. **Ge fiender olika egenskaper på olika nivåer:**
   - Justera fiendernas hastighet, hälsa och skada beroende på vilken nivå spelaren befinner sig på.

```csharp
public void AdjustDifficulty(int currentLevel)
{
    // Öka fiendernas hälsa och skada med varje nivå
    foreach (Enemy enemy in FindObjectsOfType<Enemy>())
    {
        enemy.maxHealth += currentLevel * 10;  // Öka hälsan baserat på nivå
        enemy.damage += currentLevel * 5;  // Öka skadan
    }
}
```

2. **Använd fiendevågor:**
   - Skapa vågor av fiender med ökad svårighetsgrad. När spelaren besegrar en våg kan du öka antalet fiender och deras styrka.

##### **Steg 2: Skapa varierade nivåer**

1. **Skapa nivåer med olika teman:**
   - Designa nivåer med olika teman och utmaningar. Vissa nivåer kan fokusera mer på pussel, medan andra kan vara mer actionfyllda.

2. **Lägg till unika hinder:**
   - Introducera nya hinder på varje nivå, såsom rörliga plattformar, farliga fällor eller blockeringar som kräver att spelaren använder ett specifikt objekt för att fortsätta.

##### **Steg 3: Balansera spelets progression**

1. **Skapa en progression av power-ups:**
   - Börja med att ge spelaren enklare power-ups tidigt i spelet, och introducera mer kraftfulla power-ups senare för att hålla spelet intressant.

2. **Justera mängden resurser:**
   - Ge spelaren färre hälsopotions och power-ups på svårare nivåer, och placera dem på mer svåråtkomliga platser.

---

### Nästa lektion:
I nästa lektion kommer vi att:
- Lära oss att implementera **spelsparande på olika nivåer** och låta spelaren välja att fortsätta där de senast slutade.
- Skapa ett **huvudmenysystem** och en **nivåväljare** för att låta spelaren starta om eller välja nivåer.
- Fortsätta bygga upp spelets logik och design för att skapa en sammanhängande upplevelse.

---

### Hemuppgift:
- Fortsätt att designa nivåer och balansera spelets svårighetsgrad genom att justera fiendernas och power-ups funktioner.
- Experimentera med att skapa fler kombinerade power-ups och utmaningar i spelet.

Spelet börjar nu få mer djup och komplexitet, och vi

 kommer att fortsätta att arbeta mot en mer polerad och sammanhängande upplevelse!
