# ¿Qué es un Patrón de Diseño?

## Definición Fundamental
Los patrones de diseño son soluciones habituales a problemas que ocurren con frecuencia en el desarrollo de software. Son como **planos prefabricados** que se pueden personalizar para resolver un problema de diseño recurrente en tu código.

> **Advertencia Importante:**
> No se puede elegir un patrón y copiarlo en el programa como si se tratara de una función (`Func<T>`) o una librería (`Nuget package`).
> * **El patrón NO es código:** Es un concepto general.
> * **El patrón es una solución:** Tú debes implementarla según las necesidades de tu programa.

**El código del mismo patrón aplicado a dos programas distintos puede verse totalmente diferente.**

---

## Niveles de Patrones

No todos los patrones tienen el mismo alcance. Podemos dividirlos por su nivel de abstracción:

### 1. Idioms (Nivel Bajo)
Son los patrones más básicos y específicos de un lenguaje.
* **Contexto:** Se aplican a un único lenguaje de programación.
* *Ejemplo en C#:* El uso de `using` para manejar `IDisposable` es un idiom de .NET para la gestión de recursos.

### 2. Patrones de Diseño (Nivel Medio)
Soluciones a problemas comunes de diseño de componentes.
* **Contexto:** Independientes del lenguaje (se pueden hacer en C#, Java, Python, etc.).
* *Ejemplo:* Singleton, Factory Method.

### 3. Patrones de Arquitectura (Nivel Alto)
Son los más universales y definen la estructura global de la aplicación.
* **Contexto:** Organizan cómo se comunican los módulos enteros de un sistema.
* *Ejemplo:* MVC (Model-View-Controller), Microservicios.

---

## Clasificación de los Patrones


Los patrones de diseño clásicos (GoF - Gang of Four) se dividen en tres categorías principales según su propósito:

### 🏗️ Patrones Creacionales
Proporcionan mecanismos de **creación de objetos** que incrementan la flexibilidad y la reutilización de código existente.
* *El problema que resuelven:* "¿Cómo creo este objeto sin quedar atado a su clase concreta?"
* *Ejemplo:* Factory Method, Builder, Singleton.

### 🧩 Patrones Estructurales
Explican cómo **ensamblar objetos y clases** en estructuras más grandes, manteniendo la flexibilidad y eficiencia.
* *El problema que resuelven:* "¿Cómo hago que estas dos clases que no se conocen trabajen juntas?" o "¿Cómo simplifico esta estructura compleja?"
* *Ejemplo:* Adapter, Facade, Decorator.

### 📡 Patrones de Comportamiento
Se encargan de una **comunicación efectiva** y la asignación de responsabilidades entre objetos.
* *El problema que resuelven:* "¿Quién es responsable de qué?" y "¿Cómo se pasan mensajes los objetos de forma desacoplada?"
* *Ejemplo:* Observer, Strategy, Command.
