Här kommer lektion 2, som bygger vidare på grunderna och lägger till interaktivitet och en enkel inventarie!

---

### Lektion 2: Interaktivitet och Insamling av Föremål (2 timmar)

#### Steg 1: Skapa Samlingsbara Föremål (30 minuter)
1. **Skapa en ny scen för föremålet** – Skapa en ny 2D-scen och lägg till en *Area2D* nod som huvudnod. Namnge scenen "Collectible".
2. **Lägg till en Sprite till föremålet** – Lägg till en *Sprite* nod under *Area2D*-noden och välj en textur (exempelvis en ikon eller en annan bild) för ditt föremål.
3. **Lägg till en CollisionShape2D** – Lägg till en *CollisionShape2D* nod till *Area2D*-noden och skapa en form som omsluter föremålet.
4. **Spara scenen som Collectible.tscn**.

#### Steg 2: Programmera Samlingsfunktionen (20 minuter)
1. **Skapa ett Script för Collectible**:
   - Högerklicka på *Area2D*-noden och välj **Attach Script**.
   
2. **Script för insamling**:
   - Kopiera och klistra in koden nedan:

     ```gd
     extends Area2D

     signal collected  # Signal för när föremålet samlas upp

     func _ready():
         connect("body_entered", self, "_on_body_entered")

     func _on_body_entered(body):
         if body.name == "Player":  # Om spelaren rör vid föremålet
             emit_signal("collected")  # Sänder signalen för insamling
             queue_free()  # Tar bort föremålet från scenen
     ```

3. **Exportera signalen** – Spara scenen igen och se till att signalen *collected* är aktiv för att meddela när föremålet samlas upp.

#### Steg 3: Lägg till Samlingsbara Föremål i Huvudscenen (20 minuter)
1. **Öppna huvudscenen (t.ex., Main.tscn)** och instansiera *Collectible* scenen där.
2. **Placera flera föremål på olika platser** i scenen för att spelaren ska kunna samla dem.
3. **Anslut signalen till spelaren**:
   - Klicka på ett av föremålen i scenen, gå till *Node* och anslut *collected*-signalen till **Player**.

#### Steg 4: Skapa en Enkel Inventarie (30 minuter)
1. **Lägg till en inventarie-ruta i scenen**:
   - Lägg till en *Control* nod under huvudscenen (t.ex., "UI").
   - Under *Control*-noden, skapa en *VBoxContainer* eller *HBoxContainer* för att hålla insamlade föremål.

2. **Programmera inventarielogik i Player**:
   - Öppna *Player.gd*-scriptet och lägg till en array för inventariet:

     ```gd
     var inventory = []  # Lista för insamlade föremål

     func add_to_inventory(item):
         inventory.append(item)
         update_inventory_display()
     ```

3. **Uppdatera inventarie-displayen**:
   - Lägg till en funktion för att uppdatera UI med insamlade föremål:

     ```gd
     func update_inventory_display():
         var inventory_ui = get_node("UI/Inventory")
         inventory_ui.clear_children()  # Rensa föregående föremål
         for item in inventory:
             var icon = Sprite.new()
             icon.texture = item  # Du kan behöva sätta rätt textur här
             inventory_ui.add_child(icon)
     ```

4. **Anslut signalerna från Collectible till inventariet**:
   - Öppna *Collectible.gd*-scriptet och uppdatera det så att när signalen "collected" sänds, föremålet läggs till i spelarens inventarie.

     ```gd
     func _on_body_entered(body):
         if body.name == "Player":
             emit_signal("collected")
             body.add_to_inventory(self)  # Lägg till i spelarens inventarie
             queue_free()
     ```

#### Steg 5: Testa Interaktivitet och Inventarie (20 minuter)
1. **Starta spelet och testa** – Flytta karaktären och försök samla föremålen.
2. **Kontrollera inventariet** – Se till att varje föremål dyker upp i UI:n när de samlas upp.
3. **Justera och finjustera** – Experimentera med utseendet och hur inventariet visas.

---

Nu har du en grundläggande insamlingsmekanik och ett inventariesystem som visar insamlade föremål! Nästa lektion kan vi lägga till fler avancerade funktioner, såsom att använda föremål eller visa detaljerad information om dem.