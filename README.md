# diggr.ai

**AI-native Latent Defect Insurance platform for UK construction projects.**

diggr.ai replaces the insurance broker with AI agents that match projects to insurers, manage submissions, compare terms, and coordinate the entire placement — faster, cheaper, and more transparent.

---

## Architecture

```
diggr-ai/
├── apps/
│   ├── api/                 # NestJS backend (TypeScript)
│   │   ├── src/modules/     # Domain modules (scheme, insurer, matching, etc.)
│   │   ├── prisma/          # Database schema & migrations
│   │   └── test/            # API tests
│   └── web/                 # Next.js frontend (TypeScript)
│       ├── src/app/         # App Router pages
│       ├── src/components/  # React components
│       └── src/lib/         # Utilities & API client
├── packages/
│   └── shared/              # Shared types, constants, validation (Zod)
├── infra/
│   ├── docker/              # Docker Compose for local dev
│   └── terraform/           # AWS infrastructure (future)
└── .github/workflows/       # CI/CD pipelines
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 14, TypeScript, Tailwind CSS, React Query, Zustand |
| Backend | NestJS, TypeScript, Prisma ORM, BullMQ |
| Database | PostgreSQL 16 + pgvector |
| Cache | Redis 7 |
| Storage | AWS S3 (MinIO locally) |
| AI | Anthropic Claude API |
| Auth | Auth0 / Clerk |
| Payments | Stripe Connect |
| Infra | AWS (eu-west-2), Docker, Terraform |

## Prerequisites

- Node.js 20+
- Docker & Docker Compose
- Git

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/your-org/diggr-ai.git
cd diggr-ai

# 2. Install dependencies
npm install

# 3. Start infrastructure (Postgres, Redis, MinIO, Mailpit)
npm run docker:up

# 4. Copy environment config
cp .env.example .env

# 5. Run database migrations
npm run db:generate
npm run db:migrate

# 6. Seed sample data (insurers, sample scheme)
npm run db:seed

# 7. Start development servers
npm run dev
```

The API runs at **http://localhost:4000** (Swagger docs at /api/docs).
The web app runs at **http://localhost:3000**.

## Local Services

| Service | URL | Purpose |
|---------|-----|---------|
| Web App | http://localhost:3000 | Next.js frontend |
| API | http://localhost:4000 | NestJS backend |
| Swagger | http://localhost:4000/api/docs | API documentation |
| MinIO Console | http://localhost:9001 | S3 file browser |
| Mailpit | http://localhost:8025 | Email testing UI |
| Bull Board | http://localhost:3100 | Job queue dashboard |
| Prisma Studio | `npm run db:studio` | Database browser |

## Key Commands

```bash
# Development
npm run dev              # Start both frontend and backend
npm run dev:api          # Start backend only
npm run dev:web          # Start frontend only

# Database
npm run db:generate      # Generate Prisma client
npm run db:migrate       # Run migrations
npm run db:seed          # Seed sample data
npm run db:studio        # Open Prisma Studio

# Infrastructure
npm run docker:up        # Start Docker services
npm run docker:down      # Stop Docker services
npm run docker:logs      # Tail Docker logs

# Quality
npm run lint             # Lint all workspaces
npm run test             # Test all workspaces
npm run build            # Build all workspaces
```

## Phase 1 Modules

| Module | Status | Description |
|--------|--------|-------------|
| Auth | 🟡 Scaffold | JWT/Auth0 integration, role-based access |
| Scheme | ✅ Core | CRUD, status model, lifecycle management |
| Intake | 🟡 Scaffold | Multi-step wizard, validation, readiness |
| Document | ✅ Core | Upload, S3 storage, classification pipeline |
| Insurer | ✅ Core | Directory, appetite rules, wording library |
| Matching | ✅ Core | Rule-based matching engine with scoring |
| Notification | 🟡 Scaffold | In-app + email notifications |
| Audit | 🟡 Scaffold | Immutable action logging |
| Admin | 🟡 Scaffold | Insurer config, status management |

## Seed Data

The seed script creates:
- **8 sample insurers** with realistic appetite rules (Premier Guarantee, LABC Warranty, AHCI, Build-Zone, Protek, ICW, Ark Insurance, Global Home Warranties)
- **1 sample client** organisation (Thames Developments Ltd)
- **1 sample scheme** (42-unit BTR in Manchester)

## Contributing

1. Create a feature branch from `develop`
2. Write tests for new features
3. Ensure `npm run lint` and `npm run build` pass
4. Submit a PR with a clear description

---

**diggr.ai** — Confidential. All rights reserved.
