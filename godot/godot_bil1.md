Här kommer en serie på tre lektioner som steg-för-steg förklarar och lär ut denna kod för en nybörjare i Godot. Vi tar det steg för steg och täcker grunderna i Godot, variabelhantering, logik för bilens rörelse och styrning, samt UI-element.

---

### Lektion 1: Introduktion till Variabler och Input i Godot

**Mål:** I den här lektionen lär vi oss om variabler, hur man definierar dem och använder dem för att styra bilens acceleration och växlingar.

#### Steg 1: Skapa en ny Scen och Bilens Grundstruktur
1. **Skapa en ny 2D-scen för bilen**:
   - I Godot, skapa en ny **2D-scen** och lägg till en **CharacterBody2D**-nod som bilens huvudnod.
   - Namnge scenen "Car" och spara den som en separat fil, t.ex., "Car.tscn".

2. **Lägg till en Sprite för bilen**:
   - Lägg till en **Sprite2D** under **CharacterBody2D** och ladda upp en bilbild som representerar bilen.

3. **Lägg till Script**:
   - Högerklicka på "Car"-noden och välj **Attach Script** för att skapa ett nytt skript. Använd GDScript och döp det till "Car.gd".

#### Steg 2: Lära oss Variabler och @export
1. **Skapa och exportera variabler**:
   - Vi börjar med att lägga till variabler som beskriver bilens hastighet, maxhastighet, acceleration, och friktion. Använd `@export` så att de blir justerbara från Godots editor.

   ```gd
   extends CharacterBody2D

   @export var max_speed := 100.0
   @export var acceleration := 100.0
   @export var friction := 50.0
   var speed := 0.0  # Bilens aktuella hastighet
   ```

2. **Förklara variablerna**:
   - **`max_speed`**: Bilens maxhastighet.
   - **`acceleration`**: Hur snabbt bilen kan öka sin hastighet.
   - **`friction`**: Används för att gradvis sakta ner bilen när man släpper accelerationen.

#### Steg 3: Använda Input för Acceleration och Broms
1. **Definiera input för att styra bilen**:
   - Gå till **Project > Project Settings > Input Map** och skapa två nya actions: `accelerate` och `brake`. Koppla dem till `W` (accelerate) och `S` (brake).
   
2. **Lägg till kod för att öka hastigheten**:
   - I `_process(delta)`, lägg till kod som styr hur hastigheten förändras baserat på input.

   ```gd
   func _process(delta: float) -> void:
       if Input.is_action_pressed("accelerate"):
           speed += acceleration * delta
       elif Input.is_action_pressed("brake"):
           speed -= acceleration * delta
       else:
           # Gradvis minskning av hastigheten mot 0
           speed = move_toward(speed, 0, friction * delta)
       
       # Begränsa hastigheten till max_speed
       speed = clamp(speed, 0, max_speed)
   ```

3. **Testa spelet**:
   - Kör spelet och testa om bilen accelererar och bromsar som förväntat. Förklara `delta` som tidssteget mellan frames för smidiga rörelser.

---
