# Banco de Preguntas y Control de Lectura — Fase 2 (10 Preguntas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Tema:** Entity Framework Core 10, Fluent API, Data Seeding, .AsNoTracking() y Persistencia en PostgreSQL  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Ponderación en Asignatura:** 3.0% de la Calificación Total | Puntuación en Google Forms: 20 Puntos (10 Preguntas × 2 pts c/u)

---

## 📝 Banco Oficial de Preguntas de Opción Múltiple

### Pregunta 1
**¿Por qué en arquitecturas limpias como Onion Architecture se prefiere Fluent API sobre Data Annotations para configurar el mapeo relacional?**
- A) Porque Fluent API se ejecuta más rápido en el navegador web del usuario.
- B) Porque desacopla el núcleo de dominio de las dependencias y atributos del ORM, manteniendo las entidades puras y agnósticas. *(Correcta)*
- C) Porque Data Annotations no es compatible con el motor de base de datos PostgreSQL.
- D) Porque Fluent API elimina la necesidad de crear migraciones de base de datos.

*Justificación Técnica:* Colocar atributos de Entity Framework en `Core.Domain` viola el principio de inversión de dependencias y contamina el dominio con detalles técnicos de base de datos.

---

### Pregunta 2
**¿Cuál es la función técnica de la instrucción `.HasPrecision(18, 2)` al configurar propiedades monetarias como `Price` o `CostPrice`?**
- A) Limitar la cantidad máxima de dígitos que un usuario puede ingresar en el teclado a 18 caracteres.
- B) Mapear la propiedad a un tipo numérico de coma flotante IEEE 754 de 64 bits.
- C) Garantizar que la base de datos almacene valores decimales exactos con 18 dígitos totales y 2 decimales, previniendo errores de redondeo financiero. *(Correcta)*
- D) Forzar a que todos los precios terminen obligatoriamente en `.99`.

*Justificación Técnica:* Los tipos decimales de precisión fija en SQL (`NUMERIC`/`DECIMAL`) son esenciales para sistemas de facturación e inventario para evitar discrepancias por redondeo de números de coma flotante.

---

### Pregunta 3
**¿Qué efecto tiene la configuración `.OnDelete(DeleteBehavior.Restrict)` en la relación entre Categoría y Productos?**
- A) Elimina automáticamente en cascada todos los productos pertenecientes a una categoría cuando esta se borra.
- B) Convierte la clave foránea `CategoryId` en `NULL` en todos los productos afectados.
- C) Impide la eliminación de una categoría si todavía existen productos vinculados a ella, protegiendo la integridad referencial del inventario. *(Correcta)*
- D) Oculta la categoría únicamente en la interfaz visual pero la conserva en PostgreSQL.

*Justificación Técnica:* `DeleteBehavior.Restrict` rechaza la operación `DELETE` en la base de datos si la clave foránea está siendo referenciada por registros hijos.

---

### Pregunta 4
**¿Qué beneficio de rendimiento aporta invocar `.AsNoTracking()` en consultas de lectura de Entity Framework Core?**
- A) Guarda los resultados en la memoria caché de Redis automáticamente.
- B) Desactiva el mecanismo `ChangeTracker`, liberando memoria y reduciendo el tiempo de procesamiento en consultas de solo lectura en más de un 35%. *(Correcta)*
- C) Cifra el tráfico entre la API y PostgreSQL utilizando TLS 1.3.
- D) Ejecuta la consulta en segundo plano sin esperar la respuesta de la base de datos.

*Justificación Técnica:* El ChangeTracker mantiene copias de los objetos en memoria para detectar cambios futuros; si solo se van a leer datos (como en un Dashboard), no es necesario rastrearlos.

---

