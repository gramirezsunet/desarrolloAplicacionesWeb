<p align="center">
  <img src="REAF-F4/Banner_Google_Classroom_GR.jpeg" alt="Banner Asignatura DAW" width="100%" />
</p>

---

<table>
  <tr>
    <td width="95" align="center" style="border:none;">
      <img src="REAF-F4/unet-logo.png" alt="Logo UNET" width="80" />
    </td>
    <td style="border:none;">
      <h1 style="border:none; margin:0; padding:0;">Sistema de Gestión de Inventario Empresarial (ERP)</h1>
      <h3 style="border:none; margin:0; padding:0; color:#0b3c7b;">Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)</h3>
    </td>
  </tr>
</table>

**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Email:** [gramirezs@unet.edu.ve](mailto:gramirezs@unet.edu.ve)  
**Período Académico:** Septiembre / Octubre, 2026  
**San Cristóbal, Estado Táchira, Venezuela**

> 🚀 **Plataforma Interactiva de Recomendaciones (Fase 4):** [Abrir REAF-F4 en Vivo](https://gramirezsunet.github.io/desarrolloAplicacionesWeb/REAF-F4/)

---

## 📌 Descripción General

El presente proyecto constituye una solución integral de software empresarial orientada a la gestión de inventario, existencias, catalogación y control financiero para el sector comercial de ferretería, herramientas y materiales de construcción.

La arquitectura del sistema implementa estándares de desarrollo empresarial, aplicando **Onion Architecture** en el backend para lograr un desacoplamiento estricto entre el dominio del negocio y la infraestructura tecnológica, combinado con una aplicación de página única (**SPA**) reactiva construida en **React 18**, **Vite** y **Tailwind CSS**.

---

## 🏛️ Arquitectura del Sistema

El ecosistema se distribuye en una arquitectura por capas concéntricas (Onion Architecture) y un cliente desacoplado:

```
┌────────────────────────────────────────────────────────┐
│                   Frontend (SPA)                       │
│             React 18 + Vite + Tailwind CSS             │
└──────────────────────────┬─────────────────────────────┘
                           │ HTTP / JSON (REST API)
┌──────────────────────────▼─────────────────────────────┐
│                 Presentation.API                       │
│    Controladores REST, Middlewares RFC 7807, JWT Auth   │
├────────────────────────────────────────────────────────┤
│                 Core.Application                       │
│       Casos de Uso, DTOs, Validaciones (Fluent)        │
├────────────────────────────────────────────────────────┤
│                   Core.Domain                          │
│     Entidades del Dominio, Enums, Reglas de Negocio    │
├────────────────────────────────────────────────────────┤
│                 Infrastructure                         │
│       EF Core 10, Npgsql (PostgreSQL), Repositorios    │
└────────────────────────────────────────────────────────┘
```

### Componentes Clave:
1. **Core.Domain:** Contiene las entidades puras (`Product`, `Category`, `User`, `BaseEntity`) y enumeraciones (`UserRole`), sin dependencias de frameworks externos.
2. **Core.Application:** Implementa los contratos de servicios, DTOs de entrada/salida y validaciones declarativas con **FluentValidation**.
3. **Infrastructure:** Administra la persistencia con **Entity Framework Core 10**, configuración relacional vía **Fluent API**, siembra de datos (*data seeding*) y el patrón **Repository**.
4. **Presentation.API:** Expone los endpoints RESTful protegidos por **JWT Bearer**, autorización basada en roles (**RBAC**), política de **CORS** y captura global de excepciones estandarizada (**RFC 7807**).
5. **Frontend (SPA):** Interfaz moderna y responsiva con gestión de estado global (**Context API**), cliente HTTP centralizado, soporte para tema oscuro/institucional UNET, alternancia dinámica del imagotipo institucional y **Dashboard de Indicadores KPI** para analítica en tiempo real.

---

## 🎨 Sistema de Diseño, Modo Oscuro e Identidad Visual

La interfaz de usuario implementa la identidad visual oficial de la Universidad Nacional Experimental del Táchira (UNET) mediante una paleta cromática basada en el Azul Institucional (`#003366`) y soporte completo de **Modo Oscuro (*Dark Mode*)**:

- **Alternancia Dinámica de Logotipo:**
  - **Modo Claro (*Light Mode*):** Se proyecta el logo corporativo policromático sobre fondo blanco (`unet-logo.png`).
  - **Modo Oscuro (*Dark Mode*):** Se proyecta automáticamente el imagotipo blanco con canal alfa transparente (`unet-logo-dark.png`), preservando las dimensiones exactas y garantizando contraste óptimo contra fondos oscuros (`bg-slate-900` / `bg-unet-950`).
- **Persistencia de Tema:** El estado de preferencia de color se almacena en el almacenamiento local del navegador (`localStorage`) y se administra de forma reactiva mediante `ThemeContext`.

---

## ✨ Sistema de Animaciones y Micro-interacciones (Motion UI)

El frontend integra un catálogo de animaciones fluidas y elegantes configuradas en `tailwind.config.js`:

| Animación / Efecto | Utilidad CSS | Descripción Funcional |
| :--- | :--- | :--- |
| **Orbes Ambientales Flotantes** | `animate-float-slow`, `animate-float-reverse`, `animate-float-delayed` | Esferas difuminadas en tonos cian, azul UNET e índigo que se desplazan armónicamente en el fondo del Login. |
| **Entrada Suave de Tarjetas** | `animate-fade-in-up` | Aparición vertical con interpolación de opacidad y escala para formularios y contenedores principales. |
| **Apertura Elástica de Modales** | `animate-pop-in` | Transición de escala (`0.95` a `1.0`) y difuminado de fondo (*backdrop blur*) al abrir ventanas modales. |
| **Destello en Botones de Acción** | `shimmer` | Barrido de luz diagonal animado que recorre los botones principales al interactuar con ellos. |
| **Resplandor y Pulsación de Alertas** | `pulse-glow`, `animate-pulse` | Señalización visual sutil en indicadores críticos y productos con quiebre de stock. |
| **Elevación Tridimensional en KPIs** | `hover:-translate-y-1.5 hover:shadow-xl` | Respuesta táctil al cursor con elevación y expansión de sombra en tarjetas estadísticas. |
| **Transición Cruzada entre Vistas** | `animate-fade-in` | Desvanecimiento fluido al conmutar entre las pestañas de *Dashboard* y *Catálogo*. |

---

## 📸 Galería Visual y Capturas de Pantalla de la Aplicación

A continuación se presentan las capturas de pantalla de alta fidelidad que ilustran el comportamiento visual, la identidad institucional UNET, el soporte de Modo Oscuro y los módulos clave del sistema:

### 1. Autenticación Institucional y Pantalla de Acceso (Login)
*Proyección de la tarjeta Glassmorphism con orbes ambientales animados, alternancia dinámica del logo institucional UNET y accesos rápidos de prueba.*

| Modo Claro (*Light Mode*) | Modo Oscuro (*Dark Mode*) |
| :---: | :---: |
| ![Login Modo Claro](docs/screenshots/01_login_light.png) | ![Login Modo Oscuro](docs/screenshots/02_login_dark.png) |

---

### 2. Dashboard de Analítica & Indicadores KPI
*Monitoreo en tiempo real de valorización monetaria de inventario ($), unidades físicas disponibles, rotación de existencias, salud de almacén y gráficos comparativos de stock óptimo vs. mínimo de seguridad.*

| Dashboard - Modo Claro | Dashboard - Modo Oscuro |
| :---: | :---: |
| ![Dashboard Modo Claro](docs/screenshots/03_dashboard_light.png) | ![Dashboard Modo Oscuro](docs/screenshots/04_dashboard_dark.png) |

---

### 3. Catálogo Operativo de Inventario & Gestión de Fichas
*Búsqueda predictiva multi-criterio (Nombre, SKU, Marca, Ubicación), filtrado por rubros, badges de estado de existencias (Óptimo, Crítico, Agotado) y acciones CRUD.*

| Catálogo - Modo Claro | Catálogo - Modo Oscuro |
| :---: | :---: |
| ![Catálogo Modo Claro](docs/screenshots/05_catalogo_productos_light.png) | ![Catálogo Modo Oscuro](docs/screenshots/07_catalogo_dark.png) |

---

### 4. Modal de Registro y Edición de Productos
*Formulario interactivo modal con animación `pop-in`, efecto backdrop blur y validaciones declarativas organizadas en tres secciones: Clasificación, Información Financiera y Ubicación física en Almacén.*

<div align="center">
  <img src="docs/screenshots/06_modal_nuevo_producto.png" alt="Modal de Registro de Producto" width="85%" />
</div>

---

## 🗄️ Modelo Entidad-Relación (Base de Datos PostgreSQL)

El esquema relacional mapeado a través de **Entity Framework Core 10 (Code-First + Fluent API)** se estructura de la siguiente manera:

```mermaid
erDiagram
    CATEGORIES ||--o{ PRODUCTS : "clasifica (1:N)"

    CATEGORIES {
        uuid Id PK "Identificador único (UUID)"
        varchar_50 Name "Nombre de categoría"
        varchar_250 Description "Descripción del rubro"
        timestamp CreatedAt "Fecha de registro"
    }

    PRODUCTS {
        uuid Id PK "Identificador único (UUID)"
        uuid CategoryId FK "Clave foránea a Categories"
        varchar_150 Name "Nombre comercial"
        varchar_20 SKU UK "Código de barra único (SKU)"
        varchar_500 Description "Especificaciones técnicas"
        numeric_18_2 Price "Precio de venta (PVP)"
        numeric_18_2 CostPrice "Costo unitario de compra"
        int Stock "Existencia física actual"
        int MinStock "Stock mínimo de seguridad"
        int MaxStock "Capacidad máxima de bodega"
        varchar_100 Location "Ubicación física en almacén"
        varchar_30 UnitOfMeasure "Unidad de medida"
        varchar_80 Brand "Marca comercial / Fabricante"
        boolean IsActive "Estado activo/inactivo"
        timestamp CreatedAt "Fecha de registro"
    }

    USERS {
        uuid Id PK "Identificador único (UUID)"
        varchar_50 Username UK "Nombre de usuario único"
        varchar_100 Email UK "Correo institucional único"
        varchar_250 PasswordHash "Hash SHA-256 de contraseña"
        varchar_20 Role "Rol RBAC (Admin / Employee)"
        timestamp CreatedAt "Fecha de registro"
    }
```

---

## 🚀 Tecnologías Empleadas

- **Backend:** .NET 10 (C# 14), ASP.NET Core Web API.
- **ORM & Base de Datos:** Entity Framework Core 10, Npgsql, PostgreSQL 15+.
- **Seguridad:** JSON Web Tokens (JWT) con algoritmo HMAC-SHA256, Hashing SHA-256 de contraseñas.
- **Frontend:** React, Vite, Tailwind CSS, Lucide React Icons.
- **Contenerización & DevOps:** Docker, Docker Compose (Multi-stage builds), Nginx Alpine.

---

## 🛠️ Requisitos Previos

Para ejecutar la aplicación en un entorno de desarrollo local se requiere:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (recomendado para despliegue unificado)
- [SDK de .NET 10](https://dotnet.microsoft.com/download) (para ejecución local del backend)
- [Node.js 20 LTS](https://nodejs.org/) (para ejecución local del frontend)
- [PostgreSQL 15+](https://www.postgresql.org/) (en caso de no utilizar Docker)

---

## 📦 Puesta en Marcha con Docker Compose

La forma más rápida de inicializar todo el stack (Base de Datos + API + Frontend) es mediante Docker Compose:

```bash
# 1. Clonar el repositorio
git clone <URL_DEL_REPOSITORIO>
cd desarrolloAplicacionesWeb

# 2. Compilar e inicializar los tres contenedores en segundo plano
docker compose up --build -d

# 3. Verificar el estado de los contenedores
docker compose ps
```

### Puntos de Acceso del Sistema:
- **Frontend SPA:** [http://localhost:8080](http://localhost:8080) (vía Nginx) o [http://localhost:5173](http://localhost:5173) (vía Vite Dev)
- **Backend API REST:** [http://localhost:5000/api](http://localhost:5000/api)
- **Base de Datos PostgreSQL:** `localhost:5432` (`inventory_db`)

---

## 👤 Credenciales Preconfiguradas (Datos de Siembra)

El sistema incluye una siembra inicial de usuarios para pruebas de autorización RBAC:

| Rol | Usuario | Contraseña | Permisos |
| :--- | :--- | :--- | :--- |
| **Administrador** | `admin` | `admin123` | Acceso total: CRUD productos, categorías, analítica KPI y control de catálogo. |
| **Empleado** | `empleado` | `empleado123` | Consulta y actualización de inventario, sin permisos de eliminación ni gestión de categorías. |

---

## 🧪 Pruebas Unitarias Automatizadas (Testing Suite)

El proyecto cuenta con una batería integral de pruebas unitarias automatizadas que garantiza la confiabilidad, estabilidad y correcto cumplimiento de las reglas de negocio en la capa de aplicación (`Core.Application`), sin depender de infraestructura externa o bases de datos físicas.

### 🧰 Ecosistema y Herramientas de Testing:
- **xUnit.net v2.8:** Framework estándar para la definición, estructuración y ejecución paralela de casos de prueba (`[Fact]` y `[Theory]`).
- **Moq v4.20:** Librería para la creación de dobles de prueba (*mocks*) sobre las interfaces de repositorios (`IRepository<T>`, `IProductRepository`, `ITokenService`), permitiendo aislar completamente la lógica de negocio.
- **FluentAssertions v6.12:** Biblioteca de aserciones expresivas y legibles que facilita la verificación de estados, colecciones y excepciones esperadas.
- **FluentValidation v11.9:** Motor de validación declarativa testeado rigurosamente ante datos límite y entradas anómalas.

---

### 📋 Módulos y Cobertura de Pruebas:

| Componente Bajo Prueba (SUT) | Archivo de Prueba | Casos Cubiertos | Reglas de Negocio Validadas |
| :--- | :--- | :---: | :--- |
| **`ProductService`** | `ProductServiceTests.cs` | 8 | • Mapeo bidireccional DTO / Entidad.<br>• Unicidad obligatoria del código SKU.<br>• Validación de existencia de categoría asociada.<br>• Persistencia y aislamiento de dependencias. |
| **`CategoryService`** | `CategoryServiceTests.cs` | 4 | • Conteo dinámico de productos por categoría.<br>• Normalización y saneamiento de cadenas (*Trim*).<br>• Bloqueo de eliminación cuando existen productos asociados (Integridad referencial). |
| **`UserService`** | `UserServiceTests.cs` | 3 | • Autenticación exitosa con credenciales válidas y generación de JWT.<br>• Rechazo de contraseña inválida mediante hash criptográfico SHA-256.<br>• Manejo de usuario inexistente retornando `null`. |
| **`CreateProductValidator`** | `CreateProductValidatorTests.cs` | 14 | • Longitud de nombre (3 a 150 caracteres).<br>• Formato alfanumérico estricto del SKU (`^[A-Z0-9\-]{3,20}$`).<br>• Precio de venta estrictamente mayor a 0.<br>• Coherencia de inventario (`MaxStock > MinStock`). |
| **`CreateCategoryValidator`** | `CreateCategoryValidatorTests.cs` | 4 | • Obligatoriedad y límites de caracteres en el nombre (2 a 80).<br>• Límite máximo de descripción (250 caracteres). |

**Total de Pruebas Automatizadas:** 31 pruebas unitarias ejecutadas con 100% de tasa de éxito.

---

### 🔬 Metodología y Proceso de Preparación de la Suite de Pruebas:

La suite de pruebas fue concebida y desarrollada siguiendo una metodología rigurosa de ingeniería de software orientada a la verificación de la capa de aplicación:

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                   Metodología de Preparación de Pruebas Unitarias                      │
├───────────────────┬───────────────────┬───────────────────┬────────────────────────────┤
│ 1. Arquitectura   │ 2. Aislamiento    │ 3. Patrón AAA     │ 4. Verificación            │
│    y Proyecto     │    (Moq + DIP)    │    (Casos & Límites)    (Docker SDK & CI)      │
├───────────────────┼───────────────────┼───────────────────┼────────────────────────────┤
│ • xUnit.net 2.8   │ • IRepository<T>  │ • Arrange (Setup) │ • dotnet test              │
│ • FluentAssertion │ • IProductRepo    │ • Act (Ejecución) │ • Contenedor .NET 10       │
│ • Proyecto .csproj│ • ITokenService   │ • Assert (Verif.) │ • 31/31 Pruebas Exitosas   │
└───────────────────┴───────────────────┴───────────────────┴────────────────────────────┘
```

#### 1. Estructuración y Enlace de Proyectos:
- Se creó el proyecto independiente `tests/Core.Application.Tests/Core.Application.Tests.csproj` basado en .NET 10.
- Se configuraron referencias directas a `Core.Application` y `Core.Domain`, evitando deliberadamente cualquier dependencia con `Infrastructure` o `Presentation.API` para garantizar que las pruebas sean exclusivamente unitarias.
- Se incorporó el proyecto de pruebas al archivo de solución principal (`InventorySystem.sln`).

#### 2. Aislamiento de Capas e Inversión de Dependencias (DIP):
- Para comprobar la lógica de negocio sin conexión a una base de datos PostgreSQL real, se empleó **Moq** para interceptar todas las llamadas a las interfaces de persistencia y seguridad:
  - `Mock<IRepository<Category>>`: Simula la consulta y persistencia de rubros.
  - `Mock<IProductRepository>`: Simula consultas enriquecidas con categorías y validaciones de existencia de SKU (`ExistsSKUAsync`).
  - `Mock<ITokenService>`: Simula la generación de credenciales criptográficas JWT.

#### 3. Implementación del Patrón AAA (*Arrange, Act, Assert*):
Cada prueba unitaria fue construida bajo tres fases claramente delimitadas:
- **Arrange (Disposición):** Se inicializan las entidades de prueba en memoria y se programa el comportamiento esperado de los dobles de prueba utilizando `.Setup(...).ReturnsAsync(...)`.
- **Act (Ejecución):** Se invoca el método del servicio (`System Under Test` o `SUT`) con los parámetros preparados.
- **Assert (Verificación):** Se validan los resultados empleando **FluentAssertions** (`result.Should().NotBeNull()`, `result.Should().HaveCount(2)`) y se verifica con Moq que los repositorios fueron llamados exactamente el número de veces requerido (`_productRepoMock.Verify(r => r.SaveChangesAsync(), Times.Once)`).

#### 4. Validación Declarativa de Fronteras y Límites (*Boundary Testing*):
- En las pruebas de validadores (`CreateProductValidatorTests` y `CreateCategoryValidatorTests`), se emplearon atributos `[Theory]` y `[InlineData]` para someter el sistema a casos de prueba parametrizados con valores anómalos:
  - Cadenas vacías, espacios en blanco y longitudes inferiores o superiores a los umbrales reglamentarios.
  - Formatos inválidos de SKU (minúsculas, caracteres especiales, espacios intermedios).
  - Precios negativos o iguales a cero y contradicciones lógicas de stock (`MaxStock <= MinStock`).

#### 5. Ejecución Determinista en Entorno Contenerizado:
- La validación final se ejecuta de forma reproducible dentro de una imagen de contenedor oficial de .NET SDK (`mcr.microsoft.com/dotnet/sdk:10.0`), asegurando que la suite pueda ejecutarse en cualquier entorno de desarrollo o integración continua (CI/CD) sin necesidad de herramientas locales preinstaladas.

---

### ⚙️ Procedimiento de Ejecución de Pruebas:

#### Opción A: Ejecución mediante Docker (No requiere .NET instalado en la máquina anfitriona)
```bash
docker run --rm -v "${PWD}:/app" -w /app mcr.microsoft.com/dotnet/sdk:10.0 dotnet test tests/Core.Application.Tests/Core.Application.Tests.csproj --verbosity normal
```

#### Opción B: Ejecución local con .NET SDK
```bash
# Desde la raíz del repositorio
dotnet test tests/Core.Application.Tests/Core.Application.Tests.csproj
```

---

## 📂 Estructura del Repositorio

```
desarrolloAplicacionesWeb/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # Pipeline de Integración Continua (GitHub Actions)
├── docs/
│   └── screenshots/           # Capturas de pantalla de la interfaz (Light/Dark Mode)
├── src/
│   ├── backend/
│   │   ├── InventorySystem.sln # Solución principal de .NET
│   │   ├── Core.Domain/       # Entidades puras y enums del negocio
│   │   ├── Core.Application/  # DTOs, interfaces de servicio y validadores
│   │   ├── Infrastructure/    # DbContext, Fluent API y repositorios EF Core
│   │   └── Presentation.API/  # Controladores REST, Middlewares y Dockerfile
│   └── frontend/
│       ├── public/            # Recursos estáticos e isotipos institucionales
│       ├── src/               # Componentes React, contextos y cliente HTTP
│       ├── Dockerfile         # Construcción multi-stage con Nginx
│       └── nginx.conf         # Configuración del servidor web de producción
├── tests/
│   └── Core.Application.Tests/ # Suite de pruebas unitarias xUnit + Moq
│       ├── Services/          # Pruebas de lógica de negocio y servicios
│       └── Validations/       # Pruebas de reglas declarativas FluentValidation
├── docker-compose.yml         # Orquestación multicontenedor local
├── DEPLOYMENT.md              # Guía de despliegue en la nube (Fly.io / Render)
├── .gitignore                 # Exclusiones de Git para .NET, Node y Docker
└── README.md                  # Documentación principal del proyecto
```

---

## ☁️ Despliegue en Producción

Para consultar los procedimientos de compilación de imágenes de contenedor, publicación en Docker Hub y despliegue en servicios en la nube (como Fly.io o Render), revise el documento [DEPLOYMENT.md](DEPLOYMENT.md).
