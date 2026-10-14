# Library Management System

A complete library management system featuring a **Java 17 object-oriented backend** and a modern **web-based Single-Page Application (SPA) frontend**. It manages physical and digital book inventories, members, loans, fines, auditing, and advanced search through a **REST API** documented with Swagger.

![Java](https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk&logoColor=white)
![Javalin](https://img.shields.io/badge/Javalin-6.1.3-blue)
![SQLite](https://img.shields.io/badge/SQLite-3-003B57?logo=sqlite&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8-646CFF?logo=vite&logoColor=white)
![Alpine.js](https://img.shields.io/badge/Alpine.js-ES6+-8BC0D0?logo=alpinedotjs&logoColor=white)

---

## Key Features

- **Catalog management** — physical and digital books with secure download URLs, authors, ISBNs, and stock tracking.
- **Member management** — registration, tracking, and business rule enforcement.
- **Transactional loan management** — automatic status calculation (Active, Overdue, Returned) and dynamic fee and fine calculations.
- **Multi-criteria search engine** — phonetic normalization and accent-insensitive character matching.
- **Barcodes (Code 128) and QR codes** — optical identification with mathematical ISBN validation.
- **Dynamic pagination** across all listings.
- **OWASP security hardening** — XSS sanitization, restricted CORS, and prepared statements to prevent SQL injection.
- **Immutable audit trail** — traceability logs for every operation.
- **Integrated Swagger UI / OpenAPI 3.0** — interactive API documentation available at runtime.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/26e8a029-4ff0-4863-a762-1575d1c0f24a" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e541eeb9-24c8-4a30-9a0b-b688529c0199" />

---

## Architecture

```text
┌─────────────────────────────────────────┐
│   Frontend SPA (Browser)                │
│   HTML5 · Alpine.js · Tailwind · Vite   │
└─────────────────┬───────────────────────┘
                  │ HTTP / JSON (REST :3001)
┌─────────────────▼───────────────────────┐
│   Javalin 6 Server (Embedded Jetty)     │
│   CORS · Jackson JSON · Swagger UI      │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│   Business Logic (OOP Design)           │
│   LibroService · UsuarioService ·       │
│   PrestamoService · BusquedaService ·   │
│   BarcodeService · AuditoriaService     │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│   SQLite 3 (WAL + Foreign Keys)         │
└─────────────────────────────────────────┘
```

The core is built around **object-oriented programming**, featuring inheritance (`LibroFisico` / `LibroDigital` ← `Libro`), generic interfaces (`Obligaciones<T>`), a domain model in `com.biblioteca.models`, and decoupled services in `com.biblioteca.services`.

---

## Getting Started (Windows)

The following scripts are included in the project root:

```bat
INSTALAR_DEPENDENCIAS.bat   :: Installs Maven, Node.js, and frontend dependencies
COMPILAR.bat                :: Builds the fat JAR (sistema-biblioteca/app/biblioteca.jar)
INICIAR_SISTEMA.bat         :: Starts the backend (:3001) and frontend (:5173)
DETENER_SISTEMA.bat         :: Stops both services
```

**Requirements:** Java 17+, Maven, and Node.js.

Once the system is running:

- 🖥️ **Web application:** http://localhost:5173
- 📘 **Swagger UI (interactive API documentation):** http://localhost:3001/swagger
- 🗄️ **Database:** `sistema-biblioteca/database/biblioteca.db` (SQLite, created automatically)

---

## Technology Stack

| Layer | Technology |
|---|---|
| Backend | Java 17 LTS, Javalin 6.1.3 (Jetty 11) |
| Database | SQLite 3 (sqlite-jdbc, WAL mode, foreign keys enabled) |
| Frontend | SPA: HTML5, Vanilla JavaScript ES6+, Alpine.js, Tailwind CSS, Vite 8 |
| API | REST + JSON, OpenAPI 3.0 + Swagger UI |
| Packaging | Self-contained fat JAR (Maven Shade Plugin) |

---

## Repository Structure

```text
java-library-management-system/
├── sistema-biblioteca/
│   ├── java-core/        # Java source code (Maven)
│   ├── frontend/         # SPA (Vite + Alpine.js + Tailwind)
│   ├── app/              # Compiled biblioteca.jar
│   ├── database/         # biblioteca.db (SQLite)
│   └── runtime/          # Runtime binaries
├── maven/                # Local Maven distribution
├── documentacion/        # UML diagrams and technical documentation
└── *.bat                 # Automation scripts
```
