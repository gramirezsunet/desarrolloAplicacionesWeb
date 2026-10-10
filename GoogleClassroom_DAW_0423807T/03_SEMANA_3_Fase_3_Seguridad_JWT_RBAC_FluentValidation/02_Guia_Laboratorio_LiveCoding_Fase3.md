# Guía de Laboratorio y Live Coding — Fase 3
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Objetivo de la Práctica
Configurar la autenticación **JWT Bearer** en ASP.NET Core 10, implementar el servicio de generación de tokens (`TokenService`), aplicar control de acceso granular **RBAC** en controladores y crear validadores defensivos con **FluentValidation**.

---

## 📦 Paso 1: Instalación de Paquetes NuGet de Seguridad y Validación

```bash
# Paquete de autenticación JWT Bearer en Presentation.API
dotnet add src/backend/Presentation.API/Presentation.API.csproj package Microsoft.AspNetCore.Authentication.JwtBearer --version 10.0.0

# Paquete de FluentValidation en Core.Application
dotnet add src/backend/Core.Application/Core.Application.csproj package FluentValidation --version 11.9.0
dotnet add src/backend/Core.Application/Core.Application.csproj package FluentValidation.DependencyInjectionExtensions --version 11.9.0
```

---

## 🔑 Paso 2: Servicio de Emisión de Tokens JWT (`TokenService.cs`)

Cree `src/backend/Infrastructure/Services/TokenService.cs`:

```csharp
namespace Infrastructure.Services;

using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;
using Core.Application.Interfaces;
using Core.Domain.Entities;
using Microsoft.Extensions.Configuration;
using Microsoft.IdentityModel.Tokens;

public class TokenService : ITokenService
{
    private readonly IConfiguration _config;

    public TokenService(IConfiguration config)
    {
        _config = config;
    }

    public string GenerateToken(User user)
    {
        var secretKey = _config["JwtSettings:Key"] ?? "UNET_DESARROLLO_DE_APLICACIONES_WEB_SECRET_KEY_2026_JWT_SUPER_SECURE!";
        var issuer = _config["JwtSettings:Issuer"] ?? "UNET_Inventory_API";
        var audience = _config["JwtSettings:Audience"] ?? "UNET_Inventory_Clients";

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(secretKey));
        var credentials = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

        var claims = new List<Claim>
        {
            new(JwtRegisteredClaimNames.Sub, user.Id.ToString()),
            new(JwtRegisteredClaimNames.Email, user.Email),
            new(ClaimTypes.Name, user.Username),
            new(ClaimTypes.Role, user.Role.ToString())
        };

        var tokenDescriptor = new SecurityTokenDescriptor
        {
            Subject = new ClaimsIdentity(claims),
            Expires = DateTime.UtcNow.AddHours(8),
            Issuer = issuer,
            Audience = audience,
            SigningCredentials = credentials
        };

        var tokenHandler = new JwtSecurityTokenHandler();
        var token = tokenHandler.CreateToken(tokenDescriptor);

        return tokenHandler.WriteToken(token);
    }
}
```

---

## ⚙️ Paso 3: Configuración del Middleware de Autenticación en `Program.cs`

Agregue en `src/backend/Presentation.API/Program.cs`:

```csharp
using System.Text;
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.IdentityModel.Tokens;
using FluentValidation;

var key = Encoding.UTF8.GetBytes(builder.Configuration["JwtSettings:Key"] ?? "UNET_DESARROLLO_DE_APLICACIONES_WEB_SECRET_KEY_2026_JWT_SUPER_SECURE!");

builder.Services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
})
.AddJwtBearer(options =>
{
    options.RequireHttpsMetadata = false;
    options.SaveToken = true;
    options.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuerSigningKey = true,
        IssuerSigningKey = new SymmetricSecurityKey(key),
        ValidateIssuer = true,
        ValidIssuer = builder.Configuration["JwtSettings:Issuer"] ?? "UNET_Inventory_API",
        ValidateAudience = true,
        ValidAudience = builder.Configuration["JwtSettings:Audience"] ?? "UNET_Inventory_Clients",
        ValidateLifetime = true,
        ClockSkew = TimeSpan.Zero
    };
});

builder.Services.AddAuthorization();

// Registrar validadores de FluentValidation del ensamblado Core.Application
builder.Services.AddValidatorsFromAssemblyContaining<Core.Application.Validations.CreateProductValidator>();
```

No olvide añadir en el pipeline:
```csharp
app.UseAuthentication();
app.UseAuthorization();
```

---

## 🔒 Paso 4: Protección de Endpoints con RBAC (`ProductsController.cs`)

```csharp
namespace Presentation.API.Controllers;

using Core.Application.DTOs;
using Core.Application.Interfaces;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
[Authorize] // Requiere token JWT para cualquier acción
public class ProductsController : ControllerBase
{
    private readonly IProductService _productService;

    public ProductsController(IProductService productService)
    {
        _productService = productService;
    }

    [HttpGet] // Accesible para Admin y Employee
    public async Task<IActionResult> GetAll()
    {
        return Ok(await _productService.GetAllProductsAsync());
    }

    [HttpPost] // Creación de productos
    public async Task<IActionResult> Create([FromBody] CreateProductDto dto)
    {
        var result = await _productService.CreateProductAsync(dto);
        return CreatedAtAction(nameof(GetAll), new { id = result.Id }, result);
    }

    [HttpDelete("{id:guid}")]
    [Authorize(Roles = "Admin")] // RESTRINGIDO EXCLUSIVAMENTE A ADMINISTRADORES
    public async Task<IActionResult> Delete(Guid id)
    {
        await _productService.DeleteProductAsync(id);
        return NoContent();
    }
}
```

---

## 🧪 Paso 5: Pruebas con Postman / Swagger
1. Realice petición `POST /api/auth/login` con credenciales de `Admin` y copie el token.
2. Invoque `DELETE /api/products/{id}` pasando el token en el encabezado `Authorization: Bearer <token>` -> Debe responder `204 No Content`.
3. Inicie sesión con un usuario con rol `Employee` e intente invocar `DELETE /api/products/{id}` -> Debe responder `403 Forbidden`.
