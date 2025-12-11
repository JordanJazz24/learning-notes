# Resumen OOP

## **POO (Programación Orientada a Objetos)**
Es un paradigma de programación que utiliza "objetos" para diseñar aplicaciones y programas informáticos. Se basa en encapsular datos (estado) y comportamiento (métodos) en unidades lógicas, facilitando el mantenimiento y la escalabilidad del software.

### **Clase**:
Las clases son tipos de datos definidos por el usuario, que contienen atributos (datos) y métodos (comportamientos). Se pueden considerar como un "molde" o plantilla para crear objetos.
<img width="747" height="477" alt="image" src="https://github.com/user-attachments/assets/e38ef544-045f-44a4-ab34-ad995221d70e" />


### **Objetos**:
Son instancias concretas (ejemplares) de una clase. Cada objeto tiene sus propios valores para los atributos.
<img width="841" height="673" alt="image" src="https://github.com/user-attachments/assets/738c73ee-aca4-451d-ae9a-cca0ed357175" />

### Jerarquia de clases

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

## Conceptos Clave

- **Abstraccion:** Consiste en crear modelos de objetos basados en "cosas" del mundo real, pero limitados a su contexto específico, representando todos los datos necesarios para dicho contexto y omitiendo el resto.

- **Encapsulamiento:** Ocultar el estado o implementacion interna de un objeto, permitiendo el acceso controlado únicamente a través de interfaces públicas (métodos/propiedades) para proteger la integridad de los datos
<img width="619" height="590" alt="image" src="https://github.com/user-attachments/assets/41ae1851-7ae4-4375-be85-2583432e515b" />

- **Herencia:** Mecanismo que permite crear nuevas clases basadas en una clase existente (padre), reutilizando sus atributos y comportamientos comunes. Las clases hijas pueden agregar nuevos miembros o sobrescribir los existentes.

- **Polimorfismo:** es la capacidad que tiene un programa de detectar la verdadera clase de un objeto e invocar su implementación
