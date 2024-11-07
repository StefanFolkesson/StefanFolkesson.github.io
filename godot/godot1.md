### Lektion 1: Introduktion till Godot 4.0 och Grunderna i 2D-spelutveckling (2 timmar)

#### Steg 1: Bekanta dig med Godot 4.0:s Gränssnitt (20 minuter)

1. **Ladda ner och installera Godot 4.0**:
   - Besök [Godots officiella webbplats](https://godotengine.org) och ladda ner den senaste versionen av Godot 4.0.

2. **Skapa ett nytt projekt**:
   - Starta Godot och klicka på **New Project**.
   - Ange ett projektnamn och välj en plats på din dator.
   - Se till att **Renderer** är inställd på **Forward+** för 2D-projekt.
   - Klicka på **Create & Edit** för att öppna projektet.

3. **Utforska Godots gränssnitt**:
   - **Scene Panel**: Här bygger du scener och hanterar nodhierarkier.
   - **Inspector Panel**: Här kan du se och redigera egenskaper för valda noder.
   - **Node System**: Förstå hur varje objekt är en nod som kan kopplas till andra noder för att skapa komplexa funktioner.

#### Steg 2: Skapa en Enkel 2D-scen (20 minuter)

1. **Lägg till en 2D-scen**:
   - Klicka på **Scene** > **New Scene**.
   - Lägg till en **Node2D** som huvudnod genom att klicka på **+** och välja **Node2D**.

2. **Lägg till en bakgrund**:
   - Högerklicka på **Node2D** och välj **Add Child Node**.
   - Välj **Sprite2D**.
   - Med **Sprite2D** markerad, gå till **Inspector** och klicka på **Textures** > **Load** för att ladda upp en bakgrundsbild.

3. **Spara scenen**:
   - Klicka på **Scene** > **Save As** och spara scenen som `Main.tscn`.

#### Steg 3: Skapa en Spelkaraktär (30 minuter)

1. **Lägg till en karaktärs-nod**:
   - Högerklicka på **Node2D** i scenen och välj **Add Child Node**.
   - Välj **CharacterBody2D** och namnge den `Player`.

2. **Lägg till en Sprite till Player-noden**:
   - Högerklicka på `Player` och välj **Add Child Node**.
   - Välj **Sprite2D**.
   - Med **Sprite2D** markerad, gå till **Inspector** och ladda upp en bild för karaktären under **Texture**.

3. **Lägg till en CollisionShape2D**:
   - Högerklicka på `Player` och välj **Add Child Node**.
   - Välj **CollisionShape2D**.
   - Med **CollisionShape2D** markerad, gå till **Inspector** och välj en form som passar din sprite under **Shape** (t.ex. **RectangleShape2D**).

#### Steg 4: Programmera Rörelse för Spelkaraktären (30 minuter)

1. **Skapa ett skript för Player**:
   - Högerklicka på `Player` och välj **Attach Script**.
   - Välj **GDScript** som språk och klicka på **Create**.

2. **Skriv kod för rörelse**:
   - Öppna det skapade skriptet och ersätt innehållet med följande kod:

     ```gdscript
     extends CharacterBody2D

     @export var speed := 200.0  # Justerbar hastighet

     func _process(delta):
         var velocity = Vector2.ZERO  # Rörelsevektor

         if Input.is_action_pressed("ui_right"):
             velocity.x += 1
         if Input.is_action_pressed("ui_left"):
             velocity.x -= 1
         if Input.is_action_pressed("ui_down"):
             velocity.y += 1
         if Input.is_action_pressed("ui_up"):
             velocity.y -= 1

         velocity = velocity.normalized() * speed
         velocity = move_and_slide(velocity)
     ```

3. **Testa rörelsen**:
   - Klicka på **Project** > **Project Settings** > **Input Map**.
   - Se till att åtgärderna `ui_right`, `ui_left`, `ui_down` och `ui_up` är mappade till önskade tangenter (t.ex. piltangenterna).
   - Klicka på **Play Scene** (den gröna pilen) för att testa spelet. Använd de definierade tangenterna för att flytta karaktären.

#### Steg 5: Justera och Förfina (20 minuter)

1. **Experimentera med hastigheten**:
   - Ändra värdet på `speed` i skriptet för att justera karaktärens rörelsehastighet.

2. **Lägg till väggar eller gränser**:
   - För att begränsa karaktärens rörelse kan du lägga till **StaticBody2D**-noder med tillhörande **CollisionShape2D**-noder som fungerar som väggar.

3. **Spara och testa**:
   - Se till att spara alla ändringar och testa spelet för att säkerställa att allt fungerar som förväntat.

---

Det här avslutar den första lektionen. Nästa gång kommer vi att bygga vidare på detta genom att lägga till interaktiva objekt som karaktären kan samla upp och placera i ett enkelt inventarie.
[Lektion 2](godot2.md)