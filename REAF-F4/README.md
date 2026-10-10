# REAF-F4: Recomendaciones Estratégicas, Funcionales y Arquitectónicas (Fase 4)

Este directorio contiene la aplicación web interactiva y la documentación de recomendaciones técnicas para la **Fase 4** de la asignatura **Desarrollo de Aplicaciones Web**, adaptadas a los modelos de negocio específicos de los 5 grupos registrados.

---

## 🎯 **Acrónimo del Proyecto**
* **R** &mdash; Recomendaciones
* **E** &mdash; Estratégicas
* **A** &mdash; Arquitectónicas y
* **F** &mdash; Funcionales para la
* **F4** &mdash; Fase 4

---

## 🚀 **Estructura y Contenido de la Aplicación**

La aplicación interactiva está construida como una Single Page Application (SPA) en `index.html` con las siguientes capacidades:

1. **Explorador Dinámico por Grupos:**
   * **Grupo 1 (Distribución Polar):** Logística en ruta, liquidación ciega de camiones, balance de envases vacíos (*Empty Groups*) e impresión térmica de tickets.
   * **Grupo 2 (Agencia de Lotería):** Terminal POS rápida con teclado numérico, algoritmo de control de riesgo de banca, escáner/verificador de tickets premiados y resultados en vivo.
   * **Grupo 3 (Gestión de Ganado DAW):** Ficha 360° del bovino, mapa interactivo de potreros, cálculo de Ganancia Diaria de Peso ($\text{GDP}$) y pesaje masivo en manga.
   * **Grupo 4 (E-commerce Almacén):** Catálogo con búsqueda predictiva, checkout guiado (*Stepper*), carga de comprobantes de pago y tablero Kanban administrativo.
   * **Grupo 5 (Licorería + Discoteca / Club Nocturno):** Modelo híbrido (Modo Día / Modo Noche), plano interactivo de mesas/zonas VIP, pantalla KDS de barra para bartenders, máquina de estados de comandas (`Recibido -> Preparado -> Entregado`), cuentas abiertas con abonos mixtos y control de mermas/cortesías.

2. **Matriz y Cuadro de Mando de Evaluación Oficial (Sesión 9 de Octubre):**
   * Puntuación máxima de **80 Puntos (4 criterios equitativos de 20 pts c/u)** y ponderación del 32.0%.
   * Calificaciones oficiales y porcentajes obtenidos por cada grupo (G1: No Presentó, G2: No Presentó, G3: 60 pts / 75.0%, G4: 68 pts / 85.0%, G5: 50 pts / 62.5%).
   * Observaciones y retroalimentación técnica individualizada para cada equipo con directrices para la Fase 5.
   * Filtro interactivo por estado (*Todos*, *Evaluados*, *Pendientes*).

3. **Matriz Comparativa de Implementación:**
   * Tabla con buscador en tiempo real que compara los componentes Frontend clave, flujos de integración y analítica de negocio entre los 5 proyectos.

4. **Checklist Transversal de Calidad Industrial:**
   * 10 puntos de control con almacenamiento de progreso en `localStorage` (Autenticación JWT, Interceptor RFC 7807, RBAC Guards, Skeletons, Paginación, Docker, etc.).

5. **Modo Claro / Oscuro Institucional UNET & Exportación a PDF/Impresión.**

---

## 💻 **Cómo Visualizar la Aplicación**

Simplemente abre el archivo `REAF-F4/index.html` en cualquier navegador web moderno:
```bash
# Abrir directamente en Windows:
start REAF-F4/index.html
```

O sírvelo con cualquier servidor estático local:
```bash
npx serve REAF-F4
# o
python -m http.server 8080 --directory REAF-F4
```
