Det är en bra idé! Vi kan lägga till en visuell representation av ratten eller hjulens riktning på skärmen. Detta gör vi genom att skapa en bild som representerar rattens vinkel och använda skript för att styra och återställa vinkeln när spelaren svänger eller släpper svängknapparna.

### Så här gör vi det:

1. **Lägg till en rattbild** i UI.
2. **Uppdatera rattens vinkel** i koden när spelaren svänger.
3. **Gradvis återställning av vinkeln** när spelaren släpper svängknapparna.

---

### Steg 1: Lägg till en Rattbild i UI
1. **Skapa en CanvasLayer och lägg till Rattbilden**:
   - I huvudscenen, lägg till en **CanvasLayer**-nod för att hantera UI-elementen (om du inte redan har en).
   - Under **CanvasLayer**, lägg till en **Sprite2D**-nod och namnge den "SteeringWheel".
   - Välj en bild som representerar en ratt (en enkel bild på en ratt kan användas, men till exempel en cirkel fungerar också).

2. **Placera Rattbilden**:
   - Placera **SteeringWheel**-bilden på skärmen, förslagsvis längst ner eller på sidan, så att den syns väl men inte stör själva spelområdet.

### Steg 2: Uppdatera Rattens Vinkel i Koden
1. Gå tillbaka till bilens skript **Car.gd** och lägg till variabler för rattens vinkel och återställningshastighet:

   ```gd
   var steering_angle = 0.0  # Aktuell rattvinkel
   var max_steering_angle = 30.0  # Maxvinkel för visuell ratt
   var steering_reset_speed = 60.0  # Hastighet för att återställa till mitten
   ```

2. **Uppdatera Rattvinkeln**:
   - I `_process(delta)`-funktionen, lägg till logik för att öka och minska `steering_angle` när spelaren svänger och återställ den när spelaren släpper svängknapparna.

   ```gd
   func _process(delta):
       # Växling och hastighetslogik som tidigare

       # Uppdatera rattens vinkel när spelaren svänger
       if Input.is_action_pressed("turn_right"):
           steering_angle = min(steering_angle + turn_speed * delta * 10, max_steering_angle)
       elif Input.is_action_pressed("turn_left"):
           steering_angle = max(steering_angle - turn_speed * delta * 10, -max_steering_angle)
       else:
           # Återställ vinkeln gradvis mot 0 när ingen svänger
           steering_angle = move_toward(steering_angle, 0, steering_reset_speed * delta)

       # Uppdatera rattbilden på skärmen
       update_steering_wheel()

       # Resten av bilens rörelse- och växellogik

       
       # Styra bilen
       if speed != 0:
           var steering_wheel = get_tree().root.get_node("MainScene/CanvasLayer/SteeringWheel")  # Justera sökvägen om det behövs
           rotation += deg_to_rad(steering_wheel.rotation_degrees) * delta * sign(speed) * 0.5

       # Uppdatera bilens rörelse
       velocity = Vector2(speed, 0).rotated(rotation)
       move_and_slide()
   ```

### Steg 3: Uppdatera Rattbildens Rotation
Lägg till en funktion som uppdaterar rattbildens rotation baserat på `steering_angle`:

```gd
func update_steering_wheel():
    var steering_wheel = get_tree().root.get_node("Main/CanvasLayer/SteeringWheel")  # Justera sökvägen om det behövs
    steering_wheel.rotation_degrees = steering_angle
```

### Vad koden gör:
- **Svängning**: När spelaren trycker på vänster eller höger svängknapp, justeras `steering_angle` inom gränsen för `max_steering_angle`.
- **Återställning till mitten**: När inga svängknappar är nedtryckta, återgår `steering_angle` gradvis till 0 med hjälp av `move_toward`.
- **Rattens rotation**: `update_steering_wheel()` kallar på `steering_angle` och justerar bildens rotation för att matcha aktuell rattvinkel.


### Vill man fippla mer med styrningen?
Omk du vill hantera framhjulsdrift kan du lägga till denna kod istället för uppdatera bilens rörelse
```gd

       # Styra bilen
       if speed != 0:
           var wheelbase = 100 # Avstånd mellan fram- och bakaxeln
           var steering_wheel = get_tree().root.get_node("MainScene/CanvasLayer/SteeringWheel")  # Justera sökvägen om det behövs
           var turning_radius = wheelbase / tan(deg_to_rad(steering_wheel.rotation_degrees)) if steering_wheel.rotation_degrees != 0 else INF
		   var angular_velocity = speed / turning_radius  # Vinkelhastighet baserad på styrvinkeln och hastigheten
		   rotation += angular_velocity * delta * sign(speed)

		   # Justera positionen för att simulera framaxelstyrning
		   var forward_vector = Vector2(cos(rotation), sin(rotation)) * speed * delta
		   position += forward_vector
---

Nu kommer rattbilden att visa vilken riktning bilen svänger i, och den återgår mjukt till mitten när spelaren slutar svänga. Detta ger en visuell representation av svängningen och en tydlig återkoppling när ratten släpps!