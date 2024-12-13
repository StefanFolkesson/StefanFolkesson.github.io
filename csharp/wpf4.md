### WPF Lektion 4: Händelsehantering och Kommandon

#### **Mål**
Förstå hur man hanterar användarinteraktioner genom händelsehantering och kommandon i WPF.

---

### **Händelsehantering i WPF**
Händelser i WPF fungerar på ett hierarkiskt sätt, med tre huvudsakliga typer av händelser:
- **Direkta händelser:** Går bara till det element som utlöser händelsen.
- **Bubblande händelser:** Går från det utlösande elementet uppåt i visuell trädstruktur.
- **Tunnlande händelser:** Går från roten i trädet ned till det utlösande elementet.

#### **Skapa en enkel händelsehanterare**
1. Lägg till en knapp i `MainWindow.xaml`:

```xml
<Button Content="Klicka mig" Click="OnButtonClick" Width="100" Height="50" />
```

2. Lägg till händelsehanteraren i `MainWindow.xaml.cs`:

```csharp
private void OnButtonClick(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Knappen klickades!");
}
```

3. **Kör applikationen:** Klicka på knappen för att se meddelandet.

---

### **Vad är Kommandon?**
Kommandon är ett alternativ till traditionell händelsehantering, framför allt i applikationer som använder MVVM. Ett kommando kan aktiveras av olika element och kopplas till samma logik.

#### **Nyckelkomponenter i Kommandon**
- **`ICommand`-gränssnittet:** Definierar kommandon.
- **CanExecute:** Kontrollerar om kommandot kan exekveras.
- **Execute:** Utför kommandot.

---

### **Implementera ett Kommando i MVVM**

1. **Skapa en klass för kommandon:**
   Lägg till en ny klass `RelayCommand.cs`:

```csharp
using System;
using System.Windows.Input;

namespace WPFApp
{
    public class RelayCommand : ICommand
    {
        private readonly Action<object> _execute;
        private readonly Func<object, bool> _canExecute;

        public RelayCommand(Action<object> execute, Func<object, bool> canExecute = null)
        {
            _execute = execute;
            _canExecute = canExecute;
        }

        public event EventHandler CanExecuteChanged;

        public bool CanExecute(object parameter)
        {
            return _canExecute == null || _canExecute(parameter);
        }

        public void Execute(object parameter)
        {
            _execute(parameter);
        }

        public void RaiseCanExecuteChanged()
        {
            CanExecuteChanged?.Invoke(this, EventArgs.Empty);
        }
    }
}
```

2. **Lägg till ett kommando i ViewModel:**
   Uppdatera `MainViewModel.cs`:

```csharp
public class MainViewModel : INotifyPropertyChanged
{
    public ICommand ClickCommand { get; }

    public MainViewModel()
    {
        ClickCommand = new RelayCommand(OnButtonClick);
    }

    private void OnButtonClick(object parameter)
    {
        MessageBox.Show("Knappen aktiverades via ett kommando!");
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

3. **Bind kommandot till knappen i XAML:**
   Uppdatera `MainWindow.xaml`:

```xml
<Button Content="Kommando" Command="{Binding ClickCommand}" Width="100" Height="50" />
```

4. **Koppla ViewModel till View:**
   I `MainWindow.xaml.cs`, se till att ViewModel är kopplad:

```csharp
public MainWindow()
{
    InitializeComponent();
    DataContext = new MainViewModel();
}
```

5. **Kör applikationen:** Klicka på knappen för att se meddelandet.

---

### **Kommandon med parametrar**
1. Uppdatera `OnButtonClick` i ViewModel:

```csharp
private void OnButtonClick(object parameter)
{
    string message = parameter?.ToString() ?? "Ingen parameter";
    MessageBox.Show($"Parametern är: {message}");
}
```

2. Skicka en parameter från XAML:

```xml
<Button Content="Skicka parameter" Command="{Binding ClickCommand}" CommandParameter="Hej WPF" />
```

3. **Kör applikationen:** Knappen skickar en parameter till kommandot.

---

### **Vad blir nästa steg?**
I nästa lektion kommer vi att fokusera på avancerad binding och hur du kan arbeta effektivt med DataContext och Value Converters.

