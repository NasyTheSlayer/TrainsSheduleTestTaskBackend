# Train Schedule Application Backend

## Project Overview
This repository contains a backend application for a train schedule system built with NestJS and TypeScript. The application provides a RESTful API for managing train schedules with user authentication.

## Technologies
- **Framework**: [NestJS](https://nestjs.com/) (v10.3.8)
- **Language**: TypeScript
- **Database**: PostgreSQL
- **ORM**: TypeORM
- **Authentication**: JWT (JSON Web Tokens)

## Features

### 🔐 Authentication
- User registration and login
- JWT-based authentication with refresh tokens
- Secure password handling with bcrypt

### 🚆 Train Schedule Management
- Complete CRUD operations for trains
- Search functionality
- Pagination support

### 🛠️ API Design
- RESTful API following best practices
- Appropriate HTTP status codes
- Request validation with DTOs
- Standardized API response format

## Project Structure

```
src/
├── common/           # Shared components, filters, responses
├── configs/          # Application configuration
├── modules/
│   ├── auth/         # Authentication module
│   ├── postgres/     # Database connection module
│   ├── train/        # Train schedule management module
│   └── user/         # User management module
├── app.module.ts     # Main application module
├── main.ts           # Application entry point
└── setup-cors.ts     # CORS configuration
```

## Modules

### Auth Module
Handles user authentication with endpoints:
- `POST /auth/register` - Create a new user account
- `POST /auth/login` - Authenticate a user
- `POST /auth/refresh` - Refresh the access token

### Train Module
Core functionality for managing train schedules:
- `GET /trains` - List all trains with search and pagination
- `GET /trains/:id` - Get train by ID
- `POST /trains` - Create a new train
- `PUT /trains/:id` - Update a train (full update)
- `PATCH /trains/:id` - Update a train (partial update)
- `DELETE /trains/:id` - Delete a train

### User Module
Manages user-related operations.

## Data Models

### Train Entity
```typescript
@Entity()
export class Train {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  number: string;

  @Column()
  departure: string;

  @Column()
  destination: string;

  @Column()
  carrier: string;

  @Column('timestamp')
  departureTime: Date;

  @Column('timestamp')
  arrivalTime: Date;

  @CreateDateColumn()
  createdAt: Date;
}
```

### User Entity
```typescript
@Entity()
export class User {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column({ unique: true })
  email: string;

  @Column()
  password: string;
  
  @CreateDateColumn()
  createdAt: Date;
  
  @UpdateDateColumn()
  updatedAt: Date;
}
```

## Running the Application

### Installation
```bash
$ npm install
```

### Starting the Database
```bash
$ npm run start:docker:db
```

### Running the App
```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

### Testing
```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Environment Configuration
The application uses environment variables for configuration. Key variables include:
- `APP_PORT` - Application port (default: 8080)
- `APP_HOST` - Application host (default: 0.0.0.0)
- `DB_PORT` - Database port (default: 5432)
- `DB_HOST` - Database host
- `DB_USERNAME` - Database username
- `DB_PASSWORD` - Database password
- `DB_NAME` - Database name
- `JWT_ACCESS_SECRET` - JWT access token secret
- `JWT_ACCESS_EXPIRES_IN` - JWT access token expiration (default: 1h)
- `JWT_REFRESH_SECRET` - JWT refresh token secret
- `JWT_REFRESH_EXPIRES_IN` - JWT refresh token expiration (default: 30d)

## Development Tools
- ESLint and Prettier for code quality
- Husky for Git hooks
- TypeORM migrations for database schema management
