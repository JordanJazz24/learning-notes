## **POO (Programación Orientada a Objetos)**
Es un paradigma de programación que utiliza "objetos" para diseñar aplicaciones y programas informáticos. Se basa en encapsular datos (estado) y comportamiento (métodos) en unidades lógicas, facilitando el mantenimiento y la escalabilidad del software.

### **Clase**:
Es la definición abstracta,es  el molde o la plantill; Define **qué** atributos y comportamientos tendrá algo, pero no existe físicamente en la memoria como un dato concreto todavía.<img width="747" height="477" alt="image" src="https://github.com/user-attachments/assets/e38ef544-045f-44a4-ab34-ad995221d70e" />

### **Objetos**:
Es la instancia concreta creada a partir de la clase. Ocupa espacio en memoria y tiene datos específicos.<img width="841" height="673" alt="image" src="https://github.com/user-attachments/assets/738c73ee-aca4-451d-ae9a-cca0ed357175" />

## Jerarquia de clases

#### Clase padre, superclase o clase base:
Clase que define atributos y comportamientos comunes (genéricos), los cuales pueden ser heredados por otras clases (llamadas hijas o subclases).

### Subclases o clases hijas:
Clase que hereda el estado (atributos) y comportamiento (métodos) definidos por su clase padre, pero que puede agregar nuevos métodos y atributos, o modificar los heredados.

<img width="610" height="681" alt="image" src="https://github.com/user-attachments/assets/c9d4d5e3-2833-4c3a-a695-baa7476dc5ae" />

### Ejemplo:
```c#
using System;

// Clase base (padre)
public class Persona
{
    // Propiedades comunes
    public string Nombre { get; }
    public string Apellido { get; }
    public int Edad { get; }

    // Constructor
    public Persona(string nombre, string apellido, int edad)
    {
        Nombre = !string.IsNullOrWhiteSpace(nombre) ? nombre : throw new ArgumentException("Nombre inválido");
        Apellido = !string.IsNullOrWhiteSpace(apellido) ? apellido : throw new ArgumentException("Apellido inválido");
        Edad = edad >= 0 ? edad : throw new ArgumentException("Edad no puede ser negativa");
    }

    // Método común
    public virtual void Presentarse()
    {
        Console.WriteLine($"Hola, soy {Nombre} {Apellido} y tengo {Edad} años.");
    }
}
```
```c#
// Clase derivada (hija)
public class Empleado : Persona
{
    // Propiedades adicionales
    public string Puesto { get; }
    public decimal Salario { get; }

    // Constructor (usa base() para heredar el constructor de Persona)
    public Empleado(string nombre, string apellido, int edad, string puesto, decimal salario) 
        : base(nombre, apellido, edad)
    {
        Puesto = !string.IsNullOrWhiteSpace(puesto) ? puesto : throw new ArgumentException("Puesto inválido");
        Salario = salario >= 0 ? salario : throw new ArgumentException("Salario no puede ser negativo");
    }

    // Sobrescritura del método (override)
    public override void Presentarse()
    {
        base.Presentarse(); // Reutiliza el método de Persona
        Console.WriteLine($"Trabajo como {Puesto} y mi salario es {Salario:C}.");
    }

    // Método adicional específico de Empleado
    public void Trabajar()
    {
        Console.WriteLine($"{Nombre} está trabajando en {Puesto}...");
    }
}
```
```c#
// Ejemplo de uso
class Program
{
    static void Main()
    {
        Persona persona = new Persona("Ana", "Gómez", 30);
        persona.Presentarse(); 
        // Output: "Hola, soy Ana Gómez y tengo 30 años."

        Empleado empleado = new Empleado("Carlos", "Ruiz", 28, "Desarrollador", 50000);
        empleado.Presentarse(); 
        /* Output:
           "Hola, soy Carlos Ruiz y tengo 28 años.
           Trabajo como Desarrollador y mi salario es $50,000.00."
        */
        empleado.Trabajar(); 
        // Output: "Carlos está trabajando en Desarrollador..."
    }
}
```

## Pilares del POO

- **Abstraccion:** Consiste en crear modelos de objetos basados en "cosas" del mundo real, pero limitados a su contexto específico, representando todos los datos necesarios para dicho contexto y omitiendo el resto.

- **Encapsulamiento:** Ocultar el estado o implementacion interna de un objeto, permitiendo el acceso controlado únicamente a través de interfaces públicas (métodos/propiedades) para proteger la integridad de los datos

- **Herencia:** Mecanismo que permite crear nuevas clases basadas en una clase existente (padre), reutilizando sus atributos y comportamientos comunes. Las clases hijas pueden agregar nuevos miembros o sobrescribir los existentes.

- **Polimorfismo:** Capacidad de objetos de diferentes clases de responder al mismo mensaje (método) de formas distintas. Permite al programa tratar a un objeto hijo como si fuera su padre, ejecutando la implementación específica correcta en tiempo de ejecución.
Ejemplo: Un List<IPago> puede contener PagoPaypal, PagoTarjeta, PagoCripto, pero todos implementan un método Procesar().

## Relaciones entre clases

### **Depedencia:** 
La dependencia es el tipo de relación más básica y débil entre clases. Existe una dependencia entre dos clases cuando ciertos cambios en la definición de una clase puede provocar modifi- caciones en otra.
<img width="1027" height="266" alt="image" src="https://github.com/user-attachments/assets/6f30c828-516a-426c-ade6-a3d753cf21b4" />

### **Asociacion:** 
La asociación puede verse como un tipo especializado de dependencia, en la que un objeto siempre tiene acceso a los objetos con los que interactúa, mientras que la dependencia simple no establece un vínculo permanente entre los objetos
<img width="1185" height="340" alt="image" src="https://github.com/user-attachments/assets/bd2a9cdf-4c08-4560-be6b-b4544b2c190d" />
<img width="915" height="333" alt="image" src="https://github.com/user-attachments/assets/de788c11-d0dd-40c5-8840-a000ef428336" />

### **Agregacion:** 
La agregación es un tipo especializado de asociación que representa relaciones “uno a muchos”, “muchos a muchos” o “todo a parte” entre múltiples objetos, mientras que una asociación simple describe relaciones entre un par de objetos.
<img width="1119" height="295" alt="image" src="https://github.com/user-attachments/assets/61309f88-c14d-46a4-842f-b0033a533abc" />

### **Composicion :** 
La composición es un tipo específico de agregación en la que un objeto se compone de una o más instancias del otro. La diferencia entre ésta y otras relaciones está en que el componente sólo puede existir como parte del contenedor.
<img width="1218" height="387" alt="image" src="https://github.com/user-attachments/assets/47b26332-943b-4af9-9190-93b1b0a54524" />












