# Semana 1 — Fase 1: Fundamentos Arquitectónicos, Ecosistema .NET 10 y Resiliencia REST
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 📖 1. Contexto Tecnológico: Evolución y Capacidades de .NET 10 (C# 14)

El ecosistema .NET ha experimentado una profunda transformación arquitectónica a lo largo de las últimas dos décadas:

1. **2002 - .NET Framework:** Entorno monolítico fuertemente acoplado a la API Win32 de Windows, caracterizado por un alto consumo de recursos y falta de portabilidad.
2. **2016 - .NET Core:** Rediseño modular completo desde cero, de código abierto (MIT) y multiplataforma nativa (Linux, macOS, Windows).
3. **2020 - .NET 5:** Unificación definitiva de todos los runtimes de Microsoft (.NET Core, Xamarin, Mono) bajo una sola base de código.
4. **2026 - .NET 10 & C# 14:** Plataforma madura orientada a microservicios *Cloud-Native*, caracterizada por compilación AOT (Ahead-Of-Time), tiempos de arranque en milisegundos, baja huella de memoria en contenedores Docker y tipado estático reforzado.

---

## 🏛️ 2. Arquitectura de Cebolla (Onion Architecture)

Propuesta por Jeffrey Palermo en 2008, la **Onion Architecture** sitúa el modelo del dominio en el centro neurálgico del sistema, organizando la solución en capas concéntricas regidas por la **Regla de Dependencia**:

> *"Las capas externas pueden depender de las capas internas, pero las capas internas jamás deben conocer los detalles de las externas."*

```
┌────────────────────────────────────────────────────────┐
│               Capa de Presentación (API)               │
│         Controladores REST, Middlewares, Filtros       │
├────────────────────────────────────────────────────────┤
│                 Capa de Infraestructura                │
│    EF Core 10, Repositorios, Conexiones a PostgreSQL   │
├────────────────────────────────────────────────────────┤
│                  Capa de Aplicación                    │
│       Casos de Uso, DTOs, Validadores, Interfaces      │
├────────────────────────────────────────────────────────┤
│                   Núcleo de Dominio                    │
│      Entidades Puras, Enumeraciones, Reglas Base       │
└────────────────────────────────────────────────────────┘
```

### Desglose de Responsabilidades:

1. **`Core.Domain` (Núcleo Agnóstico):** Contiene entidades puras (`Product`, `Category`, `User`, `BaseEntity`) y enums (`UserRole`). No tiene referencias a NuGet, Entity Framework ni ASP.NET Core.
2. **`Core.Application`:** Orquesta la lógica del negocio mediante interfaces (`IProductService`, `IProductRepository`), DTOs inmutables y validadores con FluentValidation.
3. **`Infrastructure`:** Implementa los accesos a datos, mapeo relacional con Fluent API, repositorios concretos y servicios externos.
4. **`Presentation.API`:** Expone los endpoints HTTP, configura la inyección de dependencias en `Program.cs`, aplica autenticación JWT y maneja errores globales.

---

## 💉 3. Inyección de Dependencias (DI) y Ciclos de Vida

El contenedor nativo de Inversión de Control (IoC) de .NET administra el ciclo de vida de los servicios registrados:

| Ciclo de Vida | Método de Registro | Comportamiento | Caso de Uso en DAW |
| :--- | :--- | :--- | :--- |
| **`Transient`** | `AddTransient<T, U>()` | Se crea una instancia nueva cada vez que se solicita. | Validadores ligeros de FluentValidation. |
| **`Scoped`** | `AddScoped<T, U>()` | Se crea una sola instancia por cada petición HTTP (Request) y se desecha al terminar la respuesta. | `DbContext`, `IProductService`, `IProductRepository`. |
| **`Singleton`** | `AddSingleton<T, U>()` | Se crea una única instancia durante toda la vida útil de la aplicación. | `TokenService`, cachés inmutables, loggers. |

> ⚠️ **Advertencia de Dependencia Cautiva (Captive Dependency):**  
> Nunca inyecte un servicio `Scoped` dentro de un servicio `Singleton`. Esto provocaría que el servicio scoped quede atrapado en memoria permanentemente, compartiendo estados entre distintos usuarios y generando fugas de memoria o condiciones de carrera.

---

## 🛡️ 4. Resiliencia y Manejo Centralizado de Excepciones (RFC 7807)

El estándar **RFC 7807 (Problem Details for HTTP APIs)** define un esquema JSON uniforme para transmitir errores en APIs web, evitando respuestas caóticas o dispersas.

### Estructura del Documento Problem Details:
```json
{
  "type": "https://httpstatuses.com/404",
  "title": "Recurso No Encontrado",
  "status": 404,
  "detail": "El producto con ID 'a8c1f9d4-...' no existe en el inventario.",
  "instance": "/api/products/a8c1f9d4-..."
}
```

### Principio de Ocultamiento de Trazas (Security by Design):
Bajo ninguna circunstancia se deben enviar Stack Traces al cliente en respuestas de error 500. El middleware global captura cualquier excepción inesperada, registra el error internamente en los logs del servidor y devuelve un mensaje genérico controlado al cliente.
