Perfekt! 😊 **Databindning (Data Binding)** är en av de mest kraftfulla funktionerna i **WPF** och är central i MVVM-arkitekturen. Det gör det möjligt att koppla UI-komponenter direkt till data utan att skriva mycket kod bakom (code-behind). På så sätt hålls UI och logik separerade.

---

## 🔑 **Grundläggande om Databindning**

### **Vad är Databindning?**
Databindning innebär att egenskaper hos UI-kontroller (som `TextBox`, `ListBox`, `Label` osv.) kopplas till data från:
- **ViewModel**
- **Model**
- **Resurser**
- **Andra kontroller**

WPF hanterar automatiskt synkronisering mellan UI och data.

---

## 📌 **Bindningens Komponenter**

1. **Target** → UI-komponenten som visar eller tar emot data.  
   _Exempel:_ `TextBox.Text`

2. **Source** → Källan till datan (t.ex. ViewModel).  
   _Exempel:_ en egenskap i ViewModel.

3. **Binding Path** → Egenskapen i Source som binds.  
   _Exempel:_ `"UserName"`.

4. **Binding Mode** → Bestämmer riktningen på datan.  
   _Exempel:_ `OneWay`, `TwoWay`.

5. **UpdateSourceTrigger** → När värdet ska uppdateras.  
   _Exempel:_ `PropertyChanged`, `LostFocus`.

---

## 🔄 **Bindningslägen (Binding Modes)**

1. **OneWay**: Data flödar från källan till UI.  
   _Exempel:_ Ett `TextBlock` visar data, men kan inte ändra den.  

2. **TwoWay**: Data flödar i båda riktningarna.  
   _Exempel:_ En `TextBox` som både visar och uppdaterar data.  

3. **OneTime**: Data sätts en gång vid laddning.  
   _Exempel:_ För värden som inte ska uppdateras.  

4. **OneWayToSource**: Data flödar från UI till datakällan.  
   _Exempel:_ För loggning av UI-händelser.  

5. **Default**: Standardläge baserat på kontrollen.  
   _Exempel:_ `TextBox.Text` → `TwoWay`, `TextBlock.Text` → `OneWay`.

---

## 🚀 **Exempel på Enkel Databindning**

### **ViewModel**

```csharp
using System.ComponentModel;

public class MainViewModel : INotifyPropertyChanged
{
    private string userName;

    public string UserName
    {
        get => userName;
        set
        {
            userName = value;
            OnPropertyChanged(nameof(UserName));
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

📝 **Förklaring:** `INotifyPropertyChanged` ser till att UI uppdateras när `UserName` ändras.

---

### **View (XAML)**

```xml
<Window x:Class="DataBindingExample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Databindning i WPF" Height="200" Width="300">
    
    <Window.DataContext>
        <local:MainViewModel />
    </Window.DataContext>

    <StackPanel Margin="20">
        <TextBox Text="{Binding UserName, UpdateSourceTrigger=PropertyChanged}" 
                 Width="200" Height="30" />
        <TextBlock Text="{Binding UserName}" FontSize="16" Margin="0,10,0,0"/>
    </StackPanel>
</Window>
```

📝 **Förklaring:**
- **`TextBox`** är kopplad till `UserName` och uppdaterar datan direkt (`TwoWay`).  
- **`TextBlock`** visar samma data och uppdateras automatiskt.

---

## 🔄 **Binding Modes i Praktiken**

### **OneWay Binding**

```xml
<TextBlock Text="{Binding UserName, Mode=OneWay}"/>
```
📝 **Endast visning**: UI uppdateras om `UserName` ändras, men inte tvärtom.

### **TwoWay Binding**

```xml
<TextBox Text="{Binding UserName, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"/>
```
📝 **Synkronisering i båda riktningar**: UI och data hålls synkroniserade.

---

## 🎨 **Binding till Flera Egenskaper**

Du kan också binda flera UI-element till olika data.

### **ViewModel**

```csharp
private int age;
public int Age
{
    get => age;
    set
    {
        age = value;
        OnPropertyChanged(nameof(Age));
    }
}
```

### **XAML**

```xml
<TextBox Text="{Binding UserName}" Width="200" />
<TextBox Text="{Binding Age}" Width="200" Margin="0,10,0,0"/>
<TextBlock Text="{Binding UserName}" />
<TextBlock Text="{Binding Age}" />
```

📝 **Förklaring:** Två olika egenskaper (`UserName`, `Age`) binds till sina respektive `TextBox` och `TextBlock`.

---

## ✨ **Converter i Databindning**

Vill du ändra hur data visas? Använd en **Converter**!

### **Bool till Text Converter**

```csharp
using System;
using System.Globalization;
using System.Windows.Data;

public class BoolToTextConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (bool)value ? "Aktiv" : "Inaktiv";
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (string)value == "Aktiv";
    }
}
```

### **XAML med Converter**

```xml
<Window.Resources>
    <local:BoolToTextConverter x:Key="BoolToTextConverter"/>
</Window.Resources>

<CheckBox Content="{Binding IsActive, Converter={StaticResource BoolToTextConverter}}" />
```

📝 **Förklaring:** Beroende på om `IsActive` är `true` eller `false`, visas "Aktiv" eller "Inaktiv".

---

## 📚 **Sammanfattning av Databindning**

| **Begrepp**         | **Förklaring**                                                                 |
|---------------------|--------------------------------------------------------------------------------|
| **Binding**         | Kopplar UI till data.                                                          |
| **INotifyPropertyChanged** | Meddelar UI om att en datavärde har ändrats.                              |
| **Binding Modes**   | Styr hur data flödar (OneWay, TwoWay, osv).                                     |
| **UpdateSourceTrigger** | Bestämmer när datan uppdateras (`PropertyChanged`, `LostFocus`).            |
| **Converters**      | Omvandlar data mellan källa och visning.                                       |

---
