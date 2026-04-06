# System Evidence Appendix

## Purpose
Provide system-specific evidence references to support policy controls without duplicating policy text. This appendix does not replace organizational records (training logs, risk register, audits).

## Architecture and Data Flow
- `CAIQ_architecture_overview.md` (system overview, data residency, major services)

## Identity and Access Management
- Backend JWT auth and RBAC: `ssc-web-portal-backend-main/src/middlewares/auth.js`
- Role definitions and route enforcement: `ssc-web-portal-backend-main/src/routes/`
- Azure AD SSO for admin: `ssc-web-portal-backend-main/src/controllers/adminAuthController.js`

## Cryptography and Data Protection
- AES field encryption utilities: `ssc-web-portal-backend-main/src/utils/utility.js`
- Password hashing and JWT issuance: `ssc-web-portal-backend-main/src/utils/authUtils.js`
- HSTS and security headers: `ssc-web-portal-backend-main/src/index.js`
- S3 signed URLs for file transfer: `ssc-web-portal-backend-main/src/utils/awsUtility.js`

## Logging, Monitoring, and Auditability
- Request logging: `ssc-web-portal-backend-main/src/index.js`
- Security event logging: `ssc-web-portal-backend-main/src/utils/supabaseLogger.js`
- Error handling and telemetry: `ssc-web-portal-backend-main/src/middlewares/error.js`

## Secure Development and Change Management
- CI/CD configs: `ssc-web-portal-backend-main/buildspec.yml`, `ssc-web-portal-backend-main/appspec.yml`
- Code quality gates: `ssc-web-portal-backend-main/.husky/`, `ssc-web-portal-backend-main/.eslintrc.json`
- Tests: `ssc-web-portal-backend-main/tests/`, `ssc-web-portal-backend-main/vitest.config.js`

## Data Retention
- Retention cron jobs: `ssc-web-portal-backend-main/src/configs/appConfigs.js`
- Document validity tracking: `ssc-web-portal-backend-main/src/routes/documentUpload/index.js`

## Rate Limiting and Abuse Prevention
- Rate limiters: `ssc-web-portal-backend-main/src/middlewares/rateLimiters.js`
- Sliding window storage: `ssc-web-portal-backend-main/src/middlewares/slidingRateLimiter.js`

## Notes and Gaps
- Organizational policies, training logs, risk registers, and audit evidence are not present in-repo and must be maintained outside the codebase.
