# Vibe Code Canon: Technical Documentation Framework

## Overview

This framework provides canonical standards for production-grade technical documentation. It is designed for AI agents to generate consistent, high-quality documentation while remaining fully human-readable and maintainable.

**Purpose:** Define rules, structures, and standards for all technical documentation across projects.

**Audience:** AI agents (primary) and human developers (secondary).

---

## CRITICAL: Documentation Format Standards

**This project uses enterprise-grade documentation formats:**

### API Documentation
- **Format:** OpenAPI 3.0+ (formerly Swagger)
- **File Extension:** `.yaml` or `.json`
- **Location:** `/api-specs/` or `/docs/api-specs/`
- **Tools:** Swagger UI, Redoc, OpenAPI Generator
- **Validation:** `swagger-cli validate`, `openapi-generator validate`

### All Other Technical Documentation
- **Format:** reStructuredText (.rst)
- **File Extension:** `.rst`
- **Location:** `/docs/source/`
- **Tools:** Sphinx, Read the Docs
- **Build:** `sphinx-build -b html source build`

### Deprecated Formats (Reference Only)
- **Markdown (.md):** Existing canon examples in `01-documentation-canons/` are provided in Markdown for historical reference and ease of understanding
- **Usage:** Canon files themselves remain in Markdown for agent readability
- **Actual Documentation:** All production documentation MUST be in reStructuredText (.rst) or OpenAPI
- **Exception:** README.md, CHANGELOG.md, and ADRs may use Markdown

**Critical Rule:** When generating documentation:
1. API specs → OpenAPI (.yaml)
2. Technical docs → reStructuredText (.rst)
3. Canon examples are Markdown → translate to .rst in production

---

## When to Use This Framework

**USE this framework when:**
- Writing **technical documentation** for any software project
- Documenting **APIs** (REST, GraphQL, gRPC, internal services)
- Creating **architecture documentation** (system design, C4 models)
- Documenting **deployment procedures** (infrastructure, CI/CD, runbooks)
- Writing **database documentation** (schemas, migrations, ERDs)
- Creating **security documentation** (threat models, compliance)
- Documenting **testing strategies** (test plans, coverage)
- Writing **user guides** or **developer guides**
- Creating **Architecture Decision Records (ADRs)**
- Maintaining **changelogs** or **configuration documentation**

**SKIP this framework when:**
- Writing application code (this is about documentation, not code)
- Creating UI mockups or designs (use design tools)
- Writing marketing content or blog posts
- Creating project management documents (use PM tools)
- Writing personal notes or informal documentation

**Quick Decision:** If the task involves creating or updating **technical documentation for software**, dive deeper. Otherwise, skip this directory.

---

## Core Principle

**Agents don't need templates. Agents need rules + examples.**

This canon system provides:
1. **Rules** - How to generate each documentation type
2. **Structures** - Where files should be placed and what access levels they need
3. **Examples** - Real-world illustrations of correct documentation
4. **References** - Quick syntax lookups for documentation formats

---

## Directory Structure

