# 21210379PDD

# 1. Singleton

**Ejemplo de la vida real**:  
Imagina un sistema que gestiona una base de datos. Solo queremos una única instancia de conexión a la base de datos para evitar múltiples conexiones que consumen recursos innecesariamente.

**Contexto**:  
El patrón Singleton asegura que una clase tenga solo una instancia y proporciona un punto de acceso global a esta instancia.

**Código C#**:
```csharp
public class DatabaseConnection
{
    // Instancia privada estática de la clase DatabaseConnection
    private static DatabaseConnection _instance;
    
    // Objeto para asegurar la sincronización en entornos multihilo
    private static readonly object _lock = new object();

    // Constructor privado para evitar instanciación externa
    private DatabaseConnection() { }

    // Método público para obtener la instancia única
    public static DatabaseConnection GetInstance()
    {
        // Bloqueo para asegurar que solo un hilo pueda acceder a esta sección
        lock (_lock)
        {
            // Si no hay una instancia, la crea
            if (_instance == null)
                _instance = new DatabaseConnection();
        }
        // Devuelve la instancia única
        return _instance;
    }

    // Método para simular la conexión a la base de datos
    public void Connect() => Console.WriteLine("Conectado a la base de datos.");
}
```
# 2. Factory Method

**Ejemplo de la vida real**:  
Imagina una aplicación que genera diferentes tipos de reportes, como PDF, Excel o Word. Según la solicitud del usuario, la aplicación debe crear el tipo adecuado de reporte.

**Contexto**:  
El Factory Method define una interfaz para crear un objeto, pero permite a las subclases decidir qué clase instanciar.

**Código C#**:
```csharp
// Clase abstracta que define la interfaz para los reportes
public abstract class Report
{
    // Método abstracto que debe ser implementado por las subclases
    public abstract void Generate();
}

// Clase que representa un reporte en PDF
public class PdfReport : Report
{
    // Implementación del método Generate para generar un reporte en PDF
    public override void Generate() => Console.WriteLine("Generando reporte en PDF.");
}

// Clase que representa un reporte en Excel
public class ExcelReport : Report
{
    // Implementación del método Generate para generar un reporte en Excel
    public override void Generate() => Console.WriteLine("Generando reporte en Excel.");
}

// Clase abstracta que define la interfaz para la fábrica de reportes
public abstract class ReportFactory
{
    // Método abstracto que debe ser implementado por las subclases para crear reportes
    public abstract Report CreateReport();
}

// Fábrica concreta para crear reportes en PDF
public class PdfReportFactory : ReportFactory
{
    // Implementación del método CreateReport para crear un reporte en PDF
    public override Report CreateReport() => new PdfReport();
}

// Fábrica concreta para crear reportes en Excel
public class ExcelReportFactory : ReportFactory
{
    // Implementación del método CreateReport para crear un reporte en Excel
    public override Report CreateReport() => new ExcelReport();
}
```
# 3. Abstract Factory

**Ejemplo de la vida real**:  
Imagina una aplicación de interfaz gráfica que necesita crear widgets como botones y menús para diferentes sistemas operativos, como Windows y Mac.

**Contexto**:  
El patrón Abstract Factory permite crear familias de objetos relacionados sin especificar sus clases concretas.

**Código C#**:
```csharp
// Interfaz para representar un botón
public interface IButton
{
    // Método para pintar el botón
    void Paint();
}

// Interfaz para representar un menú
public interface IMenu
{
    // Método para pintar el menú
    void Paint();
}

// Implementación de IButton para un botón de Windows
public class WindowsButton : IButton
{
    // Implementación del método Paint para dibujar el botón en Windows
    public void Paint() => Console.WriteLine("Dibujando botón en Windows.");
}

// Implementación de IButton para un botón de Mac
public class MacButton : IButton
{
    // Implementación del método Paint para dibujar el botón en Mac
    public void Paint() => Console.WriteLine("Dibujando botón en Mac.");
}

// Implementación de IMenu para un menú de Windows
public class WindowsMenu : IMenu
{
    // Implementación del método Paint para dibujar el menú en Windows
    public void Paint() => Console.WriteLine("Dibujando menú en Windows.");
}

// Implementación de IMenu para un menú de Mac
public class MacMenu : IMenu
{
    // Implementación del método Paint para dibujar el menú en Mac
    public void Paint() => Console.WriteLine("Dibujando menú en Mac.");
}

// Interfaz de la fábrica para crear botones y menús
public interface IGuiFactory
{
    // Método para crear un botón
    IButton CreateButton();
    // Método para crear un menú
    IMenu CreateMenu();
}

// Fábrica concreta para crear widgets de Windows
public class WindowsFactory : IGuiFactory
{
    // Implementación del método CreateButton para crear un botón de Windows
    public IButton CreateButton() => new WindowsButton();
    
    // Implementación del método CreateMenu para crear un menú de Windows
    public IMenu CreateMenu() => new WindowsMenu();
}

// Fábrica concreta para crear widgets de Mac
public class MacFactory : IGuiFactory
{
    // Implementación del método CreateButton para crear un botón de Mac
    public IButton CreateButton() => new MacButton();
    
    // Implementación del método CreateMenu para crear un menú de Mac
    public IMenu CreateMenu() => new MacMenu();
}
```
# 4. Builder

**Ejemplo de la vida real**:  
Imagina que estás construyendo una casa. El proceso de construcción tiene pasos específicos como construir las puertas, ventanas y el techo.

