# Universidad Nacional Experimental del Táchira (UNET)
## Decanato de Docencia | Departamento de Ingeniería Informática
### Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Profesor / Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez (`gramirezs@unet.edu.ve`)  
**Período Académico:** Septiembre, 2026 | San Cristóbal, Estado Táchira, Venezuela

---

# 📚 Guía de Configuración y Estructura en Google Classroom
### Estándar de Evaluación: Cuestionario (20 Pts) + Asignación (80 Pts) = 100 Pts por Fase

Esta guía describe el diseño pedagógico y la configuración técnica del aula virtual en **Google Classroom** y **Google Forms**, donde **CADA FASE se estructura con exactamente 100 Puntos** divididos en:
- **Cuestionario de 10 Preguntas:** Máximo **20 Puntos** (2 pts por pregunta en Google Forms).
- **Asignación Práctica:** Máximo **80 Puntos** (evaluados mediante Rúbrica en Classroom).

---

## 1. 🛠️ Configuración General del Aula Virtual

| Parámetro | Valor de Configuración |
| :--- | :--- |
| **Nombre de la Clase** | Desarrollo de Aplicaciones Web (0423807T) - UNET 2026 |
| **Sección** | Sección 1 / Lapso Académico 2026-2 |
| **Materia** | Ingeniería Informática - Desarrollo Web Full-Stack |
| **Aula** | Laboratorio de Informática / Modalidad Híbrida (Google Meet + Classroom) |
| **Correo Institucional del Facilitador** | `gramirezs@unet.edu.ve` |
| **Repositorio Oficial de Código** | `https://github.com/toulouse817/desarrolloAplicacionesWeb.git` |

---

## 2. ⚖️ Configuración del Libro de Calificaciones (Ponderada por Categoría)

En la sección **Ajustes de la clase > Calificaciones** de Google Classroom:
1. **Cálculo de la calificación general:** Seleccionar **Ponderada por categoría**.
2. **Mostrar la calificación general a los alumnos:** Activado.
3. **Categorías de Calificación:** Configurar las 3 categorías con sus porcentajes oficiales aprobados por la UNET:

```
┌────────────────────────────────────────────────────────┐
│             CALIFICACIÓN TOTAL DEL CURSO: 100.0%       │
├──────────────────────────┬─────────────────────────────┤
│ Unidad I: Backend        │ 40.0% (Fases 1, 2 y 3)      │
│ Unidad II: Frontend & QA │ 40.0% (Fase 4: React+xUnit) │
│ Unidad III: DevOps & Demo│ 20.0% (Fase 5: Docker+Live) │
└──────────────────────────┴─────────────────────────────┘
```

---

## 📊 3. Matriz Estandarizada: 20 pts Cuestionario + 80 pts Asignación

En cada una de las 5 fases semanales, la suma de puntos es exactamente **100 Puntos de Fase**, y Classroom aplica la ponderación porcentual correspondiente:

| Unidad Temática | Fase / Semana | Actividad a Publicar en Classroom | Puntos en Classroom / Forms | % en Nota Final del Curso | % de la Unidad |
| :---: | :---: | :--- | :---: | :---: | :---: |
| **Unidad I**<br>*(40.0%)* | **Fase 1**<br>*(10.0% Curso)* | • **Cuestionario 1:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 1:** Núcleo Onion & Middleware RFC 7807 | **20 Pts**<br>**80 Pts** | **2.0%**<br>**8.0%** | **10.0%** |
| **Unidad I**<br>*(40.0%)* | **Fase 2**<br>*(15.0% Curso)* | • **Cuestionario 2:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 2:** EF Core 10, Fluent API & Data Seeding | **20 Pts**<br>**80 Pts** | **3.0%**<br>**12.0%** | **15.0%**<br>*(25% acum.)* |
| **Unidad I**<br>*(40.0%)* | **Fase 3**<br>*(15.0% Curso)* | • **Cuestionario 3:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 3:** Auth Stateless JWT, RBAC & FluentValidation | **20 Pts**<br>**80 Pts** | **3.0%**<br>**12.0%** | **15.0%**<br>*(Fin U1: 40%)* |
| **Unidad II**<br>*(40.0%)* | **Fase 4**<br>*(40.0% Curso)* | • **Cuestionario 4:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 4:** Frontend SPA + KPIs + Suite xUnit & Moq | **20 Pts**<br>**80 Pts** | **8.0%**<br>**32.0%** | **40.0%**<br>*(Fin U2: 80%)* |
| **Unidad III**<br>*(20.0%)* | **Fase 5**<br>*(20.0% Curso)* | • **Cuestionario 5:** Control de Lectura (10 preg × 2 pts)<br>• **Asignación 5:** Docker Compose, CI/CD y Sustentación Técnica | **20 Pts**<br>**80 Pts** | **4.0%**<br>**16.0%** | **20.0%**<br>*(Fin U3: 100%)* |
| **TOTAL** | **5 Semanas** | **10 Instrumentos Principales de Evaluación** | **100 Pts / Fase** | **100.0%** | **100.0%** |

---

## 4. 📑 Estructura de Temas en "Trabajo de Clase"