```
01-technical-documentation/
│
├── README.md                                    # This file
│
├── 00-core-canons/                              # Universal rules (foundation)
│   ├── _core_canon.md                           # Universal writing rules
│   ├── _template.md                             # Persona template
│   └── _docs-canon.md                           # Technical documentation standards
│
├── 01-documentation-canons/                     # Rules for each doc type
│   │
│   ├── api-documentation/                       # API-specific canons
│   │   ├── _rest-api-canon.md                   # REST API documentation rules
│   │   ├── _graphql-api-canon.md                # GraphQL API documentation rules
│   │   ├── _grpc-api-canon.md                   # gRPC API documentation rules
│   │   └── _internal-api-canon.md               # Internal API documentation rules
│   │
│   ├── documentation-ui/                        # Documentation UI/theming canons
│   │   ├── _documentation-ui-canon.md           # UI/theming standards (Sphinx, Furo)
│   │   └── _documentation-classification-canon.md # Public vs private classification
│   │
│   ├── deployment/                              # Deployment canons
│   │   └── _documentation-deployment-canon.md   # Documentation hosting/deployment
│   │
│   ├── _architecture-canon.md                   # Architecture documentation rules
│   ├── _deployment-canon.md                     # Deployment documentation rules (DEPRECATED - use deployment/)
│   ├── _operations-canon.md                     # Operations/runbook rules
│   ├── _database-canon.md                       # Database documentation rules
│   ├── _security-canon.md                       # Security documentation rules
│   ├── _configuration-canon.md                  # Configuration documentation rules
│   ├── _testing-canon.md                        # Testing documentation rules
│   ├── _user-guide-canon.md                     # User guide rules
│   ├── _adr-canon.md                            # ADR (Architecture Decision Records) rules
│   └── _changelog-canon.md                      # Changelog documentation rules
│
├── 02-examples/                                 # Minimal illustrative examples
│   ├── rest-api-example/                        # REST API example
│   │   ├── api-spec.yaml                        # Example OpenAPI specification
│   │   └── api-reference.rst                    # Example narrative documentation
│   │
│   ├── architecture-example/                    # Architecture docs example
│   │   └── 00-overview.rst                      # Example architecture document
│   │
│   ├── operations-example/                      # Operations docs example
│   │   └── runbook.rst                          # Example runbook
│   │
│   └── complete-sphinx-setup/                   # Sphinx configuration example
│       ├── conf.py                              # Example Sphinx config
│       └── index.rst                            # Example documentation homepage
│
├── 03-reference/                                # Quick syntax references
│   ├── docs-conversations.md                    # Original design conversation
│   ├── diagrams-net-guide.md                    # diagrams.net usage guide
│   ├── rest-syntax.md                           # reStructuredText quick reference (planned)
│   ├── openapi-syntax.md                        # OpenAPI quick reference (planned)
│   ├── graphql-syntax.md                        # GraphQL SDL quick reference (planned)
│   ├── proto3-syntax.md                         # Protocol Buffers quick reference (planned)
│   └── access-levels.md                         # Access level classification guide (planned)
│
└── CHANGELOG.md                                 # Canon version history
```

---

## How to Use This Framework

### For AI Agents

When tasked with creating technical documentation:

1. **Identify the documentation type** (API, architecture, deployment, etc.)
2. **Read the corresponding canon** from `01-documentation-canons/`
3. **Check syntax references** in `03-reference/` as needed
4. **Review example** in `02-examples/` to see correct implementation
5. **Generate documentation** following the canon rules
6. **Place files** in the structure specified by the canon
7. **Set access levels** as specified by the canon and instruct the user on where and how to store, access, and manage the documentation as per the access level classification guide in `03-reference/access-levels.md`

### For Human Developers

When you need to understand documentation standards:

1. **Start with `00-core-canons/_docs-canon.md`** for overall structure
2. **Read specific canon** for the documentation type you're creating
3. **Reference examples** in `02-examples/` for working code
4. **Check `03-reference/`** for syntax questions
5. **Validate your work** using `scripts/validate-docs.sh`

---

## Validation & CI/CD

**Local Validation:**

