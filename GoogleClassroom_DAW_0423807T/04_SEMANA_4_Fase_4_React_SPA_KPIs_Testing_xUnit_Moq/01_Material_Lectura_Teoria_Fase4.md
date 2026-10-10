# Semana 4 — Fase 4: Frontend SPA React 18, Dashboards KPI & Pruebas Unitarias con xUnit y Moq
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez

---

## ⚛️ 1. Arquitectura del Cliente SPA (React 18 + Vite + Tailwind CSS)

El cliente web se implementa como una **Single Page Application (SPA)** reactiva y modular que consume los servicios de la API REST mediante contratos JSON.

```
┌────────────────────────────────────────────────────────┐
│                   App (Enrutador)                      │
├──────────────────────────┬─────────────────────────────┤
│      AuthContext         │        ThemeContext         │
│  (Token JWT, User, Rol)  │  (Light / Dark Mode UNET)   │
├──────────────────────────┴─────────────────────────────┤
│                     Vistas / Vistas                    │
│  ┌───────────────────────┐  ┌───────────────────────┐  │
│  │     DashboardKPI      │  │   ProductCatalogView  │  │
│  │ (Métricas Financieras)│  │ (Filtros, CRUD, Modal)│  │
│  └───────────────────────┘  └───────────────────────┘  │
└────────────────────────────────────────────────────────┘
```

### Componentes Clave:
1. **`AuthContext`:** Administra el ciclo de vida de la sesión (login, logout, almacenamiento persistente en `localStorage` y adjunción automática del token `Bearer` en clientes Axios).
2. **`ThemeContext` & Identidad Institucional UNET:** Permite alternar dinámicamente entre **Modo Claro** (Azul UNET `#003366`) y **Modo Oscuro** (`bg-slate-900`/`bg-unet-950`), conmutando automáticamente el imagotipo corporativo policromático (`unet-logo.png`) por el logo blanco transparente (`unet-logo-dark.png`).
3. **`DashboardKPI`:** Componente analítico en tiempo real que calcula y renderiza:
   - **Valorización Total del Inventario:** $\sum (\text{Stock} \times \text{Precio Venta})$ y $\sum (\text{Stock} \times \text{Costo})$.
   - **Margen de Ganancia Proyectado (%):** $\frac{\text{Ventas Estimadas} - \text{Costo Total}}{\text{Ventas Estimadas}} \times 100$.
   - **Alertas de Stock Crítico:** Productos con $\text{Stock} \le \text{MinStock}$ resaltados visualmente con badges ámbar y rojo.
   - **Capacidad de Almacén:** Porcentaje de ocupación respecto a `MaxStock`.

---

## 🧪 2. Calidad de Software con Pruebas Unitarias Automatizadas (xUnit & Moq)

En el backend corporativo, las pruebas unitarias permiten verificar de manera **determinista y aislada** que la lógica de negocio de los casos de uso (`ProductService`, `CategoryService`) cumpla con las especificaciones sin interactuar con la base de datos real.

### Componentes de la Suite de Pruebas:
- **`xUnit`:** Motor ejecutor de pruebas (*Test Runner*), aserciones (`Assert.Equal`, `Assert.ThrowsAsync`) y decoradores (`[Fact]`, `[Theory]`).
- **`Moq`:** Framework de simulación (*Mocking*) que genera réplicas controladas de interfaces de persistencia (`Mock<IProductRepository>`), permitiendo simular respuestas y verificar que los métodos del repositorio hayan sido invocados exactamente una vez (`Times.Once`).

### Ejemplo de Prueba Unitaria Aislada:
```csharp
[Fact]
public async Task GetProductByIdAsync_WhenNotFound_ThrowsKeyNotFoundException()
{
    // Arrange (Preparar el escenario simulado)
    var nonExistentId = Guid.NewGuid();
    var mockRepo = new Mock<IProductRepository>();
    mockRepo.Setup(r => r.GetByIdAsync(nonExistentId)).ReturnsAsync((Product?)null);

    var service = new ProductService(mockRepo.Object);

    // Act & Assert (Ejecutar y comprobar la excepción de negocio)
    await Assert.ThrowsAsync<KeyNotFoundException>(() => service.GetProductByIdAsync(nonExistentId));
    mockRepo.Verify(r => r.GetByIdAsync(nonExistentId), Times.Once);
}
```

---

## 🎨 3. Sistema de Animaciones y Micro-interacciones (Motion UI)

El frontend integra animaciones fluidas configuradas en Tailwind CSS para enriquecer la experiencia de usuario:
- **Orbes Flotantes en Login:** `animate-float-slow` que generan ambientación tecnológica de fondo.
- **Transición de Modales:** `animate-pop-in` con desenfoque de fondo (`backdrop-blur-sm`).
- **Elevación de KPIs:** `hover:-translate-y-1.5 hover:shadow-xl` que brinda retroalimentación táctil inmediata al usuario.
