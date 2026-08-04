
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

-----



## 💾 Tipos de Datos en Profundidad

Entender cómo C\# maneja los datos "bajo el capó" es lo que diferencia a un programador de un buen ingeniero de software.

### ¿Qué son los Datos?

En su nivel más bajo, toda la información en un programa es solo una serie de **bits** (interruptores binarios en estado 0 o 1, "apagado" o "encendido"). Cuando agrupas 8 bits, formas un **byte**. Con un solo byte, puedes representar 256 combinaciones diferentes. C\# abstrae toda esta complejidad, permitiéndote trabajar con tipos de datos como `int`, `string`, etc., en lugar de manipular bits directamente.

### Tipos por Valor vs. Tipos por Referencia (¡Concepto Clave\!)

Esta es una de las distinciones más importantes en C\# y .NET. Entenderla te ahorrará incontables horas de depuración en el futuro.

  * **Tipos por Valor (Value Types):** Las variables de este tipo **contienen el dato directamente**. Piensa en ellas como una caja que tiene el valor *dentro* de ella. Ejemplos comunes son `int`, `double`, `decimal`, `bool`, y `char`.
      * Cuando copias una variable de tipo valor, creas una **copia independiente** del dato.
  * **Tipos por Referencia (Reference Types):** Estas variables no contienen el dato, sino una **"dirección" o referencia a la ubicación en memoria donde está el dato**. Piensa en ellas como una nota adhesiva con la dirección de una casa. El dato real (el objeto) está en la casa. Ejemplos son `string`, `arrays`, y cualquier clase que tú crees.
      * Cuando copias una variable de tipo referencia, solo estás copiando la dirección. **Ambas variables apuntan al mismo objeto original**. Si modificas el objeto a través de una variable, el cambio será visible a través de la otra.

### Cómo Elegir el Tipo de Dato Correcto

  * **Precisión ante todo:** No elijas un tipo de dato solo porque ocupa menos memoria (eso es "optimización prematura"). Elige el tipo que **mejor representa la naturaleza de tus datos**.
  * **Usa `decimal` para Dinero y Finanzas:** Aunque ocupa más memoria que `double` o `float`, el tipo `decimal` está diseñado para cálculos financieros y matemáticos donde la precisión es crítica y los errores de redondeo son inaceptables.
  * **Evita la Optimización Prematura:** No asumas que usar tipos de datos más pequeños (como `byte` en lugar de `int`) hará tu aplicación más rápida. La prioridad es la **corrección y la legibilidad**. Más adelante, si el rendimiento es un problema, se usan herramientas especiales (profilers) para medir y encontrar los cuellos de botella reales.

-----

## 🔄 Conversión de Tipos de Datos

Es muy común necesitar convertir un dato de un tipo a otro. C\# ofrece varias formas de hacerlo, cada una con sus reglas.

### Conversión Implícita vs. Explícita

  * **Conversión Ampliadora (Widening Conversion):** Ocurre cuando conviertes de un tipo que almacena menos información a uno que puede almacenar más (ej: de `int` a `decimal`). No hay riesgo de perder datos, por lo que el compilador la realiza **automáticamente (implícitamente)** por ti.
  * **Conversión Reductora (Narrowing Conversion):** Ocurre cuando conviertes de un tipo que almacena más información a uno que almacena menos (ej: de `decimal` a `int`). Aquí **existe el riesgo de perder datos**, por lo que el compilador te exige que seas **explícito** y le digas que sabes lo que estás haciendo.

### Técnicas de Conversión

1.  **Casting (Conversión Explícita):** Es la forma más directa. Le dices al compilador "confía en mí, quiero forzar esta conversión". Se usa para conversiones reductoras.
    ```csharp
    decimal myDecimal = 3.14m;
    int myInt = (int)myDecimal; // myInt será 3. ¡Se pierden los decimales!
    ```
2.  **Métodos de Ayuda:** Muchos tipos de datos tienen métodos incorporados para ayudar con las conversiones.
      * `variable.ToString()`: Casi cualquier variable puede convertirse a un `string`.
      * `tipo.Parse()`: Convierte un `string` al tipo de dato especificado. **¡Cuidado\!** Si el string no tiene un formato válido, tu programa se detendrá con una excepción (error).
        ```csharp
        string numberStr = "123";
        int parsedNumber = int.Parse(numberStr);
        ```
