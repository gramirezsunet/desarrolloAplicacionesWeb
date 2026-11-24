# REAP-PI: Recomendaciones Estratégicas y Análisis de Propuestas — Programa Integrador

Este directorio contiene la plataforma web interactiva para analizar las propuestas del **Programa Integrador** de la asignatura **Desarrollo de Aplicaciones Web (0423807T — UNET)**, evaluando su alineación con las **Fases 1 y 2** (Arquitectura Onion, validación de stock/reglas de negocio, RFC 7807, EF Core 10, Fluent API y borrado lógico) y su proyección hacia las **Fases 3, 4 y 5** (JWT/RBAC, React 18 + KPIs accionables, xUnit/Moq y Docker/CI-CD).

---

## 🎯 **Acrónimo**
* **R** &mdash; Recomendaciones y
* **E** &mdash; Evaluación con
* **A** &mdash; Análisis de
* **P** &mdash; Propuestas del
* **PI** &mdash; Programa Integrador

---

## 🚀 **Funcionalidades de la Plataforma (`index.html`)**

1. **Indicadores Estadísticos y Control de Listado Oficial (23/11/2026):**
   * Seguimiento de los **19 estudiantes** oficialmente inscritos: **12 entregaron (63.2%)** (8 en 3 equipos y 4 individuales) vs. **7 sin reportarse (36.8%)**.
   * Todas las **7 propuestas** pertenecen a alumnos del listado oficial (ordenadas iniciando con **Equipo 1: Sistema de Taxis**, luego **Equipos 2–3** según el listado oficial y posteriormente las entregas individuales por orden de presentación). Se destaca como observación formal que la **Propuesta 7 (Cero Stock — Alejandra Patiño)** fue entregada sin portada ni identificación en el PDF (indispensable corregir).
   * Filtros interactivos (*Todos*, *Entregaron*, *Individuales*, *Sin Reportar*) y buscador por nombre o cédula.

2. **Observaciones Técnicas Constructivas por Propuesta (Fases 1–5):**
   * Diagnóstico detallado de las **7 propuestas** con aciertos, brechas en **Fase 1 y Fase 2** (stock/capacidad, RFC 7807, Fluent API, `DeleteBehavior.Restrict` y borrado lógico) y hoja de ruta para **Fases 3, 4 y 5**, más botón de copiado rápido para Google Classroom.

3. **Analizador Interactivo en Vivo:**
   * Motor heurístico en navegador para evaluar borradores o nuevas propuestas frente a los 10 criterios críticos de las Fases 1–5, devolviendo puntaje de madurez, desglose por fase y recomendaciones constructivas.

4. **Matriz Comparativa y Checklist Fases 1–5:**
   * Tabla comparativa filtrable entre las 7 propuestas y checklist interactivo de 12 puntos persistido en `localStorage`.

5. **Identidad Visual Institucional UNET:**
   * Mantiene la estética, paleta, modo Claro/Oscuro (`unet-logo.png` / `unet-logo-dark.png`) y banner oficial (`Banner_Google_Classroom_GR.jpeg`) de `REAF-F4`.

---

## 💻 **Cómo Visualizar la Aplicación**

```bash
# Abrir directamente en Windows:
start REAP-PI/index.html

# O servir localmente:
python -m http.server 8080 --directory REAP-PI
```
