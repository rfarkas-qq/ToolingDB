# OBSOLETE

Development Rules & Guidelines

## 1. Architecture & Fundamentals

**Runtime:** Node.js (LTS), ESM

**App type:** REST / API-first (OpenAPI), optional SSR/SPA separation

**Architecture:** Clean Architecture / Hexagonal
- `domain` (pure logic)
- `application` (use cases)
- `infrastructure` (DB, APIs)
- `interface` (HTTP, CLI)

**Principles:**
- Dependency inversion
- No framework leakage into domain

## 2. Backend Stack

**Framework:** Fastify (performance, schema-first)

**Validation:** Zod (shared with frontend)

**ORM/DB:** Prisma + PostgreSQL

**Config:** dotenv + typed config

**Auth:** JWT / OAuth2 (if needed)

**Logging:** pino (structured logs)

**Errors:** central error mapping → HTTP codes

## 3. Frontend Basics (if applicable)

**HTML:** Semantic HTML5 (`header`, `nav`, `main`, `section`, `article`, `footer`)

**Accessibility:** ARIA only when semantic HTML is insufficient

**CSS Methodology:** BEM
- `block__element--modifier`

**Styling:** CSS Modules / SCSS

**State:** minimal, explicit (no hidden globals)

## 4. Testing-First Workflow (Mandatory)

**Approach:** TDD / test-first

**Unit tests:** Vitest / Jest
- domain logic
- use cases

**Integration tests:**
- API endpoints
- DB (test containers)

**E2E (optional):** Playwright

**Coverage:** gates in CI

## 5. Code Quality & Review Rules

**Linting:** ESLint (strict)

**Formatting:** Prettier

**Static typing:** TypeScript strict

**Commits:** Conventional Commits

**PR Checklist:**
- tests added/updated
- no business logic in controllers
- naming clarity
- no unused abstractions

## 6. API & Contracts

**OpenAPI spec** as single source of truth

**DTOs** separated from domain models

**Versioning:** `/v1`

**Idempotency** for write endpoints

## 7. Security & Robustness

- Input validation everywhere
- Rate limiting
- CORS explicit
- Secrets never in repo
- Graceful shutdown
- Health/readiness endpoints

## 8. DevOps Baseline

**Docker:** multi-stage

**CI:** test → lint → build

**Env separation:** dev/test/prod

**Observability:** ready (logs + metrics hooks)

