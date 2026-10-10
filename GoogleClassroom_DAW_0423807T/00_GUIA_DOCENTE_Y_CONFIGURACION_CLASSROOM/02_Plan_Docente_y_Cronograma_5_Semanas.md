# Plan Docente y Cronograma de Ejecución (5 Semanas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez (`gramirezs@unet.edu.ve`)

---

## 🕒 Esquema Metodológico de Sesión (120 Minutos por Fase)

Cada semana formativa consta de 1 sesión lectiva principal estructurada bajo el modelo pedagógico de cuatro momentos estratégicos:

```
┌─────────────────┬─────────────────┬───────────────────┬─────────────────┐
│  00 - 25 min    │  25 - 70 min    │   70 - 100 min    │  100 - 120 min  │
├─────────────────┼─────────────────┼───────────────────┼─────────────────┤
│ Fundamentación  │  Live Coding y  │   Laboratorio /   │ Retrospectiva,  │
│    Teórica y    │  Demostración   │   Taller Guiado   │  Preguntas y    │
│  Decisiones de  │   Práctica del  │    para los       │   Asignación    │
│     Diseño      │   Facilitador   │   Estudiantes     │    por Fase     │
└─────────────────┴─────────────────┴───────────────────┴─────────────────┘
```

---

## 📅 Cronograma Detallado de 5 Semanas

