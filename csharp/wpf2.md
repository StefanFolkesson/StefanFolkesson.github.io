### WPF Lektion 2: Data Binding och MVVM-designmönstret

#### **Mål**
Förstå grunderna i data binding i WPF och lär dig MVVM (Model-View-ViewModel)-designmönstret.

---

### **Vad är Data Binding?**
Data binding är en teknik som kopplar data mellan UI-element och logik i bakgrunden (vanligtvis en ViewModel eller en datakälla).

#### **Nyckelkoncept inom Data Binding:**
- **One-Way Binding:** Data flödar från källan till UI-elementet (t.ex. från ViewModel till en TextBox).
- **Two-Way Binding:** Data flödar mellan källan och UI-elementet i båda riktningarna (vanligt för inmatningselement).
- **Binding Paths:** Du kan binda till specifika egenskaper i din datakälla.

---

### **Skapa ett Projekt med Data Binding**

1. **Starta ett nytt WPF-projekt:**
   - Följ samma steg som i Lektion 1, men ge projektet namnet “DataBindingDemo”.

2. **Lägg till en egenskap i MainWindow.xaml.cs:**
   - Vi börjar med en enkel egenskap som UI ska binda till.

```csharp
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace DataBindingDemo
{
    public partial class MainWindow : Window, INotifyPropertyChanged
    {
        private string _textData;

        public string TextData
        {
            get { return _textData; }
            set
            {
                _textData = value;
                OnPropertyChanged();
            }
        }

        public MainWindow()
        {
            InitializeComponent();
            DataContext = this;
            TextData = "Hej, WPF!";
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged([CallerMemberName] string propertyName = null)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

3. **Bind egenskapen i XAML:**
   - Öppna MainWindow.xaml och uppdatera den med en TextBox och en TextBlock som binder till egenskapen `TextData`.

```xml
<Window x:Class="DataBindingDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Data Binding Demo" Height="350" Width="525">
    <StackPanel Margin="20">
        <TextBox Text="{Binding TextData, UpdateSourceTrigger=PropertyChanged}" Margin="0,0,0,10" />
        <TextBlock Text="{Binding TextData}" FontSize="16" FontWeight="Bold" />
    </StackPanel>
</Window>
```

4. **Kör applikationen:**
   - TextBox och TextBlock bör visa samma text. Om du ändrar texten i TextBox kommer ändringen även att uppdateras i TextBlock tack vare Two-Way Binding.

---

### **Vad är MVVM?**
MVVM (Model-View-ViewModel) är ett designmönster som separerar logik (ViewModel) från presentation (View) och data (Model).

#### **MVVM-Komponenter:**
1. **Model:** Representerar data och affärslogik.
2. **View:** UI-delen som visas för användaren (XAML).
3. **ViewModel:** Hanterar bindings och kommandohantering mellan Model och View.

---

### **Implementera MVVM i WPF**

1. **Skapa en Model:**
   - Lägg till en ny klass, `Person.cs`:

```csharp
namespace DataBindingDemo
{
    public class Person
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
    }
}
```

2. **Skapa en ViewModel:**
   - Lägg till en ny klass, `MainViewModel.cs`:

```csharp
using System.Collections.ObjectModel;
using System.ComponentModel;

namespace DataBindingDemo
{
    public class MainViewModel : INotifyPropertyChanged
    {
        private string _searchText;

        public string SearchText
        {
            get { return _searchText; }
            set
            {
                _searchText = value;
                OnPropertyChanged();
            }
        }

        public ObservableCollection<Person> People { get; set; }

        public MainViewModel()
        {
            People = new ObservableCollection<Person>
            {
                new Person { FirstName = "Anna", LastName = "Svensson" },
                new Person { FirstName = "Björn", LastName = "Andersson" },
                new Person { FirstName = "Cecilia", LastName = "Johansson" }
            };
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

3. **Koppla ViewModel till View:**
   - Öppna MainWindow.xaml och ändra `DataContext` till ViewModel.

```csharp
public MainWindow()
{
    InitializeComponent();
    DataContext = new MainViewModel();
}
```

4. **Visa data i View:**
   - Uppdatera XAML för att visa en lista och ett sökfilter.

```xml
<Window x:Class="DataBindingDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MVVM Demo" Height="350" Width="525">
    <StackPanel Margin="20">
        <TextBox Text="{Binding SearchText, UpdateSourceTrigger=PropertyChanged}" PlaceholderText="Sök" Margin="0,0,0,10" />
        <ListBox ItemsSource="{Binding People}">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <TextBlock Text="{Binding FirstName}" />
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
    </StackPanel>
</Window>
```

5. **Kör applikationen:**
   - TextBox och ListBox visar och filtrerar data dynamiskt.

---

### **Vad blir nästa steg?**
Nästa lektion kommer vi att fördjupa oss i stilar, templates och resurser för att skapa en mer visuellt tilltalande applikation.

