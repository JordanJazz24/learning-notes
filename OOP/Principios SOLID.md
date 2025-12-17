# Single Responsibility Principle
> **"Una clase debe tener una, y solo una, razón para cambiar."**

Si tienes que modificar una clase por dos motivos diferentes (ej: cambió la base de datos Y cambió el formato del reporte PDF), entonces esa clase está violando el SRP.

<img width="637" height="861" alt="image" src="https://github.com/user-attachments/assets/2d30220c-b999-4944-a1d3-a9842358ebf3" />

# Open/Closed Principle
> **Las clases deben estar abiertas a la extensión pero cer- radas a la modificación.**

Una clase está abierta si puedes extenderla, crear una subclase y hacer lo que quieras con ella (añadir nuevos métodos o campos, sobrescribir el comportamiento base, etc.). La clase está cerrada si está lista al 100 % para que otras clases la utilicen; su interfaz está claramente definida y no se cambiará en el futuro.

<img width="819" height="615" alt="image" src="https://github.com/user-attachments/assets/2871fa6f-4851-48b6-8e57-2e640e197a8b" />
<img width="859" height="877" alt="image" src="https://github.com/user-attachments/assets/537c0905-9188-47e9-bd6d-2342ec6c72b9" />

# Liskov Substitution Principle
> **Al extender una clase, recuerda que debes tener la capacidad de pasar objetos de las subclases en lugar de objetos de la clase padre, sin descomponer el código cliente.**

Esto significa que la subclase debe permanecer compatible con el comportamiento de la superclase. Al sobrescribir un método, extiende el comportamiento base en lugar de sustituirlo con algo totalmente distinto.

- Los tipos de parámetros en el método de una subclase deben coincidir o ser más abstractos que los tipos de parámetros del método de la superclase
- El tipo de retorno en el método de una subclase debe coincidir o ser un subtipo del tipo de retorno del método de la superclase.
- Un método de una subclase no debe arrojar tipos de excepcio- nes que no se espere que arroje el método base. En otras pala- bras, los tipos de excepciones deben coincidir o ser subtipos de los que el método base es capaz de arrojar.
- Una subclase no debe fortalecer (hacer mas estrictas) las condiciones previas. Por ejemplo, el método base tiene un parámetro con el tipo int . Si una subclase sobrescribe este método y requiere que el valor de un argumento pasado al método sea positivo (lanza- ndo una excepción si el valor es negativo), esto amplía las co- ndiciones previas. El código cliente, que solía funcionar bien pasando números negativos al método, ahora se descompone si empieza a funcionar con un objeto de esta subclase.