### 🚀 SEMANA 1: FASE 1 — Fundamentos Arquitectónicos, Ecosistema .NET 10 y Resiliencia en APIs REST
* **Unidad Temática:** Unidad I: Backend Corporativo (Parte 1).
* **Objetivo Pedagógico:** Comprender la evolución tecnológica del ecosistema .NET hasta su versión 10; estructurar la solución desacoplada aplicando Onion Architecture; configurar la Inyección de Dependencias nativa con ciclos de vida apropiados; y centralizar la captura de excepciones bajo la norma RFC 7807 (Problem Details).
* **Desglose de Sesión (120 min):**
  * **00-25m:** Evolución .NET (.NET Framework -> .NET Core -> .NET 10 / C# 14), filosofía de capas concéntricas (Onion Architecture), Inversión de Dependencias (DIP) y RFC 7807.
  * **25-70m:** Live Coding: Creación de la solución `desarrolloAplicacionesWeb.sln`, separación en `Core.Domain`, `Core.Application`, `Infrastructure` y `Presentation.API`. Implementación de `ExceptionMiddleware.cs`.
  * **70-100m:** Taller Práctico: Los estudiantes replican la arquitectura base y configuran el pipeline de middlewares en `Program.cs`.
  * **100-120m:** Q&A, verificación de respuestas `application/problem+json` y publicación de la Tarea Semana 1.
* **Entregable:** Repositorio con solución multicapa y middleware global de excepciones funcional.

---

### 🗄️ SEMANA 2: FASE 2 — Persistencia Relacional con Entity Framework Core 10, Fluent API & Siembra de Datos
* **Unidad Temática:** Unidad I: Backend Corporativo (Parte 2).
* **Objetivo Pedagógico:** Dominar el modelado relacional Code-First en PostgreSQL 15 con EF Core 10; aplicar Fluent API para configurar restricciones de integridad foránea (`Restrict`), precisión financiera (`numeric(18,2)`) e índices únicos $O(1)$; implementar optimizaciones con `.AsNoTracking()` y estrategia de Data Seeding.
* **Desglose de Sesión (120 min):**
  * **00-25m:** Modelado Code-First vs Database-First, Fluent API vs Data Annotations, rendimiento de consultas de solo lectura (`.AsNoTracking`), prevención de borrado accidental con `DeleteBehavior.Restrict`.
  * **25-70m:** Live Coding: Creación de `ApplicationDbContext`, configuración de `ProductConfiguration.cs` y `CategoryConfiguration.cs`, creación de migraciones automáticas y método `OnModelCreating` con siembra inicial de inventario.
  * **70-100m:** Taller Práctico: Conexión de la API a PostgreSQL local o Dockerizado, ejecución de migraciones y verificación de tablas e índices en pgAdmin / CLI.
  * **100-120m:** Retrospectiva, revisión de consultas generadas y publicación de la Tarea Semana 2.
* **Entregable:** Capa `Infrastructure` con repositorios, DbContext configurado y base de datos sembrada con datos de ferretería.

---

### 🔐 SEMANA 3: FASE 3 — Seguridad Stateless (JWT), Autorización Granular (RBAC) & Validación Defensiva
* **Unidad Temática:** Unidad I: Backend Corporativo (Parte 3).
* **Objetivo Pedagógico:** Implementar autenticación stateless mediante JSON Web Tokens (JWT RFC 7519); estructurar la matriz de permisos basada en roles (RBAC: Admin vs Employee); y blindar la entrada de datos con validaciones desacopladas usando FluentValidation frente a vulnerabilidades OWASP.
* **Desglose de Sesión (120 min):**
  * **00-25m:** Anatomía de un JWT (Header, Payload/Claims, Signature), hashing seguro de contraseñas SHA-256, matriz de control de acceso RBAC, vulnerabilidades de Mass Assignment y BOLA en APIs.
  * **25-70m:** Live Coding: Implementación de `TokenService.cs`, configuración del esquema Bearer en `Program.cs`, creación de `CreateProductValidator.cs` con FluentValidation y protección de endpoints con `[Authorize(Roles = "Admin")]`.
  * **70-100m:** Taller Práctico: Pruebas de autenticación con Postman: generación de token, acceso con rol Employee vs Admin (validación de código 403 Forbidden y 400 Bad Request en validaciones).
  * **100-120m:** Revisión de seguridad defensiva, cierre de la Unidad I (40% de la nota acumulada) y asignación Semana 3.
* **Entregable:** API completa y blindada con autenticación JWT, RBAC funcional y validaciones automáticas.

---

### ⚛️ SEMANA 4: FASE 4 — Frontend SPA React 18, Dashboard KPI & Pruebas Unitarias Automatizadas
* **Unidad Temática:** Unidad II: Frontend y Analítica (40%).
* **Objetivo Pedagógico:** Desarrollar una Single Page Application (SPA) con React 18, Vite y Tailwind CSS que incorpore selector de Modo Oscuro institucional UNET; construir un Dashboard interactivo de Indicadores KPI; y redactar pruebas unitarias deterministas con xUnit y Moq.
* **Desglose de Sesión (120 min):**
  * **00-25m:** Arquitectura de clientes SPA reactivos, gestión de estado con Context API (`AuthContext`, `ThemeContext`), diseño con Tailwind CSS y pirámide de pruebas (Unit Testing con xUnit + Moq).
  * **25-70m:** Live Coding: Montaje de la SPA React con Vite, consumo de API con Axios, creación del `DashboardKPI` (tarjetas financieras, alertas de stock mínimo), alternancia de logo UNET día/noche y suite de pruebas `ProductServiceTests.cs` con Moq.
  * **70-100m:** Taller Práctico: Los estudiantes ejecutan las pruebas `dotnet test` y prueban la reactividad del frontend conectándose al backend.
  * **100-120m:** Demostración de cobertura de pruebas, retroalimentación del diseño UI/UX y asignación Semana 4.
* **Entregable:** Frontend React conectado a la API con Dashboard analítico y proyecto de pruebas unitarias xUnit con 100% de aserciones aprobadas.

---

### 🐳 SEMANA 5: FASE 5 — Contenerización Multi-stage, DevOps, CI/CD y Sustentación Técnica
* **Unidad Temática:** Unidad III: Sustentación y DevOps (20%).
* **Objetivo Pedagógico:** Empaquetar la solución utilizando construcciones Docker multietapa (Multi-stage); orquestar PostgreSQL, la API en .NET 10 y el frontend en Nginx con Docker Compose; automatizar flujos CI/CD en GitHub Actions; y sustentar el proyecto integrador ante jurado evaluador.
* **Desglose de Sesión (120 min):**
  * **00-25m:** Principios de contenerización ligera, optimización de imágenes (<120MB), redes internas en Docker Compose, automatización de compilación y pruebas en pipelines GitHub Actions.
  * **25-50m:** Live Coding: Configuración de `Dockerfile` para API (.NET 10) y SPA (Nginx), ensamblaje de `docker-compose.yml` con healthchecks y workflow `.github/workflows/ci-cd.yml`.
  * **50-110m:** **Sustentación Técnica y Live Demo:** Demostraciones en vivo de los proyectos desarrollados (Proyecto Base, MediStock ERP o LogiTrack Enterprise) ante el tribunal evaluador.
  * **110-120m:** Rueda de preguntas de ingeniería, retroalimentación final y entrega de calificaciones definitivas.
* **Entregable:** Repositorio en GitHub con pipeline de CI/CD en verde, despliegue con `docker-compose up` y sustentación oral completada.
