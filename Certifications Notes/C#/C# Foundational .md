
## 📝 Fundamentos de C\# y el Entorno .NET

Esta es la base de todo. Entender cómo funciona la plataforma y cómo interactuar con ella es el primer paso.

### El Ecosistema .NET

  * **.NET SDK y .NET Runtime (CLR):** Piensa en el **SDK (Software Development Kit)** como tu caja de herramientas para construir la aplicación (compilador, librerías, etc.). El **Runtime (o CLR - Common Language Runtime)** es el motor que necesita el usuario final para *ejecutar* esa aplicación. Tú, como desarrollador, necesitas el SDK; tus usuarios solo necesitan el Runtime.
  * **Biblioteca de Clases de .NET (.NET Class Library):** Es una gigantesca colección de código pre-hecho por Microsoft que te ahorra miles de horas de trabajo. La clase `Console` que usas para escribir en pantalla es un ejemplo perfecto; vive dentro de esta biblioteca.

### Salida por Consola: `Write` vs. `WriteLine`

  * `Console.WriteLine()`: Escribe el texto que le pases y luego **agrega un salto de línea** (como presionar "Enter"). Es ideal para mostrar mensajes uno debajo del otro.
  * `Console.Write()`: Escribe el texto y **deja el cursor justo al final**, en la misma línea. Úsalo cuando quieras que la siguiente escritura aparezca inmediatamente después, sin saltos.

-----

## Variables y Tipos de Datos

Las variables son los "contenedores" de tus datos. Elegir el tipo correcto y nombrarlas bien es crucial.

  * **Sensibilidad a Mayúsculas (Case-Sensitive):** En C\#, `string miVariable;` y `string mivariable;` son **dos variables completamente diferentes**. Esta es una fuente común de errores para principiantes.
  * **Inferencia de Tipos con `var`:** La palabra clave `var` es un atajo muy útil. Le dices al compilador: "Oye, mira el valor que le estoy asignando a esta variable y deduce tú mismo el tipo de dato".
      * **Regla de oro:** Una variable declarada con `var` **debe ser inicializada en la misma línea**. El compilador necesita ver el valor para saber qué tipo es.
        ```csharp
        // Correcto 👍
        var message = "Hello, world!"; // El compilador sabe que 'message' es un string.

        // Incorrecto 👎
        // var message;
        // message = "Hello, world!"; // Esto genera un error de compilación.
        ```
  * **Precisión en Operaciones Matemáticas:** Cuando realices divisiones que puedan resultar en decimales, evita usar tipos enteros (`int`). Si divides `int 7 / int 5`, el resultado será `1` (la parte decimal se trunca). Para obtener un resultado preciso, utiliza tipos de datos que soporten decimales, como `decimal`, `double`, o `float`.
      * **Pro-tip:** Usa `decimal` para cálculos financieros o cuando la precisión es crítica. Usa `double` para cálculos científicos o gráficos donde el rendimiento es más importante que la precisión perfecta.

-----

## 🔠 Manipulación de Cadenas de Texto (Strings)

Trabajar con texto es una de las tareas más comunes. C\# te da herramientas muy potentes para ello.

  * **Secuencias de Escape:** Son "códigos especiales" que empiezan con una barra invertida `\` para representar caracteres que son difíciles de escribir directamente.
      * `\n`: Nueva línea.
      * `\t`: Tabulación.
      * `\"`: Comillas dobles (para poder poner comillas dentro de un string que ya usa comillas).
      * `\\`: Barra invertida (para poder escribir una barra invertida literal).
      * `\uXXXX`: Para insertar caracteres Unicode específicos usando su código hexadecimal de 4 dígitos.
  * **Cadenas Literales Textuales (Verbatim Strings):** Usando el símbolo `@` al inicio de una cadena (`@"..."`), le dices a C\# que ignore las secuencias de escape y respete todos los espacios y saltos de línea tal cual los escribes. Es extremadamente útil para rutas de archivos.
    ```csharp
    // Sin @, tendrías que escapar las barras invertidas
    string oldPath = "c:\\source\\repos";

    // Con @, es mucho más limpio y legible
    string newPath = @"c:\source\repos";
    ```
  * **Interpolación de Cadenas (String Interpolation):** Esta es la forma moderna y recomendada de construir cadenas a partir de variables. Usando el símbolo `$` al inicio, puedes incrustar variables y expresiones directamente dentro de la cadena usando llaves `{}`.
    ```csharp
    string name = "Ana";
    int version = 11;

    // Forma antigua (concatenación)
    string messageOld = "Welcome, " + name + "! You are using .NET version " + version + ".";

    // Forma moderna y superior (interpolación) 😎
    string messageNew = $"Welcome, {name}! You are using .NET version {version}.";
    ```
  * **Combinación de Verbatim e Interpolación:** Puedes usar `@` y `$` juntos (`$@"..."`) para crear una cadena que es tanto literal como interpolada. ¡Lo mejor de ambos mundos\!

-----

## 🧮 Operadores y Expresiones

