# Tarea y Asignación Práctica — Semana 5 (Fase 5)
### Contenerización Docker Compose, DevOps, CI/CD y Sustentación Técnica
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Categoría en Classroom:** Unidad III: Sustentación y DevOps  
**Puntuación en Google Classroom:** 80 Puntos Máximos | Ponderación en Asignatura: 16.0% (de 20% de la Unidad III)

---

## 📌 Enunciado del Proyecto Integrador

El estudiante o equipo debe configurar la contenerización multi-stage de la aplicación completa, orquestar los microservicios mediante **Docker Compose**, estructurar el pipeline de Integración Continua (**CI/CD**) en **GitHub Actions**, y presentar la **Sustentación Técnica Oral y Demostración en Vivo (*Live Demo*)** ante el jurado evaluador.

### Requerimientos Obligatorios:
1. **Dockerfiles Multi-stage (Backend y Frontend):**
   - Backend en .NET 10 publicado en runtime `aspnet:10.0-alpine` (< 120 MB).
   - Frontend en React/Vite servido por servidor web ligero `nginx:alpine`.
2. **Orquestación con `docker-compose.yml`:**
   - Servicios: `db` (PostgreSQL 15), `api` (.NET 10) y `spa` (React/Nginx).
   - Configuración de persistencia por volumen para Postgres y healthcheck `service_healthy`.
3. **Pipeline CI/CD con GitHub Actions (`.github/workflows/ci-cd.yml`):**
   - Automatización de compilación de backend y frontend, y ejecución de `dotnet test`.
4. **Sustentación Técnica Oral (15 min) y Live Demo:**
   - Demostración de arranque en frío con `docker compose up --build`.
   - Validación en vivo de Login JWT, Restricción RBAC 403 y Dashboard KPI.

---

## 📋 Formato de Entrega
- Enlace al repositorio GitHub con el pipeline de GitHub Actions en estado verde (Passing).
- Archivo `docker-compose.yml` completamente funcional.
- Sustentación técnica oral completada ante el jurado evaluador.

---

## 📊 Rúbrica de Evaluación Estandarizada (80 Puntos Máximos)

| Criterio | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos Máx. |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. Dockerfiles Multi-stage** | Optimización estricta (<120MB), separación clara de etapas SDK y Runtime liviano. (20 pts) | Dockerfiles funcionales pero con imágenes pesadas. (16 pts) | Dockerfiles con errores menores de sintaxis. (12 pts) | No incluye Dockerfiles. (0-8 pts) | **20 pts** |
| **2. Orquestación Docker Compose & Healthcheck** | Orquestación limpia de los 3 servicios con healthcheck `pg_isready` y red interna. (20 pts) | Orquestación funcional pero sin comprobación de salud. (16 pts) | Contenedores que requieren pasos manuales para iniciar. (12 pts) | Falla al ejecutar `docker-compose up`. (0-8 pts) | **20 pts** |
| **3. Pipeline CI/CD GitHub Actions** | Workflow automatizado ejecutando build y pruebas xUnit en cada push en verde. (10 pts) | Workflow funcional pero solo compila sin correr pruebas. (8 pts) | Errores en configuración YAML del workflow. (6 pts) | No configuró GitHub Actions. (0-4 pts) | **10 pts** |
| **4. Sustentación Oral y Demostración en Vivo** | Live Demo impecable, flujo de usuarios completo (Admin/Employee), respuestas técnicas sólidas. (30 pts) | Demostración funcional con detalles menores en respuestas. (24 pts) | Dificultades durante la demo o fallas de contenedores. (18 pts) | Incapacidad para defender el sistema. (0-10 pts) | **30 pts** |
| **TOTAL** | — | — | — | — | **80 Pts** |