3.  **La Clase `Convert`:** Proporciona un conjunto de métodos para convertir entre una amplia gama de tipos. Es más robusta que el casting en algunos casos.
    ```csharp
    string value = "456";
    int convertedValue = Convert.ToInt32(value);
    ```

### Diferencia Clave: Casting Trunca, `Convert` Redondea

  * **Casting `(int)`:** Simplemente **corta (trunca)** la parte decimal. `(int)1.999m` resulta en `1`.
  * **`Convert.ToInt32()`:** Intenta **redondear** al número entero más cercano (usando redondeo bancario o "al par más cercano" por defecto). `Convert.ToInt32(1.999m)` resulta en `2`.

### Conversión Segura con `TryParse()`

¿Qué pasa si intentas convertir un texto como `"hola"` a un número? `int.Parse()` fallará y romperá tu programa. La forma profesional de manejar esto es con `TryParse()`.

  * El método `int.TryParse()` intenta la conversión.
      * Si tiene éxito, devuelve `true` y guarda el resultado en una variable que le pasas con la palabra clave `out`.
      * Si falla, devuelve `false` y no lanza una excepción.
  * La palabra clave `out` significa que el método puede "devolver" un valor a través de ese parámetro, además de su valor de retorno normal (`true`/`false`).

<!-- end list -->

```csharp
string value = "123a";
int numericValue;

// Intenta convertir 'value'. Si funciona, 'success' será true y 'numericValue' tendrá el número.
bool success = int.TryParse(value, out numericValue);

if (success)
{
    Console.WriteLine($"Conversión exitosa: {numericValue}");
}
else
{
    Console.WriteLine("La conversión falló. El valor no es un número válido.");
}
```

-----

## ⛓️ Operaciones con Arrays y Strings

Tanto los arrays como los strings tienen una gran cantidad de métodos de ayuda muy potentes para manipularlos.

### Métodos de Ayuda de la Clase `Array`

  * `Array.Sort()`: Ordena los elementos del array (alfabéticamente para strings, numéricamente para números).
  * `Array.Reverse()`: Invierte el orden de los elementos del array.
  * `Array.Clear()`: "Limpia" los elementos de un array, estableciéndolos a su valor por defecto (`0` para números, `null` para tipos de referencia).
  * `Array.Resize()`: Cambia el número de elementos que puede contener un array.

### `null` vs. Cadena Vacía (`""`)

Al usar `Array.Clear()` en un array de strings, los elementos se establecen a `null`.

  * **`null`:** Significa que la variable **no apunta a ningún objeto en memoria**. Es la ausencia de una referencia.
  * **Cadena Vacía (`""`)**: Es un objeto `string` real que existe en memoria, pero que simplemente **no tiene caracteres**.

### Métodos de `String` que Interactúan con Arrays

  * `string.ToCharArray()`: Convierte un string en un array de caracteres (`char[]`).
  * `string.Split(delimitador)`: Divide un string en un array de strings (`string[]`) usando un carácter o cadena como separador.
    ```csharp
    string csvData = "Juan,Perez,30";
    string[] items = csvData.Split(','); // items será un array con ["Juan", "Perez", "30"]
    ```
  * `string.Join(delimitador, array)`: Es la operación inversa a `Split`. Une los elementos de un array en un solo string, poniendo un delimitador entre ellos.
    ```csharp
    string[] names = { "Ana", "Luis", "Eva" };
    string result = string.Join(" | ", names); // result será "Ana | Luis | Eva"
    ```

# 🌐 Formateo de Cadenas y Datos (String Formatting)

C# ofrece dos maneras principales de inyectar variables dentro de un texto: el estilo clásico (**Composite Formatting**) y el estilo moderno (**String Interpolation**). Ambas son perfectamente válidas, pero tienen casos de uso distintos.

## 1. Formateo Compuesto (Composite Formatting)

Es la forma tradicional. Utiliza marcadores de posición numerados (llamados *tokens*) dentro de una cadena base, y luego se le pasan las variables en orden como argumentos. El conteo siempre empieza en `{0}`.

- Funciona con `string.Format()` o directamente dentro de `Console.WriteLine()`.

```csharp
string first = "Hello";
string second = "World";
// El {0} se reemplaza por 'first' y el {1} por 'second'
string result = string.Format("{0} {1}!", first, second);
```

