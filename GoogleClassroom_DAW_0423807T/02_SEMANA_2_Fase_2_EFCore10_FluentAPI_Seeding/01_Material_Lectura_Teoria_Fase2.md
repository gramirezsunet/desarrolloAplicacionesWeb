# Semana 2 — Fase 2: Mapeo Objeto-Relacional con EF Core 10, Fluent API & Data Seeding
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🗄️ 1. Persistencia Relacional y Enfoque Code-First

En arquitecturas corporativas modernas, el enfoque **Code-First** permite que el modelo de dominio en C# defina la estructura de la base de datos PostgreSQL, asegurando que el código sea la **Única Fuente de Verdad (Single Source of Truth)**.

### Ventajas de Code-First con Entity Framework Core 10:
1. **Control de Versiones del Esquema:** Las migraciones de EF Core se almacenan en archivos de C# rastreables en Git.
2. **Portabilidad:** Permite ejecutar pruebas unitarias con proveedores en memoria (`InMemory`) o bases de datos de integración en Docker sin modificar la lógica.
3. **Tipado Fuerte en Consultas:** Las consultas LINQ son validadas en tiempo de compilación, eliminando errores de sintaxis en sentencias SQL crudas.

---

## 📐 2. Fluent API vs. Data Annotations

La separación de responsabilidades exige que el núcleo del dominio no esté acoplado a detalles de infraestructura. Por esta razón, en la **Onion Architecture** se prohíbe el uso de atributos como `[Key]`, `[MaxLength]` o `[Column]` sobre las entidades en `Core.Domain`.

En su lugar, se emplea el patrón **Fluent API** en clases dedicadas que implementan `IEntityTypeConfiguration<T>` dentro de la capa `Infrastructure`:

```
┌───────────────────────────────┐
│        Core.Domain            │
│  Entidad Product (Limpia)     │
└──────────────▲────────────────┘
               │ Mapeo desacoplado
┌──────────────┴────────────────┐
│        Infrastructure         │
│     ProductConfiguration      │
│   (Reglas Fluent API & BD)    │
└───────────────────────────────┘
```

### Reglas Críticas Configuradas con Fluent API:
* **Precisión Monetaria Contable:** `builder.Property(p => p.Price).HasPrecision(18, 2);` — Evita errores catastróficos de redondeo producidos por tipos de coma flotante (`float`/`double`).
* **Integridad Referencial Restrictiva:** `builder.HasOne(p => p.Category).WithMany(c => c.Products).HasForeignKey(p => p.CategoryId).OnDelete(DeleteBehavior.Restrict);` — Impide que un usuario elimine una categoría padre si aún existen productos dependientes.
* **Índices Únicos $O(1)$:** `builder.HasIndex(p => p.SKU).IsUnique();` — Garantiza unicidad del código de barras y acelera las consultas de búsqueda por SKU a tiempo constante.

---

## ⚡ 3. Optimización de Lectura con `.AsNoTracking()`

Entity Framework Core utiliza internamente un componente llamado `ChangeTracker` para detectar qué propiedades de una entidad han cambiado y generar sentencias `UPDATE`.

Sin embargo, en operaciones de solo lectura (como alimentar el **Dashboard KPI** o listar catálogos), el ChangeTracker genera una sobrecarga innecesaria de CPU y memoria:

```csharp
// Consulta no rastreada: Reduce el consumo de memoria en más del 35%
var products = await _context.Products
    .AsNoTracking()
    .Include(p => p.Category)
    .ToListAsync();
```

---

## 🌱 4. Estrategia de Siembra de Datos (Data Seeding)

Para garantizar que el sistema sea inmediatamente operativo al desplegarse en desarrollo o producción, se configuran datos maestros en el método `OnModelCreating`:
- Creación de categorías base de ferretería (Herramientas Manuales, Materiales de Construcción, Electricidad, Plomería).
- Siembra de productos con SKUs normalizados, costos, precios de venta y umbrales de stock mínimo/máximo para validar las alertas del sistema.
- Creación de usuarios semilla con roles `Admin` y `Employee` con contraseñas hasheadas en SHA-256.
