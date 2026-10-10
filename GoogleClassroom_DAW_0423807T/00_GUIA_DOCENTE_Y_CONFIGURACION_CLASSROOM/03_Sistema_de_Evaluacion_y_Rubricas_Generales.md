# Sistema de Evaluación y Rúbricas Generales
### Estándar: Cuestionario (20 Pts) + Asignación Práctica (80 Pts) = 100 Pts por Fase
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 📊 1. Esquema Institucional de Calificación en Porcentajes (%)

El plan de evaluación oficial del Departamento de Ingeniería Informática divide el curso en **3 Unidades Temáticas** desarrolladas en **5 Fases Semanales**, totalizando exactamente el **100% de la calificación definitiva**.

Cada semana se califica sobre **100 Puntos de Fase** (20 pts Cuestionario + 80 pts Asignación):

```
┌────────────────────────────────────────────────────────┐
│             CALIFICACIÓN TOTAL DEL CURSO: 100.0%       │
├──────────────────────────┬─────────────────────────────┤
│ Unidad I: Backend        │ 40.0% (Fases 1, 2 y 3)      │
│ Unidad II: Frontend & QA │ 40.0% (Fase 4: React+xUnit) │
│ Unidad III: DevOps & Demo│ 20.0% (Fase 5: Docker+Live) │
└──────────────────────────┴─────────────────────────────┘
```

### Tabla Maestra de Evaluación Estandarizada:

| Unidad Temática | Fase / Semana | Actividad Evaluada en Classroom | Puntos en la Actividad | % en Nota Final | % de la Unidad |
| :---: | :---: | :--- | :---: | :---: | :---: |
| **Unidad I**<br>*(40.0% Total)* | **Semana 1 / Fase 1**<br>*(10.0% Curso)* | • **Cuestionario 1:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 1:** Núcleo Onion & Middleware RFC 7807 | **20 Pts**<br>**80 Pts** | **2.0%**<br>**8.0%** | **10.0%** |
| **Unidad I**<br>*(40.0% Total)* | **Semana 2 / Fase 2**<br>*(15.0% Curso)* | • **Cuestionario 2:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 2:** EF Core 10, Fluent API & Data Seeding | **20 Pts**<br>**80 Pts** | **3.0%**<br>**12.0%** | **15.0%**<br>*(25% acum.)* |
| **Unidad I**<br>*(40.0% Total)* | **Semana 3 / Fase 3**<br>*(15.0% Curso)* | • **Cuestionario 3:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 3:** Auth Stateless JWT, RBAC & Validaciones | **20 Pts**<br>**80 Pts** | **3.0%**<br>**12.0%** | **15.0%**<br>*(Fin U1: 40%)* |
| **Unidad II**<br>*(40.0% Total)* | **Semana 4 / Fase 4**<br>*(40.0% Curso)* | • **Cuestionario 4:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 4:** Frontend React SPA & Suite xUnit/Moq | **20 Pts**<br>**80 Pts** | **8.0%**<br>**32.0%** | **40.0%**<br>*(Fin U2: 80%)* |
| **Unidad III**<br>*(20.0% Total)* | **Semana 5 / Fase 5**<br>*(20.0% Curso)* | • **Cuestionario 5:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 5:** Docker Compose, CI/CD y Sustentación Técnica | **20 Pts**<br>**80 Pts** | **4.0%**<br>**16.0%** | **20.0%**<br>*(Fin U3: 100%)* |
| **TOTAL** | **5 Semanas** | **10 Instrumentos Principales de Evaluación** | **100 Pts / Fase** | **100.0%** | **100.0%** |

---

## 📝 2. Configuración en Google Forms y Classroom

1. **Google Forms (Cuestionarios):** Cada cuestionario consta de **10 preguntas valoradas en 2 puntos cada una (Total: 20 Puntos)**.
2. **Google Classroom (Asignaciones):** Cada asignación práctica se califica sobre **80 Puntos** mediante rúbrica analítica detallada.
3. **Ponderación por Categoría:** En Google Classroom, active **"Ponderada por categoría"** con las 3 Unidades (40% / 40% / 20%).

---

## 📋 3. Rúbricas Analíticas Estandarizadas (80 Puntos por Asignación)

### Asignación 1 (Fase 1 - 80 Puntos):
- Arquitectura Onion & Desacoplamiento de Capas: **25 pts**
- Modelado de Entidades Base (`BaseEntity`, `Product`): **15 pts**
- `ExceptionMiddleware` RFC 7807 (`application/problem+json`): **30 pts**
- Repositorio GitHub y Documentación README: **10 pts**
*(Total: 80 Puntos)*

### Asignación 2 (Fase 2 - 80 Puntos):
- Fluent API & Reglas de Persistencia (`HasPrecision`, `Restrict`, Índices $O(1)$): **30 pts**
- `ApplicationDbContext` & Migraciones Versionadas: **20 pts**
- Siembra de Datos (Data Seeding) Representativa: **15 pts**
- Repositorio con Optimización `.AsNoTracking()`: **15 pts**
*(Total: 80 Puntos)*

### Asignación 3 (Fase 3 - 80 Puntos):
- Autenticación JWT & Claims (HMAC SHA-256): **25 pts**
- Matriz de Permisos RBAC (`401` y `403` respetados): **25 pts**
- FluentValidation Defensivo (`MaxStock > MinStock`, precios > 0): **20 pts**
- Evidencias de Pruebas en Postman (4 escenarios probados): **10 pts**
*(Total: 80 Puntos)*

### Asignación 4 (Fase 4 - 80 Puntos):
- Frontend React SPA, Modo Oscuro Institucional UNET y Motion UI: **25 pts**
- Dashboard KPI Analítico y Catálogo con Búsqueda y Modal: **25 pts**
- Conexión HTTP (Axios) & Context API (`AuthContext`, `ThemeContext`): **10 pts**
- Suite de Pruebas Unitarias Automatizadas con xUnit y Moq (100% verde): **20 pts**
*(Total: 80 Puntos)*

### Asignación 5 (Fase 5 - 80 Puntos):
- Dockerfiles Multi-stage optimizados (<120MB): **20 pts**
- Orquestación Docker Compose con Healthchecks y Postgres: **20 pts**
- Pipeline CI/CD automatizado con GitHub Actions: **10 pts**
- Sustentación Técnica Oral y Demostración en Vivo (*Live Demo* ante Jurado): **30 pts**
*(Total: 80 Puntos)*
