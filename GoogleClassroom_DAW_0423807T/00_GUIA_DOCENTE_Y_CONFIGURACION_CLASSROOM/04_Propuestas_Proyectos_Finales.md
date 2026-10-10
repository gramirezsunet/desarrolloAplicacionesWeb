# Propuestas de Proyectos Finales para Estudiantes
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Introducción y Selección de Proyecto

Los estudiantes pueden optar por completar y extender el **Proyecto Base Oficial (Sistema de Gestión de Inventario para Ferretería)** o seleccionar una de las dos propuestas avanzadas de software empresarial descritas a continuación.

Todas las propuestas deben cumplir obligatoriamente con la misma arquitectura:
- **Backend:** .NET 10 (C# 14), Onion Architecture, Entity Framework Core 10, PostgreSQL 15, JWT Bearer, FluentValidation, Middleware RFC 7807.
- **Frontend:** React 18, Vite, Tailwind CSS, Dark Mode institucional UNET, Dashboard Analítico de KPIs.
- **DevOps & QA:** Pruebas unitarias xUnit + Moq, Docker Multi-stage y Docker Compose.

---

## 🏥 Propuesta A: MediStock ERP (Gestión Farmacéutica y Hospitalaria)

### 📋 Descripción:
Sistema integral para el control de inventario clínico y farmacéutico con estricta trazabilidad de medicamentos, lotes de fabricación, fechas de caducidad y despacho de recetas médicas.

### 🗄️ Entidades Principales:
1. `Medication`: Código sanitario único, nombre comercial, principio activo, concentración, forma farmacéutica, precio, costo y temperatura requerida de almacenamiento.
2. `Batch` (Lote): Número de lote, fecha de fabricación, fecha de caducidad, cantidad recibida y stock disponible.
3. `Supplier` (Proveedor): RIF, razón social, contacto, teléfono y dirección fiscal.
4. `Prescription` (Receta / Orden): Folio, médico emisor, paciente, fecha de emisión y estado (Pendiente, Despachada, Anulada).
5. `PrescriptionDetail`: Medicamento, dosis prescrita, cantidad despachada.

### 👥 Roles del Sistema (RBAC):
- `Admin`: Gestión total del sistema, configuración de catálogos y auditoría.
- `Doctor`: Emisión y consulta de recetas médicas.
- `Pharmacist`: Despacho de medicamentos, registro de lotes y control de mermas.

### 📊 Dashboard de Indicadores KPI:
- **Semáforo de Caducidad:** Alerta roja para lotes con vencimiento `< 30 días`, amarilla `< 90 días`, verde `> 90 días`.
- **Tasa de Rotación de Antibióticos y Medicamentos Esenciales.**
- **Valor Monetario de Mermas por Caducidad vs. Ventas.**

---

## 🚚 Propuesta B: LogiTrack Enterprise (Trazabilidad Logística y Encomiendas)

### 📋 Descripción:
Plataforma empresarial para la administración de paquetes, capacidad volumétrica de bodegas, asignación de rutas y rastreo en tiempo real de envíos terrestres.

### 🗄️ Entidades Principales:
1. `Shipment` (Envío): Guía de rastreo única (Tracking Number), remitente, destinatario, peso (kg), volumen ($m^3$), valor declarado, costo de flete y estado (En Bodega, En Tránsito, Entregado, Retenido).
2. `Warehouse` (Bodega / Centro de Distribución): Nombre, ciudad, dirección, capacidad máxima en $m^3$ y ocupación actual.
3. `Courier` (Repartidor / Vehículo): Placa, chofer, capacidad de carga, teléfono y estado operativo.
4. `TrackingCheckpoint` (Punto de Control): Fecha/hora UTC, ubicación actual, descripción del evento y usuario que registró el hito.

### 👥 Roles del Sistema (RBAC):
- `LogisticsAdmin`: Creación de bodegas, reportes financieros y gestión de tarifas.
- `Dispatcher`: Asignación de paquetes a vehículos y rutas de despacho.
- `Courier`: Actualización del estado de entrega en ruta y registro de checkpoints.

### 📊 Dashboard de Indicadores KPI:
- **Porcentaje de Ocupación Volumétrica por Bodega.**
- **Tiempo Promedio de Tránsito (Lead Time de Entrega).**
- **Índice de Incidencias y Paquetes Retenidos.**
- **Valorización Diaria de Fletes Facturados.**

---

## 🛠️ Criterios de Sustentación para Proyectos Finales

1. Demostración en vivo en localhost con `docker-compose up --build`.
2. Flujo completo: Login como Admin -> Gestión de Catálogos -> Visualización en Dashboard KPI -> Login como Empleado/Rol Secundario -> Verificación de restricción de permisos 403.
3. Ejecución en vivo de la suite de pruebas unitarias con `dotnet test`.