## 2. Interpolación de Cadenas (String Interpolation)

Es la sintaxis moderna (anteponiendo el símbolo `$`). En lugar de números, se coloca el nombre de la variable directamente dentro de las llaves `{}`. Es mucho más legible y es la opción recomendada por defecto en el día a día.

```csharp
string first = "Hello";
string second = "World";
string result = $"{first} {second}!"; // Output: Hello World!
```

---

## 🌍 Especificadores de Formato Numérico y Cultural

Dentro de las llaves (ya sea en formato compuesto o interpolado) se puede añadir un especificador de formato usando los dos puntos `:` 

**Sintaxis:** `{variable:Formato}`

> ⚠️ **Nota del Senior:** El resultado de estos formatos depende de la cultura (*Culture-Specific*) de la computadora donde se ejecuta el código. Por ejemplo, la cultura `en-US` (Estados Unidos) usa el punto `.` para decimales y la coma `,` para miles, además del símbolo `$`. La cultura `es-ES` (España) o `es-MX` (México) cambiará los símbolos y la moneda automáticamente.

### 💰 Formateo de Moneda (`:C`)

Formatea un número (`int` o `decimal`) como dinero, añadiendo el símbolo de moneda correspondiente y dos decimales por defecto.

```csharp
decimal price = 123.45m;
Console.WriteLine($"Price: {price:C}"); // Output (en-US): $123.45
```

### 🔢 Formateo de Números Generales (`:N`)

Hace que los números grandes sean más legibles añadiendo separadores de miles. Por defecto muestra 2 decimales.

**Control de precisión:** Se puede añadir un número justo después del especificador para forzar la cantidad de decimales exactos que se desean mostrar (ej: `:N4`).

```csharp
decimal measurement = 123456.78912m;
Console.WriteLine($"Default: {measurement:N}");   // Output: 123,456.79 (Redondea a 2)
Console.WriteLine($"Preciso: {measurement:N4}"); // Output: 123,456.7891 (Fuerza 4)
```

### 📊 Formateo de Porcentajes (`:P`)

Multiplica automáticamente el valor por 100, le añade el símbolo de porcentaje `%` y lo redondea a 2 decimales por defecto. Al igual que con `:N`, se pueden controlar los decimales agregando un número (ej: `:P2`).

```csharp
decimal tax = .36785m;
Console.WriteLine($"Tax rate: {tax:P2}"); // Output: 36.79%
```

---

## 🔀 Combinando Enfoques

Se pueden realizar operaciones matemáticas directamente dentro de las llaves y aplicarles formato en la misma línea, o ir acumulando texto formateado en una misma variable.

```csharp
decimal price = 67.55m;
decimal salePrice = 59.99m;

// Guardamos el texto formateado en una variable usando string.Format
string yourDiscount = string.Format("You saved {0:C2} off the regular {1:C2} price. ", 
                                     (price - salePrice), price);

// Concatenamos usando interpolación y formato de porcentaje en la misma línea
yourDiscount += $"A discount of {(price - salePrice)/price:P2}!";
```

---

## 🧰 Métodos Incorporados para Manipulación de Strings

Los strings en C# son **inmutables** (no cambian en memoria, cada modificación crea un string nuevo bajo el capó). Para facilitarnos la vida, la clase `string` tiene un arsenal de métodos útiles agrupados por su comportamiento:

| Categoría | Métodos Clave | ¿Qué hacen? |
|-----------|---------------|-----------|
| **Alineación y Espacios** | `PadLeft()`, `PadRight()` | Añaden espacios en blanco (o caracteres) a la izquierda o derecha para alinear columnas de texto en pantallas o reportes. |
| **Limpieza y Comparación** | `Trim()`, `TrimStart()`, `TrimEnd()`, `Length` | Eliminan los espacios vacíos innecesarios al inicio o al final del texto. `Length` indica cuántos caracteres tiene la cadena. |
| **Búsqueda e Inspección** | `Contains()`, `StartsWith()`, `EndsWith()`, `Substring()` | Devuelven un booleano (`true`/`false`) si el texto contiene, empieza o termina con cierta palabra. `Substring()` extrae un fragmento del texto indicando la posición. |
| **Modificación de Contenido** | `Replace()`, `Insert()`, `Remove()` | Reemplazan caracteres por otros, insertan texto en una posición específica o eliminan fragmentos de la cadena. |
| **Conversión a Estructuras** | `Split()`, `ToCharArray()` | Convierten el string en piezas manejables, ya sea un array de palabras (`string[]`) o un array de letras individuales (`char[]`). |

