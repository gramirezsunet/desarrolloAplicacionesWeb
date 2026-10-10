# Glosario Técnico de Términos y Acrónimos
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Departamento de Ingeniería Informática**

---

| Término / Acrónimo | Definición Técnica |
| :--- | :--- |
| **API** | *Application Programming Interface*. Protocolo estructurado de comunicación e intercambio de datos entre sistemas de software independientes. |
| **BOLA** | *Broken Object Level Authorization*. Vulnerabilidad crítica del OWASP Top 10 donde un usuario manipula identificadores (ej. UUID en URL) para acceder o modificar recursos que no le pertenecen. |
| **ChangeTracker** | Mecanismo interno de Entity Framework Core que registra el estado y modificaciones de las entidades en memoria para generar sentencias `UPDATE` o `INSERT`. Se desactiva con `.AsNoTracking()`. |
| **CI/CD** | *Continuous Integration / Continuous Deployment*. Práctica de ingeniería que automatiza la compilación, ejecución de pruebas unitarias y despliegue del software mediante pipelines. |
| **CORS** | *Cross-Origin Resource Sharing*. Mecanismo de seguridad de los navegadores que restringe las peticiones HTTP realizadas desde un dominio de origen distinto al del servidor. |
| **Data Seeding** | Estrategia de inicialización de bases de datos que inserta registros maestros predeterminados (categorías, usuarios admin, productos) al crear el esquema relacional. |
| **DTO** | *Data Transfer Object*. Objeto plano utilizado para transportar información entre capas o mediante HTTP sin exponer la estructura de las entidades del dominio. |
| **EF Core 10** | *Entity Framework Core 10*. Mapeador objeto-relacional (ORM) moderno, multiplataforma y de alto rendimiento para el ecosistema .NET. |
| **Fluent API** | Patrón de diseño basado en encadenamiento de métodos utilizado en EF Core para configurar explícitamente el esquema relacional fuera de las clases del dominio. |
| **JWT** | *JSON Web Token (RFC 7519)*. Estándar compacto y autocontenido para transmitir afirmaciones de identidad (*claims*) firmadas digitalmente con algoritmos criptográficos (HMAC-SHA256). |
| **KPI** | *Key Performance Indicator*. Métrica cuantitativa estratégica para medir el desempeño, valorización y estado operativo de un proceso de negocio. |
| **Mock** | Objeto simulado que imita el comportamiento de dependencias reales (como repositorios o bases de datos) en pruebas unitarias aisladas. |
| **Multi-stage Build** | Patrón de construcción en Docker que separa la etapa de compilación pesada con SDKs de la etapa final de ejecución ligera para minimizar el peso de las imágenes (<120MB). |
| **Onion Architecture** | Patrón arquitectónico concéntrico propuesto por Jeffrey Palermo donde las reglas de negocio residen en el núcleo central y las dependencias apuntan exclusivamente hacia adentro. |
| **RBAC** | *Role-Based Access Control*. Mecanismo de seguridad que otorga o restringe permisos a operaciones según los roles asignados a los usuarios (ej. Admin vs Employee). |
| **RFC 7807** | *Problem Details for HTTP APIs*. Estándar internacional que estandariza las respuestas de error en formato JSON (`application/problem+json`) en servicios web RESTful. |
| **SPA** | *Single Page Application*. Aplicación web cliente que carga una única página HTML y actualiza dinámicamente sus vistas interactuando con una API mediante peticiones asíncronas. |
| **xUnit** | Framework de pruebas automatizadas y ejecutor de tests de código abierto para la plataforma .NET. |
