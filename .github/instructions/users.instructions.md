# Users Service Implementation Instructions

## 1. Nx Project Structure
1. Use Nx generators to create the following projects under `services/users/`:
    1. `api` (Fastify API application)
        - Example: `npx nx g @nx/fastify:app services/users/api`
    2. `ui` (React microfrontend)
        - Example: `npx nx g @nx/react:app services/users/ui`
    3. `models` (JSON-schema models ported to TypeScript)
        - Example: `npx nx g @nx/js:lib services/users/models`
    4. `sdk` (TypeScript SDK for API calls)
        - Example: `npx nx g @nx/js:lib services/users/sdk`

## 2. API Setup
1. Scaffold a Fastify API in `services/users/api/`.
2. Use shared server configs from `shared/server`.
3. Organize API by feature/resource (e.g., `users/`, `metadata/`).
4. For each feature:
    1. Create `controller.ts`, `service.ts`, `repository.ts`, and `tests/`.
    2. Register all routes in the main Fastify server.

## 3. User Metadata
1. Design flexible models to allow arbitrary metadata per user.
2. Ensure users are tied to both account and project (allow duplicates).

## 4. Testing
1. Write unit tests for controllers, services, and repositories.

## 5. Frontend
1. Scaffold a React microfrontend in `ui/` for user management screens.

## 6. SDK
1. Implement TypeScript SDK for interacting with Users API.

## 7. Documentation
1. Document API endpoints, models, and SDK usage.