---

# 🔍 Búsqueda Avanzada y Manipulación de Substrings

Esta sección cubre cómo localizar caracteres, extraer fragmentos de texto específicos mediante límites y limpiar cadenas utilizando métodos avanzados de la clase `string`.

---

## 1. Métodos de Localización de Índices

Para extraer información de un texto, primero debemos saber exactamente dónde se encuentra. C# calcula las posiciones utilizando un índice basado en cero (`0-indexed`).

### `IndexOf()`

Busca de izquierda a derecha y devuelve la posición de la **primera ocurrencia** de un carácter o cadena. Si no encuentra nada, devuelve `-1`.

```csharp
string text = "Hello World World";
int position = text.IndexOf("World");
Console.WriteLine(position); // Output: 6
```

### `LastIndexOf()`

Busca de derecha a izquierda (desde el final de la cadena hacia el principio) y devuelve la posición de la **última ocurrencia**.

```csharp
string text = "Hello World World";
int position = text.LastIndexOf("World");
Console.WriteLine(position); // Output: 12
```

### `IndexOfAny(char[])`

Examina la cadena y devuelve el índice de la primera coincidencia de **cualquier** carácter que se encuentre dentro del array proporcionado. Es ideal para buscar múltiples tipos de símbolos a la vez.

```csharp
string text = "Hello123World456";
char[] digits = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' };
int position = text.IndexOfAny(digits);
Console.WriteLine(position); // Output: 5 (posición del '1')
```

> 💡 **Tip de Sobrecarga:** `IndexOf` e `IndexOfAny` aceptan un parámetro opcional llamado `startPosition`. Esto le dice al método que ignore el inicio de la cadena y comience a buscar a partir de ese índice en adelante.

```csharp
string text = "Hello World World";
int position = text.IndexOf("World", 7); // Comienza a buscar desde posición 7
Console.WriteLine(position); // Output: 12
```

---

## 2. Extracción de Substrings con `Substring()`

El método `Substring()` corta una cadena y devuelve un fragmento. Su funcionamiento requiere entender sus parámetros: `Substring(inicio, longitud)`.

### Algoritmo para extraer texto entre símbolos

Para extraer el contenido dentro de un paréntesis sin incluir el paréntesis mismo, se debe calcular la longitud matemática del texto interior y desplazar el índice inicial en `+1`:

```csharp
string message = "Find what is (inside the parentheses)";

int openingPosition = message.IndexOf('(');
int closingPosition = message.IndexOf(')');

// Sumamos 1 para saltarnos el carácter '(' y no incluirlo en el resultado
openingPosition += 1; 

int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length)); 
// Output: inside the parentheses
```

### Extracción múltiple en bucle

Cuando una cadena tiene múltiples bloques de texto que queremos extraer, combinamos `IndexOf()`, un bucle `while` y una sobrecarga de `Substring(inicio)` que recorta la cadena eliminando lo que ya procesamos:

```csharp
string message = "(What if) there are (more than) one (set of parentheses)?";

while (true)
{
    int openingPosition = message.IndexOf('(');
    if (openingPosition == -1) break; // Si ya no hay más '(', salimos del bucle

    openingPosition += 1;
    int closingPosition = message.IndexOf(')');
    int length = closingPosition - openingPosition;
    Console.WriteLine(message.Substring(openingPosition, length));

    // Modificamos 'message' para que contenga solo el texto restante sin procesar
    message = message.Substring(closingPosition + 1);
}
// Output:
// What if
// more than
// set of parentheses
```

---

## 3. Modificación y Limpieza: `Remove()` vs `Replace()`

C# proporciona métodos directos para alterar el contenido de un string (recordando que los strings son **inmutables** y estos métodos devuelven una nueva cadena en memoria).

### `Remove(inicio, longitud)`

Elimina una cantidad específica de caracteres a partir de una posición exacta. Se usa cuando la estructura física del texto es fija (por ejemplo, archivos de ancho fijo o registros de bases de datos antiguas).

