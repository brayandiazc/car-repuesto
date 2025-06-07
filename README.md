# 📌 CarRepuesto

Sistema para la gestión digital de mantenimientos preventivos y correctivos del sector automotriz, permitiendo la recepción, seguimiento y cierre de tickets de mantenimiento de vehículos.
Proyecto basado en [Python](https://www.python.org/), [Django](https://www.djangoproject.com/) y [PostgreSQL](https://www.postgresql.org/). Incluye autenticación, manejo de datos y funcionalidades CRUD.

## 🗺️ Diagrama de Flujo

```mermaid
flowchart TD
    A[Usuario accede al sistema] --> B{¿Autenticado?}
    B -- Sí --> C[Mostrar dashboard principal]
    B -- No --> Z[Mostrar pantalla de login]
    Z --> AA[Validar usuario y contraseña]
    AA -- Credenciales válidas --> C
    AA -- Credenciales inválidas --> Z

    C --> D[Crear nuevo ticket de mantenimiento]
    C --> E[Visualizar lista de tickets]
    C --> F[Filtrar tickets por estado, tipo o vehículo]

    D --> G[Ingresar datos del vehículo]
    D --> H[Seleccionar tipo de mantenimiento]
    D --> I[Describir problema o solicitud]
    D --> J[Seleccionar prioridad]
    D --> K[Registrar ticket]
    K --> E

    E --> L[Seleccionar ticket para actualizar estado]
    L --> M{¿Actualizar estado?}
    M -- Sí --> N[Registrar nuevo estado y comentarios]
    N --> O[Actualizar historial del ticket]
    O --> E

    M -- No --> E

    F --> E

    E --> P{¿Cerrar ticket?}
    P -- Sí --> Q[Actualizar estado a Cerrado]
    Q --> O
    P -- No --> E

    O --> R[Consultar historial de cambios y comentarios]

    style Z fill:#fff3cd,stroke:#856404
    style AA fill:#fff3cd,stroke:#856404
```

## 🌿 Diagrama de Ramas (Git Flow)

```mermaid
gitGraph
   commit id: "Main"
   branch staging
   checkout staging
   commit id: "Staging 1"
   branch develop
   checkout develop
   commit id: "Develop 1"
   branch feature/login
   checkout feature/login
   commit id: "Feature: Login"
   checkout develop
   merge feature/login id: "Merge: Login"
   branch feature/tickets
   checkout feature/tickets
   commit id: "Feature: Tickets"
   checkout develop
   merge feature/tickets id: "Merge: Tickets"
   checkout staging
   merge develop id: "Merge: Develop -> Staging"
   commit id: "Staging 2"
   checkout main
   merge staging id: "Merge: Staging -> Main"
   commit id: "Release"
```

## 🏛️ Modelo Entidad-Relación

```mermaid
erDiagram
    USER {
      int id PK
      string username
      string email
      string password_hash
      string role
      boolean is_active
      datetime created_at
      datetime updated_at
    }
    VEHICLE {
      int id PK
      string plate
      string brand
      string model
      int year
      string owner_name
      string owner_contact
      datetime created_at
      datetime updated_at
    }
    TICKET {
      int id PK
      int vehicle_id FK
      int user_id FK
      string type
      string description
      string priority
      string status
      datetime created_at
      datetime updated_at
      datetime closed_at
    }
    TICKETHISTORY {
      int id PK
      int ticket_id FK
      int user_id FK
      string old_status
      string new_status
      string comment
      datetime changed_at
    }
    COMMENT {
      int id PK
      int ticket_id FK
      int user_id FK
      string content
      datetime created_at
    }

    USER ||--o{ TICKET : "registra"
    VEHICLE ||--o{ TICKET : "tiene"
    TICKET ||--o{ TICKETHISTORY : "historial"
    TICKET ||--o{ COMMENT : "comentarios"
    USER ||--o{ TICKETHISTORY : "modifica"
    USER ||--o{ COMMENT : "escribe"
```

## 🖼️ Vista Previa

| Inicio                | Funcionalidad               |
| --------------------- | --------------------------- |
| ![main](img/main.png) | ![feature](img/feature.gif) |

## ⚙️ Requisitos

* Python 3.10+
* Django 4.2
* PostgreSQL 13+

## 🚀 Instalación

```bash
git clone https://github.com/usuario/carrepuesto.git
cd carrepuesto
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python manage.py migrate
python manage.py runserver
```

## 🧪 Tests

```bash
pytest        # Pruebas funcionales
flake8 .      # Estilo de código
black --check .  # Formato
```

## 🔐 Acceso de Ejemplo

**Admin:**
📧 [admin@mail.com](mailto:admin@mail.com) — 🔑 Abc123#

**Invitado:**
📧 [user@mail.com](mailto:user@mail.com) — 🔑 Abc123#

## 🛣️ Roadmap

* [ ] Login con redes sociales
* [ ] API pública
* [ ] Dashboard mejorado

## 🖇️ Contribuye

```bash
# Fork → Crea rama → Cambios → Commit → Pull Request
```

Lee [CONTRIBUTING.md](.github/CONTRIBUTING.md) para más detalles.

## 📄 Licencia

MIT — ver [LICENSE](LICENSE.md)

⌨️ con ❤️ por [Brayan Diaz C](https://github.com/brayandiazc)
