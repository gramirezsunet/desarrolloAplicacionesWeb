# Guía de Laboratorio y Live Coding — Fase 5
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Objetivo de la Práctica
Configurar los archivos **Dockerfile Multi-stage** para el backend y frontend, construir la orquestación con **Docker Compose** integrando *Healthchecks*, y configurar el pipeline de **CI/CD con GitHub Actions**.

---

## 🐳 Paso 1: Creación del Dockerfile Multi-stage para Backend (`Presentation.API/Dockerfile`)

Cree `src/backend/Presentation.API/Dockerfile`:

```dockerfile
# ETAPA 1: Compilación y Publicación
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /app

# Copiar archivos de proyecto y restaurar dependencias
COPY src/backend/Core.Domain/Core.Domain.csproj src/backend/Core.Domain/
COPY src/backend/Core.Application/Core.Application.csproj src/backend/Core.Application/
COPY src/backend/Infrastructure/Infrastructure.csproj src/backend/Infrastructure/
COPY src/backend/Presentation.API/Presentation.API.csproj src/backend/Presentation.API/
RUN dotnet restore src/backend/Presentation.API/Presentation.API.csproj

# Copiar todo el código fuente y publicar en modo Release
COPY src/backend/ src/backend/
WORKDIR /app/src/backend/Presentation.API
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false

# ETAPA 2: Runtime Ligero Final (< 120 MB)
FROM mcr.microsoft.com/dotnet/aspnet:10.0-alpine AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 5000
ENV ASPNETCORE_URLS=http://+:5000
ENTRYPOINT ["dotnet", "Presentation.API.dll"]
```

---

## ⚛️ Paso 2: Creación del Dockerfile Multi-stage para Frontend (`src/frontend/Dockerfile`)

Cree `src/frontend/Dockerfile`:

```dockerfile
# ETAPA 1: Compilación de la SPA con Node
FROM node:20-alpine AS build
WORKDIR /app
COPY src/frontend/package*.json ./
RUN npm install
COPY src/frontend/ .
RUN npm run build

# ETAPA 2: Servidor Web Nginx Ultraligero
FROM nginx:alpine AS final
COPY --from=build /app/dist /usr/share/nginx/html
COPY src/frontend/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

## 🐙 Paso 3: Orquestación Total con `docker-compose.yml`

Cree `docker-compose.yml` en la raíz del repositorio:

```yaml
version: '3.8'

services:
  # Base de Datos Relacional PostgreSQL
  db:
    image: postgres:15-alpine
    container_name: inventory_db_container
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgrespassword
      POSTGRES_DB: inventory_db
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres -d inventory_db"]
      interval: 5s
      timeout: 5s
      retries: 5

  # Backend RESTful API en ASP.NET Core 10
  api:
    build:
      context: .
      dockerfile: src/backend/Presentation.API/Dockerfile
    container_name: inventory_api_container
    restart: always
    ports:
      - "5000:5000"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://+:5000
      - ConnectionStrings__DefaultConnection=Host=db;Port=5432;Database=inventory_db;Username=postgres;Password=postgrespassword
      - JwtSettings__Key=UNET_DESARROLLO_DE_APLICACIONES_WEB_SECRET_KEY_2026_JWT_SUPER_SECURE!
      - JwtSettings__Issuer=UNET_Inventory_API
      - JwtSettings__Audience=UNET_Inventory_Clients
    depends_on:
      db:
        condition: service_healthy

  # Frontend React SPA servido por Nginx
  spa:
    build:
      context: .
      dockerfile: src/frontend/Dockerfile
    container_name: inventory_spa_container
    restart: always
    ports:
      - "8080:80"
    depends_on:
      - api

volumes:
  postgres_data:
```

---

## 🚀 Paso 4: Automatización CI/CD con GitHub Actions

Cree `.github/workflows/ci-cd.yml`:

```yaml
name: CI/CD Pipeline DAW 2026

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  backend-build-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup .NET 10
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '10.0.x'
      - name: Restore dependencies
        run: dotnet restore
      - name: Build solution
        run: dotnet build --no-restore -c Release
      - name: Run Unit Tests
        run: dotnet test --no-build --verbosity normal

  frontend-build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Install dependencies
        working-directory: ./src/frontend
        run: npm install
      - name: Build SPA
        working-directory: ./src/frontend
        run: npm run build
```

---

## 🧪 Paso 5: Despliegue y Comprobación Local

```bash
# 1. Compilar y levantar todo el ecosistema
docker compose up --build -d

# 2. Verificar estado y salud
docker ps

# 3. Acceder al sistema
# Frontend SPA: http://localhost:8080
# Swagger API: http://localhost:5000/swagger
```
