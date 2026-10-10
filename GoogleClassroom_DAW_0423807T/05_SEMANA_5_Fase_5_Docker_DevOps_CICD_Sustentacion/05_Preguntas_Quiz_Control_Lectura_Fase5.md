# Banco de Preguntas y Control de Lectura — Fase 5 (10 Preguntas)
## Asignatura: Desarrollo de Aplicaciones Web (Código: 0423807T)
**Universidad Nacional Experimental del Táchira (UNET)**  
**Tema:** Contenerización Multi-stage, Docker Compose, CI/CD con GitHub Actions y DevOps  
**Categoría en Classroom:** Unidad III: Sustentación y DevOps  
**Ponderación en Asignatura:** 2.0% de la Calificación Total | Puntuación en Google Forms: 20 Puntos (10 Preguntas × 2 pts c/u)

---

## 📝 Banco Oficial de Preguntas de Opción Múltiple

### Pregunta 1
**¿Cuál es la ventaja principal del patrón Multi-Stage Build en un archivo `Dockerfile` para aplicaciones web en producción?**
- A) Permite ejecutar la aplicación sin instalar Docker en el servidor.
- B) Separa la etapa pesada de compilación (que requiere el SDK de .NET o Node.js) de la etapa final de ejecución (runtime ligero como Alpine o Nginx), reduciendo drásticamente el tamaño de la imagen a menos de 120 MB y disminuyendo la superficie de ataque. *(Correcta)*
- C) Permite que PostgreSQL se instale dentro del mismo archivo ejecutable de la API.
- D) Acelera la velocidad de descarga de la conexión a internet.

*Justificación Técnica:* Los multi-stage builds permiten descartar compiladores, herramientas de depuración y código fuente intermedio, dejando únicamente los binarios optimizados en una imagen base mínima.

---

### Pregunta 2
**En `docker-compose.yml`, ¿por qué se utiliza la directiva `depends_on` con la condición `service_healthy` para el servicio de la API?**
- A) Para obligar a la API a reiniciar cada 5 minutos.
- B) Para garantizar que el contenedor de la API no intente arrancar ni conectarse a PostgreSQL hasta que el motor de base de datos haya superado exitosamente su prueba de salud (`pg_isready`) y esté completamente listo para aceptar conexiones. *(Correcta)*
- C) Para asignar mayor memoria RAM al contenedor de Nginx.
- D) Para cifrar el código fuente de los controladores de C#.

*Justificación Técnica:* En Docker, un contenedor puede estar en estado "running" pero su servicio interno aún inicializándose. El healthcheck previene caídas por fallo de conexión en el arranque inicial.

---

### Pregunta 3
**En un pipeline de CI/CD configurado con GitHub Actions para este proyecto integrador, ¿cuál es la función primordial del paso `dotnet test`?**
- A) Publicar automáticamente la aplicación en la tienda de Google Play.
- B) Ejecutar de forma automatizada la suite de pruebas unitarias con xUnit y Moq para asegurar que ningún cambio reciente rompa la lógica del negocio antes de proceder a la construcción del software. *(Correcta)*
- C) Generar contraseñas aleatorias para los usuarios administradores.
- D) Formatear los archivos CSS con Tailwind.

*Justificación Técnica:* El principio de Integración Continua (CI) se basa en la validación automatizada mediante pruebas de regresión en cada commit o pull request.

---

### Pregunta 4
**¿Qué función cumple el archivo de configuración `nginx.conf` dentro del contenedor del cliente frontend SPA?**
- A) Compilar el código de C# 14 en tiempo de ejecución.
- B) Servir los archivos estáticos generados por Vite (HTML, JS, CSS) y redirigir todas las rutas de navegación al archivo `index.html` (soporte de fallback para enrutamiento SPA). *(Correcta)*
- C) Crear las tablas relacionales en la base de datos PostgreSQL.
- D) Hashear las contraseñas con el algoritmo SHA-256.

*Justificación Técnica:* Al tratarse de una SPA con enrutamiento del lado del cliente, cualquier recarga de ruta debe devolver el `index.html` para que el enrutador de React gestione la vista.

