### Lektion 3: Lägg till UI och Simulera Framaxelstyrning

**Mål:** Lägg till UI för att visa växel och rattvinkel, och justera bilens rotation för att simulera framaxelstyrning.

#### Steg 1: Lägg till UI-element
1. **Skapa UI-element**:
   - Lägg till en **CanvasLayer**-nod och lägg till en **Label** för växel och en **Sprite2D** för rattens vinkel.

2. **Spara referenser till UI-elementen**:
   - Lägg till referenser till `gear_label` och `steering_wheel` i `_ready` för enklare åtkomst.

   ```gd
   var gear_label
   var steering_wheel

   func _ready() -> void:
       gear_label = get_node("CanvasLayer/GearLabel")  # kanske behöver uppdatera  sökvägen
       steering_wheel = get_node("CanvasLayer/SteeringWheel")
       update_gear_display()
   ```

#### Steg 2: Visa Växel och Styrning i UI
1. **Uppdatera UI**:
   - Lägg till kod för att uppdatera växel och rattvinkel i UI:

   ```gd
   func update_gear_display() -> void:
       if gear > 0:
           gear_label.text = "Växel: " + str(gear)
       elif gear < 0:
           gear_label.text = "Växel: R"
       else:
           gear_label.text = "Växel: N"

   func update_steering_wheel() -> void:
       steering_wheel.rotation_degrees = steering_angle * 2
   ```

2. **Använd UI-funktionerna i `_process`**:
   - Lägg till `update_gear_display()` och `update_steering_wheel()` i `_process` så att UI hålls uppdaterat.

#### Steg 3: Simulera Framaxelstyrning
1. **Lägg till variabel för hjulbas**:
   - Lägg till en variabel för avståndet mellan fram- och bakaxeln.

   ```gd
   @export var wheelbase := 100.0
   ```

2. **Beräkna rotation baserat på styrvinkel**:
   - Använd `steering_angle` och `speed` för att uppdatera bilens rotation.

   ```gd
   if speed != 0:
       var turning_radius = wheelbase / tan(deg_to_rad(steering_angle)) if steering_angle != 0 else INF
       var angular_velocity = speed / turning_radius
       rotation += angular_velocity * delta * sign(speed)
   ```

3. **Testa spelet**:
   - Kör