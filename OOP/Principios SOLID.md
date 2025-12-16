# Single Responsibility Principle
> **"Una clase debe tener una, y solo una, razón para cambiar."**

Si tienes que modificar una clase por dos motivos diferentes (ej: cambió la base de datos Y cambió el formato del reporte PDF), entonces esa clase está violando el SRP.

<img width="637" height="861" alt="image" src="https://github.com/user-attachments/assets/2d30220c-b999-4944-a1d3-a9842358ebf3" />

# Open/Closed Principle
> **Las clases deben estar abiertas a la extensión pero cer- radas a la modificación.**

Una clase está abierta si puedes extenderla, crear una subclase y hacer lo que quieras con ella (añadir nuevos métodos o campos, sobrescribir el comportamiento base, etc.). La clase está cerrada si está lista al 100 % para que otras clases la utilicen; su interfaz está claramente definida y no se cambiará en el futuro.

