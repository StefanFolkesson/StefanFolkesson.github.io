
### Lektion 2: Lägg till Styrning och Växlar

**Mål:** Här lär vi oss hur bilen kan svänga och använda växlingar för att justera hastighet.

#### Steg 1: Lägga till Växlingar
1. **Definiera variabler för växlar**:
   - Låt oss lägga till variabler för växlar och koppla dem till maxhastigheten.

   ```gd
   @export var base_max_speed := 100.0
   @export var max_gear := 5
   @export var min_gear := -1
   var gear := 1  # Startväxeln är framåt
   ```

2. **Logik för Växlingar**:
   - Använd kod för att växla upp och ner när knapparna för växling trycks.

   ```gd
   func handle_gear_change() -> void:
       if Input.is_action_just_pressed("gear_up") and gear < max_gear:
           gear += 1
       elif Input.is_action_just_pressed("gear_down") and gear > min_gear:
           gear -= 1
       
       # Justera maxhastighet baserat på växeln
       max_speed = base_max_speed * abs(gear)
   ```

3. **Koppla kod för växling**:
   - I `_process(delta)`, lägg till ett anrop till `handle_gear_change()`.

#### Steg 2: Styrning med Rattvinkel
1. **Definiera styrvinkel och logik för att vrida bilen**:
   - Lägg till variabler för att representera rattens vinkel och max styrvinkel.

   ```gd
   @export var max_steering_angle := 40.0
   var steering_angle := 0.0
   ```

2. **Lägg till styrningslogik**:
   - Skriv kod för att uppdatera rattens vinkel när du trycker på styrknapparna.

   ```gd
   func update_steering_angle(delta: float) -> void:
       if Input.is_action_pressed("turn_right"):
           steering_angle = min(steering_angle + turn_speed * delta, max_steering_angle)
       elif Input.is_action_pressed("turn_left"):
           steering_angle = max(steering_angle - turn_speed * delta, -max_steering_angle)
       else:
           steering_angle = move_toward(steering_angle, 0, steering_reset_speed * delta)
   ```

3. **Testa styrning och växlingar**:
   - Kör spelet och testa växlingarna och styrningen.

---
