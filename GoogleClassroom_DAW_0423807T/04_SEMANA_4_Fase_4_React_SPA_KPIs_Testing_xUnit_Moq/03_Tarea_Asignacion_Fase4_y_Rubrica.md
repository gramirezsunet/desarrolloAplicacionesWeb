# Tarea y Asignación Práctica — Semana 4 (Fase 4)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Categoría en Classroom:** Unidad II: Frontend y Analítica  
**Puntuación en Google Classroom:** 80 Puntos Máximos | Ponderación en Asignatura: 32.0% (de 40% de la Unidad II)

---

## 📌 Enunciado del Proyecto

El estudiante o equipo debe desarrollar el cliente **Frontend en React 18 SPA con Vite y Tailwind CSS** conectado a la API REST, implementando el **Modo Oscuro Institucional UNET**, el **Dashboard de Indicadores KPI**, el catálogo con filtrado y modal, y la suite de **Pruebas Unitarias Automatizadas en C# con xUnit y Moq**.

### Requerimientos Obligatorios:

#### 1. Frontend SPA React & Identidad UNET:
- **Autenticación en Frontend:** Formulario de Login reactivo con efecto glassmorphism, orbes ambientales animados y almacenamiento seguro de token en `localStorage`.
- **Tema Institucional UNET:** Alternancia interactiva entre Modo Claro (Azul UNET `#003366`) y Modo Oscuro, conmutando dinámicamente el imagotipo institucional UNET.
- **Dashboard de Indicadores KPI:** 4 tarjetas estadísticas (Valor Total del Inventario, Unidades en Existencia, Alertas de Stock Bajo Mínimo y Margen Bruto Estimado).
- **Catálogo y Modal:** Tabla responsiva con buscador predictivo por SKU/Nombre, filtrado por categorías, badges de estado de stock y modal interactivo para registrar/editar productos.

#### 2. Suite de Pruebas Unitarias Automatizadas con xUnit y Moq:
- Proyecto `tests/UnitTests` configurado con xUnit y Moq.
- Implementar un mínimo de 4 pruebas unitarias aisladas para `ProductService` y/o `CategoryService`:
  1. `GetById_WhenExists_ReturnsDto`
  2. `GetById_WhenNotFound_ThrowsKeyNotFoundException`
  3. `CreateProduct_WhenValid_ReturnsCreatedDto`
  4. `DeleteProduct_WhenNotFound_ThrowsKeyNotFoundException`
- 100% de las pruebas deben ejecutarse exitosamente con `dotnet test`.

---

## 📋 Formato de Entrega
- Enlace al repositorio GitHub con el código del backend, pruebas y frontend integrados.
- Video demostrativo corto (3-5 min) o capturas de pantalla evidenciando:
  1. Login y persistencia del token.
  2. Alternancia de tema Claro/Oscuro y cambio de logo UNET.
  3. Creación de un nuevo producto desde el modal y actualización inmediata de los KPIs.
  4. Ejecución de `dotnet test` con todas las pruebas en verde.

---

## 📊 Rúbrica de Evaluación Estandarizada (80 Puntos Máximos)

| Criterio | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos Máx. |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. UI/UX, Modo Oscuro e Identidad UNET** | Diseño impecable, Azul UNET oficial, conmutación reactiva de logo claro/oscuro, animaciones sutiles. (25 pts) | Interfaz funcional y atractiva, pero sin alternancia de logos o detalles menores de contraste. (20 pts) | Interfaz básica sin estilos institucionales o sin modo oscuro. (15 pts) | Interfaz rota o componentes desalineados. (0-10 pts) | **25 pts** |
| **2. Dashboard KPI y Catálogo Reactivo** | Cálculos matemáticos exactos en KPIs, reactividad inmediata al crear/editar productos, modal fluido. (25 pts) | Catálogo funcional pero KPIs estáticos o que requieren recargar la página. (20 pts) | Errores en cálculos de valorización o filtros defectuosos. (15 pts) | Catálogo incompleto o sin modal de registro. (0-10 pts) | **25 pts** |
| **3. Conexión HTTP & Gestión de Estado** | `AuthContext` y `ThemeContext` bien modularizados, manejo de errores de API y bloqueo de rutas por rol. (10 pts) | Conexión funcional con alguna fuga de estado menor. (8 pts) | Falta manejo de respuestas de error de la API. (6 pts) | El frontend no se comunica con la API backend. (0-4 pts) | **10 pts** |
| **4. Suite de Pruebas xUnit & Moq** | 4+ pruebas deterministas bien estructuradas (Arrange-Act-Assert), mocks rigurosos y `dotnet test` 100% verde. (20 pts) | Pruebas funcionales pero con solo 2 escenarios o aserciones poco rigurosas. (16 pts) | Pruebas que dependen de base de datos real (no usan mocks). (12 pts) | Pruebas fallidas o sin proyecto de testing. (0-8 pts) | **20 pts** |
| **TOTAL** | — | — | — | — | **80 Pts** |