---

### Pregunta 5
**Durante la sustentación técnica del proyecto integrador, ¿cuál es el propósito de realizar una prueba de arranque en frío con `docker-compose down -v` y `docker-compose up --build`?**
- A) Demostrar que el sistema es completamente reproducible, portátil y que la estrategia de inicialización autocurable con Data Seeding funciona sin requerir configuraciones manuales previas. *(Correcta)*
- B) Borrar permanentemente el repositorio de GitHub.
- C) Comprobar la duración de la batería de la computadora.
- D) Instalar un antivirus en el sistema operativo del servidor.

*Justificación Técnica:* El valor supremo de la contenerización es la reproducibilidad absoluta del entorno en cualquier máquina sin intervención manual.

---

### Pregunta 6
**¿Por qué en el `docker-compose.yml` se define un volumen con nombre (`postgres_data:/var/lib/postgresql/data`) para el servicio de base de datos?**
- A) Para que la base de datos sea más rápida al buscar productos.
- B) Para garantizar la persistencia de los datos en el disco del host, evitando que la información se pierda cuando el contenedor se detiene o se destruye. *(Correcta)*
- C) Para permitir la conexión por Wi-Fi a PostgreSQL.
- D) Para enviar correos electrónicos automáticos.

*Justificación Técnica:* Los contenedores son efímeros por naturaleza; los volúmenes desacoplan el almacenamiento de datos del ciclo de vida del contenedor.

---

### Pregunta 7
**En GitHub Actions, ¿qué evento del disparador `on:` asegura que el pipeline se ejecute tanto al integrar cambios directos como al revisar solicitudes de extracción de código?**
- A) `on: [push, pull_request]` *(Correcta)*
- B) `on: click`
- C) `trigger: manual_only`
- D) `schedule: weekly`

*Justificación Técnica:* El bloque `on: [push, pull_request]` es la convención estándar en CI/CD para validar ramas principales y pull requests antes del merge.

---

### Pregunta 8
**¿Qué parámetro en la instrucción `docker-compose up -d` indica que los contenedores deben levantarse en segundo plano (*detached mode*)?**
- A) `--verbose`
- B) `-d` *(Correcta)*
- C) `--stop`
- D) `-p 8080`

*Justificación Técnica:* La bandera `-d` desacopla la terminal del proceso de los contenedores, permitiendo seguir utilizando la línea de comandos.

---

### Pregunta 9
**¿Cuál es la diferencia fundamental entre una imagen base estándar como `mcr.microsoft.com/dotnet/aspnet:10.0` y su variante Alpine `mcr.microsoft.com/dotnet/aspnet:10.0-alpine`?**
- A) Alpine es más pesada y contiene herramientas de diseño gráfico.
- B) Alpine utiliza una distribución Linux ultracompacta y orientada a la seguridad basada en `musl libc` y `BusyBox`, reduciendo el peso de la imagen base a menos de 50 MB. *(Correcta)*
- C) Alpine no soporta conexiones de red.
- D) Solo funciona en computadoras con procesadores de 32 bits.

*Justificación Técnica:* Alpine Linux es el estándar corporativo para imágenes de producción debido a su huella mínima y reducido vector de vulnerabilidades.

---

### Pregunta 10
**Durante la defensa técnica oral, si el tribunal evaluador solicita verificar que un usuario con rol `Employee` no pueda eliminar categorías, ¿qué evidencia técnica debe presentarse?**
- A) Una presentación en PowerPoint con diapositivas animadas.
- B) Una petición en vivo mediante Postman o el cliente SPA con token de `Employee` recibiendo código de estado `403 Forbidden` y el log del servidor denegando el acceso RBAC. *(Correcta)*
- C) Una llamada telefónica al facilitador de la materia.
- D) El borrado manual del archivo `docker-compose.yml`.

*Justificación Técnica:* La sustentación de ingeniería de software exige demostraciones empíricas y verificables en tiempo de ejecución.
