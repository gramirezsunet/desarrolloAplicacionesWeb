## **Instrucciones y Evaluación de la Fase 4 \- ERP**

*Asignatura: Desarrollo de Aplicaciones Web | Prof. Gabriel A. Ramírez S.*

Estimados estudiantes, en la evaluación de hoy llevaremos a cabo la revisión técnica de la Fase 4 de su proyecto ERP. Esta fase abarca el desarrollo del Frontend SPA (React \+ Vite \+ Tailwind CSS), la construcción del Dashboard de Indicadores KPI y la implementación de Pruebas Unitarias (xUnit & Moq). 

La evaluación tiene un valor total de 80 puntos, distribuidos equitativamente en 4 criterios de 20 puntos cada uno.

Para asegurar un proceso de aprendizaje colaborativo y transparente, utilizaremos el instrumento de Rúbrica de Evaluación y Retroalimentación de la Fase 4 (REAF-F4) durante las exposiciones. Durante sus presentaciones, cada equipo responderá y demostrará el cumplimiento de las siguientes preguntas y criterios fundamentales:

1. **Criterio 1: Arquitectura Frontend SPA y Componentización (20 pts)** – Estructura del proyecto en React \+ Vite, enrutamiento y diseño responsivo con Tailwind (10 pts); Modularidad, reusabilidad de componentes y gestión de estado (10 pts).  
2. **Criterio 2: Consumo de APIs REST y Manejo de Estado (20 pts)** – Integración asíncrona, control de errores y peticiones HTTP al backend ERP (5 pts); Autenticación con JWT, seguridad y manejo de estado local/global (10 pts).  
3. **Criterio 3: Dashboard de Indicadores KPI y Visualización de Datos (20 pts)** – Diseño e implementación de tarjetas KPI e indicadores clave (10 pts); Gráficos interactivos, filtros dinámicos e integración en tiempo real (10 pts).  
4. **Criterio 4: Pruebas Unitarias y Cobertura (xUnit & Moq) (20 pts)** – Definición y ejecución de pruebas unitarias para validación de lógica de negocio en xUnit (10 pts); Simulación e independencia de servicios mediante Moq y cobertura adecuada (10 pts).

### **Justificación y Contexto Técnico de los Criterios de Evaluación**

El diseño de una Single Page Application (SPA) moderna requiere una arquitectura sólida e interactiva que atienda de forma eficiente las necesidades del cliente. La estructuración adecuada mediante React y Vite, junto con Tailwind CSS, acelera los tiempos de carga y asegura la sostenibilidad del proyecto a largo plazo a través de la modularización de componentes. Este desacoplamiento en módulos funcionales potencia la escalabilidad y sienta las bases de un trabajo colaborativo fluido.

Del mismo modo, el desarrollo de interfaces adaptables e intuitivas garantiza una experiencia de usuario fluida e independiente del dispositivo o plataforma. La evaluación de este apartado es clave para constatar que los estudiantes apliquen los estándares actuales de componentización, organización del código y programación declarativa en el entorno Frontend.  
La integración eficiente entre la capa cliente y el backend del ERP constituye la columna vertebral del funcionamiento empresarial, donde el procesamiento asíncrono de peticiones y la gestión rigurosa de errores respaldan la estabilidad del sistema. La implementación de autenticación mediante Tokens JWT resguarda la aplicación ante accesos no autorizados, asegurando el control de acceso en rutas y sesiones.

Por otra parte, la preservación de un estado local y global uniforme garantiza la actualización inmediata de la información en toda la plataforma. Este indicador permite comprobar la idoneidad del equipo para estructurar flujos de datos confiables y preparados para responder a eventualidades en tiempo real.

En la gestión corporativa, la alta dirección requiere de datos consolidados para la toma estratégica de decisiones. La creación de un Dashboard interactivo que convierta datos complejos e indicadores clave de rendimiento (KPI) en paneles visuales agiliza la evaluación del desempeño operativo dentro del ERP.

Asimismo, la inclusión de filtros dinámicos y la sincronización de datos en tiempo real enriquecen la capacidad de análisis y diagnóstico. La valoración de este criterio asegura que los estudiantes reconozcan el impacto real del software en el negocio, transformando registros de base de datos en información de valor estratégico.

Garantizar la calidad del software a través de la verificación automatizada de la lógica de negocio previene fallas en producción. El uso del framework xUnit permite certificar el funcionamiento individual de los algoritmos y operaciones críticas del ERP, asegurando el cumplimiento de las especificaciones definidas.

En paralelo, el empleo de dobles de prueba con Moq posibilita el aislamiento completo de los servicios frente a la infraestructura de base de datos, agilizando la ejecución y asegurando la independencia de las pruebas. La medición de este aspecto consolida el compromiso con la calidad y promueve el uso de estándares de prueba reconocidos en la industria.

### **Ejemplos de Evidencias Concretas por Criterio**

Para validar la ejecución técnica, cada equipo deberá presentar durante la exposición las siguientes evidencias prácticas en vivo y en el repositorio del proyecto:

