# Banco de Preguntas y Control de Lectura — Fase 3 (10 Preguntas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Tema:** Autenticación Stateless (JWT RFC 7519), Matriz RBAC, FluentValidation y Seguridad OWASP  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Ponderación en Asignatura:** 3.0% de la Calificación Total | Puntuación en Google Forms: 20 Puntos (10 Preguntas × 2 pts c/u)

---

## 📝 Banco Oficial de Preguntas de Opción Múltiple

### Pregunta 1
**¿Por qué un token JSON Web Token (JWT) se considera un mecanismo de autenticación "Stateless" (sin estado)?**
- A) Porque el token se borra automáticamente cada vez que el usuario cierra el navegador.
- B) Porque el servidor valida la autenticidad y los privilegios del usuario verificando únicamente la firma criptográfica del token, sin necesidad de consultar una tabla de sesiones activas en la base de datos. *(Correcta)*
- C) Porque el token no contiene ningún dato del usuario.
- D) Porque los tokens JWT solo funcionan con bases de datos NoSQL.

*Justificación Técnica:* Al ser un token autocontenido con claims y firma digital, el servidor backend no requiere almacenar estado de sesión en memoria ni en base de datos.

---

### Pregunta 2
**¿Cuál es la diferencia semántica y técnica entre los códigos de estado HTTP `401 Unauthorized` y `403 Forbidden` en un esquema RBAC?**
- A) Son exactamente iguales y se usan de forma intercambiable según el gusto del programador.
- B) `401 Unauthorized` indica que el cliente no ha proporcionado credenciales válidas (no está autenticado), mientras que `403 Forbidden` indica que el servidor sabe quién es el usuario pero este no tiene los permisos requeridos por su rol. *(Correcta)*
- C) `401` significa que la base de datos está caída y `403` que el servidor tiene poco disco duro.
- D) `403` solo se devuelve cuando el usuario es Administrador.

*Justificación Técnica:* RFC 7235 / RFC 9110 especifica que 401 es un fallo de autenticación (identidad desconocida), mientras que 403 es un fallo de autorización (permisos insuficientes).

---

### Pregunta 3
**¿Qué vulnerabilidad del OWASP API Security Top 10 se previene al utilizar DTOs específicos de entrada validados con FluentValidation en lugar de enlazar entidades del dominio directamente en las acciones del controlador?**
- A) SQL Injection exclusivamente.
- B) Mass Assignment (Asignación Masiva) y BOLA (Broken Object Level Authorization), evitando que un atacante altere propiedades protegidas inyectando campos extra en el JSON. *(Correcta)*
- C) Cross-Site Scripting (XSS) en archivos CSS.
- D) Errores de sintaxis de C# en el servidor.

*Justificación Técnica:* Exponer la entidad directa permite que un cliente envíe campos maliciosos (ej. `IsAdmin: true` o `Balance: 99999`). Los DTOs inmutables con validación estricta aíslan las entidades.

---

### Pregunta 4
**En el estándar JWT (RFC 7519), ¿dónde se ubican los datos del usuario como su identificador único, correo electrónico y rol asignado?**
- A) En el Header (Cabecera).
- B) En el Payload (Carga Útil) bajo el formato de *Claims*. *(Correcta)*
- C) En la Firma criptográfica (Signature).
- D) En la URL del navegador.

*Justificación Técnica:* El payload contiene los pares clave-valor conocidos como claims que definen los atributos y permisos del usuario.

---

### Pregunta 5
**Al configurar la inyección de dependencias en .NET 10, ¿cuál es el ciclo de vida recomendado para los validadores de FluentValidation (`AbstractValidator<T>`)?**
- A) `Singleton`
- B) `Transient` *(Correcta)*
- C) `ThreadStatic`
- D) `Manual Static`

*Justificación Técnica:* Los validadores son objetos ligeros y sin estado interno persistente, por lo que registrarlos como `Transient` garantiza instanciación bajo demanda y recolección de basura eficiente.

---

### Pregunta 6
**En la Matriz de Control de Acceso (RBAC) de nuestro sistema, ¿cuál es el comportamiento esperado cuando un usuario con rol `Employee` intenta eliminar un producto (`DELETE /api/products/{id}`)?**
- A) El producto se elimina sin restricciones.
- B) El servidor rechaza la petición retornando un código de error HTTP `403 Forbidden` con documento RFC 7807. *(Correcta)*
- C) El servidor se apaga automáticamente.
- D) Se redirige al empleado a la página de inicio de sesión.

*Justificación Técnica:* La autorización granular restringe las operaciones destructivas de catálogo exclusivamente al rol `Admin`.

---

### Pregunta 7
**¿Por qué en `CreateProductValidator.cs` se incluye la regla `.GreaterThan(x => x.MinStock)` para la propiedad `MaxStock`?**
- A) Para obligar a que el producto tenga un precio mayor a \$100.
- B) Para garantizar la coherencia lógica de inventario, impidiendo que la capacidad máxima de almacenamiento sea menor o igual al umbral mínimo de seguridad. *(Correcta)*
- C) Porque PostgreSQL no permite valores negativos en tablas.
- D) Para acelerar la velocidad de renderizado en React.

*Justificación Técnica:* La validación defensiva modela invariantes del negocio para impedir estados inconsistentes en la bodega física.

---

### Pregunta 8
**¿Qué algoritmo criptográfico simétrico se utiliza para firmar los tokens JWT en nuestro proyecto `TokenService.cs`?**
- A) MD5
- B) HMAC SHA-256 (`SecurityAlgorithms.HmacSha256`) *(Correcta)*
- C) ROT13
- D) Base64 sin cifrar

*Justificación Técnica:* HMAC SHA-256 es el estándar de firma criptográfica simétrica ampliamente adoptado para autenticación segura en APIs RESTful.

---

### Pregunta 9
**¿Cuál es la cabecera estándar de HTTP mediante la cual el cliente frontend debe enviar el token JWT al servidor en cada petición protegida?**
- A) `Cookie: session_token=...`
- B) `Authorization: Bearer <Token_JWT>` *(Correcta)*
- C) `Content-Type: application/jwt`
- D) `X-User-Role: Admin`

*Justificación Técnica:* El esquema de autenticación Bearer en la cabecera `Authorization` está estandarizado por el RFC 6750.

---

### Pregunta 10
**¿Por qué las contraseñas de los usuarios en la tabla `Users` NUNCA deben almacenarse en texto plano?**
- A) Porque ocupan más espacio en disco que el texto plano.
- B) Porque una brecha de seguridad en la base de datos expondría inmediatamente las credenciales de todos los usuarios; se deben almacenar exclusivamente hashes criptográficos (ej. SHA-256 con salt). *(Correcta)*
- C) Porque C# 14 no permite cadenas de texto con contraseñas.
- D) Porque Entity Framework Core no admite contraseñas en texto plano.

*Justificación Técnica:* El almacenamiento seguro con funciones hash criptográficas unidireccionales es un principio fundamental de ciberseguridad exigido por OWASP y normativas internacionales.
