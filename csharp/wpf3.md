### WPF Lektion 3: Stilar, Templates och Resurser

#### **Mål**
Förstå hur man anpassar utseendet på en WPF-applikation med stilar, control templates och resurser.

---

### **Vad är Stilar?**
Stilar i WPF tillåter dig att definiera återanvändbara egenskaper och visuella inställningar för kontroller. Detta gör det enklare att hålla enhetlig design i hela applikationen.

#### **Skapa en enkel stil**
1. Öppna `MainWindow.xaml`.
2. Lägg till en stil i fönstrets resurser:

```xml
<Window.Resources>
    <Style TargetType="Button">
        <Setter Property="Background" Value="LightBlue" />
        <Setter Property="FontSize" Value="16" />
        <Setter Property="Margin" Value="5" />
    </Style>
</Window.Resources>
```

3. Lägg till några knappar i layouten:

```xml
<StackPanel>
    <Button Content="Knapp 1" />
    <Button Content="Knapp 2" />
    <Button Content="Knapp 3" />
</StackPanel>
```

4. **Kör applikationen:** Alla knappar får nu samma stil.

---

### **Vad är Templates?**
Templates gör det möjligt att helt anpassa utseendet på en kontroll. Det finns två huvudtyper:
- **ControlTemplate:** Används för att definiera hur en kontroll ska ritas.
- **DataTemplate:** Används för att definiera hur data ska visas.

#### **Exempel på ControlTemplate**
1. Lägg till en anpassad template i resurser:

```xml
<Window.Resources>
    <ControlTemplate x:Key="RoundButtonTemplate" TargetType="Button">
        <Border Background="LightGreen" CornerRadius="15" BorderBrush="Black" BorderThickness="2">
            <ContentPresenter HorizontalAlignment="Center" VerticalAlignment="Center" />
        </Border>
    </ControlTemplate>
</Window.Resources>
```

2. Använd templaten på en knapp:

```xml
<Button Content="Rund Knapp" Template="{StaticResource RoundButtonTemplate}" />
```

3. **Kör applikationen:** Knappen visas nu som en grön rundad rektangel.

---

### **Vad är Resurser?**
Resurser i WPF används för att lagra återanvändbara objekt som stilar, templates och penslar.

#### **Globala resurser**
Globala resurser kan definieras i en separat fil, t.ex. `App.xaml`:

```xml
<Application.Resources>
    <SolidColorBrush x:Key="PrimaryColor" Color="RoyalBlue" />
</Application.Resources>
```

Använd sedan resursen i valfri XAML-fil:

```xml
<Button Content="Global Färg" Background="{StaticResource PrimaryColor}" />
```

#### **Dynamiska resurser**
Dynamiska resurser kan ändras vid körtid:

```xml
<Button Content="Dynamisk Färg" Background="{DynamicResource PrimaryColor}" />
```

Du kan ändra resursen med kod:

```csharp
this.Resources["PrimaryColor"] = new SolidColorBrush(Colors.Red);
```

---

### **Praktisk uppgift: Anpassa ett gränssnitt**
1. Skapa en stil för TextBox:

```xml
<Style TargetType="TextBox">
    <Setter Property="BorderBrush" Value="Gray" />
    <Setter Property="FontSize" Value="14" />
    <Setter Property="Padding" Value="5" />
</Style>
```

2. Skapa en data template för att visa personer:

```xml
<DataTemplate x:Key="PersonTemplate">
    <StackPanel Orientation="Horizontal">
        <TextBlock Text="{Binding FirstName}" FontWeight="Bold" Margin="0,0,5,0" />
        <TextBlock Text="{Binding LastName}" />
    </StackPanel>
</DataTemplate>
```

3. Uppdatera din ListBox för att använda denna template:

```xml
<ListBox ItemsSource="{Binding People}" ItemTemplate="{StaticResource PersonTemplate}" />
```

4. **Kör applikationen:** Personens förnamn och efternamn visas i en enkel layout.

---

### **Vad blir nästa steg?**
I nästa lektion kommer vi att fokusera på händelsehantering och kommandon för att hantera användarinteraktioner effektivt.

