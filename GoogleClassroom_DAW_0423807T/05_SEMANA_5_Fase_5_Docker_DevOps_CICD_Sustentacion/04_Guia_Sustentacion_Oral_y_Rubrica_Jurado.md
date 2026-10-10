# Guía de Sustentación Técnica Oral y Rúbrica de Jurado — Fase 5
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Componente:** Evaluación Oral y Live Demo (Integrada en la Asignación 5 - 30 pts de 80 pts)

---

## 🎯 Objetivo de la Evaluación Final
Evaluar de manera integral la competencia profesional de los estudiantes para defender técnicamente su solución Full-Stack en vivo frente al tribunal evaluador, respondiendo preguntas de ingeniería y demostrando la operatividad del sistema contenerizado.

---

## 🎤 1. Protocolo y Estructura de la Defensa (15 Minutos por Equipo)

```
┌────────────────────────────────────────────────────────┐
│     CRONOMETRAJE RIGUROSO DE DEFENSA TÉCNICA           │
├───────────────┬────────────────────────────────────────┤
│ 00 - 03 min   │ Justificación Arquitectónica y Dominio  │
│ 03 - 08 min   │ Demostración en Vivo (Live Demo)       │
│ 08 - 11 min   │ Suite de Pruebas Unitarias y CI/CD     │
│ 11 - 15 min   │ Preguntas de Ingeniería del Jurado     │
└───────────────┴────────────────────────────────────────┘
```

### Reglas de la Demostración en Vivo:
1. **Arranque en Frío:** El proyecto debe ser levantado frente al jurado con `docker compose down -v` seguido de `docker compose up --build -d`.
2. **Flujo de Usuario Completo:**
   - Inicio de sesión con usuario `Admin` (validar token JWT en DevTools).
   - Creación de una categoría y un producto con stock crítico.
   - Constatación visual en el **Dashboard KPI** de la actualización de montos y alertas de stock.
   - Cierre de sesión e inicio con usuario `Employee`.
   - Intento de eliminación de un producto -> Demostrar bloqueo visual y respuesta `403 Forbidden` de la API.
3. **Calidad y Testing:**
   - Ejecución de la suite de pruebas unitarias `dotnet test` demostrando 100% de éxito en aserciones.
   - Demostración del pipeline en GitHub Actions con status "Passing" (verde).

---

## 📊 2. Rúbrica de Evaluación del Desempeño Oral y Live Demo (30 Puntos)

| Criterio Evaluado | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. Demostración en Vivo / Live Demo** | Flujo integral fluido: Login JWT, RBAC 403 comprobado, modal con animaciones, KPIs en tiempo real sin fallos. (12 pts) | Flujo mayormente funcional con algún detalle menor en la interfaz o lentitud leve. (10 pts) | Fallas durante el Live Demo que requieren reiniciar contenedores. (7 pts) | La aplicación no responde o la base de datos no conecta. (0-4 pts) | **12 pts** |
| **2. Rigor Arquitectónico y Código** | Onion Architecture estricta, EF Core Fluent API con precisión decimal monetaria y validación defensiva en DTOs. (10 pts) | Arquitectura comprensible con leves acoplamientos entre capas. (8 pts) | Mezcla de lógica en controladores o entidades con Data Annotations. (6 pts) | Código desorganizado sin patrones reconocibles. (0-3 pts) | **10 pts** |
| **3. Dominio Conceptual y Defensa Oral** | Respuestas precisas, fundamentadas en ingeniería de software, seguridad OWASP y conceptos de .NET/React. (8 pts) | Buenas respuestas con dudas menores en conceptos de inyección de dependencias o JWT. (6 pts) | Dificultad para explicar el funcionamiento del código presentado. (4 pts) | Incapacidad para responder preguntas básicas del jurado. (0-2 pts) | **8 pts** |
| **TOTAL SUSTENTACIÓN** | — | — | — | — | **30 Pts** |
