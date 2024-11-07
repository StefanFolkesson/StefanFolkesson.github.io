### Lektion 2: Lägg till Växlar och Enkel Styrning

**Mål:** Lägg till växlingar för att justera maxhastighet och implementera en enkel rattstyrning.

#### Steg 1: Lägga till Växlar
1. **Definiera nya variabler för växlingar**:
   - Lägg till variabler för växlar och maxhastighet per växel.

   ```gd
   @export var base_max_speed := 100.0
   @export var max_gear := 5
   @export var min_gear := -1
   var gear := 1  # Startväxeln är framåt
   ```

2. **Skapa input för växlingar**:
   - Gå till **Input Map** och skapa två nya actions:
     - `gear_up`: koppla till `pil upp`
     - `gear_down`: koppla till `pil ned`

3. **Implementera växeländring**:
   - Skriv en funktion `handle_gear_change()` som hanterar växeländringar och justerar maxhastigheten:

   ```gd
   func handle_gear_change() -> void:
       if Input.is_action_just_pressed("gear_up") and gear < max_gear:
           gear += 1
       elif Input.is_action_just_pressed("gear_down") and gear > min_gear:
           gear -= 1
       
       # Justera maxhastighet baserat på växeln
       max_speed = base_max_speed * abs(gear)
   ```

4. **Använd växelfunktionen i `_process`**:
   - Lägg till `handle_gear_change()` i `_process` så att växlarna uppdateras varje frame.

#### Steg 2: Lägg till Enkel Styrning
1. **Definiera variabler för styrvinkel**:
   - Lägg till en variabel för rattens vinkel och max styrvinkel.

   ```gd
   @export var max_steering_angle := 40.0
   var steering_angle := 0.0
   ```

2. **Skapa input för styrning**:
   - Lägg till nya actions i **Input Map**:
     - `turn_left`: koppla till `A`
     - `turn_right`: koppla till `D`

3. **Implementera styrning**:
   - Skriv logik för att hantera styrvinkeln i `_process`:

   ```gd
   func update_steering_angle(delta: float) -> void:
       if Input.is_action_pressed("turn_right"):
           steering_angle = min(steering_angle + 100 * delta, max_steering_angle)
       elif Input.is_action_pressed("turn_left"):
           steering_angle = max(steering_angle - 100 * delta, -max_steering_angle)
       else:
           steering_angle = move_toward(steering_angle, 0, 60.0 * delta)
   ```

4. **Använd styrvinkeln för att rotera bilen**:
   - Använd följande rad för att rotera bilen baserat på styrvinkeln i `_process`:

   ```gd
   rotation += deg_to_rad(steering_angle) * delta
   ```

5. **Testa styrning och växlingar**:
   - Kör spelet och testa om styrning och växling fungerar som förväntat.

---
[Bil lektion 3](godot_bil3.md)