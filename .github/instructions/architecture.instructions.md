# AppKiosk Core Platform

## Core Platform Architecture

The AppKiosk Core platform is a PaaS platform designed to help development teams get their application out the door as quickly as possible. 

### Key Values of the Core Platform

1. Flexibility is Key
2. Decoupled Services are the key to faster development
3. Simple solutions lead to simple software
4. When utilizing external services, create factories so that these services can be swapped out easily.

### Services Provided by the Core Development Platform

- Auth Service
    - Provides User Pool or Tenant for applications
    - Will use 3rd party provider for actual user storage and authentication
        - AWS Cognito
        - Fusion Auth
    - Allows applications/projects to theme and brand their login
    - Provides Oauth Client credentials or SAML configs to allow integration to application's APIs and resources
    - Allows Applications to create and manage their tenant including creating OAuth credentials for service calls to the core platform itself.
- Account Management Service
    - Keeps track of an account in the core system.
    - An account is an entity that will be billed by the core platform for resources used.
    - Keeps track of projects and applications that belong to an account
- Users Service
    - Allows projects and applications to keep metadata about the users that are a part of that project/application
    - Needs to be flexible to allow for any metadata that the applications need to store about the user.
    - User is tied to an account and a project. This means a user could have duplicate entries in the system.
- Permissions Service
    - Allows projects and applications to manage permissions using RBAC
    - Allow projects to add hooks into the auth service to have permissions added to tokens at login.
        - Max permissions enforced to prevent a token from getting to larg
    - Provide cached endpoints for non-token permissions
- Licensing Service
    - Allows projects and applications to manage licenses.
    - Flexible to allow custom entitlements
    - Applied to any entity (organization, user, device)
    - Multiple ways to enforce
        - License Key
        - Token/user login
        - Certificates
- Billing Service
    - Allows projects and applications to bill customers for their services
    - Licensed-based
    - Subscription-based
    - One time payments
    - Payment processor

### NX structure

The Core platform uses nx for the monorepo management. The monorepo will be structured accourdinglu

```
services/
    {service_name}/
        api/ (api application project)
        ui/ (microfrontend application project)
        models/ (shared js library containing models)
        sdk/ (shared js library containing sdk)
shared/
    server/ (shared js library containing shared fastify server elements)
    logging/ (shared js library containing logging configs)
    util/ (shared js library containing shared utilities)
    sdk/ (shared js library containing common sdk utilities, i.e http client)
```

- APIs will all be fastify apis and share some common configs through a shared server library
- Frontends will be microfrontends build in react
- Models will be written in json-schema but ported to typescript. This allows for the models to be used for both compile-time type safety as well as runtime validation in fastify. 
- SDKs will have common functions for calling the APIs. These will begin with Typescript SDKs but could be ported to other languages as need requires.

### API structure

The APIs will be feature/resource based. This means that each feature/resource will receive its own directory. Inside that directory will have all the files related to that feature/resouce. For example: 

```
users/
    controller.ts (contains route/request/validation/respons logic)
    service.ts (contains business logic)
    repository.ts (contains data layer logic)
    tests/
        controller.spec.ts (contains controller tests)
        service.spec.ts (contains service tests)
        repository.ts (contains repository tests)
```

All routes in the controllers will be registered in the main fastify server to keep things modular.