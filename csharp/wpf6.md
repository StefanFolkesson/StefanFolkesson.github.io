### WPF Lektion 6: Navigering och Flerfönsterhantering

#### **Mål**
Lär dig skapa applikationer med flera sidor, navigera mellan dem och hantera flerfönsterlayout i WPF.

---

### **Navigering mellan sidor**
WPF erbjuder en inbyggd mekanism för navigering mellan sidor med hjälp av klasserna `Frame` och `Page`.

#### **Skapa en applikation med Frame och Page**

1. **Lägg till sidor:**
   - Högerklicka på projektet och välj **Add > New Item > Page**.
   - Namnge sidorna `Page1.xaml` och `Page2.xaml`.

2. **Lägg till en Frame i MainWindow:**
   
```xml
<Window x:Class="WPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Navigering" Height="400" Width="600">
    <Grid>
        <Frame x:Name="MainFrame" NavigationUIVisibility="Hidden" />
    </Grid>
</Window>
```

3. **Navigera till en sida från koden:**
   I `MainWindow.xaml.cs`:

```csharp
public MainWindow()
{
    InitializeComponent();
    MainFrame.Navigate(new Page1());
}
```

4. **Navigera mellan sidor:**
   I `Page1.xaml`:

```xml
<Button Content="Gå till sida 2" Click="NavigateToPage2" />
```

   I `Page1.xaml.cs`:

```csharp
private void NavigateToPage2(object sender, RoutedEventArgs e)
{
    NavigationService.Navigate(new Page2());
}
```

5. **Kör applikationen:** Klicka på knappen för att navigera till sida 2.

---

### **Navigering med MVVM**
I MVVM-designmönstret hanteras navigering via kommandon och ViewModels istället för direkt i koden.

#### **Exempel på navigering i MVVM**

1. **Skapa en NavigationService:**
   Lägg till en ny klass `NavigationService.cs`:

```csharp
using System;
using System.Windows.Controls;

public class NavigationService
{
    private readonly Frame _frame;

    public NavigationService(Frame frame)
    {
        _frame = frame;
    }

    public void Navigate(Type pageType)
    {
        _frame.Navigate(Activator.CreateInstance(pageType));
    }
}
```

2. **Registrera NavigationService i MainWindow:**

```csharp
public partial class MainWindow : Window
{
    public NavigationService NavigationService { get; private set; }

    public MainWindow()
    {
        InitializeComponent();
        NavigationService = new NavigationService(MainFrame);
        DataContext = new MainViewModel(NavigationService);
        MainFrame.Navigate(new Page1());
    }
}
```

3. **Använd NavigationService i ViewModel:**

```csharp
public class MainViewModel
{
    private readonly NavigationService _navigationService;

    public ICommand NavigateCommand { get; }

    public MainViewModel(NavigationService navigationService)
    {
        _navigationService = navigationService;
        NavigateCommand = new RelayCommand(o => _navigationService.Navigate(typeof(Page2)));
    }
}
```

4. **Bind kommandot till en knapp i XAML:**

```xml
<Button Content="Gå till sida 2" Command="{Binding NavigateCommand}" />
```

---

### **Flerfönsterhantering**
I vissa scenarier kan du behöva skapa och hantera flera fönster i din applikation.

#### **Skapa och öppna ett nytt fönster**

1. **Skapa ett nytt fönster:**
   Högerklicka på projektet och välj **Add > New Item > Window (WPF)**. Namnge fönstret `SecondWindow.xaml`.

2. **Öppna fönstret från koden:**
   I `MainWindow.xaml.cs`:

```csharp
private void OpenSecondWindow(object sender, RoutedEventArgs e)
{
    SecondWindow secondWindow = new SecondWindow();
    secondWindow.Show();
}
```

3. **Lägg till en knapp i MainWindow för att öppna det nya fönstret:**

```xml
<Button Content="Öppna nytt fönster" Click="OpenSecondWindow" />
```

4. **Kör applikationen:** Klicka på knappen för att öppna det nya fönstret.

---

### **Dialogfönster och modala fönster**
Dialogfönster används för att interagera med användaren på ett fokuserat sätt.

#### **Exempel på ett dialogfönster:**

1. Öppna ett dialogfönster med `ShowDialog`:

```csharp
private void OpenDialog(object sender, RoutedEventArgs e)
{
    SecondWindow dialog = new SecondWindow();
    bool? result = dialog.ShowDialog();

    if (result == true)
    {
        MessageBox.Show("Dialogen stängdes med OK.");
    }
}
```

2. Sätt dialogresultatet i `SecondWindow`:

```csharp
private void OnOkClicked(object sender, RoutedEventArgs e)
{
    this.DialogResult = true;
}
```

3. Lägg till en OK-knapp i `SecondWindow.xaml`:

```xml
<Button Content="OK" Click="OnOkClicked" />
```

---

### **Vad blir nästa steg?**
Nästa lektion kommer vi att fokusera på att bygga ett avslutande projekt som kombinerar allt vi har lärt oss, inklusive data binding, navigering, och MVVM-designmönstret.

