# Suggested Project Structure - mystsh Monorepo

The following structure utilizes a modern monorepo approach (e.g., Turborepo or Nx) to manage all aspects of the mystsh platform in a single repository.

```text
mystsh/
├── apps/                        # Application entry points
│   ├── teen-mobile/             # Teen-facing mobile app (React Native or Flutter)
│   ├── parent-dashboard/        # Parent management web/mobile app
│   └── api-server/              # Main backend API (Node.js/Express/FastAPI)
│
├── packages/                    # Shared internal libraries
│   ├── ui-kit/                  # Shared UI components (Tailwind CSS/React)
│   ├── database/                # Database schemas, migrations (Prisma/Drizzle)
│   ├── card-issuer-sdk/         # Integration logic for Stripe/Marqeta
│   ├── common-types/            # Shared TypeScript types for API/Client sync
│   └── auth-core/               # Shared authentication and RBAC logic
│
├── docs/                        # Project documentation (Markdown)
│   ├── product/                 # PRD, PR/FAQ, Roadmap
│   ├── architecture/            # System Design, Infrastructure, Security
│   └── api/                     # OpenAPI/Swagger definitions
│
├── infrastructure/              # Infrastructure as Code (Terraform/Pulumi)
│   ├── dev/
│   ├── staging/
│   └── production/
│
├── .github/                     # CI/CD workflows and GitHub Actions
├── .husky/                      # Git hooks (linting, formatting)
├── turbo.json                   # Monorepo task runner configuration
├── package.json                 # Global project metadata
└── README.md                    # Project landing page and setup guide
```

## Key Rationale
- **Code Sharing:** Shared types and business logic between the mobile apps and the backend reduce duplication and errors.
- **Consistent UI:** A shared UI kit ensures a unified look and feel for both parent and teen experiences.
- **Simplified Deployment:** Orchestrating deployments of interdependent services is easier in a monorepo.
- **Improved DX:** Atomic commits across frontend and backend simplify feature development and testing.