```csharp
string text = "Hello World";
string result = text.Remove(5, 6); // Elimina 6 caracteres empezando en posición 5
Console.WriteLine(result); // Output: Hello
```

### `Replace(antiguo, nuevo)`

Busca todas las ocurrencias de una subcadena y las reemplaza por otra. Si se reemplaza por una cadena vacía `""`, funciona como un eliminador global.

```csharp
// Ejemplo de Replace para limpiar datos estructurados
string message = "This--is--ex-amp-le--da-ta";
message = message.Replace("--", " ");
message = message.Replace("-", "");
Console.WriteLine(message); 
// Output: This is example data
```

### Comparativa de uso

| Método | Caso de Uso | Ejemplo |
|--------|-----------|---------|
| `Remove()` | Eliminar por posición exacta | Eliminar caracteres específicos en una posición conocida |
| `Replace()` | Buscar y reemplazar patrones | Limpiar caracteres especiales o normalizar formato |

---

# 🎛️ Parámetros Opcionales y Argumentos Nombrados

---

## Parámetros Opcionales

Un parámetro es **opcional** cuando tiene un valor por defecto. Los parámetros **requeridos deben venir primero**.

```csharp
void RSVP(string name, int partySize = 1, string allergies = "none", bool inviteOnly = true)
{
    Console.WriteLine($"Guest: {name}, Party: {partySize}, Allergies: {allergies}");
}

RSVP("Alice");                           // Usa todos los valores por defecto
RSVP("Bob", 3);                          // Omite allergies e inviteOnly
RSVP("Charlie", 2, "gluten");            // Omite inviteOnly
RSVP("Diana", 4, "nuts", false);         // Especifica todos
```

---

## Argumentos Nombrados

Los **argumentos nombrados** mejoran la legibilidad al especificar explícitamente qué parámetro recibe cada valor.

```csharp
// ❌ Confuso
RSVP("Linh", 2, "none", false);

// ✅ Claro
RSVP(name: "Linh", partySize: 2, allergies: "none", inviteOnly: false);
```

---

## Combinando Argumentos Posicionales y Nombrados

| Válido ✅ | Inválido ❌ |
|---------|----------|
| `RSVP("Linh", 2, allergies: "none")` | `RSVP(name: "Linh", 2)` |
| `RSVP("Linh", inviteOnly: false)` | `RSVP(2, "Linh")` |
| `RSVP(name: "Linh", allergies: "nuts")` | Posicionales **NO** pueden seguir a nombrados |

**Regla:** Los argumentos **posicionales deben venir primero** y respetando el orden de los parámetros.


## 🛡️ Depuración, Pruebas y Manejo de Excepciones

Esta sección cubre el ciclo de estabilidad del software: cómo aseguramos que el código funcione (testing), cómo encontramos las fallas si no lo hace (debugging) y cómo gestionamos los errores inevitables en tiempo de ejecución (exception handling).

---

### 1. Conceptos Fundamentales: Errores vs. Excepciones

* **Build Errors (Errores de Compilación):** Errores de sintaxis o tipo (por ejemplo, falta un `;` o usar un tipo no válido). Ocurren *antes* de que el programa se ejecute y son detectados por el compilador.
* **Exceptions (Excepciones):** Errores que ocurren *mientras* la aplicación se está ejecutando (Runtime). Por ejemplo, intentar dividir por cero, falta de conexión a base de datos o intentar acceder a un archivo que no existe.

> 🧠 **Manejo de Excepciones (Exception Handling):** Es el proceso mediante el cual el desarrollador anticipa y gestiona estos problemas en tiempo de ejecución usando bloques `try-catch-finally`, evitando que la aplicación falle catastróficamente ("crash") ante el usuario final.

---

### 2. Clasificación del Software Testing

El testing valida que el software cumpla con sus requerimientos. Se divide en dos grandes categorías:

| Categóría | Descripción | Ejemplos |
| --- | --- | --- |
| **Pruebas Funcionales** | Verifican **QUÉ** hace el sistema (si cumple con las reglas de negocio y comportamiento esperado). | • **Unit Testing** (pruebas aisladas de un método/clase, responsabilidad típica del dev).<br>

<br>• **Integration Testing** (prueba interacción entre componentes).<br>

<br>• **System & Acceptance Testing** (E2E / Validación de negocio). |
| **Pruebas No Funcionales** | Verifican **CÓMO** lo hace (rendimiento, seguridad, comportamiento en carga). | • **Performance Testing**<br>

