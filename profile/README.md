![SaySo Campus Pixel Art](./sayso.png)

<h1 align="center">SaySo | Campus Complaint Management System</h1>

<p align="center">
  <strong>Your voice. Your campus. Your SaySo.</strong>
</p>

<p align="center">
  A centralized platform for reporting, managing, tracking, and resolving campus complaints.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-22-green?logo=node.js" alt="Node.js" />
  <img src="https://img.shields.io/badge/TypeScript-Enabled-blue?logo=typescript" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Express.js-Backend-black?logo=express" alt="Express" />
  <img src="https://img.shields.io/badge/MySQL-Database-blue?logo=mysql" alt="MySQL" />
  <img src="https://img.shields.io/badge/Redis-Caching-red?logo=redis" alt="Redis" />
  <img src="https://img.shields.io/badge/Docker-Containerized-blue?logo=docker" alt="Docker" />
</p>

---

## 1. Overview

**SaySo** is a campus complaint management system designed to improve communication between students, university staff, and administrators.

Traditional campus complaint processes can be difficult to track, lack transparency, and make it challenging for students to know whether their concerns are being addressed.

SaySo provides a centralized digital platform where students can report campus-related problems, staff members can manage and resolve assigned complaints, and administrators can oversee the entire complaint resolution process.

The platform consists of three role-based client applications:

- **Student Portal:** Submit complaints and track their progress.
- **Staff Portal:** Manage assigned complaints and provide resolutions.
- **Admin Portal:** Manage users, departments, complaint categories, assignments, and platform operations.

All three applications communicate with a centralized backend API.

## 2. Project Objectives

- Provide a centralized campus complaint reporting system.
- Improve communication between students and university departments.
- Make complaint resolution more transparent.
- Enable staff members to manage assigned complaints efficiently.
- Allow administrators to monitor complaint activity.
- Maintain complaint history and status tracking.
- Provide secure, role-based access to platform resources.

## 3. System Architecture

SaySo follows a centralized backend architecture.

```text
                    SAYSO ECOSYSTEM
                           |
             +-------------+-------------+
             |             |             |
        Student Portal  Staff Portal  Admin Portal
             |             |             |
             +-------------+-------------+
                           |
                      REST API
                           |
                   Node.js + Express
                           |
             +-------------+-------------+
             |             |             |
           MySQL         Redis        Middleware
             |             |             |
             +-------------+-------------+
                           |
                      Drizzle ORM
```

## 4. User Roles and Responsibilities

### 4.1 Student Portal

- Register and authenticate.
- Create new complaints.
- Select complaint categories and relevant departments.
- Provide complaint descriptions and supporting information.
- View submitted complaints.
- Track complaint status.
- View complaint history.
- Communicate through complaint comments.
- Receive updates about complaint progress.

### 4.2 Staff Portal

- Authenticate as staff.
- View complaints assigned to them.
- Access complaint details.
- Update complaint status.
- Add comments and progress updates.
- Manage assigned complaint workloads.
- Review complaint history.
- Mark complaints as resolved when appropriate.

### 4.3 Admin Portal

- Manage student and staff accounts.
- Manage departments.
- Manage complaint categories.
- Manage complaint records.
- Assign complaints to appropriate staff members.
- Monitor complaint status and resolution progress.
- Manage tags and complaint classification.
- View complaint statistics and operational summaries.
- Monitor platform activity.

Access to protected resources is controlled through authentication and role-based authorization.

## 5. Technology Stack

### Backend

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| TypeScript | Type-safe application development |
| Express.js | REST API framework |
| Drizzle ORM | Database queries and schema management |
| MySQL 8 | Relational database |
| Redis | Caching and temporary data storage |

### Infrastructure and Development

| Technology | Purpose |
|---|---|
| Docker | Containerization |
| Docker Compose | Local multi-container development |
| GitHub Actions | CI/CD automation |
| AWS EC2 | Backend deployment |
| GitHub | Source control and collaboration |

## 6. Backend Architecture

The backend follows a modular, layered architecture.

```text
Client Request
      |
      v
Express Router
      |
      v
Authentication Middleware
      |
      v
Authorization Middleware
      |
      v
Controller
      |
      v
Service Layer
      |
      v
Database Operations
      |
      v
MySQL / Redis
      |
      v
JSON Response
```

### Architectural responsibilities

**Routes**
- Define API endpoints.
- Connect endpoints to middleware and controllers.

**Middlewares**
- Authenticate requests.
- Authorize user roles.
- Validate incoming requests.
- Handle errors and other cross-cutting concerns.

