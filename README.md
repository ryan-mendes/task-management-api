# Task Management API

REST API for managing tasks, built with NestJS and PostgreSQL. Users authenticate with JWT and can create, update, filter and delete their tasks.

![NestJS](https://img.shields.io/badge/NestJS-10-E0234E?logo=nestjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white)

## Features

- Task CRUD with filtering by title and status
- User registration and JWT authentication (global guard)
- Password hashing with bcrypt
- DTO validation with `class-validator`
- Schema versioning with TypeORM migrations
- Environment-based configuration via `ConfigService`

## Tech stack

| Layer | Technology |
|---|---|
| Framework | NestJS 10 |
| Language | TypeScript |
| Database | PostgreSQL + TypeORM |
| Auth | `@nestjs/jwt`, bcrypt |
| Infra | Docker Compose |

## Project structure

```
src/
├── auth/       # Login endpoint, JWT guard
├── users/      # User registration
├── task/       # Task controller, service and DTOs
└── db/         # Entities, migrations and TypeORM config
```

## Getting started

**Requirements:** Node.js 18+, Docker

```bash
git clone https://github.com/ryan-mendes/task-management-api.git
cd task-management-api
npm install
cp .env.example .env
docker compose up -d        # starts PostgreSQL
npm run migration:run
npm run start:dev           # http://localhost:3000
```

## API

All `/task` routes require `Authorization: Bearer <token>`.

| Method | Route | Description |
|---|---|---|
| POST | `/users` | Create a user |
| POST | `/auth/login` | Authenticate and receive a JWT |
| POST | `/task` | Create a task |
| GET | `/task` | List tasks (`?title=&status=`) |
| GET | `/task/:id` | Get a task by id |
| PUT | `/task/:id` | Update a task |
| DELETE | `/task/:id` | Delete a task |

Example:

```bash
curl -X POST http://localhost:3000/task \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title":"Write docs","description":"API reference","status":"TO_DO","expirationDate":"2025-01-31"}'
```

## Migrations

```bash
npm run migration:create -name=migration-name
npm run migration:run
npm run migration:revert
```

## Credits

Built as a NestJS study project based on the original proposal by [deyvissonbrenoveras/task-management-api](https://github.com/deyvissonbrenoveras/task-management-api).
