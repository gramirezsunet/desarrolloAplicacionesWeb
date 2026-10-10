# Guía de Laboratorio y Live Coding — Fase 4
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## 🎯 Objetivo de la Práctica
Construir la interfaz de usuario reactiva en **React 18** con **Tailwind CSS**, implementar el selector de Modo Oscuro con soporte de imagotipos UNET, crear el **Dashboard KPI** de inventario y programar la suite de pruebas unitarias automatizadas con **xUnit** y **Moq** en C#.

---

## 📦 Paso 1: Creación del Proyecto de Pruebas Unitarias en .NET

```bash
# Crear proyecto de pruebas unitarias xUnit
dotnet new xunit -o tests/UnitTests -f net10.0

# Añadir a la solución y vincular referencias
dotnet sln add tests/UnitTests/UnitTests.csproj
dotnet add tests/UnitTests/UnitTests.csproj reference src/backend/Core.Application/Core.Application.csproj
dotnet add tests/UnitTests/UnitTests.csproj reference src/backend/Core.Domain/Core.Domain.csproj

# Instalar paquete Moq
dotnet add tests/UnitTests/UnitTests.csproj package Moq --version 4.20.72
```

---

## 🧪 Paso 2: Creación de la Suite de Pruebas Unitarias (`ProductServiceTests.cs`)

Cree `tests/UnitTests/Services/ProductServiceTests.cs`:

```csharp
namespace UnitTests.Services;

using System;
using System.Threading.Tasks;
using Core.Application.DTOs;
using Core.Application.Interfaces;
using Core.Application.Services;
using Core.Domain.Entities;
using Moq;
using Xunit;

public class ProductServiceTests
{
    private readonly Mock<IProductRepository> _mockRepo;
    private readonly ProductService _service;

    public ProductServiceTests()
    {
        _mockRepo = new Mock<IProductRepository>();
        _service = new ProductService(_mockRepo.Object);
    }

    [Fact]
    public async Task GetProductByIdAsync_WhenProductExists_ReturnsProductDto()
    {
        // Arrange
        var productId = Guid.NewGuid();
        var existingProduct = new Product
        {
            Id = productId,
            Name = "Taladro Percutor 1/2",
            SKU = "FERR-TAL-002",
            Price = 65.00m,
            CostPrice = 40.00m,
            Stock = 12
        };

        _mockRepo.Setup(r => r.GetByIdAsync(productId)).ReturnsAsync(existingProduct);

        // Act
        var result = await _service.GetProductByIdAsync(productId);

        // Assert
        Assert.NotNull(result);
        Assert.Equal(productId, result.Id);
        Assert.Equal("Taladro Percutor 1/2", result.Name);
        _mockRepo.Verify(r => r.GetByIdAsync(productId), Times.Once);
    }

    [Fact]
    public async Task GetProductByIdAsync_WhenNotFound_ThrowsKeyNotFoundException()
    {
        // Arrange
        var nonExistentId = Guid.NewGuid();
        _mockRepo.Setup(r => r.GetByIdAsync(nonExistentId)).ReturnsAsync((Product?)null);

        // Act & Assert
        await Assert.ThrowsAsync<KeyNotFoundException>(() => _service.GetProductByIdAsync(nonExistentId));
        _mockRepo.Verify(r => r.GetByIdAsync(nonExistentId), Times.Once);
    }
}
```

Ejecute las pruebas desde la terminal:
```bash
dotnet test
```

---

## ⚛️ Paso 3: Inicialización del Frontend con Vite y Tailwind CSS

```bash
# Crear proyecto React con Vite
npm create vite@latest src/frontend -- --template react
cd src/frontend
npm install
npm install -D tailwindcss postcss autoprefixer lucide-react axios
npx tailwindcss init -p
```

Configure `tailwind.config.js` para los colores institucionales UNET:
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        unet: {
          50: '#f0f7ff',
          100: '#e0effe',
          500: '#0284c7',
          800: '#075985',
          900: '#003366', // Azul Institucional UNET
          950: '#031c36',
        }
      }
    },
  },
  plugins: [],
}
```

---

## 📊 Paso 4: Implementación del Componente `DashboardKPI.jsx`

Cree `src/frontend/src/components/DashboardKPI.jsx`:

```jsx
import React from 'react';
import { DollarSign, Package, AlertTriangle, TrendingUp } from 'lucide-react';

export const DashboardKPI = ({ products }) => {
  const totalItems = products.reduce((acc, p) => acc + p.stock, 0);
  const totalValue = products.reduce((acc, p) => acc + (p.stock * p.price), 0);
  const totalCost = products.reduce((acc, p) => acc + (p.stock * p.costPrice), 0);
  const criticalStockCount = products.filter(p => p.stock <= p.minStock).length;
  const estimatedProfit = totalValue - totalCost;

  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
      {/* KPI 1: Valorización Total */}
      <div className="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg">
        <div className="flex items-center justify-between">
          <div>
            <p className="text-sm font-medium text-slate-500 dark:text-slate-400">Valorización Inventario</p>
            <h3 className="text-2xl font-bold text-slate-800 dark:text-white mt-1">${totalValue.toFixed(2)}</h3>
          </div>
          <div className="p-3 bg-blue-50 dark:bg-blue-900/30 text-unet-900 dark:text-blue-400 rounded-xl">
            <DollarSign className="w-6 h-6" />
          </div>
        </div>
      </div>

      {/* KPI 2: Unidades Físicas */}
      <div className="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg">
        <div className="flex items-center justify-between">
          <div>
            <p className="text-sm font-medium text-slate-500 dark:text-slate-400">Existencia Total</p>
            <h3 className="text-2xl font-bold text-slate-800 dark:text-white mt-1">{totalItems} Unidades</h3>
          </div>
          <div className="p-3 bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 rounded-xl">
            <Package className="w-6 h-6" />
          </div>
        </div>
      </div>

      {/* KPI 3: Alertas de Stock Crítico */}
      <div className="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg">
        <div className="flex items-center justify-between">
          <div>
            <p className="text-sm font-medium text-slate-500 dark:text-slate-400">Bajo Stock Mínimo</p>
            <h3 className="text-2xl font-bold text-amber-600 dark:text-amber-400 mt-1">{criticalStockCount} Ítems</h3>
          </div>
          <div className="p-3 bg-amber-50 dark:bg-amber-900/30 text-amber-600 dark:text-amber-400 rounded-xl">
            <AlertTriangle className="w-6 h-6" />
          </div>
        </div>
      </div>

      {/* KPI 4: Utilidad Estimada */}
      <div className="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg">
        <div className="flex items-center justify-between">
          <div>
            <p className="text-sm font-medium text-slate-500 dark:text-slate-400">Margen Proyectado</p>
            <h3 className="text-2xl font-bold text-purple-600 dark:text-purple-400 mt-1">${estimatedProfit.toFixed(2)}</h3>
          </div>
          <div className="p-3 bg-purple-50 dark:bg-purple-900/30 text-purple-600 dark:text-purple-400 rounded-xl">
            <TrendingUp className="w-6 h-6" />
          </div>
        </div>
      </div>
    </div>
  );
};
```
