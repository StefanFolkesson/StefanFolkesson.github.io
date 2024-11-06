Självklart! Här kommer lektion 3, där vi utökar spelet med användbara föremål och feedback till spelaren.

---

### Lektion 3: Användbara Föremål och Feedback till Spelaren (2 timmar)

#### Steg 1: Lägg till Olika Typer av Föremål (30 minuter)

1. **Skapa en ny föremålsscen**:
   - Duplicera scenen `Collectible.tscn` (från Lektion 2) och namnge den `UsableItem.tscn`.
   - Byt ut sprite-bilden om du vill ha en annan ikon som representerar ett specifikt föremål (t.ex. en hälsodryck eller power-up).

2. **Lägg till en variabel för föremålstyp**:
   - I `UsableItem.gd`-skriptet, skapa en variabel för att definiera typen av föremål:

     ```gdscript
     extends Area2D

     signal collected
     @export var item_type: String = "default"  # Typ av föremål, t.ex., "health", "speed"

     func _ready() -> void:
         body_entered.connect(_on_body_entered)

     func _on_body_entered(body: Node) -> void:
         if body.name == "Player":
             collected.emit(item_type)
             queue_free()
     ```

3. **Uppdatera koden för insamling**:
   - När spelaren samlar upp föremålet, lägg till föremålstypen i spelarens inventarie.

#### Steg 2: Anpassa Player-skriptet för Olika Föremål (30 minuter)

1. **Uppdatera `add_to_inventory`-funktionen**:
   - Ändra funktionen i `Player.gd` för att hantera olika typer av föremål:

     ```gdscript
     func add_to_inventory(item_type: String) -> void:
         inventory.append(item_type)
         update_inventory_display()
         if item_type == "health":
             increase_health()
         elif item_type == "speed":
             increase_speed()
     ```

2. **Skapa funktioner för olika effekter**:
   - Lägg till funktioner i `Player.gd` för att hantera de olika föremålen, t.ex., en hälsodryck som ger hälsa eller en power-up som ökar hastigheten tillfälligt:

     ```gdscript
     func increase_health() -> void:
         health = min(health + 20, max_health)  # Öka hälsa
         update_health_display()

     func increase_speed() -> void:
         speed *= 1.5  # Öka hastigheten tillfälligt
         yield(get_tree().create_timer(5.0).timeout)
         speed /= 1.5  # Återställ hastigheten
     ```

3. **Uppdatera inventariet och användbara föremål**:
   - När ett föremål används, ta bort det från inventariet och uppdatera UI.

#### Steg 3: Visa Spelarens Hälsa och Effekter (30 minuter)

1. **Skapa en hälsobar**:
   - Under din `UI`-nod, lägg till en **ProgressBar** för att representera spelarens hälsa. Ställ in min- och maxvärden för att matcha spelarens hälsopoäng.

2. **Uppdatera hälsobaren i Player-skriptet**:
   - Lägg till en funktion för att uppdatera hälsan och länka den till `ProgressBar`:

     ```gdscript
     var health: int = 100
     var max_health: int = 100

     func update_health_display() -> void:
         var health_bar = $UI/HealthBar
         health_bar.value = health
     ```

3. **Använd hälsodrycker**:
   - När spelaren samlar en hälsodryck, kör `increase_health`-funktionen och uppdatera hälsan med `update_health_display()`.

#### Steg 4: Lägg till Visuell Feedback för Samling och Effekter (30 minuter)

1. **Lägg till partikeleffekter för samling**:
   - Under varje användbart föremål (t.ex. “health” eller “speed”), lägg till en **Particles2D**-nod och konfigurera en enkel effekt (t.ex., en kort gnista).
   - Aktivera effekten när föremålet samlas upp genom att starta partikeln från `_on_body_entered`-funktionen i `UsableItem.gd`:

     ```gdscript
     func _on_body_entered(body: Node) -> void:
         if body.name == "Player":
             $Particles2D.emitting = true
             collected.emit(item_type)
             queue_free()
     ```

2. **Använd visuell feedback för hastighetsökning**:
   - Ändra spelarens sprite-färg eller lägg till en visuell effekt när spelarens hastighet ökar. Exempel:

     ```gdscript
     func increase_speed() -> void:
         $Sprite2D.modulate = Color(1, 0.5, 0.5)  # Ändrar färgen
         speed *= 1.5
         yield(get_tree().create_timer(5.0).timeout)
         speed /= 1.5
         $Sprite2D.modulate = Color(1, 1, 1)  # Återställ färgen
     ```

#### Steg 5: Testa och Finjustera (10 minuter)

1. **Spela igenom spelet**:
   - Kontrollera att varje typ av föremål fungerar som förväntat.

2. **Justera hastighet och hälsa**:
   - Anpassa effekternas varaktighet och styrka för att skapa bra balans i spelet.

3. **Spara allt och dokumentera**:
   - Skriv korta kommentarer i koden för att beskriva varje funktion.

---

Efter denna lektion kommer ditt spel ha ett inventariesystem där spelaren kan samla, använda, och se effekterna av olika föremål!