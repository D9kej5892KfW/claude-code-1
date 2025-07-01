# [Project Name] - Production System

## Architecture Overview
- Microservices: auth-service, user-service, payment-service
- Frontend: Next.js 14 with TypeScript strict mode
- Database: PostgreSQL 15 with connection pooling
- Infrastructure: AWS ECS with Terraform IaC
- See @docs/architecture-diagram.png for visual overview

## Critical Commands
```bash
# Development
pnpm dev          # Start all services locally
pnpm test:e2e     # Run full test suite (takes 5min)
pnpm build:prod   # Production build with optimizations

# Infrastructure  
terraform plan    # Always run before apply
kubectl get pods  # Check cluster health
```

## Code Quality Standards
- TypeScript strict mode REQUIRED
- Test coverage >85% (check with `pnpm test:coverage`)
- All API endpoints MUST have OpenAPI docs
- Security: Use @src/utils/validation for all inputs
- Performance: Follow patterns in @src/patterns/optimization.ts

## Domain Knowledge
- User states: `draft`, `active`, `suspended`, `deleted`
- Payment flow: See @docs/payment-sequence.md
- Rate limits: 1000 req/min per API key
- Error codes: Follow @src/types/errors.ts enum

## Debugging Workflows
- "Check logs in CloudWatch for service X"
- "Trace request ID through all microservices" 
- "Verify database migrations are applied"
- "Check Redis cache hit rates"

## Security Protocol
- NEVER log sensitive data (PII, tokens, passwords)
- All external APIs require timeout + retry logic
- Use @src/middleware/auth.ts for authentication
- Follow OWASP guidelines in @docs/security-checklist.md