**Controllers**
- Handle HTTP requests and responses.
- Extract request information.
- Delegate business logic to services.

**Services**
- Contain application business logic.
- Coordinate database operations.
- Implement complaint management workflows.

**Database Layer**
- Define database schemas.
- Execute database queries using Drizzle ORM.
- Maintain relationships between application entities.

**Utilities**
- Provide reusable helper functions.
- Handle common application operations.

## 7. Database Design

SaySo uses MySQL as its primary relational database.

| Table | Responsibility |
|---|---|
| `students` | Student account information |
| `staff` | Staff account information |
| `departments` | University department information |
| `complaints` | Complaint records |
| `complaint_comments` | Comments and discussions |
| `complaint_status_history` | Historical complaint status changes |
| `categories` | Complaint categories |
| `tags` | Complaint classification tags |
| `complaint_tags` | Relationship between complaints and tags |
| `staff_departments` | Staff and department relationships |

Drizzle ORM manages schema definitions, migrations, and database queries.

## 8. Complaint Lifecycle

```text
Student submits complaint
          |
          v
Complaint is created
          |
          v
Admin reviews complaint
          |
          v
Complaint assigned to staff
          |
          v
Staff investigates issue
          |
          v
Staff updates complaint
          |
          v
Complaint resolved
          |
          v
Student reviews resolution
```

The exact status transitions are governed by backend business rules.

## 9. Getting Started

### Prerequisites

- Node.js 22 or later
- npm
- Docker
- Docker Compose
- Git
- Basic TypeScript and Express.js knowledge
- Basic SQL knowledge (recommended)

### Clone the Repository

```bash
git clone https://github.com/SayySoo/sayso-server.git
cd sayso-server
```

### Install Dependencies

```bash
npm install
```

For a clean dependency installation:

```bash
npm ci
```

### Environment Configuration

Create a local environment file using the example configuration provided by the project.

```bash
cp .env.example .env
```

Configure the required database, Redis, authentication, and application settings.

Never commit actual credentials, private keys, production environment files, or other secrets.

If `.env.example` is not available, consult the maintainers for the required environment variable names.

### Start Development Environment

```bash
docker compose up -d
npm run dev
```

The current backend development setup uses port `8000`.

Health check:

```bash
curl http://localhost:8000/health
```

## 10. Database and Drizzle Commands

| Command | Purpose |
|---|---|
| `npm run db:generate` | Generate migration files |
| `npm run db:migrate` | Apply generated migrations |
| `npm run db:push` | Push schema changes to the database |
| `npm run db:studio` | Open Drizzle Studio |

Recommended workflow for schema changes:

1. Update the appropriate schema file.
2. Generate a migration.
3. Review the generated SQL migration.
4. Apply the migration locally.
5. Verify the resulting database structure.
6. Commit both the schema and migration files.

Avoid using schema push operations against production databases without explicit approval.

## 11. Testing and Build

```bash
npm test
npm run build
npm run dev
```

Before submitting a contribution, make sure tests pass and the production build completes successfully.

## 12. Docker Development

The current development environment includes:

| Service | Container | Port |
|---|---|---|
| Backend API | campusfix-api | 8000 |
| MySQL | campusfix-mysql | 3306 |
| Redis | campusfix-redis | 6379 |

Useful commands:

```bash
# Start services
docker compose up -d

# View running containers
docker compose ps

# View logs
docker compose logs -f

# Stop services
docker compose down

# Rebuild and restart
docker compose up -d --build
```

Do not remove persistent database volumes unless you intentionally want to delete local database data.

## 13. Contribution Guidelines

Contributions are welcome!

### Step 1: Fork or Clone

```bash
git clone https://github.com/SayySoo/sayso-server.git
cd sayso-server
```

### Step 2: Create a Branch

Avoid committing directly to `main`.

```bash
git checkout -b feature/your-feature-name
```

Suggested branch naming conventions:

| Type | Prefix | Example |
|---|---|---|
| New feature | `feature/` | `feature/complaint-assignment` |
| Bug fix | `fix/` | `fix/auth-validation` |
| Refactoring | `refactor/` | `refactor/complaint-service` |
| Documentation | `docs/` | `docs/api-documentation` |
| Tests | `test/` | `test/complaint-service` |

### Step 3: Make Your Changes

- Follow the existing project structure.
- Use TypeScript types wherever possible.
- Keep controllers focused on HTTP handling.
- Keep business logic inside service modules.
- Use Drizzle ORM for database operations.
- Validate incoming request data.
- Handle errors consistently.
- Respect existing authentication and authorization rules.
- Avoid unnecessary dependencies.
- Never expose sensitive information.

