# Guía de Laboratorio y Live Coding — Fase 1
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Objetivo de la Práctica
Estructurar desde la terminal una solución desacoplada en .NET 10 aplicando **Onion Architecture**, configurar la inyección de dependencias modular y codificar un **Middleware Global de Excepciones** conforme a la norma **RFC 7807**.

---

## 🔨 Paso 1: Creación de la Estructura de Proyectos por CLI

Ejecute los siguientes comandos en PowerShell o Bash para estructurar el backend:

```bash
# 1. Crear directorio raíz y solución .NET
mkdir desarrolloAplicacionesWeb
cd desarrolloAplicacionesWeb
dotnet new sln -n InventarioEmpresarial

# 2. Crear proyectos de biblioteca de clases para cada capa concéntrica
dotnet new classlib -o src/backend/Core.Domain -f net10.0
dotnet new classlib -o src/backend/Core.Application -f net10.0
dotnet new classlib -o src/backend/Infrastructure -f net10.0

# 3. Crear proyecto Web API para la capa de presentación
dotnet new webapi -o src/backend/Presentation.API -f net10.0

# 4. Vincular proyectos a la solución
dotnet sln add src/backend/Core.Domain/Core.Domain.csproj
dotnet sln add src/backend/Core.Application/Core.Application.csproj
dotnet sln add src/backend/Infrastructure/Infrastructure.csproj
dotnet sln add src/backend/Presentation.API/Presentation.API.csproj

# 5. Establecer la Regla de Dependencia (Referencias entre capas)
dotnet add src/backend/Core.Application/Core.Application.csproj reference src/backend/Core.Domain/Core.Domain.csproj
dotnet add src/backend/Infrastructure/Infrastructure.csproj reference src/backend/Core.Domain/Core.Domain.csproj
dotnet add src/backend/Presentation.API/Presentation.API.csproj reference src/backend/Core.Application/Core.Application.csproj
dotnet add src/backend/Presentation.API/Presentation.API.csproj reference src/backend/Infrastructure/Infrastructure.csproj
```

---

## 📦 Paso 2: Modelado del Núcleo de Dominio (`Core.Domain`)

Cree la entidad base en `src/backend/Core.Domain/Common/BaseEntity.cs`:

```csharp
namespace Core.Domain.Common;

public abstract class BaseEntity
{
    public Guid Id { get; set; } = Guid.NewGuid();
    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
}
```

Cree la entidad `Product.cs` en `src/backend/Core.Domain/Entities/Product.cs`:

```csharp
namespace Core.Domain.Entities;

using Core.Domain.Common;

public class Product : BaseEntity
{
    public string Name { get; set; } = string.Empty;
    public string SKU { get; set; } = string.Empty;
    public string? Description { get; set; }
    public decimal Price { get; set; }
    public decimal CostPrice { get; set; }
    public int Stock { get; set; }
    public int MinStock { get; set; } = 5;
    public int MaxStock { get; set; } = 100;
    public string Location { get; set; } = "Almacén Principal";
    public string UnitOfMeasure { get; set; } = "Unidad";
    public string? Brand { get; set; }
    public bool IsActive { get; set; } = true;
    public Guid CategoryId { get; set; }
    public Category Category { get; set; } = null!;
}
```

---

## 🛡️ Paso 3: Implementación del Middleware RFC 7807

Cree el archivo `src/backend/Presentation.API/Middleware/ExceptionMiddleware.cs`:

```csharp
namespace Presentation.API.Middleware;

using System.Net;
using System.Text.Json;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;

public class ExceptionMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<ExceptionMiddleware> _logger;

    public ExceptionMiddleware(RequestDelegate next, ILogger<ExceptionMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (KeyNotFoundException ex)
        {
            _logger.LogWarning(ex, "Recurso no encontrado: {Message}", ex.Message);
            await HandleExceptionAsync(context, HttpStatusCode.NotFound, "Recurso No Encontrado", ex.Message);
        }
        catch (InvalidOperationException ex)
        {
            _logger.LogWarning(ex, "Operación inválida de negocio: {Message}", ex.Message);
            await HandleExceptionAsync(context, HttpStatusCode.BadRequest, "Solicitud Inválida", ex.Message);
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Error crítico no controlado en el servidor.");
            await HandleExceptionAsync(context, HttpStatusCode.InternalServerError, "Error Interno del Servidor", "Ocurrió un error inesperado al procesar la solicitud.");
        }
    }

    private static async Task HandleExceptionAsync(HttpContext context, HttpStatusCode statusCode, string title, string detail)
    {
        context.Response.ContentType = "application/problem+json";
        context.Response.StatusCode = (int)statusCode;

        var problemDetails = new
        {
            type = $"https://httpstatuses.com/{(int)statusCode}",
            title,
            status = (int)statusCode,
            detail,
            instance = context.Request.Path.Value
        };

        var json = JsonSerializer.Serialize(problemDetails);
        await context.Response.WriteAsync(json);
    }
}
```

---

## ⚙️ Paso 4: Registro del Middleware en `Program.cs`

Modifique `src/backend/Presentation.API/Program.cs`:

```csharp
using Presentation.API.Middleware;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Registrar el middleware al inicio del pipeline HTTP
app.UseMiddleware<ExceptionMiddleware>();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

---

## 🧪 Paso 5: Verificación y Prueba de Funcionamiento

1. Compile la solución: `dotnet build`
2. Ejecute la API: `dotnet run --project src/backend/Presentation.API`
3. Pruebe invocar una ruta no existente o provocar un fallo controlado para constatar la cabecera `Content-Type: application/problem+json` y el cuerpo formateado bajo RFC 7807.
