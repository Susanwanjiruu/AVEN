# AVEN — School Journey Visibility Platform

AVEN is a school-journey visibility and monitoring platform concept designed to help parents and caregivers stay informed about children's journeys to and from school. It focuses on school-going children who travel on foot and brings family management, journey tracking, route monitoring, safety alerts, and caregiver communication into one connected system.

The backend manages family relationships, tracking devices, journey information, monitoring events, and notifications. The project places particular emphasis on the security and privacy of children's information and location data.

## The problem

When children walk to and from school, caregivers may have limited visibility into whether a journey has started, is progressing as expected, or has been completed. AVEN is intended to provide relevant journey information and alert caregivers when configured safety conditions require attention.

## Core capabilities

### Family and child management
- Register a parent or caregiver and child through an administrative workflow.
- Associate a child with up to two authorized parents or caregivers.
- Maintain family records, contact details, verification status, and notification preferences.

### Journey tracking
- Receive GPS coordinates and telemetry from tracking devices.
- Record journey start times, progress, completion, and history.
- Associate tracking devices with registered children.
- Support expected routes, destinations, and journey time windows.

### Route monitoring and safety events
- Compare journey activity against configured routes and time windows.
- Detect configured route deviations and other monitoring conditions.
- Generate event records and alerts for caregiver or administrator review.
- Use deterministic monitoring rules for safety-related decisions rather than relying on AI alone.

### Caregiver communication
- Send journey updates through supported WhatsApp and SMS channels.
- Share map links with authorized caregivers.
- Track notification delivery and handle failures.
- Apply controlled channel fallback while avoiding duplicate notifications.

### Administration and security
- Authenticate administrators using JWT Bearer tokens.
- Protect administrative operations with authentication and authorization.
- Hash passwords and keep credentials outside source control.
- Restrict access to sensitive family and location information.
- Support contact verification, notification preferences, and time-limited location sharing.

## Technology stack

| Technology | Purpose |
|---|---|
| Python | Backend language |
| FastAPI | REST API |
| SQLAlchemy | Database ORM |
| PostgreSQL | Relational database |
| Neon | Hosted PostgreSQL option |
| Pydantic | Request validation and response schemas |
| PyJWT | JWT handling |
| pwdlib / Argon2 | Password hashing |
| Uvicorn | ASGI server |

## Backend architecture

The backend uses a layered structure to separate responsibilities:

- **Routers** define HTTP endpoints and handle requests.
- **Services** implement application workflows and business rules.
- **Repositories** encapsulate database queries and persistence.
- **Models** define database entities and relationships.
- **Schemas** validate incoming data and shape API responses.
- **Core** contains configuration and security utilities.

This separation makes the application easier to test, maintain, and extend.

## Project structure

```text
Aven_project/
├── app/
│   ├── core/
│   ├── models/
│   ├── repositories/
│   ├── routers/
│   ├── schemas/
│   └── services/
├── database.py
├── main.py
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting started

### Prerequisites

- Python 3.12 or a compatible version
- uv
- PostgreSQL database
- Git

### Clone and install

```bash
git clone https://github.com/Susanwanjiruu/Aven_project.git
cd Aven_project
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

On Windows PowerShell, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

### Configure environment variables

Create a local `.env` file and provide the configuration required by `app/core/config.py`. The following illustrates the kinds of values used; check the application settings for the exact variable names and required fields.

```dotenv
DATABASE_URL=your_database_url
JWT_SECRET_KEY=your_random_secret
```

Use valid credentials and a securely generated signing key. Never commit real credentials, passwords, tokens, or the `.env` file.

### Run the API

```bash
uv run uvicorn main:app --reload
```

When running locally, the API is typically available at `http://127.0.0.1:8000`, with interactive documentation at `http://127.0.0.1:8000/docs`.

## API workflow

The backend includes workflows for administrator authentication, family registration, child records, journey tracking, monitoring events, and notifications. Consult the running OpenAPI documentation for the current routes and request schemas; the API surface may change as development continues.

## Privacy and safety considerations

Children's location and journey records are sensitive. Any deployment handling real users should include strict access controls, secure transport, appropriate consent and retention policies, monitoring, backups, and thorough security testing. Safety alerts should be explainable and tested against realistic edge cases. This repository should not be treated as a certified child-safety service.

## Development principles

1. Keep business rules in services rather than route handlers.
2. Keep database access in repositories.
3. Validate request data with schemas.
4. Test authorization and failure paths as well as successful requests.
5. Keep secrets and real personal data out of Git.
6. Document new configuration and API behaviour as the project evolves.

## Project status

AVEN is a developing project. The feature descriptions explain the platform's intended workflows and documented backend capabilities; they do not imply that every integration is deployed or production-ready.

## License

No license is currently specified. Until a license is added, reuse and redistribution should not be assumed to be permitted.