### Step 4: Test Your Changes

```bash
npm test
npm run build
```

If your changes involve database schemas, verify migrations locally as well.

### Step 5: Commit Your Changes

```bash
git add .
git commit -m "feat: add complaint assignment functionality"
```

Suggested commit prefixes:

- `feat:` New functionality.
- `fix:` Bug fixes.
- `refactor:` Code restructuring.
- `docs:` Documentation changes.
- `test:` Test-related changes.
- `chore:` Maintenance tasks.

### Step 6: Push Your Branch

```bash
git push origin feature/your-feature-name
```

### Step 7: Open a Pull Request

Create a Pull Request targeting the `main` branch.

Include:
- A clear description of the changes.
- The problem being addressed.
- Relevant implementation details.
- Screenshots or API examples where useful.
- Database migration details, if applicable.
- Testing information.

Wait for review and required CI checks before merging.

## 14. CI/CD Pipeline

SaySo uses GitHub Actions to automate testing, compilation, Docker image creation, and production deployment.

```text
Developer pushes code
          |
          v
GitHub Actions Triggered
          |
          v
Install Dependencies
          |
          v
Run Automated Tests
          |
          v
Compile TypeScript
          |
          v
Build Production Docker Image
          |
          v
Upload Docker Artifact
          |
          v
Organization Self-hosted Runner
          |
          v
Load Docker Image on AWS EC2
          |
          v
Recreate API Container
          |
          v
Health Check
          |
          v
Deployment Complete
```

**Deployment configuration:**

- Source repository: `SayySoo/sayso-server`
- Production branch: `main`
- Hosting platform: AWS EC2
- CI/CD platform: GitHub Actions
- Production runner: `campusfix-ec2-org`
- Container orchestration: Docker Compose

Pull requests run the test-and-build job. Production deployment is restricted to pushes to `main`.

Production credentials are maintained through GitHub repository secrets and server-side environment configuration. Never commit these credentials.

## 15. Security Guidelines

- Never commit passwords, API keys, tokens, or private SSH keys.
- Never expose production environment variables.
- Validate and sanitize incoming request data.
- Apply authentication to protected endpoints.
- Enforce role-based authorization on sensitive operations.
- Avoid exposing internal errors or stack traces in production.
- Use parameterized database operations through the ORM.
- Avoid logging passwords, tokens, or sensitive personal information.
- Ensure students cannot access other students' restricted records.
- Ensure staff members cannot perform unauthorized administrative actions.

Report security vulnerabilities privately to the repository maintainers instead of publishing exploitable details in public issues.

## 16. Project Structure

The backend follows a modular structure. The exact files and modules may evolve as the project grows.

```text
sayso-server/
│
├── src/
│   ├── config/
│   ├── controllers/
│   ├── services/
│   ├── routes/
│   ├── middlewares/
│   ├── db/
│   │   └── schema/
│   ├── utils/
│   └── ...
│
├── drizzle/
├── tests/
├── .github/
│   └── workflows/
│
├── Dockerfile
├── docker-compose.yml
├── drizzle.config.ts
├── package.json
├── tsconfig.json
└── README.md
```

This is an architectural overview, not a guarantee that every directory exists in every version.

## 17. Roadmap

Potential areas for future development include:

- Advanced complaint analytics.
- Notification system for complaint updates.
- Email notifications.
- Complaint escalation workflows.
- Detailed audit logging.
- Advanced staff workload management.
- Improved reporting and dashboards.
- API documentation and integration guides.
- Additional automated integration tests.

## 18. Important Notes for Contributors

- The `main` branch represents the production codebase.
- Do not push experimental code directly to `main`.
- Do not modify production infrastructure without approval.
- Database changes must be reviewed carefully.
- Do not commit generated secrets or local environment files.
- Keep Pull Requests focused and easy to review.
- Follow existing naming conventions and architecture.
- Discuss major architectural changes with maintainers before implementation.

## 19. License

Add the project's chosen open-source license before accepting external contributions. Until a license is added, contributors should not assume that the source code is freely reusable or redistributable.

## 20. Acknowledgements

SaySo aims to make campus problem reporting and resolution more transparent, organized, and accessible.

Thank you to everyone contributing to the development and improvement of SaySo.

---

<p align="center">
  <strong>SaySo</strong><br/>
  Your voice. Your campus. Your SaySo.
</p>
