# Tarea y Asignación Práctica — Semana 1 (Fase 1)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Puntuación en Google Classroom:** 80 Puntos Máximos | Ponderación en Asignatura: 8.0%

---

## 📌 Enunciado del Proyecto

El estudiante o equipo de trabajo debe inicializar el repositorio base del proyecto asignado (Ferretería, MediStock ERP o LogiTrack Enterprise) aplicando rigurosamente los principios de la **Onion Architecture** en **.NET 10 (C# 14)** y garantizando la resiliencia en el manejo de errores mediante el estándar **RFC 7807**.

### Requerimientos Obligatorios:
1. **Estructura Multicapa:**
   - Crear los 4 proyectos desacoplados: `Core.Domain`, `Core.Application`, `Infrastructure` y `Presentation.API`.
   - Garantizar que `Core.Domain` sea agnóstico (sin dependencias a paquetes externos).
2. **Entidades del Dominio:**
   - Implementar la clase abstracta `BaseEntity` (con `Id: Guid` y `CreatedAt: DateTime UTC`).
   - Implementar al menos dos entidades del dominio del negocio con sus relaciones conceptuales.
3. **Manejo Centralizado de Excepciones:**
   - Crear y registrar `ExceptionMiddleware` para capturar `KeyNotFoundException` (404), `InvalidOperationException` (400) y `Exception` no controlada (500).
   - Ocultar Stack Traces en errores 500 y responder con `application/problem+json`.
4. **Controlador de Prueba:**
   - Crear un endpoint que simule una excepción para demostrar la captura del middleware en Swagger o Postman.

---

## 📋 Formato de Entrega
- Enlace al repositorio en **GitHub** con commits descriptivos.
- Documento `README.md` en el repositorio explicando cómo clonar y compilar la solución con `dotnet build`.
- Captura de pantalla en Postman mostrando la respuesta JSON bajo RFC 7807 ante un error provocado.

---

## 📊 Rúbrica de Evaluación Estandarizada (80 Puntos Máximos)

| Criterio | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos Máx. |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. Arquitectura Onion & Regla de Dependencia** | 4 capas limpiamente separadas, referencias correctas hacia el centro, `Core.Domain` 100% puro. (25 pts) | Capas separadas pero con una referencia no recomendada. (20 pts) | Fusión indebida de capas o dependencias circulares. (15 pts) | Proyecto monolítico de una sola capa sin desacoplamiento. (0-10 pts) | **25 pts** |
| **2. Modelado de Entidades Base** | `BaseEntity` con UUID y UTC, entidades modeladas fielmente al negocio. (15 pts) | Entidades modeladas pero falta trazabilidad UTC o UUID. (12 pts) | Tipos de datos inconsistentes en entidades. (9 pts) | Entidades vacías o sin modelado de dominio. (0-5 pts) | **15 pts** |
| **3. ExceptionMiddleware RFC 7807** | Captura de excepciones específicas, formato exacto RFC 7807, ocultamiento de trazas sensibles. (30 pts) | Middleware funcional pero con diferencias menores en el esquema JSON devuelto. (24 pts) | Middleware que devuelve 500 genérico sin tipificar errores específicos. (18 pts) | Sin middleware; uso de try-catch dispersos en controladores. (0-10 pts) | **30 pts** |
| **4. Repositorio GitHub y Documentación** | Commits claros, `.gitignore` adecuado, README estructurado con comandos de compilación. (10 pts) | Repositorio funcional pero README incompleto. (8 pts) | Faltan instrucciones de ejecución o subida de carpetas `bin/obj`. (6 pts) | Repositorio inaccesible o entrega tardía sin justificación. (0-4 pts) | **10 pts** |
| **TOTAL** | — | — | — | — | **80 Pts** |