```
📌 [TEMA 0] INFORMACIÓN GENERAL Y RECURSOS DEL CURSO
├── Programa Analítico y Metodología (DAW-0423807T.pdf)
├── Repositorio Oficial y Boilerplate del Proyecto Integrador
├── Glosario Técnico y Estándares de Codificación
└── Guía de Instalación del Entorno de Desarrollo (.NET 10, Node.js 20, Docker, PostgreSQL)

🚀 [TEMA 1] SEMANA 1: FASE 1 - ARQUITECTURA LIMPIA, .NET 10 Y RESILIENCIA REST [10% del Curso]
├── Material: Onion Architecture, DI y Middleware RFC 7807
├── Material: Guía de Laboratorio Live Coding Fase 1
├── 📝 Cuestionario 1: Control de Lectura Fase 1 [20 Puntos | 10 preg × 2 pts]
└── 💻 Asignación 1: Creación del Núcleo y Middleware RFC 7807 [80 Puntos | Rúbrica]

🗄️ [TEMA 2] SEMANA 2: FASE 2 - PERSISTENCIA RELACIONAL CON EF CORE 10 Y FLUENT API [15% del Curso]
├── Material: Code-First, Fluent API, Data Seeding y .AsNoTracking()
├── Material: Guía de Laboratorio Live Coding Fase 2
├── 📝 Cuestionario 2: Control de Lectura Fase 2 [20 Puntos | 10 preg × 2 pts]
└── 💻 Asignación 2: Persistencia EF Core 10 y Siembra de Datos [80 Puntos | Rúbrica]

🔐 [TEMA 3] SEMANA 3: FASE 3 - SEGURIDAD STATELESS (JWT), RBAC Y FLUENTVALIDATION [15% del Curso]
├── Material: JWT RFC 7519, Matriz de Permisos RBAC y OWASP Defensivo
├── Material: Guía de Laboratorio Live Coding Fase 3
├── 📝 Cuestionario 3: Control de Lectura Fase 3 [20 Puntos | 10 preg × 2 pts]
└── 💻 Asignación 3: Módulo de Autenticación, RBAC y Validación Defensiva [80 Puntos | Rúbrica]

⚛️ [TEMA 4] SEMANA 4: FASE 4 - FRONTEND SPA REACT 18, KPIS Y TESTING AUTOMATIZADO [40% del Curso]
├── Material: React SPA, Vite, Tailwind CSS, Context API y Testing con xUnit/Moq
├── Material: Guía de Laboratorio Live Coding Fase 4
├── 📝 Cuestionario 4: Control de Lectura Fase 4 [20 Puntos | 10 preg × 2 pts]
└── 💻 Asignación 4: Frontend React SPA con Modo Oscuro, KPIs y Suite xUnit/Moq [80 Puntos | Rúbrica]

🐳 [TEMA 5] SEMANA 5: FASE 5 - CONTENERIZACIÓN MULTI-STAGE, DEVOPS Y SUSTENTACIÓN [20% del Curso]
├── Material: Multi-stage Dockerfiles, Docker Compose, CI/CD con GitHub Actions
├── Material: Guía de Laboratorio Live Coding Fase 5
├── 📝 Cuestionario 5: Control de Lectura Fase 5 [20 Puntos | 10 preg × 2 pts]
└── 💻 Asignación 5: Contenerización Docker, CI/CD y Sustentación Técnica / Live Demo [80 Puntos | Rúbrica]

🏆 [TEMA 6] PROPUESTAS DE PROYECTOS FINALES Y LINEAMIENTOS
├── Banco de Propuestas: MediStock ERP y LogiTrack Enterprise
└── Rúbrica de Defensa y Evaluación de Competencias Profesionales
```

---

## 5. 📢 Mensaje de Bienvenida Institucional para el "Tablón / Anuncios"

```markdown
👋 ¡Bienvenidos a la asignatura Desarrollo de Aplicaciones Web (Código: 0423807T)!

Estimados estudiantes del Departamento de Ingeniería Informática de la UNET:

Les doy una cordial bienvenida al período académico Septiembre 2026. A lo largo de las próximas 5 semanas, construiremos un Sistema de Gestión de Inventario Empresarial (ERP) de nivel corporativo.

Aprenderán a diseñar e implementar sistemas robustos aplicando estándares de la industria internacional:
✅ Backend: .NET 10 (C# 14), Onion Architecture, Entity Framework Core 10, PostgreSQL 15, JWT Bearer y FluentValidation.
✅ Frontend: React 18, Vite, Tailwind CSS (con Modo Oscuro Institucional UNET) y Dashboards analíticos de KPIs.
✅ Calidad & DevOps: Pruebas unitarias con xUnit y Moq, Contenerización Multi-stage con Docker Compose y pipelines CI/CD con GitHub Actions.

📌 Estructura de Evaluación Estandarizada:
Cada semana cuenta con exactamente 100 Puntos de Fase:
• Cuestionario Teórico en Google Forms: 20 Puntos (10 preguntas × 2 pts c/u).
• Asignación Práctica de Código en GitHub: 80 Puntos (según Rúbrica).

Ponderación oficial por Unidades:
• Unidad I (Backend Corporativo): 40.0% (Fases 1, 2 y 3)
• Unidad II (Frontend y Analítica): 40.0% (Fase 4)
• Unidad III (DevOps y Sustentación): 20.0% (Fase 5)

¡Mucho éxito en este ciclo formativo de alto impacto técnico!

M.Sc. Ing. Gabriel Alexis Ramírez Sánchez
Facilitador - Dpto. de Ingeniería Informática UNET
Contacto: gramirezs@unet.edu.ve
```
