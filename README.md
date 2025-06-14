# MooWords 🐄📚

MooWords is a full-scale vocabulary learning platform based on the "5 Cow Stomachs" method (extended Leitner spaced repetition system).

## 🎯 Project Goal

The goal of MooWords is to provide a scalable language learning system where users can:

- Create their own vocabulary sets.
- Share vocabulary sets with others.
- Learn words using a spaced repetition algorithm (5 cow stomachs system).
- Rate vocabulary sets with upvotes and downvotes.
- Receive learning reminders via emails and system notifications.

## 🛠️ Technical Design

- Full separation of backend and frontend layers.
- Modern stack: .NET 8 (backend) + Angular 19 (frontend).
- EF Core + ASP.NET Identity + JWT + Google OAuth + 2FA.
- CQRS architecture with MediatR.
- RabbitMQ message broker for notifications and email handling.
- Docker Compose for development environment.
- CI/CD and scalability ready.

## 📂 Repository Structure

```
MooWords/         - Main meta-repository managing the whole project and infrastructure
MooWordsAPI/      - Backend: business logic, API, authentication, database access, core application logic
MooWordsGUI/      - Frontend: Angular SPA providing user interface and communicating with the backend
MooWordsWorkers/  - Workers: background jobs, RabbitMQ consumers handling emails, notifications and async tasks
```

## ✅ Branching & Commit Guidelines

To keep our development clean, traceable, and automation-friendly (Semantic Release / GitVersion), I follow these conventions:

### 🔀 Branch Strategy

| Branch       | Purpose                       | Versioning       | Deployment                        |
| ------------ | ----------------------------- | ---------------- | --------------------------------- |
| `main`       | Production-ready code         | `vX.Y.Z`         | 🚀 Live                           |
| `develop`    | Integration & feature testing | `vX.Y.Z-alpha.N` | 🔪 Staging                        |
| `feature/*`  | New feature development       | -                | (merged into `develop`)           |
| `fix/*`      | Bugfix development            | -                | (merged into `main` or `develop`) |
| `breaking/*` | Major breaking changes        | -                | (merged into `develop`)           |

> ✅ **All merges must go through pull requests.**  
> 🔒 Direct pushes to `main` or `develop` are blocked via branch protection.

---

### ✍️ Conventional Commit Messages

I follow the [Conventional Commits](https://www.conventionalcommits.org/) standard.  
This allows automated versioning, changelog generation and CI automation.

**Format:**

```
<type>[optional scope]: <short description>

[optional body]
[optional footer(s)]
```

**Examples:**

- `feat(auth): add Google OAuth2 integration`
- `fix(notification): retry failed email jobs`
- `refactor(api): split controller logic`
- `chore: update dependencies`
- `test(auth): add login edge case tests`

**Types I use:**

- `feat` – new feature
- `fix` – bug fix
- `chore` – tooling/config updates (e.g. CI/CD, deps)
- `docs` – documentation changes
- `refactor` – code improvements (no logic change)
- `test` – testing only
- `style` – formatting, comments, whitespace

## 📌 Work Plan (MVP Roadmap)

### Phase 1 — Project Initialization & CI/CD Setup

- [x] Create separate repositories: `MooWordsAPI` (Backend), `MooWordsGUI` (Frontend), `MooWordsWorkers` (HostedServices)
- [x] Initialize backend project structure (ASP.NET 8 WebAPI, Clean Architecture)
- [x] Initialize frontend project (Angular 19 SPA)
- [x] Initialize workers project (ASP.NET 8 HostedServices)
- [x] Setup git submodules (optional: meta-repo `MooWords`)
- [x] Setup versioning:
  - Backend: MinVer integration
  - Frontend: semantic-release integration
- [x] Configure code formatters:
  - Backend: dotnet format, analyzers
  - Frontend: prettier, eslint, husky, lint-staged
- [x] Implement pre-commit hooks for both repos
- [ ] Setup Docker Compose for local development
- [x] Setup CI/CD pipelines:
  - Build, test, release workflows for backend and frontend
  - Automatic semantic version tagging
- [ ] Setup environments (development, staging, production)
- [x] Setup basic logging, monitoring and error tracking

### Phase 2 — Core Identity

- [ ] EF Core Identity + MSSQL integration
- [ ] Registration with email confirmation
- [ ] JWT authentication + refresh tokens
- [ ] Password reset & change
- [ ] Google OAuth2 login
- [ ] 2FA with TOTP (Google Authenticator)

### Phase 3 — Vocabulary Packages

- [ ] Vocabulary package CRUD
- [ ] Vocabulary item CRUD
- [ ] Public/private sharing system
- [ ] Package rating system (upvotes/downvotes)

### Phase 4 — Learning Module

- [ ] 5 Cow Stomachs repetition system implementation
- [ ] Learning sessions engine
- [ ] Learning history tracking
- [ ] Learning statistics

### Phase 5 — Notifications System

- [ ] RabbitMQ integration
- [ ] Email worker (email reminders)
- [ ] Notification system (future: Web Push)

### Phase 6 — Frontend (Angular 19)

- [ ] Authentication module (register, login, confirm email, password reset, 2FA)
- [ ] User dashboard
- [ ] Vocabulary package management UI
- [ ] Learning sessions UI
- [ ] Notification management

### Phase 7 — DevOps & Infrastructure

- [ ] 🧩 **Jenkins CI/CD Integration**

  - [ ] Deploy Jenkins on self-hosted VPS
  - [ ] Secure with HTTPS, SSH credentials & role-based access
  - [ ] Integrate GitHub Webhooks with Jenkins pipelines
  - [ ] Trigger builds and deployments for:
    - MooWordsAPI
    - MooWordsGUI
    - MooWordsWorkers

- [ ] ☸️ **Kubernetes (K8s) Setup**

  - [ ] Create manifests (YAML) for deployments, services, ingress
  - [ ] Create Helm charts (optional for scaling)
  - [ ] Add support for Horizontal Pod Autoscaling
  - [ ] Configure persistent storage (e.g. for DB, logs)
  - [ ] Integrate with Traefik or NGINX Ingress Controller

- [ ] 🧾 **Centralized Logging & Monitoring**

  - [x] Use Serilog in .NET projects
  - [ ] Push logs to centralized platform (e.g. ELK stack / Grafana Loki)
  - [ ] Add request correlation ID (traceability between services)
  - [ ] Implement health checks (via `HealthChecks` in ASP.NET)
  - [ ] Monitor RabbitMQ queues & worker metrics

- [ ] 🔒 **Security & Secrets Management**

  - [ ] Use `dotnet user-secrets` locally
  - [ ] Migrate secrets to Kubernetes Secrets or Vault in prod
  - [ ] Store environment secrets securely in GitHub Actions + Jenkins

- [ ] 📄 **Documentation & Maintainers Guide**

  - [ ] Expand READMEs in each submodule:
    - How to build, test, and deploy
    - Project architecture diagrams
    - Troubleshooting common issues
  - [ ] Add contributor guidelines and code of conduct
  - [ ] Generate OpenAPI (Swagger) docs for backend

- [ ] 🧪 **Quality Gates & Automated Checks**
  - [ ] Integrate SonarQube (optional) or static code analysis reports
  - [ ] Add test coverage enforcement on PR
  - [ ] Create dedicated CI pipeline for pull requests (build, lint, test)
