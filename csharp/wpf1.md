### WPF Lektion 1: Introduktion till WPF och dess grunder

#### **Mål**
Förstå vad WPF är och hur det fungerar, samt skapa ditt första WPF-projekt i Visual Studio.

---

### **Vad är WPF?**
Windows Presentation Foundation (WPF) är ett UI-ramverk från Microsoft som använder .NET och XAML för att bygga desktopapplikationer med avancerade grafiska funktioner. Några nyckelfunktioner:

- **XAML (eXtensible Application Markup Language):** Ett deklarativt språk för att designa UI.
- **Flexibelt layoutsystem:** Med kontroll över hur element placeras och anpassas.
- **Stöd för data binding och MVVM.**
- **Grafik och animationer:** Stöd för avancerad grafik via DirectX.

### **Skillnader jämfört med WinForms**
- WPF är modernare och stödjer fler funktioner som datavisualisering, responsiva layouter och avancerade teman.
- Bättre prestanda för grafiska applikationer tack vare DirectX.

---

### **Skapa ditt första WPF-projekt**

1. **Installera Visual Studio** (om det inte redan är installerat).
   - Se till att du har .NET Desktop Development-arbetsbelastningen installerad.

2. **Skapa ett nytt projekt:**
   - Klicka på "Create a new project."
   - Välj “WPF App (.NET 6/7)” och klicka “Next”.
   - Ange ett namn, till exempel “HelloWPF”, och klicka “Create”.

3. **Utforska projektstrukturen:**
   - **MainWindow.xaml:** För att designa ditt UI med XAML.
   - **MainWindow.xaml.cs:** För kod-bakom som hanterar logik.

4. **Kör applikationen:**
   - Tryck på `F5` eller klicka på “Start”. Du kommer att se ett tomt fönster.

---

### **Grundläggande XAML-struktur**
I MainWindow.xaml ser du något liknande:

```xml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="HelloWPF" Height="350" Width="525">
    <Grid>
        <!-- UI-element placeras här -->
    </Grid>
</Window>
```

- **`Window`**: Rot-elementet som representerar huvudfönstret.
- **`Grid`**: En layoutkontroll för att placera och organisera andra element.

---

### **Layoutsystemet i WPF**

WPF erbjuder olika layoutkontroller:

1. **Grid:**
   - Används för att skapa rader och kolumner.
   
   Exempel:
   ```xml
   <Grid>
       <Grid.RowDefinitions>
           <RowDefinition Height="*" />
           <RowDefinition Height="2*" />
       </Grid.RowDefinitions>
       <Grid.ColumnDefinitions>
           <ColumnDefinition Width="Auto" />
           <ColumnDefinition Width="*" />
       </Grid.ColumnDefinitions>
       <Button Grid.Row="0" Grid.Column="0" Content="Knapp 1" />
       <Button Grid.Row="1" Grid.Column="1" Content="Knapp 2" />
   </Grid>
   ```

2. **StackPanel:**
   - Placera element vertikalt eller horisontellt.
   
   Exempel:
   ```xml
   <StackPanel Orientation="Vertical">
       <Button Content="Knapp 1" />
       <Button Content="Knapp 2" />
   </StackPanel>
   ```

3. **Canvas:**
   - Ger absolut positionering.
   
   Exempel:
   ```xml
   <Canvas>
       <Button Content="Knapp" Canvas.Left="50" Canvas.Top="100" />
   </Canvas>
   ```

---

### **Praktisk uppgift: Din första layout**
1. Öppna `MainWindow.xaml`.
2. Ersätt koden med följande:

```xml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Min Första WPF" Height="400" Width="600">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="*" />
            <RowDefinition Height="2*" />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="2*" />
            <ColumnDefinition Width="*" />
        </Grid.ColumnDefinitions>

        <Button Grid.Row="0" Grid.Column="0" Content="Knapp 1" />
        <Button Grid.Row="0" Grid.Column="1" Content="Knapp 2" />
        <Button Grid.Row="1" Grid.Column="0" Grid.ColumnSpan="2" Content="Knapp 3" />
    </Grid>
</Window>
```

3. **Kör programmet:**
   - Du ska se tre knappar arrangerade i ett rutnät.

---

### **Vad blir nästa steg?**
I nästa lektion kommer vi att fokusera på data binding och MVVM-designmönstret för att skapa en renare och mer skalbar applikation.

Ta dig tid att experimentera med XAML och olika layoutkontroller innan du fortsätter!

