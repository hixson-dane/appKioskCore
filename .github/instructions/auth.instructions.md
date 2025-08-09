# Auth Service Implementation Instructions

## 1. Nx Project Structure
1. Use Nx generators to create the following projects under `services/auth/`:
    1. `api` (Fastify API application)
        - Example: `npx nx g @nx/fastify:app services/auth/api`
    2. `ui` (React microfrontend)
        - Example: `npx nx g @nx/react:app services/auth/ui`
    3. `models` (JSON-schema models ported to TypeScript)
        - Example: `npx nx g @nx/js:lib services/auth/models`
    4. `sdk` (TypeScript SDK for API calls)
        - Example: `npx nx g @nx/js:lib services/auth/sdk`

## 2. API Setup
1. Scaffold a Fastify API in `services/auth/api/`.
2. Use shared server configs from `shared/server`.
3. Organize API by feature/resource (e.g., `tenants/`, `oauth/`, `branding/`).
4. For each feature:
    1. Create `controller.ts`, `service.ts`, `repository.ts`, and `tests/`.
    2. Register all routes in the main Fastify server.

## 3. External Auth Providers
1. Implement factories for 3rd party providers (AWS Cognito, Fusion Auth).
2. Ensure providers can be swapped easily.

## 4. Theming & Branding
1. Add endpoints for customizing login UI per application/project.

## 5. OAuth & SAML Integration
1. Provide endpoints to generate/manage OAuth client credentials and SAML configs.

## 6. Tenant Management
1. Implement tenant creation and management APIs.
2. Allow applications to create OAuth credentials for service calls to core platform.

## 7. Testing
1. Write unit tests for controllers, services, and repositories.

## 8. Frontend
1. Scaffold a React microfrontend in `ui/` for login and management screens.

## 9. SDK
1. Implement TypeScript SDK for interacting with Auth API.

## 10. Documentation
1. Document API endpoints, models, and SDK usage.