### Pregunta 5
**¿Qué permite la estrategia de Siembra de Datos (Data Seeding) en el contexto de desarrollo del proyecto integrador?**
- A) Generar automáticamente código fuente de controladores en C#.
- B) Insertar registros maestros iniciales (categorías, usuarios, productos) al crear la base de datos, permitiendo probar reglas de negocio de inmediato. *(Correcta)*
- C) Comprimir el tamaño de la base de datos en disco duro.
- D) Probar la velocidad del internet del servidor.

*Justificación Técnica:* La siembra de datos inicializa el entorno con un estado predecible y suficiente información para validar cálculos, filtros y alertas desde el primer despliegue.

---

### Pregunta 6
**Al configurar `builder.HasIndex(p => p.SKU).IsUnique()`, ¿qué ventaja operativa se obtiene en el inventario?**
- A) Se impide la inserción de códigos de producto duplicados y la base de datos optimiza las búsquedas a complejidad algorítmica $O(1)$ mediante un árbol B-Tree. *(Correcta)*
- B) Los productos se eliminan automáticamente cuando el stock llega a cero.
- C) El código SKU se imprime automáticamente en una etiqueta física.
- D) Se habilita el pago con tarjeta de crédito para ese producto.

*Justificación Técnica:* Los índices únicos garantizan la unicidad del catálogo comercial y optimizan la recuperación de datos mediante índices de base de datos.

---

### Pregunta 7
**¿Cuál es la función del método `ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly())` en `ApplicationDbContext`?**
- A) Ejecutar todas las pruebas unitarias del proyecto.
- B) Descubrir y aplicar automáticamente todas las clases que implementan `IEntityTypeConfiguration<T>` en el ensamblado sin necesidad de registrarlas una a una manualmente. *(Correcta)*
- C) Exportar la base de datos a un archivo Excel.
- D) Conectar el servidor con la API de Google Classroom.

*Justificación Técnica:* Este método de EF Core simplifica el mantenimiento al aplicar el principio Abierto/Cerrado (OCP), registrando nuevas configuraciones de mapeo automáticamente.

---

### Pregunta 8
**¿Qué comando del CLI de .NET se utiliza para generar los archivos de migración de EF Core a partir de los cambios en el modelo?**
- A) `dotnet run migrations`
- B) `dotnet ef migrations add <NombreMigracion>` *(Correcta)*
- C) `git commit -m "migrations"`
- D) `npm run migrate`

*Justificación Técnica:* La herramienta global `dotnet-ef` provee el comando `migrations add` para crear las clases de migración relacional en C#.

---

### Pregunta 9
**¿Por qué es fundamental utilizar claves primarias basadas en `Guid` (UUID) en lugar de enteros autoincrementales (`int Id`) en arquitecturas empresariales modernas?**
- A) Porque los UUIDs ocupan menos espacio que los enteros en el disco.
- B) Porque permiten generar identificadores únicos globalmente en el cliente o servidor antes de insertar en la base de datos, facilitando migraciones distribuidas y evitando ataques de enumeración secuencial. *(Correcta)*
- C) Porque los enteros no funcionan en sistemas operativos Linux.
- D) Porque C# 14 no admite el tipo `int`.

*Justificación Técnica:* Los UUIDs mitigan vulnerabilidades de enumeración y simplifican la sincronización de datos entre múltiples entornos y microservicios.

---

### Pregunta 10
**En el método `Configure` de `ProductConfiguration.cs`, ¿cuál es el propósito de `builder.Property(p => p.MinStock).HasDefaultValue(5)`?**
- A) Forzar a que la tienda venda únicamente múltiplos de 5 productos.
- B) Establecer a nivel de esquema de base de datos un valor por defecto de 5 unidades para el umbral de seguridad cuando no se suministre un valor explícito. *(Correcta)*
- C) Borrar el producto si el stock baja de 5 unidades.
- D) Duplicar el precio del producto por 5.

*Justificación Técnica:* `HasDefaultValue` define una restricción `DEFAULT` en la columna DDL de PostgreSQL como red de seguridad para la integridad de datos.
