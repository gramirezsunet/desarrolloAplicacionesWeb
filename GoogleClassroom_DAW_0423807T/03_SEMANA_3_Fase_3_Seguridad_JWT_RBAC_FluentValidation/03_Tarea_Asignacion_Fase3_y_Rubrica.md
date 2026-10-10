# Tarea y Asignación Práctica — Semana 3 (Fase 3)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Facilitador:** M.Sc. Ing. Gabriel Alexis Ramírez Sánchez  
**Categoría en Classroom:** Unidad I: Backend Corporativo  
**Puntuación en Google Classroom:** 80 Puntos Máximos | Ponderación en Asignatura: 12.0% (Cierre Unidad I: 40% acumulado)

---

## 📌 Enunciado del Proyecto

El estudiante o equipo debe implementar el subsistema de seguridad y validación defensiva en la API REST, garantizando la autenticación **Stateless con JWT**, la autorización **RBAC** y la protección de entrada con **FluentValidation**.

### Requerimientos Obligatorios:
1. **Endpoint de Autenticación (`POST /api/auth/login`):**
   - Recibir `LoginDto` (username/email y password).
   - Validar las credenciales contra la base de datos comparando el hash SHA-256.
   - Retornar `AuthResponseDto` con el token JWT firmado, username, email y rol.
2. **Control de Acceso Basado en Roles (RBAC):**
   - Proteger endpoints de eliminación (`DELETE`) y creación/modificación de categorías para que únicamente el rol `Admin` pueda ejecutarlos.
   - Permitir al rol `Employee` consultar catálogos y registrar productos, pero denegar la eliminación devolviendo código HTTP `403 Forbidden`.
3. **Validación Defensiva con FluentValidation:**
   - Crear validadores para todos los DTOs de creación y edición.
   - Validar que precios sean $> 0$, stocks $\ge 0$, stock máximo $>$ stock mínimo y campos de texto obligatorios dentro de sus límites.
   - Si la validación falla, retornar `400 Bad Request` con el listado detallado de errores.
4. **Resguardo Criptográfico:**
   - Cifrado de contraseñas de usuarios con algoritmo seguro (SHA-256 o superior).
   - Almacenamiento seguro de la clave secreta de JWT en `appsettings.json` / Variables de entorno.

---

## 📋 Formato de Entrega
- Enlace al repositorio en GitHub actualizado.
- Colección de **Postman** (o archivo JSON de pruebas exportado) con los siguientes 4 escenarios comprobados:
  1. Login exitoso con rol Admin y Employee.
  2. Petición a endpoint protegido sin token (`401 Unauthorized`).
  3. Intento de eliminación de producto con token de Employee (`403 Forbidden`).
  4. Envío de producto con precio negativo (`400 Bad Request` con mensaje de validación).

---

## 📊 Rúbrica de Evaluación Estandarizada (80 Puntos Máximos)

| Criterio | Excelente (100%) | Bueno (80%) | Regular (60%) | Insuficiente (<60%) | Puntos Máx. |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **1. Autenticación JWT & Claims** | Tokens emitidos con firma HMAC-SHA256 válida, claims de usuario y expiración correcta. (25 pts) | JWT funcional pero omite algún claim requerido o expiración. (20 pts) | Token sin firma criptográfica válida o claves en duro inseguras. (15 pts) | No emite JWT o falla el proceso de login. (0-10 pts) | **25 pts** |
| **2. Matriz de Permisos RBAC** | Controladores protegidos con `[Authorize(Roles="...")]`; responde 403 y 401 en los escenarios exactos. (25 pts) | RBAC funcional con algún endpoint secundario sin proteger. (20 pts) | Solo valida autenticación pero no distingue roles (todos tienen acceso Admin). (15 pts) | Endpoints abiertos sin autorización. (0-10 pts) | **25 pts** |
| **3. FluentValidation Defensivo** | Validadores desacoplados en `Core.Application`, reglas completas de negocio y respuestas 400 claras. (20 pts) | Validadores funcionales pero con reglas mínimas. (16 pts) | Validaciones manuales con `if` dispersos dentro de los controladores. (12 pts) | Sin validación de datos de entrada. (0-8 pts) | **20 pts** |
| **4. Evidencias de Pruebas Postman** | Colección exportada completa con los 4 escenarios de prueba exitosamente demostrados. (10 pts) | Colección con 2 o 3 escenarios. (8 pts) | Solo capturas de pantalla aisladas. (6 pts) | Sin evidencias de pruebas de API. (0-4 pts) | **10 pts** |
| **TOTAL** | — | — | — | — | **80 Pts** |
