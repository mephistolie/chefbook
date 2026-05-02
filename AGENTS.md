# ChefBook Agents Guide

This repository is a workspace root that contains several project modules.

## Repository Map

- `chefbook-mobile` - primary mobile client
- `chefbook-backend` - Go backend with API gateway, common libraries, and microservices
- `chefbook-frontend` - web frontend stub / separate web app track
- `chefbook-graphics` - design assets and graphics sources

## How To Work In This Repository

- Start from the subproject you are changing instead of treating the whole repository as one codebase.
- Read the nearest `AGENTS.md` before making changes in a subdirectory.
- Keep changes scoped to the module that owns the behavior.
- Avoid cross-cutting refactors unless they are required for the task.
- Prefer module-local build and test commands over workspace-wide commands.
- Use `git switch` for branch changes; do not use `git checkout` to switch branches.

## Ownership Boundaries

- Mobile application work belongs under `chefbook-mobile`.
- Backend platform and service work belongs under `chefbook-backend`.
- Web frontend work belongs under `chefbook-frontend`.
- Graphics and static assets belong under `chefbook-graphics`.

## Subproject Instructions

- `chefbook-mobile/AGENTS.md` describes the Android/Kotlin multiplatform client.
- `chefbook-backend/AGENTS.md` describes backend-wide rules.
- `chefbook-backend/services/*/AGENTS.md` describe service-specific boundaries and expectations.

If a local instruction conflicts with a higher-level one, follow the more specific `AGENTS.md` in the directory you are editing.
