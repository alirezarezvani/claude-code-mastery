# Enterprise Compliance CLAUDE.md Template

Configuration for regulated industries with audit requirements, governance, and security constraints.

## When to Use

- Healthcare (HIPAA)
- Finance (SOC 2, PCI-DSS)
- Government contractors
- Any organization with compliance audits
- Projects handling PII/sensitive data

## Template

```markdown
# Project: [Project Name]

## Overview
[Brief description — include compliance context]

## Compliance Requirements
- **Primary:** [HIPAA/SOC 2/PCI-DSS/GDPR/etc.]
- **Audit cycle:** [Annual/Quarterly]
- **Last audit:** [Date]
- **Data classification:** [Public/Internal/Confidential/Restricted]

## Team & Approval Structure
- **Engineering lead:** [Name/Role]
- **Security contact:** [Name/Role]
- **Compliance officer:** [Name/Role]
- **Change approval:** [Process description]

## Tech Stack
- **Language:** [TypeScript/Java/etc.]
- **Framework:** [Next.js/Spring Boot/etc.]
- **Database:** [PostgreSQL with encryption at rest]
- **Infrastructure:** [AWS GovCloud/Azure Government/etc.]
- **Secrets management:** [HashiCorp Vault/AWS Secrets Manager]
- **Logging:** [Datadog/Splunk/etc.]

## Commands
\`\`\`bash
# Development
npm run dev              # Local dev (uses mock data)
npm run build            # Production build

# Testing
npm test                 # Unit tests
npm run test:e2e         # E2E tests
npm run test:security    # Security scan (SAST)

# Code Quality
npm run lint             # ESLint with security rules
npm run typecheck        # TypeScript strict mode
npm run audit            # Dependency audit

# Compliance
npm run compliance:check # Run compliance checklist
npm run audit:deps       # Check for vulnerable deps
\`\`\`

## Security Constraints

### ABSOLUTE PROHIBITIONS
These will fail compliance audits:

- ❌ **NEVER** log PII (names, emails, SSN, etc.)
- ❌ **NEVER** store credentials in code or config files
- ❌ **NEVER** disable SSL/TLS verification
- ❌ **NEVER** use `eval()` or dynamic code execution
- ❌ **NEVER** commit .env files or secrets
- ❌ **NEVER** use deprecated crypto algorithms (MD5, SHA1)
- ❌ **NEVER** bypass authentication checks
- ❌ **NEVER** return stack traces to users

### REQUIRED PRACTICES
These are audited:

- ✅ **ALWAYS** use parameterized queries (no string concatenation)
- ✅ **ALWAYS** validate and sanitize all inputs
- ✅ **ALWAYS** encrypt sensitive data at rest and in transit
- ✅ **ALWAYS** use secrets manager for credentials
- ✅ **ALWAYS** log security-relevant events (auth, access)
- ✅ **ALWAYS** implement rate limiting on APIs
- ✅ **ALWAYS** use HTTPS for all external calls
- ✅ **ALWAYS** implement proper session management

## Data Handling

### Classification Levels
| Level | Examples | Handling |
|-------|----------|----------|
| Public | Marketing content | No restrictions |
| Internal | Business docs | No external sharing |
| Confidential | Customer data | Encrypted, access logged |
| Restricted | PII, PHI, financial | Encrypted, MFA required, full audit trail |

### PII Fields (Do Not Log)
\`\`\`
- email
- phone
- ssn / national_id
- date_of_birth
- address
- financial_account
- health_information
- biometric_data
\`\`\`

### Safe Logging Pattern
\`\`\`typescript
// ❌ WRONG
logger.info(\`User logged in: \${user.email}\`);

// ✅ CORRECT
logger.info(\`User logged in: userId=\${user.id}\`);
\`\`\`

## Authentication & Authorization

### Auth Requirements
- MFA required for admin access
- Session timeout: 30 minutes
- Password requirements: 12+ chars, complexity rules
- Account lockout: 5 failed attempts

### Authorization Pattern
\`\`\`typescript
// Always check authorization at service layer
async function getPatientRecord(userId: string, patientId: string) {
  // 1. Verify user is authenticated
  // 2. Check user has permission for this patient
  // 3. Log access attempt
  // 4. Return data only if authorized
}
\`\`\`

## Audit Logging

### Required Audit Events
- User authentication (success/failure)
- Authorization decisions
- Data access (who accessed what, when)
- Data modifications (who changed what, old/new values)
- Administrative actions
- Security events (rate limiting, blocked requests)

### Audit Log Format
\`\`\`json
{
  "timestamp": "ISO-8601",
  "event_type": "DATA_ACCESS",
  "user_id": "uuid",
  "resource_type": "patient_record",
  "resource_id": "uuid",
  "action": "READ",
  "result": "SUCCESS",
  "ip_address": "x.x.x.x",
  "user_agent": "...",
  "correlation_id": "uuid"
}
\`\`\`

## Code Review Requirements

### Security Review Checklist
Every PR must verify:
- [ ] No hardcoded secrets
- [ ] Input validation on all endpoints
- [ ] Parameterized queries only
- [ ] No PII in logs
- [ ] Proper error handling (no stack traces)
- [ ] Authorization checks present
- [ ] Audit logging for sensitive operations

### Required Approvals
- Standard changes: 1 engineer + 1 security review
- Schema changes: + DBA approval
- Auth changes: + Security team approval
- Infrastructure: + DevOps + Security approval

## Change Management

### Before Making Changes
1. Check if change requires Change Advisory Board (CAB) approval
2. Document change in ticketing system
3. Identify rollback procedure
4. Schedule maintenance window if needed

### Deployment Restrictions
- Production deploys: Business hours only (unless emergency)
- Database migrations: Require DBA approval
- Security patches: Expedited process available

## Incident Response

If you discover a potential security issue:
1. **STOP** — Do not attempt to fix without guidance
2. **DOCUMENT** — Note what you found
3. **REPORT** — Contact security team immediately
4. **PRESERVE** — Don't delete logs or evidence

## File Structure
\`\`\`
src/
├── auth/              # Authentication (security-critical)
├── api/               # API endpoints
├── services/          # Business logic
├── audit/             # Audit logging utilities
├── security/          # Security utilities
├── types/             # TypeScript types
└── utils/             # General utilities

config/
├── security/          # Security configurations
└── compliance/        # Compliance rule definitions
\`\`\`
```

## Pairing with Hooks

This template works best with enterprise hooks. See [Enterprise Guardrails Hook](../hooks/examples/enterprise-guardrails.json).

---

📰 **Related Article:** [Hooks as Enterprise Guardrails: Compliance Without Killing Productivity](https://medium.com/@alirezarezvani)