1. **Gestión de Estado y Autenticación:** Demostración del flujo completo de inicio de sesión con JWT, almacenamiento seguro de tokens en el navegador, persistencia/limpieza del estado global al recargar o cerrar sesión, y protección efectiva de rutas privadas en React Router.  
2. **Dashboard KPI y Analítica de Negocio:** Visualización funcional de al menos tres tarjetas de métricas clave (ej. Ventas Totales, Stock Crítico, Pedidos Pendientes) y gráficos interactivos alimentados por endpoints del backend con filtrado dinámico por fechas o categorías.  
3. **Arquitectura Frontend y Mejores Prácticas:** Muestra de la estructura modular del proyecto (separación de componentes, hooks personalizados, servicios API y contextos), diseño adaptable (responsive) en distintas resoluciones e integración limpia de Tailwind CSS sin estilos duplicados.  
4. **Pruebas Unitarias y Aislamiento de Capas:** Ejecución e informe de pruebas con xUnit evidenciando casos exitosos y fallidos, con un nivel razonable de cobertura de código y un aislamiento estricto de la capa de servicios/datos utilizando simulaciones con Moq.

### **Formato de Instrumento de Evaluación y Retroalimentación (REAF-F4)**

**Opciones de Evaluación Estandarizadas por Criterio (0 \- 20 pts):**  
• **Excelente (18-20 pts):** Cumplimiento completo, arquitectura sólida, buenas prácticas y excelente sustentación.  
• **Bueno (14-17 pts):** Cumplimiento satisfactorio con mínimos detalles por optimizar.  
• **Suficiente (10-13 pts):** Cumplimiento parcial con aspectos funcionales o técnicos por mejorar.  
• **Incompleto / Deficiente (0-9 pts):** Ausencia de características clave o deficiencias graves en la implementación.

| Criterio | Descripción / Aspectos a Evaluar | Puntaje Máx. | G1 | G2 | G3 | G4 | G5 |
| ----- | ----- | :---: | ----- | ----- | ----- | ----- | ----- |
| **1\. Frontend SPA & Componentización** | • Estructura React \+ Vite, enrutamiento y Tailwind CSS (10 pts)• Modularidad y gestión de estado de componentes (10 pts) | 20 pts | — | — | 16 | 14 | 18 |
| **2\. Consumo de APIs & Estado** | • Integración de peticiones HTTP asíncronas y errores (10 pts)• Autenticación con JWT y estado local/global (10 pts) | 20 pts | — | — | 18 | 16 | 12 |
| **3\. Dashboard KPI** | • Tarjetas de métricas y métricas KPI clave (10 pts)• Gráficos interactivos y filtros dinámicos (10 pts) | 20 pts | — | — | 16 | 18 | 14 |
| **4\. Pruebas Unitarias (xUnit & Moq)** | • Pruebas unitarias de lógica de negocio en xUnit (10 pts)• Aislamiento de capas y mocks con Moq (10 pts) | 20 pts | — | — | 10 | 20 | 6 |
| **Total Fase 4:** |  | **80 pts** | — | — | **60** | **68** | **50** |

### **Observaciones y Retroalimentación**

Espacio reservado para registrar comentarios, fortalezas detectadas y oportunidades de mejora durante la evaluación:

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Grupo 1 (G1):**

* No Presentó


  **Grupo 2 (G2):**

  * No Presentó


  **Grupo 3 (G3):**

  * Completar la cobertura de pruebas unitarias y de integración (xUnit, Moq y Playwright).  
  * Añadir notificaciones detalladas en el encabezado (header) dirigidas a distintos roles de la aplicación.  
  * Optimizar el manejo de concurrencia en la gestión de inventario.  
  * Mejorar el módulo de gestión de potreros y traslado de ganado con esquemas visuales interactivos y dinámicos.  
  * Implementar lector/cargador de código QR y NFC para la identificación y registro de animales.


  **Grupo 4 (G4):**

  * Incorporar métricas de analítica relacionadas con tipos de dispositivos utilizados.  
  * Ajustar la jerarquía visual del Dashboard: reducir el tamaño de los gráficos y aumentar el tamaño de fuente en las tarjetas de KPI.  
  * Mejorar la interfaz agregando la funcionalidad de colapsar/expandir la barra de navegación lateral.  
  * Implementar exportación e impresión de reportes en formato PDF.  
  * Incorporar un módulo de gestión de promociones y cupones de descuento.


  **Grupo 5 (G5):**

  * Desarrollar la suite de pruebas unitarias faltantes para validar la lógica de negocio.  
  * Incorporar nuevos KPIs relevantes y ajustar el tamaño de las gráficas en el Dashboard.  
  * Implementar la generación y exportación de reportes en formatos PDF y Excel.  
  * Permitir precargar un croquis en el lienzo para la distribución de mesas y restringir la edición de mobiliario únicamente a los empleados.  
  * Refinar la paleta de colores y el diseño visual de la interfaz gráfica.