Att binda data från en **databas** till ett WPF-gränssnitt är en mycket användbar funktion, särskilt i större applikationer. Här går vi igenom hur du kan koppla en WPF-applikation till en databas och visa datan i gränssnittet med **databindning**.

---

## 🎯 **Mål:**
- Skapa en enkel WPF-applikation som hämtar data från en databas.  
- Visa datan i en **`DataGrid`**.  
- Använd **Entity Framework Core** för att kommunicera med databasen.

---

## 🏗️ **1. Förberedelser**

### **Installera NuGet-paket**
Vi använder **Entity Framework Core** med en lokal SQLite-databas.

⚙️ Installera följande paket i ditt projekt:

```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

📦 **För Visual Studio**  
Gå till **NuGet Package Manager** och installera:  
- `Microsoft.EntityFrameworkCore`  
- `Microsoft.EntityFrameworkCore.Sqlite`  
- `Microsoft.EntityFrameworkCore.Tools`

---

## 📂 **2. Skapa Model och DbContext**

### **Person.cs (Model)**

```csharp
public class Person
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
```

📝 **Förklaring:** Detta är en enkel modell som representerar en person.

---

### **AppDbContext.cs (Databasanslutning)**

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Person> People { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlite("Data Source=people.db");
    }
}
```

📝 **Förklaring:**  
- `DbSet<Person>` representerar tabellen i databasen.  
- SQLite används som databas, och filen heter **`people.db`**.

---

## 📊 **3. Skapa och fyll databasen**

### **DatabaseInitializer.cs**

```csharp
using System.Linq;

public static class DatabaseInitializer
{
    public static void Initialize()
    {
        using (var context = new AppDbContext())
        {
            context.Database.EnsureCreated();

            if (!context.People.Any())
            {
                context.People.AddRange(
                    new Person { Name = "Anna", Age = 25 },
                    new Person { Name = "Erik", Age = 30 },
                    new Person { Name = "Lisa", Age = 22 }
                );

                context.SaveChanges();
            }
        }
    }
}
```

📝 **Förklaring:**  
- Skapar databasen och fyller den med testdata om den inte redan finns.

---

## 🖼️ **4. Skapa UI i XAML**

### **MainWindow.xaml**

```xml
<Window x:Class="DatabaseBindingExample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Databindning till Databas" Height="300" Width="400">
    
    <Grid Margin="10">
        <DataGrid ItemsSource="{Binding People}" AutoGenerateColumns="True" />
    </Grid>
</Window>
```

📝 **Förklaring:**  
- **`DataGrid`** är bunden till en lista av personer via **`ItemsSource="{Binding People}"`**.  
- `AutoGenerateColumns="True"` gör att kolumnerna skapas automatiskt.

---

## 🔄 **5. ViewModel för Databindning**

### **MainViewModel.cs**

```csharp
using System.Collections.ObjectModel;

public class MainViewModel
{
    public ObservableCollection<Person> People { get; set; }

    public MainViewModel()
    {
        using (var context = new AppDbContext())
        {
            People = new ObservableCollection<Person>(context.People);
        }
    }
}
```

📝 **Förklaring:**  
- **`ObservableCollection<Person>`** används eftersom den automatiskt uppdaterar UI vid ändringar.  
- Datan hämtas från databasen och binds till UI.

---

## 🏠 **6. Anslut ViewModel till View**

### **MainWindow.xaml.cs**

```csharp
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
        DatabaseInitializer.Initialize(); // Skapa och fyll databasen
        DataContext = new MainViewModel(); // Koppla ViewModel till UI
    }
}
```

📝 **Förklaring:**  
- **Databasen initieras** och fylls med testdata.  
- **`DataContext`** sätts till `MainViewModel`, så att UI kan binda mot datan.

---

## 🚀 **7. Resultat**

När du kör applikationen ser du en **DataGrid** med data från databasen:

| **Id** | **Name** | **Age** |
|--------|----------|---------|
| 1      | Anna     | 25      |
| 2      | Erik     | 30      |
| 3      | Lisa     | 22      |

---

## ⚙️ **8. Lägg till Ny Data från UI**

Vill du kunna lägga till data direkt från UI? Vi kan göra det!

### **Uppdaterad XAML**

```xml
<Grid Margin="10">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel Orientation="Horizontal" Margin="0,0,0,10">
        <TextBox x:Name="NameInput" Width="100" PlaceholderText="Namn"/>
        <TextBox x:Name="AgeInput" Width="50" Margin="5,0" PlaceholderText="Ålder"/>
        <Button Content="Lägg till" Width="75" Click="AddPerson_Click"/>
    </StackPanel>

    <DataGrid ItemsSource="{Binding People}" AutoGenerateColumns="True" Grid.Row="1"/>
</Grid>
```

### **Kod bakom:**

```csharp
private void AddPerson_Click(object sender, RoutedEventArgs e)
{
    using (var context = new AppDbContext())
    {
        var person = new Person
        {
            Name = NameInput.Text,
            Age = int.TryParse(AgeInput.Text, out int age) ? age : 0
        };

        context.People.Add(person);
        context.SaveChanges();
    }

    // Uppdatera UI
    DataContext = new MainViewModel();
}
```

📝 **Förklaring:**  
- Användaren kan skriva in ett namn och en ålder och klicka på "Lägg till".  
- Personen sparas i databasen och **DataGrid** uppdateras.

---

## 📚 **Sammanfattning**

### ✔️ Steg-för-steg:
1. **Entity Framework Core** hanterar databasen.  
2. **ViewModel** innehåller data från databasen.  
3. **Databindning** kopplar datan till UI via **DataGrid**.  
4. Data kan läggas till dynamiskt från UI.

---