Entender cómo C\# evalúa las operaciones matemáticas y lógicas es fundamental para evitar bugs.

  * **Orden de Operaciones (PEMDAS):** C\# respeta el orden matemático estándar.
    1.  **P**aréntesis `()`
    2.  **E**xponentes
    3.  **M**ultiplicación `*` y **D**ivisión `/` (de izquierda a derecha)
    4.  **A**dición `+` y **S**ustracción `-` (de izquierda a derecha)
    <!-- end list -->
      * **Pro-tip:** No te fíes de tu memoria. Si una expresión es compleja, **usa paréntesis `()`** para dejar claro el orden que quieres. El código claro siempre es mejor que el código "inteligente".
  * **Operador Condicional Ternario `?:`**: Es una forma compacta de escribir un `if-else`. Su estructura es: `condicion ? valor_si_es_verdadero : valor_si_es_falso`.
    ```csharp
    int temperature = 25;
    string state = temperature > 20 ? "Caliente" : "Frio";
    // 'state' será "Caliente"
    ```

-----

## 🧠 Lógica de Control de Flujo

Esto te permite dirigir el "flujo" de tu programa, tomando decisiones y repitiendo tareas.

### Estructuras de Decisión (`if`/`else`)

  * **Expresión Booleana:** Es cualquier cosa que se evalúe como `true` o `false`. Puede ser una variable (`bool isReady = true;`), el resultado de una comparación (`age > 18`), o el valor que devuelve un método.
  * **Bloques de Código `{}`:** Un bloque de código agrupa una o más líneas que se ejecutarán juntas. En un `if`, si la condición es verdadera, se ejecuta el bloque de código que le sigue.
  * **Estructura `if`, `else if`, `else`:** Te permite evaluar múltiples condiciones en secuencia.
  * **Convenciones de Estilo para `if`:**
      * **Siempre usa llaves `{}`**, incluso para una sola línea. Esto evita errores si en el futuro agregas más código al bloque y te olvidas de poner las llaves. Es una práctica recomendada por Microsoft y te salvará de muchos dolores de cabeza.
        ```csharp
        // Recomendado 👍
        if (condition)
        {
            DoSomething();
        }

        // Evitar 👎 (aunque sea válido)
        if (condition) DoSomething();
        ```

### Estructuras de Iteración (Bucles)

  * **Arrays:** Son colecciones de tamaño fijo que guardan elementos del mismo tipo de dato. Se accede a cada elemento a través de un **índice numérico que empieza en 0**.
    ```csharp
    // Declara un array de strings que puede contener 3 elementos.
    string[] names = new string[3];
    names[0] = "Alice";
    names[1] = "Bob";
    names[2] = "Charlie";
    ```
  * **Bucle `foreach`:** Es la forma más simple y segura de **recorrer todos los elementos** de una colección (como un array). En cada iteración, te da una copia del elemento actual.
    ```csharp
    foreach (string name in names)
    {
        Console.WriteLine($"Hello, {name}!");
    }
    ```
  * **`foreach` vs. `for`:**
      * Usa `foreach` cuando solo necesites **leer** cada elemento de la colección, de principio a fin. Es más simple y menos propenso a errores.
      * Usa `for` cuando necesites más control: si necesitas modificar el elemento en el array, acceder al índice, recorrer la colección en orden inverso, o saltarte elementos.

-----

## 🛠️ Trabajando con Métodos y Objetos

Los métodos son bloques de código reutilizables. Los objetos son instancias de clases que agrupan datos y comportamiento.

  * **Métodos Estáticos vs. Métodos de Instancia:**
      * **Estáticos (Stateless):** No dependen de un objeto específico. Se llaman directamente desde la clase. `Console.WriteLine()` es estático porque no necesitas crear un "objeto consola" para usarlo. Son como herramientas de uso general.
      * **De Instancia (Stateful):** Pertenecen a un objeto específico (una instancia) y a menudo trabajan con los datos de ese objeto. Necesitas crear un objeto con `new` antes de poder llamarlos.
  * **El Operador `new`:** Cuando usas `new`, estás haciendo tres cosas:
    1.  Pides memoria para un nuevo objeto.
    2.  Creas el objeto en esa dirección de memoria.
    3.  Devuelves la "dirección" (la referencia) a ese objeto para que puedas guardarla en una variable.
    <!-- end list -->
    ```csharp
    // 'Random' es la clase (el plano).
    // 'randomGenerator' es la variable que guardará la referencia al objeto.
    // 'new Random()' es la creación del objeto (la instancia).
    Random randomGenerator = new Random();
    int randomNumber = randomGenerator.Next(1, 11); // .Next() es un método de instancia.
    ```
  * **Parámetros vs. Argumentos:**
      * **Parámetro:** Es la variable que se define en la **declaración del método**. Es el "espacio" que espera un valor.
      * **Argumento:** Es el **valor real** que le pasas al método cuando lo llamas.
  * **Métodos Sobrecargados (Overloaded):** Un mismo método puede tener varias "versiones" que se diferencian por el número y/o tipo de sus parámetros. `Console.WriteLine()` es un gran ejemplo: puedes llamarlo sin argumentos, con un string, con un número, etc.

-----

## ✒️ Buenas Prácticas y Convenciones de Código

Escribir código que funcione es solo la mitad del trabajo. La otra mitad es escribir código que otros (y tu "yo" del futuro) puedan entender.

  * **Nomenclatura de Variables:**
      * Usa nombres descriptivos en **camelCase** (ej: `firstName`, `totalAmount`).
      * Deben empezar con una letra o un guion bajo `_` (el `_` se reserva para casos especiales).
      * No pueden ser palabras clave de C\# (como `string` o `if`).
  * **Comentarios:** Usa comentarios para explicar el **"porqué"** de tu código, no el "qué". El código bien escrito ya explica qué hace; el comentario debe aclarar la intención o la razón de una decisión compleja.

¡Espero que esta organización te sirva para solidificar tus conocimientos\! Sigue así, vas por excelente camino. 👍