**Contexto**:  
El patrón Builder se usa para construir un objeto paso a paso, permitiendo que el mismo proceso de construcción pueda crear diferentes representaciones.

**Código C#**:
```csharp
// Clase que representa una Casa
public class House
{
    // Propiedades de la casa: puertas, ventanas y techo
    public string Doors { get; set; }
    public string Windows { get; set; }
    pu
```

# 5. Prototype

**Ejemplo de la vida real**:  
Imagina que estás creando fichas de ajedrez. En lugar de crear cada ficha desde cero, puedes clonar una ficha existente y modificar sus atributos según sea necesario.

**Contexto**:  
El patrón Prototype se usa para crear objetos duplicados de una instancia existente sin depender de su clase concreta.

**Código C#**:
```csharp
// Clase abstracta que representa una ficha de juego
public abstract class GamePiece
{
    // Método abstracto para clonar la ficha
    public abstract GamePiece Clone();
}

// Clase que representa una ficha de ajedrez
public class ChessPiece : GamePiece
{
    // Propiedades de la ficha: nombre y color
    public string Name { get; set; }
    public string Color { get; set; }

    // Implementación del método Clone usando MemberwiseClone para duplicar la ficha
    public override GamePiece Clone()
    {
        return this.MemberwiseClone() as ChessPiece;
    }

    // Método ToString para representar la ficha
    public override string ToString() => $"{Color} {Name}";
}
```
# 6. Adapter

**Ejemplo de la vida real**:  
Un adaptador para enchufes, donde un enchufe europeo se conecta a una toma americana usando un adaptador para convertir las interfaces.

**Contexto**:  
El patrón Adapter permite que clases con interfaces incompatibles trabajen juntas.

**Código C#**:
```csharp
// Interfaz para enchufes europeos
public interface IEuropeanPlug
{
    // Método para conectar a un socket europeo
    void ConnectEuropeanSocket();
}

// Clase que representa un enchufe europeo
public class EuropeanPlug : IEuropeanPlug
{
    // Implementación del método para conectar
    public void ConnectEuropeanSocket() => Console.WriteLine("Conectado a enchufe europeo.");
}

// Interfaz para sockets americanos
public interface IAmericanSocket
{
    // Método para conectar a un socket americano
    void ConnectAmericanSocket();
}

// Adaptador que permite conectar un enchufe europeo a un socket americano
public class PlugAdapter : IAmericanSocket
{
    // Referencia a un enchufe europeo
    private IEuropeanPlug _europeanPlug;

    // Constructor que recibe un enchufe europeo
    public PlugAdapter(IEuropeanPlug europeanPlug)
    {
        _europeanPlug = europeanPlug;
    }

    // Método que adapta la conexión al socket americano
    public void ConnectAmericanSocket() => _europeanPlug.ConnectEuropeanSocket();
}
```
7. Bridge
Ejemplo de la vida real:
Un sistema de notificaciones donde el mensaje puede enviarse a través de diferentes canales (Email, SMS), pero el tipo de mensaje es independiente del canal.
Contexto:
El patrón Bridge separa la abstracción de la implementación, permitiendo variar ambas independientemente.
**Código C#**:
```csharp
public interface IMessageSender
{
    void SendMessage(string message);
}

public class EmailSender : IMessageSender
{
    public void SendMessage(string message) => Console.WriteLine("Enviando Email: " + message);
}

public class SmsSender : IMessageSender
{
    public void SendMessage(string message) => Console.WriteLine("Enviando SMS: " + message);
}

public abstract class Message
{
    protected IMessageSender _sender;

    public Message(IMessageSender sender)
    {
        _sender = sender;
    }

    public abstract void Send(string message);
}

public class TextMessage : Message
{
    public TextMessage(IMessageSender sender) : base(sender) { }

    public override void Send(string message)
    {
        _sender.SendMessage(message);
    }
}
```
# 8. Composite

**Ejemplo de la vida real**:  
Un sistema de archivos donde las carpetas pueden contener archivos individuales o incluso otras carpetas, formando una estructura de árbol.

**Contexto**:  
El patrón Composite permite tratar objetos individuales y compuestos de manera uniforme.

**Código C#**:
```csharp
// Interfaz común para componentes del sistema de archivos
public interface IFileSystemComponent
{
    // Método para mostrar detalles del componente
    void ShowDetails();
}

// Clase que representa un archivo
public class File : IFileSystemComponent
{
    private string _name;

    // Constructor que recibe el nombre del archivo
    public File(string name)
    {
        _name = name;
    }

    // Implementación del método para mostrar detalles del archivo
    public void ShowDetails() => Console.WriteLine("Archivo: " + _name);
}

// Clase que representa una carpeta
public class Folder : IFileSystemComponent
{
    private string _name;
    private List<IFileSystemComponent> _children = new List<IFileSystemComponent>();

    // Constructor que recibe el nombre de la carpeta
    public Folder(string name)
    {
        _name = name;
    }

    // Método para agregar un componente (archivo o carpeta) a la carpeta
    public void Add(IFileSystemComponent component)
    {
        _children.Add(component);
    }

    // Implementación del método para mostrar detalles de la carpeta y sus hijos
    public void ShowDetails()
    {
        Console.WriteLine("Carpeta: " + _name);
        foreach (var child in _children)
        {
            child.ShowDetails();
        }
    }
}
```
