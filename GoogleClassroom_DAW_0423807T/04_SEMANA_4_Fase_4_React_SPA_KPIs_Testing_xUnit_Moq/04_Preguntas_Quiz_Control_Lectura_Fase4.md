# Banco de Preguntas y Control de Lectura — Fase 4 (10 Preguntas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Tema:** Frontend React 18 SPA, Context API, Tailwind CSS, Dashboards KPI y Testing con xUnit & Moq  
**Categoría en Classroom:** Unidad II: Frontend y Analítica  
**Ponderación en Asignatura:** 5.0% de la Calificación Total | Puntuación en Google Forms: 20 Puntos (10 Preguntas × 2 pts c/u)

---

## 📝 Banco Oficial de Preguntas de Opción Múltiple

### Pregunta 1
**¿Cuál es la principal ventaja de utilizar la Context API de React (`AuthContext`, `ThemeContext`) frente a pasar propiedades manualmente por componentes (*Prop Drilling*)?**
- A) Incrementa la velocidad de compilación de Vite en un 50%.
- B) Permite que cualquier componente del árbol acceda al estado global (sesión, token JWT o tema claro/oscuro) sin necesidad de pasarlo manualmente de padre a hijo a través de componentes intermedios. *(Correcta)*
- C) Guarda los datos automáticamente en PostgreSQL sin necesidad de peticiones HTTP.
- D) Reemplaza por completo el backend en .NET 10.

*Justificación Técnica:* Context API resuelve el problema de Prop Drilling centralizando el estado compartido accesible mediante hooks personalizados (`useAuth()`, `useTheme()`).

---

### Pregunta 2
**En el desarrollo del Dashboard de Inventario, ¿cómo se calcula cuantitativamente la métrica de 'Valorización Total de Inventario'?**
- A) Contando el número de productos con stock mayor a cero.
- B) Sumando el producto del stock físico disponible por el precio unitario de venta de cada artículo: $\sum (\text{Stock}_i \times \text{Price}_i)$. *(Correcta)*
- C) Restando los productos agotados del total de categorías.
- D) Multiplicando el total de usuarios administradores por el número de ventas diarias.

*Justificación Técnica:* La valorización representa el capital monetario total inmovilizado en bodega según el catálogo activo.

---

### Pregunta 3
**¿Por qué en las pruebas unitarias de servicios (`ProductService`) se utiliza la librería Moq para simular la interfaz `IProductRepository` en lugar de conectarse a una base de datos real?**
- A) Porque PostgreSQL no permite conexiones desde pruebas de software.
- B) Para aislar totalmente la lógica de negocio del servicio, logrando pruebas deterministas, ultrarrápidas y sin dependencias externas ni efectos colaterales de red o disco. *(Correcta)*
- C) Porque Moq es obligatorio para compilar en C# 14.
- D) Para evitar escribir aserciones en xUnit.

*Justificación Técnica:* Las pruebas unitarias deben evaluar unidades de código en estricto aislamiento; Moq provee réplicas controladas que simulan el comportamiento de la infraestructura.

---

### Pregunta 4
**En xUnit, ¿cuál es el propósito de estructurar los métodos de prueba bajo el patrón AAA (Arrange - Act - Assert)?**
- A) Organizar el código en tres fases claras: 1) Preparar los datos y dependencias simuladas, 2) Ejecutar la acción o método a probar, y 3) Verificar que los resultados obtenidos coincidan con lo esperado. *(Correcta)*
- B) Obligar a que la prueba se ejecute tres veces consecutivas.
- C) Compilar el backend para tres plataformas: Windows, Linux y Mac.
- D) Asignar 3 puntos a la calificación del estudiante.

*Justificación Técnica:* El patrón AAA es el estándar universal de legibilidad y mantenibilidad para pruebas automatizadas de software.

---

### Pregunta 5
**En Tailwind CSS, ¿qué utilidad permite activar el Modo Oscuro cuando la clase `dark` está presente en el elemento raíz `<html>`?**
- A) `theme: dark`
- B) `darkMode: 'class'` en `tailwind.config.js` y clases con prefijo `dark:` (ej. `dark:bg-slate-900 dark:text-white`). *(Correcta)*
- C) `color-scheme: only-dark`
- D) `enable-night-mode: true`

*Justificación Técnica:* Tailwind CSS permite alternar estilos oscuros de forma declarativa mediante la directiva `darkMode: 'class'` sincronizada con el estado de React.

---

### Pregunta 6
**¿Cómo se verifica en Moq que un método de repositorio simulado haya sido llamado exactamente una vez durante una prueba unitaria?**
- A) `mockRepo.AssertOneCall();`
- B) `mockRepo.Verify(r => r.GetByIdAsync(id), Times.Once);` *(Correcta)*
- C) `mockRepo.Count == 1;`
- D) `Assert.Single(mockRepo);`

*Justificación Técnica:* El método `Verify` con el parámetro `Times.Once` comprueba las invocaciones a nivel de contrato simulado en Moq.

---

### Pregunta 7
**¿Cuál es la función técnica del hook `useEffect` en React al cargar el catálogo de productos desde la API REST?**
- A) Renderizar elementos CSS en el servidor.
- B) Ejecutar efectos secundarios asíncronos (como realizar la petición HTTP `GET /api/products` con Axios) después de que el componente se monta en el DOM. *(Correcta)*
- C) Crear una nueva base de datos relacional en el cliente.
- D) Reemplazar la biblioteca Tailwind CSS.

*Justificación Técnica:* `useEffect` gestiona el ciclo de vida de componentes funcionales para operaciones asíncronas y suscripciones.

---

### Pregunta 8
**¿Por qué es una buena práctica almacenar la preferencia de tema (claro/oscuro) en `localStorage` del navegador?**
- A) Para que la base de datos PostgreSQL sepa qué color prefiere el usuario.
- B) Para preservar la preferencia visual del usuario entre recargas de página y sesiones futuras sin necesidad de autenticación adicional. *(Correcta)*
- C) Para ahorrar memoria RAM en el servidor de la UNET.
- D) Para evitar instalar Node.js.

*Justificación Técnica:* `localStorage` provee persistencia del lado del cliente para preferencias de interfaz de usuario de forma síncrona.

---

### Pregunta 9
**¿Cuál es el propósito del operador `Assert.ThrowsAsync<KeyNotFoundException>(...)` en xUnit?**
- A) Detener la ejecución del computador en caso de error.
- B) Verificar asíncronamente que el método probado lance exactamente la excepción `KeyNotFoundException` ante una condición anómala (ej. buscar un ID de producto que no existe). *(Correcta)*
- C) Convertir la excepción en un código HTTP 200 OK.
- D) Crear un nuevo registro en la base de datos.

*Justificación Técnica:* Probar el manejo robusto de excepciones es un pilar del testing unitario para validar flujos negativos y defensivos.

---

### Pregunta 10
**¿Qué clase de utilidad de Tailwind CSS se recomienda utilizar en contenedores de gráficos o tablas de Dashboard para evitar desbordamientos visuales en pantallas pequeñas (*Responsive Design*)?**
- A) `overflow-x-auto` *(Correcta)*
- B) `hidden`
- C) `fixed-size-100`
- D) `display-table-force`

*Justificación Técnica:* `overflow-x-auto` permite desplazamiento horizontal fluido en vistas responsivas sin alterar el diseño estructural de la página.
