### Lektion 1: Skapa Bilens Grundrörelse

**Mål:** Lära oss att hantera acceleration, bromsning och en grundläggande hastighetsbegränsning.

#### Steg 1: Skapa och Förbered Bilscenen
1. **Skapa en ny 2D-scen för bilen**:
   - Öppna Godot och skapa en ny **2D-scen**.
   - Lägg till en **CharacterBody2D**-nod och namnge den till "Car". Spara scenen som "Car.tscn".

2. **Lägg till en Sprite**:
   - Under **CharacterBody2D**, lägg till en **Sprite2D** och ladda upp en bild som representerar bilen.

3. **Lägg till ett Script**:
   - Högerklicka på "Car"-noden och välj **Attach Script**. Namnge det "Car.gd" och skapa.

#### Steg 2: Lägg till Variabler och Input
1. **Definiera variabler för rörelse**:
   - I skriptet, lägg till följande variabler för att styra bilens hastighet, maxhastighet, acceleration och friktion.

   ```gd
   extends CharacterBody2D

   @export var max_speed := 100.0
   @export var acceleration := 100.0
   @export var friction := 50.0
   var speed := 0.0  # Den aktuella hastigheten för bilen
   ```

2. **Skapa Input-actions**:
   - Gå till **Project > Project Settings > Input Map** och skapa två actions:
     - `accelerate`: koppla till `W`
     - `brake`: koppla till `S`

#### Steg 3: Implementera Grundläggande Rörelse
1. **Skriv kod för acceleration och bromsning**:
   - I `_process(delta)`, använd följande kod för att justera bilens hastighet beroende på om `accelerate` eller `brake` är tryckt.

   ```gd
   func _process(delta: float) -> void:
       # Hantera acceleration och bromsning
       if Input.is_action_pressed("accelerate"):
           speed += acceleration * delta
       elif Input.is_action_pressed("brake"):
           speed -= acceleration * delta
       else:
           # Gradvis sänkning av hastigheten när ingen knapp är tryckt
           speed = move_toward(speed, 0, friction * delta)
       
       # Begränsa hastigheten
       speed = clamp(speed, -max_speed, max_speed)

       # Uppdatera bilens position i riktning mot rotationen
       var forward_movement = Vector2(cos(rotation), sin(rotation)) * speed * delta
       position += forward_movement
   ```

2. **Testa spelet**:
   - Kör scenen. Du ska nu kunna accelerera och bromsa bilen med `W` och `S`.

---
[Bil lektion 2](godot_bil2.md)