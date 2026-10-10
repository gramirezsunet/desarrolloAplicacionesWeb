# Tarea y Asignación Práctica — Semana 2 (Fase 2)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Puntuación en Google Classroom:** 80 Puntos Máximos | Ponderación en Asignatura: 12.0%

---

## 📌 Enunciado del Proyecto

El estudiante o equipo debe configurar la capa de persistencia `Infrastructure` utilizando **Entity Framework Core 10** sobre una base de datos relacional **PostgreSQL 15**, implementando el mapeo con **Fluent API**, la siembra de datos maestros y repositorios con optimización de lectura.

### Requerimientos Obligatorios:
1. **Configuración Desacoplada con Fluent API:**
   - Crear clases `IEntityTypeConfiguration<T>` para todas las entidades del dominio.
   - Definir claves primarias UUID, nombres de tablas explícitos y longitudes máximas.
   - Configurar precisión decimal `(18,2)` en todos los campos monetarios (precios, costos).
   - Crear índice único para códigos de barras / SKU / identificadores comerciales.
   - Configurar relación 1:N con `DeleteBehavior.Restrict`.
2. **`ApplicationDbContext` y Migraciones:**
   - Crear `ApplicationDbContext` aplicando las configuraciones automáticamente mediante `ApplyConfigurationsFromAssembly`.
   - Generar y versionar en Git los archivos de migración de EF Core.
3. **Siembra de Datos (Data Seeding):**
   - Sembrar al menos 2 categorías maestras y un mínimo de 4 productos/registros representativos con precios, costos y stocks calibrados.
4. **Patrón Repository con Optimización:**
   - Implementar métodos de lectura usando `.AsNoTracking()` para optimizar el rendimiento de la API.

---

## 📋 Formato de Entrega
- Enlace al repositorio GitHub actualizado en la rama correspondiente.
- Script SQL generado o captura de la base de datos en pgAdmin / DBeaver mostrando las tablas creadas con sus índices y datos sembrados.

---

## 📊 Rúbrica de Evaluación Estandarizada (80 Puntos Máximos)

| Criterio | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos Máx. |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. Fluent API & Reglas de Persistencia** | Configuración explícita completa: `HasPrecision(18,2)`, `HasIndex().IsUnique()`, `DeleteBehavior.Restrict`. (30 pts) | Mapeo funcional con pequeñas omisiones en índices o valores por defecto. (24 pts) | Uso indebido de Data Annotations en el dominio o falta de precisión decimal. (18 pts) | Mapeo sin restricciones ni tipos de datos controlados. (0-10 pts) | **30 pts** |
| **2. DbContext & Migraciones Versionadas** | DbContext limpio, migraciones generadas y sincronizadas perfectamente con PostgreSQL. (20 pts) | Migraciones funcionales pero aplicadas manualmente sin script/CLI. (16 pts) | Errores en la generación de migraciones o tablas inconsistentes. (12 pts) | No se generaron migraciones de EF Core. (0-8 pts) | **20 pts** |
| **3. Siembra de Datos Representativa** | Datos sembrados coherentes con el sector (precios, stocks, SKUs y categorías). (15 pts) | Datos sembrados mínimos o con nombres genéricos tipo "test1". (12 pts) | Datos con claves foráneas rotas o stocks inválidos. (9 pts) | Base de datos vacía sin data seeding. (0-5 pts) | **15 pts** |
| **4. Repositorios y Optimización AsNoTracking** | Repositorio desacoplado mediante interfaces, con uso riguroso de `.AsNoTracking()` en consultas Get. (15 pts) | Repositorio funcional pero sin optimización `.AsNoTracking()`. (12 pts) | Acceso a DbContext directo sin repositorio o consultas bloqueantes. (9 pts) | Repositorios incompletos o con excepciones de ejecución. (0-5 pts) | **15 pts** |
| **TOTAL** | — | — | — | — | **80 Pts** |
