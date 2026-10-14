# Sistema de Gestión de Biblioteca (Biblioteca Core)

Sistema completo de administración de biblioteca con **backend en Java 17 orientado a objetos** y **frontend web SPA moderno**. Gestiona inventario de libros físicos y digitales, socios, préstamos, multas, auditoría y búsqueda avanzada, todo a través de una **API REST** documentada con Swagger.

![Java](https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk&logoColor=white)
![Javalin](https://img.shields.io/badge/Javalin-6.1.3-blue)
![SQLite](https://img.shields.io/badge/SQLite-3-003B57?logo=sqlite&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8-646CFF?logo=vite&logoColor=white)
![Alpine.js](https://img.shields.io/badge/Alpine.js-ES6+-8BC0D0?logo=alpinedotjs&logoColor=white)

---

##  Características principales

-  **Gestión de catálogo** — libros físicos y digitales (con URL de descarga segura), autores, ISBN y stock
-  **Gestión de socios** — registro, seguimiento e invariantes de negocio
-  **Préstamos transaccionales** — cálculo automático de estados (Activo, Vencido, Devuelto) y tarifas/multas dinámicas
-  **Motor de búsqueda multicriterio** — normalización fonética y de caracteres acentuados
-  **Códigos de barra (Code 128) y QR** — identificación óptica con validación matemática de ISBN
-  **Paginación dinámica** en todos los listados
-  **Hardening de seguridad (OWASP)** — sanitización XSS, CORS restringido, prepared statements contra inyección SQL
-  **Auditoría inmutable** — logs de trazabilidad de cada operación
-  **Swagger UI / OpenAPI 3.0** integrado en tiempo de ejecución

---

##  Arquitectura

```
┌─────────────────────────────────────────┐
│   Frontend SPA (navegador)              │
│   HTML5 · Alpine.js · Tailwind · Vite   │
└─────────────────┬───────────────────────┘
                  │ HTTP / JSON (REST :3001)
┌─────────────────▼───────────────────────┐
│   Servidor Javalin 6 (Jetty embebido)   │
│   CORS · Jackson JSON · Swagger UI      │
└─────────────────┬───────────────────────┘
┌─────────────────▼───────────────────────┐
│   Lógica de negocio (patrón OO)         │
│   LibroService · UsuarioService ·       │
│   PrestamoService · BusquedaService ·   │
│   BarcodeService · AuditoriaService     │
└─────────────────┬───────────────────────┘
┌─────────────────▼───────────────────────┐
│   SQLite 3 (WAL + Foreign Keys)         │
└─────────────────────────────────────────┘
```

El núcleo está organizado con **programación orientada a objetos**: herencia (`LibroFisico` / `LibroDigital` ← `Libro`), interfaces genéricas (`Obligaciones<T>`), modelo de dominio en `com.biblioteca.models` y servicios desacoplados en `com.biblioteca.services`.

---

##  Puesta en marcha (Windows)

Scripts incluidos en la raíz del proyecto:

```bat
INSTALAR_DEPENDENCIAS.bat   :: instala Maven, Node y dependencias del frontend
COMPILAR.bat                :: compila el fat JAR (sistema-biblioteca/app/biblioteca.jar)
INICIAR_SISTEMA.bat         :: levanta backend (:3001) y frontend (:5173)
DETENER_SISTEMA.bat         :: detiene ambos servicios
```

Requisitos: **Java 17+**, Maven y Node.js.

Una vez iniciado:

- 🖥️ **Aplicación web:** http://localhost:5173
- 📘 **Swagger UI (documentación interactiva):** http://localhost:3001/swagger
- 🗄️ **Base de datos:** `sistema-biblioteca/database/biblioteca.db` (SQLite, se crea automáticamente)

---

##  Stack tecnológico

| Capa          |                          Tecnología                          |
|        --     |                      ---                                     |
| Backend       | Java 17 LTS, Javalin 6.1.3 (Jetty 11)                        |
| Base de datos | SQLite 3 (sqlite-jdbc, modo WAL, FK activas)                 |
| Frontend      | SPA: HTML5, Vanilla JS ES6+, Alpine.js, Tailwind CSS, Vite 8 |
| API           | REST + JSON, OpenAPI 3.0 + Swagger UI                        |
| Empaquetado   | Fat JAR autocontenido (Maven Shade Plugin)                   |

---

##  Estructura del repositorio

```
sistema de bibloteca java/
├── sistema-biblioteca/
│   ├── java-core/        # Código fuente Java (Maven)
│   ├── frontend/         # SPA (Vite + Alpine.js + Tailwind)
│   ├── app/              # biblioteca.jar compilado
│   ├── database/         # biblioteca.db (SQLite)
│   └── runtime/          # Binarios de ejecución
├── maven/                # Distribución local de Maven
├── documentacion/        # Diagramas UML y manual técnico
└── *.bat                 # Scripts de automatización

