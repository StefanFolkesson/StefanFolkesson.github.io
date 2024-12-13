### WPF Lektion 7: Avslutningsprojekt – Bygga en Komplett WPF-Applikation

#### **Mål**
I detta avslutande projekt kommer du att kombinera allt du lärt dig om WPF: data binding, MVVM, navigering och flerfönsterhantering.

---

### **Projektbeskrivning**
Vi ska bygga en enkel “Kontaktbok”-applikation där användaren kan:
- Visa en lista med kontakter.
- Lägga till nya kontakter.
- Redigera eller ta bort befintliga kontakter.

#### **Funktioner**
- Master-detail vy för kontaktlistan.
- Navigering mellan olika vyer.
- Dialogfönster för att hantera kontaktformulär.
- MVVM-designmönster för tydlig kodstruktur.

---

### **Steg 1: Projektstruktur**
Skapa följande mappar för att hålla ordning:

- **Models:** För att definiera datamodeller.
- **ViewModels:** För att hantera logik och binding.
- **Views:** För alla XAML-filer.
- **Services:** För navigation och dialoger.

---

### **Steg 2: Skapa Modellen**
Skapa en klass `Contact` i **Models**-mappen:

```csharp
public class Contact
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
    public string Phone { get; set; }
}
```

---

### **Steg 3: Huvud-ViewModel**
Skapa en klass `MainViewModel` i **ViewModels**-mappen:

```csharp
using System.Collections.ObjectModel;
using System.Windows.Input;

public class MainViewModel : BaseViewModel
{
    public ObservableCollection<Contact> Contacts { get; set; }
    public Contact SelectedContact { get; set; }

    public ICommand AddContactCommand { get; }
    public ICommand EditContactCommand { get; }
    public ICommand DeleteContactCommand { get; }

    public MainViewModel()
    {
        Contacts = new ObservableCollection<Contact>();

        AddContactCommand = new RelayCommand(AddContact);
        EditContactCommand = new RelayCommand(EditContact, CanEditOrDelete);
        DeleteContactCommand = new RelayCommand(DeleteContact, CanEditOrDelete);
    }

    private void AddContact(object obj)
    {
        // Öppna dialogfönster för att lägga till en ny kontakt
    }

    private void EditContact(object obj)
    {
        // Öppna dialogfönster för att redigera vald kontakt
    }

    private void DeleteContact(object obj)
    {
        Contacts.Remove(SelectedContact);
    }

    private bool CanEditOrDelete(object obj)
    {
        return SelectedContact != null;
    }
}
```

---

### **Steg 4: Huvudfönster och Master-Detail Vy**
Skapa ett huvudfönster med en master-detail layout i `MainWindow.xaml`:

```xml
<Window x:Class="ContactBook.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Kontaktbok" Height="400" Width="600">
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="2*" />
            <ColumnDefinition Width="3*" />
        </Grid.ColumnDefinitions>

        <!-- Master-listan -->
        <ListBox ItemsSource="{Binding Contacts}"
                 SelectedItem="{Binding SelectedContact}"
                 DisplayMemberPath="FirstName" />

        <!-- Detail-vyn -->
        <StackPanel Grid.Column="1" Margin="10">
            <TextBlock Text="{Binding SelectedContact.FirstName}" FontSize="16" FontWeight="Bold" />
            <TextBlock Text="{Binding SelectedContact.LastName}" />
            <TextBlock Text="{Binding SelectedContact.Email}" />
            <TextBlock Text="{Binding SelectedContact.Phone}" />
        </StackPanel>

        <!-- Kommandoknappar -->
        <StackPanel Grid.Row="1" Orientation="Horizontal" HorizontalAlignment="Center">
            <Button Content="Lägg till" Command="{Binding AddContactCommand}" />
            <Button Content="Redigera" Command="{Binding EditContactCommand}" />
            <Button Content="Ta bort" Command="{Binding DeleteContactCommand}" />
        </StackPanel>
    </Grid>
</Window>
```

---

### **Steg 5: Dialogfönster för Kontaktformulär**
1. Skapa ett nytt fönster `ContactForm.xaml`:

```xml
<Window x:Class="ContactBook.ContactForm"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Kontaktformulär" Height="300" Width="400">
    <StackPanel Margin="10">
        <TextBox Text="{Binding Contact.FirstName}" PlaceholderText="Förnamn" />
        <TextBox Text="{Binding Contact.LastName}" PlaceholderText="Efternamn" />
        <TextBox Text="{Binding Contact.Email}" PlaceholderText="E-post" />
        <TextBox Text="{Binding Contact.Phone}" PlaceholderText="Telefon" />
        <Button Content="Spara" Command="{Binding SaveCommand}" />
    </StackPanel>
</Window>
```

2. Hantera dialogresultat i koden:

```csharp
public partial class ContactForm : Window
{
    public ContactForm(Contact contact)
    {
        InitializeComponent();
        DataContext = new ContactFormViewModel(contact);
    }
}
```

---

### **Steg 6: Navigering mellan vyer**
Använd en `Frame` i huvudfönstret om du vill implementera navigering mellan vyer, till exempel en startsida och kontaktlistan.

---

### **Vad blir nästa steg?**
Experimentera med att bygga ut din Kontaktbok-applikation. Lägg till fler fält, validering, och spara data till en fil eller databas!

