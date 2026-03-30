# Full Stack FastAPI  ---

<a href="https://github.com/fastapi/full-stack-fastapi-template/actions?query=workflow%3ATest" target="_blank"><img src="https://github.com/fastapi/full-stack-fastapi-template/workflows/Test/badge.svg" alt="Test"></a>
<a href="https://coverage-badge.samuelcolvin.workers.dev/redirect/fastapi/full-stack-fastapi-template" target="_blank"><img src="https://coverage-badge.samuelcolvin.workers.dev/fastapi/full-stack-fastapi-template.svg" alt="Coverage"></a>

## Architektur

![Architekturdiagramm](img/architecture-overview.svg)

Die Plattform ist als containerisierte Full-Stack-Anwendung aufgebaut:
- **Frontend (React/Vite)** liefert die Web-UI und spricht die Backend-API.
- **Backend (FastAPI)** kapselt Business-Logik, Authentifizierung und Metriken.
- **PostgreSQL** stellt persistente Datenhaltung bereit.
- **Traefik/Kubernetes Ingress** übernimmt Routing/TLS-Termination.
- **Monitoring-Stack** (Prometheus + Grafana) sammelt und visualisiert Laufzeitmetriken.

## Tech-Stack

- **Backend:** FastAPI, SQLModel, Pydantic, PostgreSQL
- **Frontend:** React, TypeScript, Vite, Chakra UI
- **Platform/Infra:** Docker Compose (lokal), Kubernetes (dev/staging/prod), Traefik
- **Qualität & Security:** Pytest, Playwright, CodeQL, Trivy
- **Delivery:** GitHub Actions, GHCR

## Setup

1. Repository klonen.
2. Umgebungsvariablen in `.env`/Secrets setzen (u. a. `SECRET_KEY`, `POSTGRES_PASSWORD`).
3. Lokale Entwicklungsumgebung mit Docker Compose starten.
4. Optional: Monitoring-Stack zusätzlich starten.

Vertiefung:
- Deployment/Setup: [deployment.md](./deployment.md)
- Monitoring lokal: [monitoring/README.md](./monitoring/README.md)

## Dev/Prod-Deployment

- **Development:** Deploy nach `k8s/dev` (Namespace `dev`) über GitHub Actions.
- **Staging:** Deploy nach `k8s/staging` (Namespace `staging`) über dedizierten Workflow.
- **Production:** Deploy nach `k8s/prod` (Namespace `prod`) mit Approval-Gate.

Vertiefung: [deployment.md](./deployment.md)

## CI/CD

CI/CD basiert auf GitHub Actions mit den Kernschritten:
1. Build (Backend/Frontend)
2. Tests
3. Security-Scans
4. Push nach GHCR
5. Deployment nach Kubernetes (dev/staging/prod)

Vertiefung: [deployment.md](./deployment.md)

## Monitoring

- Prometheus sammelt Applikations- und Infrastrukturmetriken.
- Grafana stellt Dashboards für Betrieb und Fehleranalyse bereit.

Vertiefung: [monitoring/README.md](./monitoring/README.md)

## Security

- Security Scans via CodeQL und Trivy in CI.
- Baseline-Policies und Prozessbeschreibung in der Security-Policy.

Vertiefung: [SECURITY.md](./SECURITY.md)

## DR (Disaster Recovery)

