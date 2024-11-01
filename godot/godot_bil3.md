
### Lektion 3: Lägga till UI och Fullständig Bilrörelse

**Mål:** Vi integrerar UI för att visa aktuell växel och rattvinkel, samt justerar bilens position.

#### Steg 1: Lägg till UI-element för Växel och Ratt
1. **Skapa UI-noder**:
   - Lägg till en **CanvasLayer**-nod med en **Label** för växeln och en **Sprite2D** för rattvinkeln.

2. **Uppdatera UI för Växel och Ratt**:
   - Hämta referenser till `gear_label` och `steering_wheel` och använd dem för att uppdatera UI.

   ```gd
   func update_gear_display() -> void:
       gear_label.text = "Växel: " + (str(gear) if gear > 0 else "R")

   func update_steering_wheel() -> void:
       steering_wheel.rotation_degrees = steering_angle * 2
   ```

#### Steg 2: Fullständig Rörelselogik
1. **Beräkna vinkelhastighet och framåtrörelse**:
   - Använd `steering_angle` och `speed` för att justera rotation och position baserat på bilens framaxel.

   ```gd
   func update_position_and_rotation(delta: float) -> void:
       if speed != 0:
           var turning_radius = wheelbase / tan(deg2rad(steering_angle)) if steering_angle != 0 else INF
           var angular_velocity = speed / turning_radius
           rotation += angular_velocity * delta * sign(speed)
           position += Vector2(cos(rotation), sin(rotation)) * speed * delta
   ```

2. **Använd alla funktioner**:
   - Anropa alla funktioner i `_process` för att uppdatera bilen.

3. **Testa fullständig rörelse**:
   - Kör spelet och se om alla funktioner fungerar tillsammans.

---

Dessa tre lektioner bör ge en nybörjare en bra förståelse för hur man skapar bilrörelser i Godot och använder UI för att visa viktiga uppgifter som växel och rattvinkel!