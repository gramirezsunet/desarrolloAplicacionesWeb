# Banco de Preguntas y Control de Lectura — Fase 1 (10 Preguntas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Tema:** Onion Architecture, Inyección de Dependencias, Ecosistema .NET 10 (C# 14) y Estándar RFC 7807  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Ponderación en Asignatura:** 2.0% de la Calificación Total | Puntuación en Google Forms: 20 Puntos (10 Preguntas × 2 pts c/u)

---

## 📝 Banco Oficial de Preguntas de Opción Múltiple

### Pregunta 1
**¿Cuál es la regla fundamental que rige el flujo de dependencias en la Onion Architecture (Arquitectura Cebolla)?**
- A) La capa de base de datos (`Infrastructure`) debe depender directamente de los controladores de la API.
- B) Las capas externas pueden depender de las capas internas, pero las capas internas jamás deben conocer los detalles de las externas. *(Correcta)*
- C) Todas las capas deben referenciarse mutuamente para permitir la inyección de dependencias bidireccional.
- D) El núcleo de dominio debe contener referencias al ORM Entity Framework para validar las entidades.

*Justificación Técnica:* La Onion Architecture establece que el núcleo de dominio (`Core.Domain`) debe ser completamente agnóstico a librerías y tecnologías de infraestructura.

---

### Pregunta 2
**En el contenedor nativo de Inyección de Dependencias de ASP.NET Core, ¿cuál es el comportamiento de un servicio registrado con ciclo de vida `Scoped`?**
- A) Se crea una única instancia que dura todo el tiempo en que el servidor web se encuentra encendido.
- B) Se crea una instancia nueva cada vez que el servicio es solicitado por un constructor.
- C) Se crea una única instancia por cada petición HTTP entrante y se destruye al finalizar la respuesta. *(Correcta)*
- D) Se almacena en la memoria caché del navegador del cliente para reducir peticiones al servidor.

*Justificación Técnica:* El ciclo `Scoped` está diseñado para objetos con estado contextual a la petición HTTP actual, como el `DbContext` y los servicios de casos de uso.

---

### Pregunta 3
**¿Qué problema arquitectónico se produce si se inyecta un servicio con ciclo de vida `Scoped` dentro de una clase registrada como `Singleton`?**
- A) Un error de compilación inmediato en C# 14.
- B) Una Dependencia Cautiva (*Captive Dependency*), donde la instancia scoped queda retenida en memoria indefinidamente, causando problemas de concurrencia y fugas de memoria. *(Correcta)*
- C) El servidor rechaza todas las peticiones con código de error HTTP 401 Unauthorized.
- D) Las consultas de Entity Framework se ejecutan en modo síncrono bloqueando el hilo principal.

*Justificación Técnica:* Un Singleton vive para siempre en el proceso; al atrapar una referencia Scoped, evita que esta se libere al terminar el request original.

---

### Pregunta 4
**Según el estándar internacional RFC 7807 (Problem Details for HTTP APIs), ¿cuál es el encabezado `Content-Type` oficial que debe retornar el servidor en las respuestas de error?**
- A) `text/html; charset=utf-8`
- B) `application/json`
- C) `application/problem+json` *(Correcta)*
- D) `application/xml-error`

*Justificación Técnica:* La especificación IETF RFC 7807 define explícitamente el MIME Type `application/problem+json` para tipificar errores en APIs REST.

---

### Pregunta 5
**Desde el punto de vista de la seguridad (Security by Design), ¿por qué es una mala práctica exponer los Stack Traces de excepciones no controladas en las respuestas 500 al cliente?**
- A) Porque el navegador web no puede renderizar texto en formato JSON.
- B) Porque revela información sensible sobre rutas de archivos en el servidor, versiones de librerías, nombres de métodos y base de datos, facilitando vectores de ataque al atacante. *(Correcta)*
- C) Porque duplica el tiempo de respuesta de la petición HTTP.
- D) Porque invalida automáticamente el token JWT del usuario conectado.

*Justificación Técnica:* El principio de divulgación mínima de información de OWASP exige ocultar trazas de depuración en entornos productivos.

---

### Pregunta 6
**¿Cuál es la responsabilidad primordial de la capa `Core.Domain` en nuestro Sistema de Gestión de Inventario?**
- A) Configurar las conexiones TCP/IP a la base de datos PostgreSQL.
- B) Definir las entidades puras del negocio (`Product`, `Category`, `User`), enums y reglas de dominio, sin depender de ningún framework o base de datos externa. *(Correcta)*
- C) Renderizar los componentes visuales en HTML y CSS.
- D) Gestionar el enrutamiento de peticiones HTTP en ASP.NET Core.

*Justificación Técnica:* `Core.Domain` es el corazón del sistema y debe mantenerse puro para garantizar su portabilidad y testeabilidad a largo plazo.

---

### Pregunta 7
**En la evolución tecnológica de .NET, ¿qué hito histórico marcó la llegada de .NET 5 y su consolidación en .NET 10?**
- A) El regreso exclusivo a entornos Windows de 32 bits.
- B) La unificación de todos los runtimes fragmentados (.NET Framework, .NET Core, Xamarin y Mono) en una plataforma única, abierta y multiplataforma de alto rendimiento. *(Correcta)*
- C) La eliminación total del lenguaje C# para usar únicamente JavaScript en el servidor.
- D) La obligación de pagar licencias propietarias por cada despliegue.

*Justificación Técnica:* .NET 5 unificó el ecosistema y .NET 10 representa la madurez cloud-native orientada a microservicios y contenedores ligeros.

---

### Pregunta 8
**¿Por qué en la clase abstracta `BaseEntity` se utiliza `DateTime.UtcNow` en lugar de `DateTime.Now` para la propiedad `CreatedAt`?**
- A) Porque `DateTime.Now` no es soportado por los procesadores de 64 bits.
- B) Para garantizar un estándar temporal universal independiente de la zona horaria del servidor o del cliente, previniendo discrepancias de auditoría en despliegues distribuidos en la nube. *(Correcta)*
- C) Porque `UtcNow` ocupa la mitad de memoria RAM que `Now`.
- D) Porque PostgreSQL rechaza fechas que no estén en la hora local de Venezuela.

*Justificación Técnica:* UTC (Tiempo Universal Coordinado) es el estándar de ingeniería para la persistencia temporal en sistemas empresariales globales.

---

### Pregunta 9
**¿Cuál es el beneficio de centralizar la captura de excepciones en un Middleware Global (`ExceptionMiddleware`) en lugar de usar bloques `try-catch` dispersos en cada controlador?**
- A) Aumenta el número de líneas de código en el proyecto.
- B) Elimina la redundancia de código, previene la fuga de excepciones no controladas y garantiza que todas las respuestas de error sigan una estructura uniforme e inmutable. *(Correcta)*
- C) Permite que el cliente modifique la base de datos sin autenticación.
- D) Desactiva el logging del servidor.

*Justificación Técnica:* El principio DRY (Don't Repeat Yourself) y la separación de aspectos transversales se logran mediante middlewares en el pipeline HTTP.

---

### Pregunta 10
**¿Cuál de los siguientes campos NO forma parte del esquema estándar de un documento Problem Details según la norma RFC 7807?**
- A) `type` (URI identificador del tipo de error).
- B) `title` (Resumen legible del problema).
- C) `password_hash` (Contraseña cifrada del administrador del sistema). *(Correcta)*
- D) `status` (Código de estado HTTP).

*Justificación Técnica:* El RFC 7807 define `type`, `title`, `status`, `detail` e `instance`. Incluir credenciales o datos sensibles viola los principios de seguridad.
