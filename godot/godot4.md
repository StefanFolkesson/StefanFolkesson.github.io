Här kommer en serie lektioner för att skapa en top-down bilstyrning i Godot. Vi börjar med grunderna och bygger successivt på för att skapa realistisk styrning och fysik för bilen.

---

### Lektion 4: Skapa Grunderna för en Top-Down Bil (2 timmar)

#### Steg 1: Skapa Bilscenen (20 minuter)
1. **Skapa en ny scen och lägg till en bilnod**:
   - Skapa en ny 2D-scen och lägg till en *KinematicBody2D*-nod. Namnge den “Car”.
2. **Lägg till en Sprite för bilen**:
   - Lägg till en *Sprite*-nod under *Car*-noden och välj en bild som representerar bilen (en bild sedd uppifrån).
3. **Lägg till en CollisionShape2D**:
   - Under *Car*-noden, lägg till en *CollisionShape2D*-nod och skapa en rektangulär form som täcker bilen.

#### Steg 2: Programmera Bilens Grundläggande Rörelse (30 minuter)
1. **Skapa ett script för bilen**:
   - Anslut ett nytt script till *Car*-noden, exempelvis *Car.gd*.

2. **Grundläggande styrning och rörelse**:
   - Kopiera och klistra in koden nedan i scriptet för att ge bilen basrörelse och styrning:

     ```gd
     extends KinematicBody2D

     var speed = 0
     var max_speed = 200
     var acceleration = 50
     var friction = 20
     var turn_speed = 100

     func _process(delta):
         if Input.is_action_pressed("ui_up"):
             speed += acceleration * delta
         elif Input.is_action_pressed("ui_down"):
             speed -= acceleration * delta
         else:
             speed = lerp(speed, 0, friction * delta)

         speed = clamp(speed, -max_speed, max_speed)

         if speed != 0:
             var direction = sign(speed)
             if Input.is_action_pressed("ui_right"):
                 rotation += direction * turn_speed * delta
             elif Input.is_action_pressed("ui_left"):
                 rotation -= direction * turn_speed * delta

         var velocity = Vector2(speed, 0).rotated(rotation)
         move_and_slide(velocity)
     ```

3. **Testa rörelsen** – Tryck på **Play** för att testa bilens rörelse. Bilen bör nu kunna accelerera framåt och bakåt och svänga åt höger och vänster när den är i rörelse.

#### Steg 3: Justera Bilens Fysik och Kontroll (30 minuter)
1. **Finjustera hastighet och friktion**:
   - Experimentera med variablerna `max_speed`, `acceleration`, och `friction` för att få en bra känsla i styrningen.

2. **Lägg till visuella indikationer**:
   - Om bilen ska sakta ner snabbare eller ha mer grepp, öka `friction`. För snabbare acceleration, öka `acceleration`.

#### Steg 4: Lägg till En Enkel Bana (40 minuter)
1. **Skapa en bana**:
   - Skapa en ny scen för banan. Lägg till en *TileMap*-nod och skapa en enkel väg med hjälp av tile-bilder.

2. **Kollision för banan**:
   - Lägg till en *StaticBody2D* och *CollisionShape2D* i banan för att lägga till kollisioner runt banan, så att bilen inte kan åka utanför.

3. **Lägg till bilen i banan**:
   - Gå tillbaka till bilscenen och spara den. Gå till banscenen och instansiera bilen som en nod i banan.
4. **Testa körupplevelsen**:
   - Kör spelet och justera bilens hastighet, acceleration och friktion för att skapa en mer realistisk körupplevelse.

