# tsdevstack

**Infrastructure as Framework** — the full-stack, cloud-native, AI-native TypeScript microservices framework.

From zero to production in an hour, not months.

You don't write Terraform. You don't configure gateways. You don't set up CI/CD. The framework generates, manages, and deploys all of it — across GCP, AWS, and Azure. You write application code, tsdevstack handles everything else.

---

### How it works

```
npx @tsdevstack/cli init        # scaffold a project
npx tsdevstack add-service      # add a NestJS backend, Next.js frontend, or Rsbuild SPA
npx tsdevstack sync             # generate secrets, gateway, docker-compose
npx tsdevstack infra:deploy     # deploy to GCP, AWS, or Azure
```

One config drives everything: Terraform infrastructure, Docker builds, Kong gateway routes, CI/CD pipelines, secret management, and observability — all generated from your service definitions. No YAML to maintain, no drift to debug.

### What you get

**Multi-cloud deployment** — same framework, same patterns across GCP (Cloud Run), AWS (ECS Fargate), and Azure (Container Apps). Switch providers without rewriting infrastructure.

**Security by default** — WAF with OWASP rules, JWT validation at the gateway, network isolation, zero-credential runtimes, non-root containers, encrypted secrets. SOC 2, GDPR, and ISO 27001 technical controls are built in, not bolted on.

**Full observability** — structured logging with PII redaction, Prometheus metrics, distributed tracing via OpenTelemetry, health checks. Locally: Grafana + Jaeger. In cloud: native provider logging with zero code changes.

**AI-native tooling** — built-in MCP server with 54 tools for deploying, querying, and debugging your stack from Claude Code, Cursor, or VS Code Copilot.

**Type-safe across the stack** — OpenAPI specs generate TypeScript HTTP clients and DTOs automatically. Types flow from backend decorators to frontend components with full validation.

### Tech stack

NestJS · Next.js · Rsbuild · Kong · PostgreSQL · Redis · Prisma · Terraform · Docker · GitHub Actions

### Architecture

```
Internet → Load Balancer (TLS + WAF) → Kong Gateway (auth + routing) → Services (private network)
                                                                           ↕
                                                                     PostgreSQL · Redis · Secret Manager
```

Services run in private subnets with no public IP. All traffic passes through Kong, which validates JWTs, enforces rate limits, and injects trusted headers. Direct backend access is blocked by design.

### Packages

| Package | Description |
|---------|-------------|
| [`@tsdevstack/cli`](https://www.npmjs.com/package/@tsdevstack/cli) | CLI tools, code generators, infrastructure deployment, and cloud secrets management |
| [`@tsdevstack/cli-mcp`](https://www.npmjs.com/package/@tsdevstack/cli-mcp) | MCP server for AI agent integration |
| [`@tsdevstack/nest-common`](https://www.npmjs.com/package/@tsdevstack/nest-common) | Shared NestJS modules (auth, secrets, observability, email) |
| [`@tsdevstack/react-bot-detection`](https://www.npmjs.com/package/@tsdevstack/react-bot-detection) | React bot detection (behavioral analysis + honeypot) |

### Documentation

Full guides, tutorials, and API reference at [tsdevstack.dev](https://tsdevstack.dev/)

### License

MIT