Självklart! 🌟 **Stilhantering (Styles)** i WPF är ett kraftfullt sätt att skapa konsekventa och återanvändbara designmallar för dina UI-komponenter. Med **Styles** kan du definiera egenskaper, utseende och beteende för kontroller på ett ställe och sedan återanvända dem i hela applikationen.

---

## 🔑 **Grundläggande Stilhantering**

### **1. Enkel Style för en kontroll**

Du kan definiera en stil direkt i en kontroll eller i fönstrets resurser.

🔹 **Exempel:** Ändra bakgrundsfärg och textstorlek för en knapp.

```xml
<Window.Resources>
    <Style TargetType="Button">
        <Setter Property="Background" Value="LightBlue"/>
        <Setter Property="FontSize" Value="16"/>
        <Setter Property="FontWeight" Value="Bold"/>
        <Setter Property="Margin" Value="5"/>
    </Style>
</Window.Resources>

<StackPanel>
    <Button Content="Knapp 1"/>
    <Button Content="Knapp 2"/>
</StackPanel>
```

📝 **Förklaring:** Alla knappar i fönstret får nu ljusblå bakgrund, större text och marginal. Det gäller automatiskt eftersom vi inte har angett ett namn på stilen.

---

### **2. Namngivna Stilar**

Om du vill ha olika stilar för olika kontroller kan du ge stilen ett **x:Key**.

🔹 **Exempel:** Två olika knappstilar.

```xml
<Window.Resources>
    <Style x:Key="PrimaryButtonStyle" TargetType="Button">
        <Setter Property="Background" Value="CornflowerBlue"/>
        <Setter Property="Foreground" Value="White"/>
        <Setter Property="FontSize" Value="14"/>
    </Style>

    <Style x:Key="SecondaryButtonStyle" TargetType="Button">
        <Setter Property="Background" Value="Gray"/>
        <Setter Property="Foreground" Value="Black"/>
        <Setter Property="FontSize" Value="12"/>
    </Style>
</Window.Resources>

<StackPanel>
    <Button Content="Primär" Style="{StaticResource PrimaryButtonStyle}"/>
    <Button Content="Sekundär" Style="{StaticResource SecondaryButtonStyle}"/>
</StackPanel>
```

📝 **Förklaring:** Här används två olika stilar för knapparna genom att ange vilken stil som ska användas.

---

### **3. Stilärvning (BasedOn)**

Du kan skapa en grundstil och sedan utöka den med fler egenskaper.

🔹 **Exempel:** Ärva en stil och lägg till fler inställningar.

```xml
<Window.Resources>
    <Style x:Key="BaseButtonStyle" TargetType="Button">
        <Setter Property="FontSize" Value="14"/>
        <Setter Property="Padding" Value="10"/>
    </Style>

    <Style x:Key="WarningButtonStyle" TargetType="Button" BasedOn="{StaticResource BaseButtonStyle}">
        <Setter Property="Background" Value="Red"/>
        <Setter Property="Foreground" Value="White"/>
    </Style>
</Window.Resources>

<StackPanel>
    <Button Content="Standardknapp" Style="{StaticResource BaseButtonStyle}"/>
    <Button Content="Varning" Style="{StaticResource WarningButtonStyle}"/>
</StackPanel>
```

📝 **Förklaring:** `WarningButtonStyle` ärver från `BaseButtonStyle` och lägger till röd bakgrund och vit text.

---

### **4. Triggers i Stilar (Dynamiska ändringar)**

Med **Triggers** kan du ändra en komponents stil baserat på händelser eller tillstånd.

🔹 **Exempel:** Ändra färg när muspekaren är över en knapp.

```xml
<Window.Resources>
    <Style TargetType="Button">
        <Setter Property="Background" Value="LightGray"/>
        <Setter Property="Foreground" Value="Black"/>

        <Style.Triggers>
            <Trigger Property="IsMouseOver" Value="True">
                <Setter Property="Background" Value="DarkGray"/>
                <Setter Property="Foreground" Value="White"/>
            </Trigger>
        </Style.Triggers>
    </Style>
</Window.Resources>

<Button Content="Håll musen över mig"/>
```

📝 **Förklaring:** När muspekaren är över knappen ändras bakgrundsfärgen till mörkgrå och texten blir vit.

---

### **5. Globala Stilar i `App.xaml`**

Om du vill använda samma stil i hela applikationen kan du definiera den i `App.xaml`.

🔹 **Exempel:** Global stil för alla knappar.

```xml
<Application x:Class="MyApp.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <Style TargetType="Button">
            <Setter Property="Background" Value="Green"/>
            <Setter Property="Foreground" Value="White"/>
            <Setter Property="FontSize" Value="16"/>
        </Style>
    </Application.Resources>
</Application>
```

📝 **Förklaring:** Alla knappar i applikationen kommer automatiskt att ha grön bakgrund och vit text.

---

### **6. Dynamiska och Statisk Resurser**

- **`StaticResource`** laddas när applikationen startar.  
- **`DynamicResource`** uppdateras om värdet ändras under körning.

🔹 **Exempel på DynamicResource:**

```xml
<Window.Resources>
    <SolidColorBrush x:Key="ButtonColor" Color="Orange"/>
</Window.Resources>

<Button Content="Dynamic Resource" Background="{DynamicResource ButtonColor}"/>
```

📝 **Förklaring:** Om `ButtonColor` ändras under körning uppdateras även knappens bakgrund.

---

## ✨ **Sammanfattning av Stilhantering**

| **Typ**            | **Funktion**                                             |
|--------------------|----------------------------------------------------------|
| **Setter**         | Sätter egenskaper på kontroller.                         |
| **x:Key**          | Identifierar stilen för selektiv användning.             |
| **BasedOn**        | Ärver en annan stil och lägger till/ändrar egenskaper.  |
| **Trigger**        | Ändrar stil baserat på tillstånd (t.ex. `IsMouseOver`). |
| **StaticResource** | Laddas vid start och ändras inte dynamiskt.             |
| **DynamicResource**| Uppdateras vid körning om värdet ändras.                |

---
