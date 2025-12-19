# Technical Assessment 

**Candidate:** Jordan Alvarez Gonzalez
**Date:** 19/12/2025

## Part 1 – Code Analysis

### Bug
El método empieza a iterar la lista de pagos sin verificar si `payments` no es nulo.  
Además, no se valida que los campos `payment.amount` o `payment.status` tengan valores válidos o existan realmente.  
Esto puede provocar que el programa falle en tiempo de ejecución o que el método no se comporte como se espera si los datos vienen en un formato incorrecto.

---

### Performance
Se debe investigar qué hace exactamente el método `save(payment)`, ya que si su función es guardar los datos en la base de datos y se reciben muchos pagos (por ejemplo 10.000), guardar cada pago uno por uno puede generar mucha latencia.  
Este tipo de implementación puede ralentizar el funcionamiento del sistema debido a la cantidad de operaciones contra la base de datos.

---

### Data Congruence
La definición de la variable `total` da a entender que se están utilizando números enteros, lo cual no es lo más adecuado para manejar datos financieros.  
Sería más apropiado utilizar un tipo de dato decimal, ya que es más preciso y ayuda a evitar posibles errores contables en el sistema.

Además, teniendo en cuenta que el procesamiento de pagos es una operación crítica que no puede quedar a medias, sería importante asegurarse de que el método `save(payment)` sea atómico a nivel de base de datos.  
De esta forma se evita que queden datos inconsistentes si ocurre algún fallo durante la ejecución.

---

### Security
Al tratarse de un método que maneja pagos, es importante validar los datos de entrada para asegurarse de que no estén siendo manipulados.  
También se debería controlar qué partes del sistema tienen acceso a este método, ya que no debería ser accesible de forma pública ni permitir modificaciones indebidas en los pagos.

---

### Maintainability
El código tiene un alto acoplamiento, ya que el estado `"completed"` está definido de forma hardcodeada.  
Si en el futuro se agregan nuevos estados o cambia la lógica del negocio, habría que modificar directamente este método.  
Abstraer esta lógica permitiría que el código sea más fácil de mantener y extender.


## Part 2 – Change of Requirements

### 1. What new problem does this introduce?
Esto podría generar pagos duplicados o que el total calculado no represente el estado real de los pagos, afectando directamente la consistencia de los datos y el negocio.

---

### 2. What concept or strategy would you use to solve it?
Para solucionar este problema se podría utilizar el concepto de idempotencia.  
De esta forma, aunque el mismo pago llegue varias veces al sistema, el resultado final sería siempre el mismo y el pago no se procesaría más de una vez.

---

### 3. What additional data or information would be required?
Sería necesario contar con algún identificador único del pago y la fecha del último intento del pago, que permita reconocer si ya fue procesado anteriormente.  

## Part 3 – Small Implementation

```csharp
 int AverageNonNegative(List<int> intList){
    if (intList == null)
        throw new ArgumentNullException(nameof(intList));

    int sum = 0; 
    int count = 0;

    foreach (int num in intList){
        if (num >= 0){
            sum += num;
            count++;
        }
    }

    return count == 0 ? 0 : (int)(sum / count);
}
```



### 1. Why did you implement it this way?
Pienso que lo principal para resolver el problema es tener en cuenta que la lista no puede ser nula y que también puede estar vacía o contener solo valores negativos.
Al principio intenté usar sintaxis LINQ de C#, pero me di cuenta de que estaba realizando dos iteraciones para obtener el resultado. Analizando esto, opté por usar un foreach manual, ya que es más simple y legible.
De esta forma utilizo solo dos variables, una para acumular la suma de los valores no negativos y otra como contador. Al final realizo un return simple, verificando si el contador es cero (lista vacía o solo valores negativos), en cuyo caso devuelvo 0, y si no, devuelvo la división entre la suma y el contador.

### 2. What happens if the input list is empty?
Si la lista está vacía o solo contiene valores negativos, el contador queda en cero.
En ese caso, devolver directamente la división podría generar una operación inválida, por lo que se valida esta condición antes de realizar el cálculo y se retorna 0 como resultado.

### 3. How would you improve it if performance became critical?
Por simplicidad utilicé una lista como estructura de datos, pero si el volumen de información fuera muy grande se podría evaluar el uso de estructuras más livianas, como un array.
De todas formas, la lógica principal se mantendría igual, ya que el método ya recorre la colección una sola vez y evita operaciones innecesarias. A mi entender, esta solución es lo suficientemente eficiente sin llegar a utilizar técnicas más complejas.

## Part 4 – Conceptual Understanding

### 1. Backend: What is idempotency and why is it important in backend systems?
Idempotencia, en palabras muy sencillas, es un mecanismo que permite que un mismo proceso pueda ejecutarse varias veces pero que el resultado final sea siempre el mismo, como si se hubiera ejecutado una sola vez.  
Esto en el backend es muy importante, ya que evita que una misma acción genere efectos duplicados cuando, por ejemplo, Un caso común es cuando un usuario hace varios clicks sobre un botón y el sistema recibe la misma acción muchas veces, pero solo debería ejecutarse una vez.

---

### 2. Frontend: Explain the difference between client-side and server-side rendering, and give an example of when each is useful.
CSR se usa en aplicaciones web cuya principal intención es ser fluidas y dinámicas, ya que el navegador recibe una página base y luego se van actualizando pequeños elementos de la interfaz usando JavaScript, sin recargar toda la página.

SSR se utiliza cuando se necesita que el contenido principal de la página se genere desde el servidor antes de enviarse al cliente.  
Este enfoque es útil cuando se busca una carga inicial más rápida, mayor manejo de la seguridad o mayor control sobre el contenido de la pagina.

---

### 3. Databases: What is a foreign key and why is it important for data integrity?
Una foreign key es importante porque es la base de las bases de datos relacionales.  
Básicamente representa una relación o conexión entre dos tablas, indicando que los datos de una tabla dependen de otra.  
Esto es importante para la integridad de los datos, ya que evita que existan registros inválidos y asegura que las relaciones entre tablas se mantengan correctas.











