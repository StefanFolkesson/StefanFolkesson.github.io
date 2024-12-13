### WPF Lektion 5: Avancerad Binding och DataContext

#### **Mål**
Förstå hur man använder avancerade data binding-tekniker i WPF, inklusive MultiBinding och Value Converters. Lär dig också att arbeta effektivt med DataContext.

---

### **Vad är DataContext?**
DataContext är den datakälla som binder till UI-elementen. Det är grunden för data binding i WPF och kan sättas på olika nivåer:

- **Globalt (på Window-nivå):** Alla element inom fönstret delar samma DataContext.
- **Lokalt (på kontrollnivå):** Endast ett specifikt element binder till den angivna DataContext.

#### **Exempel på att sätta DataContext**

1. **Sätta global DataContext:**
   I `MainWindow.xaml.cs`:

```csharp
public MainWindow()
{
    InitializeComponent();
    DataContext = new MainViewModel();
}
```

2. **Sätta lokal DataContext:**
   I `MainWindow.xaml`:

```xml
<TextBlock Text="{Binding Name}" DataContext="{Binding Source={StaticResource Person}}" />
```

---

### **MultiBinding**
MultiBinding tillåter att kombinera flera datakällor i en binding.

#### **Exempel på MultiBinding**
1. Skapa en `FullNameConverter` som kombinerar förnamn och efternamn:

```csharp
using System;
using System.Globalization;
using System.Windows.Data;

public class FullNameConverter : IMultiValueConverter
{
    public object Convert(object[] values, Type targetType, object parameter, CultureInfo culture)
    {
        return $"{values[0]} {values[1]}";
    }

    public object[] ConvertBack(object value, Type[] targetTypes, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

2. Definiera MultiBinding i XAML:

```xml
<Window.Resources>
    <local:FullNameConverter x:Key="FullNameConverter" />
</Window.Resources>

<TextBlock>
    <TextBlock.Text>
        <MultiBinding Converter="{StaticResource FullNameConverter}">
            <Binding Path="FirstName" />
            <Binding Path="LastName" />
        </MultiBinding>
    </TextBlock.Text>
</TextBlock>
```

3. Uppdatera ViewModel med egenskaperna:

```csharp
public string FirstName { get; set; } = "Anna";
public string LastName { get; set; } = "Svensson";
```

4. **Kör applikationen:** TextBlock visar det kombinerade namnet.

---

### **Value Converters**
Value Converters används för att omvandla data mellan källa och UI-element.

#### **Exempel på en enkel Value Converter**
1. Skapa en klass `BoolToVisibilityConverter`:

```csharp
using System;
using System.Globalization;
using System.Windows;
using System.Windows.Data;

public class BoolToVisibilityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (bool)value ? Visibility.Visible : Visibility.Collapsed;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

2. Definiera konverteraren i resurser:

```xml
<Window.Resources>
    <local:BoolToVisibilityConverter x:Key="BoolToVisibilityConverter" />
</Window.Resources>
```

3. Använd konverteraren i binding:

```xml
<Button Content="Visa" Visibility="{Binding IsVisible, Converter={StaticResource BoolToVisibilityConverter}}" />
```

4. Uppdatera ViewModel:

```csharp
public bool IsVisible { get; set; } = true;
```

5. **Kör applikationen:** Knappen visas eller döljs baserat på `IsVisible`.

---

### **Master-Detail Binding**
Master-Detail Binding är en vanlig design för att visa en lista med objekt (master) och detaljer om det valda objektet (detail).

#### **Exempel**
1. Skapa en lista med personer i ViewModel:

```csharp
public ObservableCollection<Person> People { get; set; } = new ObservableCollection<Person>
{
    new Person { FirstName = "Anna", LastName = "Svensson" },
    new Person { FirstName = "Björn", LastName = "Andersson" }
};

public Person SelectedPerson { get; set; }
```

2. Skapa layouten i XAML:

```xml
<ListBox ItemsSource="{Binding People}" SelectedItem="{Binding SelectedPerson}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding FirstName}" />
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>

<TextBlock Text="{Binding SelectedPerson.LastName}" />
```

3. **Kör applikationen:** Välj en person från listan för att visa detaljer.

---

### **Vad blir nästa steg?**
Nästa lektion kommer vi att titta på navigering och hur man hanterar flera fönster och sidor i en WPF-applikation.