DR-Runbooks inkl. Backup/Restore und RTO/RPO sind dokumentiert in:
- [DR.md](./DR.md)
- [deployment.md (DR-Abschnitt)](./deployment.md#disaster-recovery-dr--runbooks)

## Compliance-Checkliste (Requirement 1–10)

| Requirement | Nachweis/Artefakt |
|---|---|
| Requirement 1: Dokumentierte Zielarchitektur | [README Architektur](#architektur), [Architekturdiagramm](./img/architecture-overview.svg) |
| Requirement 2: Klare Technologieauswahl | [README Tech-Stack](#tech-stack) |
| Requirement 3: Reproduzierbares Setup | [README Setup](#setup), [deployment.md](./deployment.md) |
| Requirement 4: Trennung Dev/Prod Deployment | [README Dev/Prod-Deployment](#devprod-deployment), [`k8s/dev`](./k8s/dev), [`k8s/prod`](./k8s/prod) |
| Requirement 5: CI/CD definiert | [README CI/CD](#cicd), [Workflow-Dokumentation in deployment.md](./deployment.md) |
| Requirement 6: Monitoring nachweisbar | [README Monitoring](#monitoring), [monitoring/README.md](./monitoring/README.md) |
| Requirement 7: Security-Governance dokumentiert | [README Security](#security), [SECURITY.md](./SECURITY.md) |
| Requirement 8: Disaster Recovery dokumentiert | [README DR](#dr-disaster-recovery), [DR.md](./DR.md), [deployment.md DR](./deployment.md#disaster-recovery-dr--runbooks) |
| Requirement 9: Infrastruktur als Code/Manifeste | [`k8s/`](./k8s), [`main.tf`](./main.tf) |
| Requirement 10: Nachvollziehbare Betriebsdokumentation | [deployment.md](./deployment.md), [monitoring/README.md](./monitoring/README.md), [SECURITY.md](./SECURITY.md), [DR.md](./DR.md) |

## Technology Stack and Features

- ⚡ [**FastAPI**](https://fastapi.tiangolo.com) for the Python backend API.
    - 🧰 [SQLModel](https://sqlmodel.tiangolo.com) for the Python SQL database interactions (ORM).
    - 🔍 [Pydantic](https://docs.pydantic.dev), used by FastAPI, for the data validation and settings management.
    - 💾 [PostgreSQL](https://www.postgresql.org) as the SQL database.
- 🚀 [React](https://react.dev) for the frontend.
    - 💃 Using TypeScript, hooks, Vite, and other parts of a modern frontend stack.
    - 🎨 [Chakra UI](https://chakra-ui.com) for the frontend components.
    - 🤖 An automatically generated frontend client.
    - 🧪 [Playwright](https://playwright.dev) for End-to-End testing.
    - 🦇 Dark mode support.
- 🐋 [Docker Compose](https://www.docker.com) for development and production.
- 🔒 Secure password hashing by default.
- 🔑 JWT (JSON Web Token) authentication.
- 📫 Email based password recovery.
- ✅ Tests with [Pytest](https://pytest.org).
- 📞 [Traefik](https://traefik.io) as a reverse proxy / load balancer.
- 🚢 Deployment instructions using Docker Compose, including how to set up a frontend Traefik proxy to handle automatic HTTPS certificates.
- 🏭 CI (continuous integration) and CD (continuous deployment) based on GitHub Actions.

### Dashboard Login

[![API docs](img/login.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Dashboard - Admin

[![API docs](img/dashboard.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Dashboard - Create User

[![API docs](img/dashboard-create.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Dashboard - Items

[![API docs](img/dashboard-items.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Dashboard - User Settings

[![API docs](img/dashboard-user-settings.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Dashboard - Dark Mode

[![API docs](img/dashboard-dark.png)](https://github.com/fastapi/full-stack-fastapi-template)

### Interactive API Documentation

[![API docs](img/docs.png)](https://github.com/fastapi/full-stack-fastapi-template)

## How To Use It

You can **just fork or clone** this repository and use it as is.

✨ It just works. ✨

### How to Use a Private Repository

If you want to have a private repository, GitHub won't allow you to simply fork it as it doesn't allow changing the visibility of forks.

But you can do the following:

- Create a new GitHub repo, for example `my-full-stack`.
- Clone this repository manually, set the name with the name of the project you want to use, for example `my-full-stack`:

```bash
git clone git@github.com:fastapi/full-stack-fastapi-template.git my-full-stack
```

- Enter into the new directory:

```bash
cd my-full-stack
```

- Set the new origin to your new repository, copy it from the GitHub interface, for example:

```bash
git remote set-url origin git@github.com:octocat/my-full-stack.git
```

- Add this repo as another "remote" to allow you to get updates later:

```bash
git remote add upstream git@github.com:fastapi/full-stack-fastapi-template.git
```

- Push the code to your new repository:

```bash
git push -u origin master
```

### Update From the Original Template

After cloning the repository, and after doing changes, you might want to get the latest changes from this original template.

- Make sure you added the original repository as a remote, you can check it with:

```bash
git remote -v

origin    git@github.com:octocat/my-full-stack.git (fetch)
origin    git@github.com:octocat/my-full-stack.git (push)
upstream    git@github.com:fastapi/full-stack-fastapi-template.git (fetch)
upstream    git@github.com:fastapi/full-stack-fastapi-template.git (push)
```

- Pull the latest changes without merging:

```bash
git pull --no-commit upstream master
```

This will download the latest changes from this template without committing them, that way you can check everything is right before committing.

- If there are conflicts, solve them in your editor.

- Once you are done, commit the changes:

```bash
git merge --continue
```

### Configure

You can then update configs in the `.env` files to customize your configurations.

Before deploying it, make sure you change at least the values for:

- `SECRET_KEY`
- `FIRST_SUPERUSER_PASSWORD`
- `POSTGRES_PASSWORD`

You can (and should) pass these as environment variables from secrets.

Read the [deployment.md](./deployment.md) docs for more details.

### Generate Secret Keys

Some environment variables in the `.env` file have a default value of `changethis`.

You have to change them with a secret key, to generate secret keys you can run the following command:

```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

Copy the content and use that as password / secret key. And run that again to generate another secure key.

## How To Use It - Alternative With Copier

This repository also supports generating a new project using [Copier](https://copier.readthedocs.io).

It will copy all the files, ask you configuration questions, and update the `.env` files with your answers.

### Install Copier

You can install Copier with:

```bash
pip install copier
```

Or better, if you have [`pipx`](https://pipx.pypa.io/), you can run it with:

```bash
pipx install copier
```

**Note**: If you have `pipx`, installing copier is optional, you could run it directly.

### Generate a Project With Copier

Decide a name for your new project's directory, you will use it below. For example, `my-awesome-project`.

Go to the directory that will be the parent of your project, and run the command with your project's name:

```bash
copier copy https://github.com/fastapi/full-stack-fastapi-template my-awesome-project --trust
```

If you have `pipx` and you didn't install `copier`, you can run it directly:

```bash
pipx run copier copy https://github.com/fastapi/full-stack-fastapi-template my-awesome-project --trust
```

**Note** the `--trust` option is necessary to be able to execute a [post-creation script](https://github.com/fastapi/full-stack-fastapi-template/blob/master/.copier/update_dotenv.py) that updates your `.env` files.

### Input Variables

Copier will ask you for some data, you might want to have at hand before generating the project.

But don't worry, you can just update any of that in the `.env` files afterwards.

The input variables, with their default values (some auto generated) are:

- `project_name`: (default: `"FastAPI Project"`) The name of the project, shown to API users (in .env).
- `stack_name`: (default: `"fastapi-project"`) The name of the stack used for Docker Compose labels and project name (no spaces, no periods) (in .env).
- `secret_key`: (default: `"changethis"`) The secret key for the project, used for security, stored in .env, you can generate one with the method above.
- `first_superuser`: (default: `"admin@example.com"`) The email of the first superuser (in .env).
- `first_superuser_password`: (default: `"changethis"`) The password of the first superuser (in .env).
- `smtp_host`: (default: "") The SMTP server host to send emails, you can set it later in .env.
- `smtp_user`: (default: "") The SMTP server user to send emails, you can set it later in .env.
- `smtp_password`: (default: "") The SMTP server password to send emails, you can set it later in .env.
- `emails_from_email`: (default: `"info@example.com"`) The email account to send emails from, you can set it later in .env.
- `postgres_password`: (default: `"changethis"`) The password for the PostgreSQL database, stored in .env, you can generate one with the method above.
- `sentry_dsn`: (default: "") The DSN for Sentry, if you are using it, you can set it later in .env.

## Backend Development

Backend docs: [backend/README.md](./backend/README.md).

## Frontend Development

Frontend docs: [frontend/README.md](./frontend/README.md).

## Deployment

Deployment docs: [deployment.md](./deployment.md).

## CI/CD Pipeline (Kubernetes as Primary Deploy Target)

Primary deploy target for **all environments** is **Kubernetes** (`k8s/dev`, `k8s/staging`, `k8s/prod`). Docker Compose remains for local development only.

End-to-end delivery flow:

1. **Build** container images (backend + frontend).
2. **Test** application (automated test stage in dev pipeline).
3. **Push** images to GHCR.
4. **Deploy dev** to Kubernetes namespace `dev` via `.github/workflows/deploy-dev.yml`.
5. **Approval gate** for production via GitHub **Environment** `production` (configure Required Reviewers in repository settings).
6. **Deploy prod** to Kubernetes namespace `prod` via `.github/workflows/deploy-production.yml` after approval.

Staging deployments (`.github/workflows/deploy-staging.yml`) now also run on Kubernetes namespace `staging` and apply manifests from `k8s/staging`.


## Security Scanning & Release Gates

Security checks are implemented in `.github/workflows/security-scans.yml` and run on push/PR, weekly schedule (Monday 03:00 UTC), and manual dispatch.

Implemented scanners:

- **CodeQL** for code/dependency analysis (`python`, `javascript-typescript`).
- **Trivy (filesystem)** for dependency, secret, and IaC misconfiguration checks.
- **Trivy (container images)** for backend/frontend image vulnerabilities.

### Fail policy

- Pipeline fails automatically on **CRITICAL** findings in Trivy scans.
- CodeQL findings are published to GitHub Security for triage and tracked remediation.

### Kubernetes production baseline (RBAC/TLS)

Production baseline requires:

- dedicated ServiceAccounts per workload,
- disabled service account token automount where API access is unnecessary,
- TLS-enabled Traefik ingress (`websecure`) with explicit `spec.tls` secret.

See [`SECURITY.md`](./SECURITY.md) for the complete security evidence and handling standard.

## Development

General development docs: [development.md](./development.md).

This includes using Docker Compose, custom local domains, `.env` configurations, etc.

## Release Notes

Check the file [release-notes.md](./release-notes.md).

## License

The Full Stack FastAPI Template is licensed under the terms of the MIT license.
