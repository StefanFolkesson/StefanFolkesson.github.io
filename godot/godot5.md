---

### Lektion 5: Avancerad Bilfysik och Körmekanik (2 timmar)

#### Steg 1: Lägg till Drifting och Glidande Effekter (40 minuter)
1. **Skapa en variabel för glidande friktion**:
   - I *Car.gd*, lägg till variabler för sidofriktion för att simulera drifting:

     ```gd
     var lateral_friction = 10
     ```

2. **Beräkna glidande rörelse**:
   - Ändra *move_and_slide* logiken för att inkludera lateral friktion:

     ```gd
     func get_lateral_velocity():
         var normal = Vector2.UP.rotated(rotation)
         return normal * normal.dot(velocity)

     func apply_lateral_friction():
         velocity -= get_lateral_velocity() * lateral_friction * delta
     ```

3. **Anropa `apply_lateral_friction` i `_process`**:
   - Använd `apply_lateral_friction()` i huvudrörelsefunktionen för att skapa en glidande känsla när bilen svänger.

#### Steg 2: Lägga till Acceleration Ljud och Visuella Effekter (30 minuter)
1. **Lägg till en motorljudeffekt**:
   - Lägg till ett *AudioStreamPlayer* under bilen och välj ett motorljud som spelas när bilen accelererar.
2. **Ställ in ljudet så att det anpassar sig till hastighet**:
   - Justera ljudvolymen och tonhöjden baserat på hastigheten för att skapa en realistisk effekt.

#### Steg 3: Finputsning och Testning (30 minuter)
1. **Experimentera med variabler för en mer realistisk känsla**.
2. **Testa och justera bilens körmekanik** tills du är nöjd med känslan.

---

Efter dessa två lektioner har du en fullt fungerande bilstyrning i top-down vy med grundläggande fysik, glidande effekter, och responsiv hantering. Nästa steg kan vara att lägga till olika typer av banor, hinder, eller till och med AI-kontrollerade motståndare!