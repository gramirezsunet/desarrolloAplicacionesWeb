# Guía de Laboratorio y Live Coding — Fase 2
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Objetivo de la Práctica
Configurar la persistencia relacional con **Entity Framework Core 10** y el proveedor **Npgsql** para PostgreSQL, implementar configuraciones desacopladas con **Fluent API**, optimizar repositorios con `.AsNoTracking()` y sembrar datos iniciales representativos de inventario.

---

## 📦 Paso 1: Instalación de Paquetes NuGet en `Infrastructure`

Desde la raíz del repositorio, instale las dependencias oficiales de EF Core 10:

```bash
dotnet add src/backend/Infrastructure/Infrastructure.csproj package Npgsql.EntityFrameworkCore.PostgreSQL --version 10.0.0
dotnet add src/backend/Infrastructure/Infrastructure.csproj package Microsoft.EntityFrameworkCore --version 10.0.0
dotnet add src/backend/Infrastructure/Infrastructure.csproj package Microsoft.EntityFrameworkCore.Relational --version 10.0.0
dotnet add src/backend/Presentation.API/Presentation.API.csproj package Microsoft.EntityFrameworkCore.Design --version 10.0.0
```

---

## ⚙️ Paso 2: Implementación de Fluent API (`ProductConfiguration.cs`)

Cree `src/backend/Infrastructure/Persistence/Configurations/ProductConfiguration.cs`:

```csharp
namespace Infrastructure.Persistence.Configurations;

using Core.Domain.Entities;
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

public class ProductConfiguration : IEntityTypeConfiguration<Product>
{
    public void Configure(EntityTypeBuilder<Product> builder)
    {
        builder.ToTable("Products");
        builder.HasKey(p => p.Id);

        builder.Property(p => p.Name).IsRequired().HasMaxLength(150);
        builder.Property(p => p.SKU).IsRequired().HasMaxLength(20);
        builder.HasIndex(p => p.SKU).IsUnique(); // Búsquedas rápidas O(1)

        builder.Property(p => p.Description).HasMaxLength(500);
        builder.Property(p => p.Price).IsRequired().HasPrecision(18, 2);
        builder.Property(p => p.CostPrice).IsRequired().HasPrecision(18, 2);

        builder.Property(p => p.Stock).IsRequired();
        builder.Property(p => p.MinStock).IsRequired().HasDefaultValue(5);
        builder.Property(p => p.MaxStock).IsRequired().HasDefaultValue(100);
        builder.Property(p => p.Location).HasMaxLength(100).HasDefaultValue("Almacén Principal");
        builder.Property(p => p.UnitOfMeasure).HasMaxLength(30).HasDefaultValue("Unidad");
        builder.Property(p => p.Brand).HasMaxLength(80);
        builder.Property(p => p.IsActive).IsRequired().HasDefaultValue(true);

        // Relación 1:N con restricción de borrado
        builder.HasOne(p => p.Category)
               .WithMany(c => c.Products)
               .HasForeignKey(p => p.CategoryId)
               .OnDelete(DeleteBehavior.Restrict);
    }
}
```

---

## 🗄️ Paso 3: Configuración de `ApplicationDbContext.cs` y Data Seeding

Cree `src/backend/Infrastructure/Persistence/ApplicationDbContext.cs`:

```csharp
namespace Infrastructure.Persistence;

using System.Reflection;
using Core.Domain.Entities;
using Microsoft.EntityFrameworkCore;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

    public DbSet<Product> Products => Set<Product>();
    public DbSet<Category> Categories => Set<Category>();
    public DbSet<User> Users => Set<User>();

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        modelBuilder.ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly());

        // Siembra inicial de categorías maestras
        var catHerramientas = new Category { Id = Guid.Parse("11111111-1111-1111-1111-111111111111"), Name = "Herramientas Manuales", Description = "Martillos, destornilladores, llaves y pinzas" };
        var catConstruccion = new Category { Id = Guid.Parse("22222222-2222-2222-2222-222222222222"), Name = "Materiales de Construcción", Description = "Cemento, arena, varillas de acero y bloques" };

        modelBuilder.Entity<Category>().HasData(catHerramientas, catConstruccion);

        // Siembra inicial de productos
        modelBuilder.Entity<Product>().HasData(
            new Product
            {
                Id = Guid.Parse("aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa"),
                CategoryId = catHerramientas.Id,
                Name = "Martillo de Uña Curva 16oz",
                SKU = "FERR-MART-001",
                Description = "Martillo de acero forjado con mango ergonómico de fibra de vidrio.",
                Price = 14.50m,
                CostPrice = 8.20m,
                Stock = 35,
                MinStock = 10,
                MaxStock = 80,
                Location = "Pasillo A - Estante 2",
                Brand = "Stanley",
                UnitOfMeasure = "Unidad",
                IsActive = true
            }
        );
    }
}
```

---

## 🚀 Paso 4: Implementación del Repositorio Optimizado con `.AsNoTracking()`

Cree `src/backend/Infrastructure/Repositories/ProductRepository.cs`:

```csharp
namespace Infrastructure.Repositories;

using Core.Application.Interfaces;
using Core.Domain.Entities;
using Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

public class ProductRepository : IProductRepository
{
    private readonly ApplicationDbContext _context;

    public ProductRepository(ApplicationDbContext context)
    {
        _context = context;
    }

    public async Task<IEnumerable<Product>> GetAllReadOnlyAsync()
    {
        return await _context.Products
            .AsNoTracking()
            .Include(p => p.Category)
            .Where(p => p.IsActive)
            .ToListAsync();
    }

    public async Task<Product?> GetByIdAsync(Guid id)
    {
        return await _context.Products
            .Include(p => p.Category)
            .FirstOrDefaultAsync(p => p.Id == id);
    }

    public async Task AddAsync(Product product)
    {
        await _context.Products.AddAsync(product);
        await _context.SaveChangesAsync();
    }
}
```

---

## 🧪 Paso 5: Ejecución y Verificación de Migraciones

```bash
# 1. Crear la migración inicial
dotnet ef migrations add InitialCreate -p src/backend/Infrastructure -s src/backend/Presentation.API

# 2. Aplicar la migración a PostgreSQL
dotnet ef database update -p src/backend/Infrastructure -s src/backend/Presentation.API
```
