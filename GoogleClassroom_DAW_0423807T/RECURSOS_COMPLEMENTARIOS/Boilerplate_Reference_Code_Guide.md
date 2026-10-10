# Guía de Referencia del Código y Boilerplate
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Repositorio Oficial:** `https://github.com/toulouse817/desarrolloAplicacionesWeb.git`  
**Universidad Nacional Experimental del Táchira (UNET)**

---

## 🗺️ Mapa de Archivos y Responsabilidades del Repositorio

El repositorio oficial de la asignatura contiene la implementación de referencia completa y funcional del Sistema de Gestión de Inventario. A continuación se detalla la ubicación de cada módulo clave según las 5 fases del curso:

```
desarrolloAplicacionesWeb/
├── .github/
│   └── workflows/
│       └── ci-cd.yml                           <-- [FASE 5] Pipeline CI/CD GitHub Actions
├── docker-compose.yml                          <-- [FASE 5] Orquestación DB + API + SPA
├── DEPLOYMENT.md                               <-- [FASE 5] Guía de despliegue en producción
├── docs/
│   ├── DAW-0423807T.pdf                        <-- [TEMA 0] Documento curricular oficial
│   └── screenshots/                            <-- [TEMA 0/4] Galería visual del sistema
├── src/
│   ├── backend/
│   │   ├── Core.Domain/                        <-- [FASE 1] Núcleo Puro de Dominio
│   │   │   ├── Common/BaseEntity.cs            <-- Entidad base con UUID y UTC
│   │   │   ├── Entities/Product.cs             <-- Entidad de Producto con campos de ferretería
│   │   │   ├── Entities/Category.cs            <-- Entidad de Categoría
│   │   │   ├── Entities/User.cs                <-- Entidad de Usuario
│   │   │   └── Enums/UserRole.cs               <-- Enum de roles (Admin / Employee)
│   │   │
│   │   ├── Core.Application/                   <-- [FASE 1/3] Capa de Casos de Uso
│   │   │   ├── DTOs/                           <-- DTOs de entrada y salida
│   │   │   ├── Interfaces/                     <-- Interfaces de servicios y repositorios
│   │   │   ├── Services/                       <-- Lógica de negocio (ProductService, etc.)
│   │   │   └── Validations/                    <-- [FASE 3] Validadores FluentValidation
│   │   │
│   │   ├── Infrastructure/                     <-- [FASE 2] Persistencia y Datos
│   │   │   ├── Persistence/
│   │   │   │   ├── ApplicationDbContext.cs     <-- DbContext y Data Seeding inicial
│   │   │   │   └── Configurations/             <-- [FASE 2] Fluent API (ProductConfiguration.cs)
│   │   │   ├── Repositories/                   <-- Repositorios con .AsNoTracking()
│   │   │   └── Services/TokenService.cs        <-- [FASE 3] Emisión de JWT HMAC-SHA256
│   │   │
│   │   └── Presentation.API/                   <-- [FASE 1/3] Punto de Entrada Web
│   │       ├── Controllers/                    <-- Controladores REST con [Authorize]
│   │       ├── Middleware/                     <-- [FASE 1] ExceptionMiddleware RFC 7807
│   │       ├── Program.cs                      <-- Inyección de Dependencias y Pipeline HTTP
│   │       └── Dockerfile                      <-- [FASE 5] Multi-stage Dockerfile .NET 10
│   │
│   └── frontend/                               <-- [FASE 4] Cliente React SPA
│       ├── src/
│       │   ├── components/                     <-- DashboardKPI, Modales, Tablas
│       │   ├── contexts/                       <-- AuthContext, ThemeContext (Dark Mode)
│       │   ├── views/                          <-- LoginView, DashboardView, CatalogView
│       │   └── assets/                         <-- Imagotipos institucionales UNET
│       ├── tailwind.config.js                  <-- Paleta Azul UNET y Animaciones Motion UI
│       ├── nginx.conf                          <-- [FASE 5] Configuración servidor Nginx
│       └── Dockerfile                          <-- [FASE 5] Multi-stage Dockerfile React/Nginx
│
└── tests/
    └── UnitTests/                              <-- [FASE 4] Pruebas Unitarias
        └── Services/ProductServiceTests.cs     <-- Pruebas deterministas con xUnit y Moq
```

---

## ⚡ Comandos Rápidos de Ejecución Local

```bash
# 1. Compilar toda la solución .NET
dotnet build

# 2. Ejecutar la suite completa de pruebas unitarias
dotnet test

# 3. Levantar la aplicación completa con Docker Compose
docker-compose up --build -d

# 4. Detener y limpiar contenedores y volúmenes
docker-compose down -v
```
