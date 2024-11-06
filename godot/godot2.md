Här kommer lektion 2, som bygger vidare på grunderna och lägger till interaktivitet och en enkel inventarie!

---

### Lektion 2: Interaktivitet och Insamling av Föremål (2 timmar)

#### Steg 1: Skapa Samlingsbara Föremål (30 minuter)

1. **Skapa en ny scen för föremålet**:
   - Skapa en ny 2D-scen och lägg till en **Area2D**-nod som huvudnod. Namnge scenen `Collectible`.

2. **Lägg till en Sprite till föremålet**:
   - Under `Collectible`, lägg till en **Sprite2D**-nod och tilldela en textur (t.ex. en ikon eller annan bild) för ditt föremål.

3. **Lägg till en CollisionShape2D**:
   - Under `Collectible`, lägg till en **CollisionShape2D**-nod och skapa en form som omsluter föremålet.

4. **Spara scenen**:
   - Spara scenen som `Collectible.tscn`.

#### Steg 2: Programmera Samlingsfunktionen (20 minuter)

1. **Skapa ett skript för `Collectible`**:
   - Högerklicka på `Collectible` och välj **Attach Script**.

2. **Skriv skriptet för insamling**:
   - Använd följande kod:

     ```gdscript
     extends Area2D

     signal collected  # Signal för när föremålet samlas upp

     func _ready() -> void:
         body_entered.connect(_on_body_entered)

     func _on_body_entered(body: Node) -> void:
         if body.name == "Player":  # Om spelaren rör vid föremålet
             collected.emit()  # Sänder signalen för insamling
             queue_free()  # Tar bort föremålet från scenen
     ```

3. **Spara skriptet**:
   - Se till att spara skriptet.

#### Steg 3: Lägg till Samlingsbara Föremål i Huvudscenen (20 minuter)

1. **Öppna huvudscenen**:
   - Öppna din huvudscen (t.ex. `Main.tscn`).

2. **Instansiera `Collectible`-scenen**:
   - Dra in `Collectible.tscn` i scenen för att skapa en instans.

3. **Placera föremålen**:
   - Placera flera instanser av `Collectible` på olika platser i scenen för att spelaren ska kunna samla dem.

4. **Anslut signalen till spelaren**:
   - Markera en `Collectible`-instans i scenen.
   - Gå till **Node**-panelen, välj signalen `collected` och anslut den till spelarens nod.

#### Steg 4: Skapa en Enkel Inventarie (30 minuter)

1. **Lägg till en inventarie-ruta i scenen**:
   - Under huvudscenen, lägg till en **Control**-nod och namnge den `UI`.
   - Under `UI`, skapa en **VBoxContainer** eller **HBoxContainer** för att hålla insamlade föremål.

2. **Programmera inventarielogik i `Player`**:
   - Öppna `Player.gd`-skriptet och lägg till en array för inventariet:

     ```gdscript
     var inventory: Array[Texture2D] = []  # Lista för insamlade föremål

     func add_to_inventory(item_texture: Texture2D) -> void:
         inventory.append(item_texture)
         update_inventory_display()
     ```

3. **Uppdatera inventarie-displayen**:
   - Lägg till en funktion för att uppdatera UI med insamlade föremål:

     ```gdscript
     func update_inventory_display() -> void:
         var inventory_ui = $UI/Inventory
         inventory_ui.clear_children()  # Rensa föregående föremål
         for item_texture in inventory:
             var icon = Sprite2D.new()
             icon.texture = item_texture
             inventory_ui.add_child(icon)
     ```

4. **Anslut signalerna från `Collectible` till inventariet**:
   - I `Collectible.gd`, uppdatera `_on_body_entered`-funktionen:

     ```gdscript
     func _on_body_entered(body: Node) -> void:
         if body.name == "Player":
             collected.emit()
             body.add_to_inventory($Sprite2D.texture)  # Lägg till i spelarens inventarie
             queue_free()
     ```

#### Steg 5: Testa Interaktivitet och Inventarie (20 minuter)

1. **Starta spelet och testa**:
   - Flytta karaktären och försök samla föremålen.

2. **Kontrollera inventariet**:
   - Se till att varje föremål dyker upp i UI:n när de samlas upp.

3. **Justera och finjustera**:
   - Experimentera med utseendet och hur inventariet visas.

---
Nu har du en grundläggande insamlingsmekanik och ett inventariesystem som visar insamlade föremål! Nästa lektion kan vi lägga till fler avancerade funktioner, såsom att använda föremål eller visa detaljerad information om dem.