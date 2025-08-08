# Notas de Spring Boot

## ¿Qué es?
- Framework basado en Spring que facilita la creación de aplicaciones Java listas para producción.
- Minimiza la configuración manual y el “boilerplate”.

## Ventajas clave
- **Arranque rápido:** Proyectos listos con dependencias mínimas y configuración automática.
- **Integración fácil:** Incluye *starters* para bases de datos, web, seguridad, pruebas, etc.
- **Servidor embebido:** Usa Tomcat o Jetty integrados, no necesitas desplegar en un servidor externo.
- **Actuadores:** Permite monitorizar y gestionar la app en tiempo real (health, metrics, info).

## Estructura típica de proyecto
- `/src/main/java` — Código fuente Java.
- `/src/main/resources` — Configuración (`application.properties`/`application.yml`).
- `/src/test/java` — Pruebas.

## Archivos importantes
- `application.properties` o `application.yml`: Configuración centralizada (puerto, conexión DB, etc.).
- `pom.xml` o `build.gradle`: Gestión de dependencias.

## Anotaciones comunes
- `@SpringBootApplication` — Marca la clase principal.
- `@RestController` — Para exponer APIs REST.
- `@Service`, `@Repository`, `@Component` — Para lógica de negocio, acceso a datos, componentes generales.
- `@Autowired` — Inyección de dependencias.
- `@Entity` — Marca una clase como entidad JPA.

## Arranque de la app
- La clase principal contiene el método `main` que llama a `SpringApplication.run(...)`.

## Comandos útiles
- `mvn spring-boot:run` o `./gradlew bootRun` — Levantar la app.
- `mvn clean package` — Empaquetar la app como .jar.

---

> **TIP:** Spring Boot es ideal para microservicios, APIs REST y prototipos rápidos en Java.