```bash
# Validate all documentation
./scripts/validate-docs.sh

# Validate specific types
./scripts/validate-docs.sh --rest
./scripts/validate-docs.sh --openapi

# Install pre-commit hook
cp scripts/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

**CI/CD:**

GitHub Actions workflow (`.github/workflows/docs.yml`) automatically:
- Validates all documentation on PR/push
- Builds Sphinx documentation
- Deploys to GitHub Pages (on main branch)

---

## Documentation Types Covered

### Critical Documentation (Production Requirements)
1. **API Documentation** - REST, GraphQL, gRPC, Internal APIs
2. **Architecture Documentation** - System design, components, interactions
3. **Deployment Documentation** - Installation, infrastructure, CI/CD
4. **Operations/Runbooks** - Monitoring, troubleshooting, incident response
5. **Security Documentation** - Threat models, compliance, auth/authz

### Supporting Documentation (Best Practices)
6. **Database Documentation** - Schema, migrations, data management
7. **Configuration Documentation** - Environment variables, feature flags
8. **Testing Documentation** - Test strategy, coverage, procedures
9. **User Documentation** - Guides, tutorials, FAQs
10. **ADRs** - Architecture decision records
11. **Changelogs** - Version history, release notes

### Documentation Infrastructure (New)
12. **Documentation UI/Theming** - Sphinx themes, navigation, accessibility, visual design
13. **Documentation Classification** - Public vs private, access levels, security assessment
14. **Documentation Deployment** - Hosting platforms, CI/CD automation, authentication

---

## Key Concepts

### Canon Documents (Rules)

Each canon document specifies:
- **Files to Generate** - What files the agent should create
- **Directory Structure** - Where files should be placed
- **Access Level Requirements** - Public, Internal, Restricted, or Confidential
- **Generation Rules** - How to structure and write the content
- **When to Generate** - Lifecycle timing (design, development, testing, launch)
- **Validation** - How to verify correctness
- **Examples** - Reference to working example

### Access Levels

All documentation must be classified:
- **Level 1: Public** - End users, third-party developers, general public
- **Level 2: Internal** - Employees, authorized personnel only
- **Level 3: Restricted** - Leadership, core team, need-to-know basis
- **Level 4: Confidential** - Executive/board level only

See `03-reference/access-levels.md` for detailed classification guide.

### Documentation Formats

This framework standardizes on:
- **reStructuredText (.rst)** - ALL narrative documentation (architecture, deployment, operations, database, security, testing, user guides, configuration)
- **OpenAPI 3.0+ (.yaml)** - REST API specifications
- **Sphinx** - Documentation generation and build tool
- **GraphQL SDL** - GraphQL API schemas (if applicable)
- **Protocol Buffers (Proto3)** - gRPC service definitions (if applicable)
- **Markdown (.md)** - ONLY for: ADRs, README.md, CHANGELOG.md, and canon documentation files

**IMPORTANT:** Canon examples in `01-documentation-canons/` are written in Markdown for agent readability, but production documentation MUST be generated in reStructuredText (.rst) or OpenAPI (.yaml) formats.

---

## File Naming Conventions

- **Canon files**: Prefix with underscore `_` (e.g., `_rest-api-canon.md`)
- **Core canons**: Store in `00-core-canons/`
- **Type-specific canons**: Store in `01-documentation-canons/`
- **Examples**: Descriptive folder names in `02-examples/`
- **References**: Descriptive names in `03-reference/`

---

## Version Control

**Current Version:** 1.0.0 (December 29, 2025)

All changes to canon documents must be:
1. Documented in `CHANGELOG.md`
2. Version-bumped following semantic versioning
3. Reviewed for consistency across all canons

---

## Quick Start Example

**Task:** Document a REST API

**Agent Workflow:**
1. Read `01-documentation-canons/api-documentation/_rest-api-canon.md`
2. Discover: Need to create OpenAPI YAML + reST narrative docs
3. Check `03-reference/openapi-syntax.md` for syntax rules
4. Review `02-examples/rest-api-example/` for working example
5. Generate:
   - `/api-specs/service-api.yaml` (OpenAPI spec)
   - `/docs/source/api-reference/00-index.rst` (API overview)
   - `/docs/source/api-reference/authentication.rst` (Auth docs)
   - `/docs/source/api-reference/errors.rst` (Error codes)
6. Validate with `swagger-cli validate api-specs/service-api.yaml`
7. Done.

---

## Implementation Status

See implementation plan in task management artifact for current progress.

**Completed:**
- ✅ Core directory structure
- ✅ Core canon files organized

**In Progress:**
- 🔄 Documentation type canons
- 🔄 Examples
- 🔄 Reference materials

**Planned:**
- ⏳ Validation scripts
- ⏳ CI/CD templates

---

## Contributing

When adding new documentation types:

1. Create new canon file in `01-documentation-canons/`
2. Follow the canonical structure (see existing canons)
3. Provide minimal working example in `02-examples/`
4. Update this README
5. Update `CHANGELOG.md`

---

## References

- **Original Design Conversation:** `03-reference/docs-conversations.md`
- **Core Writing Rules:** `00-core-canons/_core_canon.md`
- **Overall Documentation Standards:** `00-core-canons/_docs-canon.md`
- **Persona Template:** `00-core-canons/_template.md`

---

## Support

For questions about:
- **How to use this framework:** Read this README + specific canon
- **Syntax questions:** Check `03-reference/`
- **Working examples:** Browse `02-examples/`
- **Design rationale:** Read `03-reference/docs-conversations.md`