<br>• **Security Testing**<br>

<br>• **Usability & Compatibility Testing** |

> 💡 **Enfoque Moderno:** En metodologías como **TDD (Test-Driven Development)**, las pruebas unitarias se escriben *antes* de escribir el código de producción.

---

### 3. Depuración de Código (Debugging)

El **debugging** es el proceso de aislar, diagnosticar y corregir comportamientos inesperados o excepciones en tiempo de ejecución.

* **❌ Práctica a evitar:** Llenar el código de `Console.WriteLine()` para "adivinar" variables o releer el código 10 veces.
* **✅ Práctica profesional:** Utilizar el **Debugger** del IDE (Visual Studio / VS Code).
* **Breakpoints (Puntos de interrupción):** Pausan la ejecución en una línea exacta.
* **Step Over / Step Into / Step Out:** Permiten avanzar línea por línea o entrar dentro de funciones.
* **Watch / Immediate Window:** Permite inspeccionar el estado exacto de variables y memoria en tiempo real.



---

### 4. La Clase `Exception` en C# y .NET

Todas las excepciones en C# son objetos que heredan de la clase base `System.Exception`.

```csharp
try
{
    // Código potencialmente peligroso
    int result = int.Parse("ABC"); 
}
catch (FormatException ex)
{
    // Manejo específico del error
    Console.WriteLine($"Error de formato: {ex.Message}");
}
catch (Exception ex)
{
    // Captura genérica de cualquier otra excepción no prevista
    Console.WriteLine($"Error inesperado: {ex.Message}");
}
finally
{
    // Código que SIEMPRE se ejecuta (ideal para liberar recursos, cerrar archivos o conexiones)
    Console.WriteLine("Limpieza terminada.");
}

```

#### Propiedades clave de un objeto `Exception`:

* **`Message`:** Texto explicativo del error.
* **`StackTrace`:** La cadena de llamadas a métodos que provocaron el error (vital para saber la línea exacta de la falla).
* **`InnerException`:** La excepción original si fue capturada y re-envuelta en otra.

---

## 💡 Consejo de Arquitectura Senior:

1. **No uses excepciones para controlar el flujo normal:** Las excepciones son **costosas en rendimiento**. No uses `try-catch` para validar si un string es número; usa `int.TryParse()` en su lugar.
2. **Atrapa solo las excepciones que puedes manejar:** Si capturas una excepción solo para tragarla (`catch { }`) sin registrarla ni solucionarla, estás escondiendo bugs graves en producción (patrón conocido como *Exception Swallowing*).

## 🐞 Depuración (Debugging) en C# con VS Code

### 1. Integración con el .NET Runtime
El depurador de VS Code no lee código fuente línea por línea; se conecta dinámicamente al **.NET Runtime (CLR)** mediante APIs internas para controlar hilos, pausar la ejecución y evaluar la memoria en tiempo real.

---

### 2. Tipos de Breakpoints

| Tipo | Descripción | Uso Práctico |
| :--- | :--- | :--- |
| **Estándar** | Pausa la ejecución siempre que pasa por esa línea. | Inspección general. |
| **Conditional** | Se activa solo si se cumple una condición (`num > 5`). | Errores en casos borde o datos específicos. |
| **Hit Count** | Se activa tras ejecutarse N veces (`= 100`). | Bucles largos (`for`/`while`). |
| **Logpoint** | **No detiene** el programa; imprime un log en la consola. | Rastrear comportamiento sin pausar el flujo. |

---

### 3. Configuración Principal: `.vscode/launch.json`

Define cómo VS Code compila y ejecuta la aplicación antes de conectar el depurador.

* **`preLaunchTask`**: Ejecuta tareas antes de depurar (ej. `"build"` para correr `dotnet build`).
* **`program`**: Ruta a la DLL compilada (`${workspaceFolder}/bin/Debug/.../Proyecto.dll`).
* **`console`**: Define la salida/entrada de la aplicación.
  * **`internalConsole`** *(Default)*: Salida rápida a *Debug Console*. **No permite** `Console.ReadLine()`.
  * **`integratedTerminal`**: Usa la terminal integrada. **Requerido si la app lee datos del usuario**.
  * **`externalTerminal`**: Abre una ventana de comandos independiente del SO.
