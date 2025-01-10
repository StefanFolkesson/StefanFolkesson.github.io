God morgon! 😊  
XAML (**eXtensible Application Markup Language**) är ett deklarativt språk som används för att skapa användargränssnitt i **WPF (Windows Presentation Foundation)**. Det är tätt integrerat med C# och används för att beskriva layouten och beteendet hos UI-komponenter.

### 🔑 **Grundläggande komponenter i XAML**

Här är de viktigaste byggstenarna du behöver känna till för att skapa en WPF-applikation:

---

### **1. Layoutkontroller (Containers)**
Layoutkontroller används för att placera och organisera UI-element.

- **`Grid`**: Rutnät som delar upp ytan i rader och kolumner.  
  📦 **Användning:** När du vill ha mer kontroll över placeringen av objekt.  
  ```xml
  <Grid>
      <Grid.RowDefinitions>
          <RowDefinition Height="Auto"/>
          <RowDefinition Height="*"/>
      </Grid.RowDefinitions>
      <TextBlock Text="Rubrik" Grid.Row="0" />
      <Button Content="Klicka här" Grid.Row="1" />
  </Grid>
  ```

- **`StackPanel`**: Staplar element vertikalt eller horisontellt.  
  📦 **Användning:** För enkel uppradning av objekt.  
  ```xml
  <StackPanel Orientation="Vertical">
      <Button Content="Knapp 1" />
      <Button Content="Knapp 2" />
  </StackPanel>
  ```

- **`DockPanel`**: Dockar element till vänster, höger, upp eller ner.  
  📦 **Användning:** Flexibel placering av element.  
  ```xml
  <DockPanel>
      <Button Content="Meny" DockPanel.Dock="Top"/>
      <TextBlock Text="Innehåll" />
  </DockPanel>
  ```

- **`Canvas`**: Fri placering av element med koordinater.  
  📦 **Användning:** När du behöver exakt kontroll över positionering.  
  ```xml
  <Canvas>
      <Button Content="Knapp" Canvas.Left="50" Canvas.Top="100"/>
  </Canvas>
  ```

---

### **2. Vanliga UI-kontroller (Controls)**
Dessa komponenter används för att bygga interaktiva element.

- **`Button`**: En klickbar knapp.  
  ```xml
  <Button Content="Tryck här" Width="100" Height="30"/>
  ```

- **`TextBox`**: För att skriva in text.  
  ```xml
  <TextBox Width="200" Height="30" />
  ```

- **`TextBlock`**: För att visa text (läsbart, ej redigerbart).  
  ```xml
  <TextBlock Text="Hej, världen!" FontSize="16"/>
  ```

- **`Label`**: Liknar `TextBlock` men används främst för etiketter.  
  ```xml
  <Label Content="Användarnamn:"/>
  ```

- **`CheckBox`**: En kryssruta för att välja något.  
  ```xml
  <CheckBox Content="Acceptera villkor"/>
  ```

- **`RadioButton`**: För att välja ett alternativ i en grupp.  
  ```xml
  <StackPanel>
      <RadioButton Content="Alternativ 1" GroupName="Val"/>
      <RadioButton Content="Alternativ 2" GroupName="Val"/>
  </StackPanel>
  ```

- **`ComboBox`**: Dropdown-lista.  
  ```xml
  <ComboBox>
      <ComboBoxItem Content="Alternativ 1"/>
      <ComboBoxItem Content="Alternativ 2"/>
  </ComboBox>
  ```

- **`ListBox`**: En lista av objekt.  
  ```xml
  <ListBox>
      <ListBoxItem Content="Objekt 1"/>
      <ListBoxItem Content="Objekt 2"/>
  </ListBox>
  ```

---

### **3. Fönster och Sidor**

- **`Window`**: Representerar huvudet på ett fönster i WPF.  
  ```xml
  <Window x:Class="WpfApp1.MainWindow"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          Title="Min Applikation" Height="350" Width="525">
      <Grid>
          <Button Content="Start" HorizontalAlignment="Center" VerticalAlignment="Center"/>
      </Grid>
  </Window>
  ```

- **`Page`**: Används i navigeringsapplikationer, t.ex. med en `Frame`.  
  ```xml
  <Page x:Class="WpfApp1.HomePage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation">
      <StackPanel>
          <TextBlock Text="Välkommen till sidan!" FontSize="20"/>
      </StackPanel>
  </Page>
  ```

---

### **4. Resurser och Stilar (Resources & Styles)**

För att återanvända design och färger.

- **Globala resurser** (i `App.xaml`):  
  ```xml
  <Application.Resources>
      <SolidColorBrush x:Key="PrimaryColor" Color="CornflowerBlue"/>
  </Application.Resources>
  ```

- **Stilar för kontroller**:  
  ```xml
  <Window.Resources>
      <Style TargetType="Button">
          <Setter Property="Background" Value="LightBlue"/>
          <Setter Property="FontWeight" Value="Bold"/>
      </Style>
  </Window.Resources>
  ```

---

### **5. Händelser (Events)**

För att hantera interaktioner, t.ex. knapptryckningar.

```xml
<Button Content="Klicka" Click="Button_Click"/>
```

**I C#:**
```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Knappen klickades!");
}
```

---

### **6. Bindning (Data Binding)**

Kopplar UI till data i ViewModel (MVVM).

```xml
<TextBox Text="{Binding UserName, UpdateSourceTrigger=PropertyChanged}" />
<TextBlock Text="{Binding UserName}" />
```

**I ViewModel:**
```csharp
public string UserName { get; set; } = "Standardnamn";
```

---

### **Sammanfattning**

- **Layout**: `Grid`, `StackPanel`, `DockPanel`, `Canvas`.  
- **UI-kontroller**: `Button`, `TextBox`, `Label`, `ComboBox`, `ListBox`.  
- **Stilar och resurser**: Återanvändbar design.  
- **Händelser**: Koppla UI till logik.  
- **Bindning**: Koppla data till UI via MVVM.

