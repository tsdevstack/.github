# tsdevstack

**Infrastructure as Framework** for TypeScript microservices.

One config file. Three cloud providers. Production-grade infrastructure — generated, not hand-written.

```bash
npx @tsdevstack/cli init
```

---

### How it works

```
npx @tsdevstack/cli init        # scaffold a project
npx tsdevstack add-service      # add a NestJS backend, Next.js frontend, or Rsbuild SPA
npx tsdevstack sync             # generate secrets, gateway, docker-compose
npm run dev                     # local development with full stack
npx tsdevstack infra:deploy     # deploy to GCP, AWS, or Azure
```

One config drives everything: Terraform infrastructure, Docker builds, Kong gateway routes, CI/CD pipelines, secret management, and observability — all generated from your service definitions. No YAML to maintain, no drift to debug.

### What you get

**Multi-cloud deployment** — same framework, same patterns across GCP (Cloud Run), AWS (ECS Fargate), and Azure (Container Apps). Switch providers without rewriting infrastructure.

**API gateway** — Kong routes auto-generated from your OpenAPI specs. JWT validation, rate limiting, CORS, bot detection. Fully customizable when you need it, or bring your own Kong config.

**Background processing** — BullMQ job queues with detached workers running in separate containers. Register, deploy, and scale workers independently from your API services.

**Object storage** — add buckets with a single command. MinIO locally, S3/GCS/Azure Blob in production. Unified `StorageModule` with presigned URLs, streaming, and per-provider adapters.

**Async messaging** — inter-service pub/sub via Redis Streams. Consumer groups, dead letter queues, retry logic. No new infrastructure — runs on the same Redis instance as caching and BullMQ.

**Authentication** — OWASP-aligned JWT token management, protected routes, session handling, email confirmation. Bring your own OIDC or use the built-in auth service template.

**Security by default** — WAF with OWASP rules, OWASP Top 10 coverage, network isolation, zero-credential runtimes, non-root containers, encrypted secrets. SOC 2, GDPR, and ISO 27001 technical controls built in.

**Observability** — structured logging with PII redaction, Prometheus metrics, distributed tracing via OpenTelemetry, health checks. Locally: Grafana + Jaeger. In cloud: native provider logging.

**Type-safe across the stack** — OpenAPI specs generate TypeScript HTTP clients with DTOs as separated imports. Both frontend and backend apps consume the same type-safe library.

**AI-native tooling** — built-in MCP server with 54 tools for deploying, querying, and debugging your stack from Claude Code, Cursor, or VS Code Copilot.

### Tech stack

NestJS · Next.js · Rsbuild · Kong · PostgreSQL · Redis · Prisma · BullMQ · Terraform · Docker · GitHub Actions

### Architecture

```
Internet → Load Balancer (TLS + WAF) → Kong Gateway (auth + routing) → Services (private network)
                                                                           ↕
                                                                     PostgreSQL · Redis · Secret Manager
```

Services run in private subnets with no public IP. All traffic passes through Kong, which validates JWTs, enforces rate limits, and injects trusted headers. Direct backend access is blocked by design.

### Packages

| Package                                                                                            | Description                                                              |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [`@tsdevstack/cli`](https://www.npmjs.com/package/@tsdevstack/cli)                                 | CLI — project scaffolding, infrastructure generation, deployment         |
| [`@tsdevstack/nest-common`](https://www.npmjs.com/package/@tsdevstack/nest-common)                 | Shared NestJS modules — auth, secrets, storage, messaging, observability |
| [`@tsdevstack/cli-mcp`](https://www.npmjs.com/package/@tsdevstack/cli-mcp)                         | MCP server — AI agent integration with 54 tools                          |
| [`@tsdevstack/react-bot-detection`](https://www.npmjs.com/package/@tsdevstack/react-bot-detection) | React bot detection — behavioral analysis + honeypot                     |

### Documentation

Guides, architecture, and API reference at **[tsdevstack.dev](https://tsdevstack.dev)**

### License

MIT
