# Velocart Backend

A robust NestJS backend for the Velocart e-commerce platform with comprehensive authentication and user management features.

## Features

- 🔐 **Authentication System**
  - User registration with email verification
  - JWT-based authentication
  - Password reset functionality
  - Change password feature
  - Role-based access control

- 📧 **Email Integration**
  - Email verification for new accounts
  - Password reset emails
  - Configurable SMTP settings

- 🗄️ **Database Integration**
  - PostgreSQL with TypeORM
  - User entity with comprehensive fields
  - Automatic password hashing

- 📚 **API Documentation**
  - Swagger/OpenAPI documentation
  - Interactive API explorer
  - Comprehensive endpoint documentation

## Prerequisites

- Node.js 18+ 
- PostgreSQL 12+
- npm or yarn

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd velocart-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Environment Configuration**
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` with your configuration:
   ```env
   # Database
   DB_HOST=localhost
   DB_PORT=5432
   DB_USERNAME=your_username
   DB_PASSWORD=your_password
   DB_NAME=velocart
   
   # JWT
   JWT_SECRET=your-super-secret-jwt-key
   
   # Email (Gmail example)
   SMTP_HOST=smtp.gmail.com
   SMTP_PORT=587
   SMTP_USER=your-email@gmail.com
   SMTP_PASS=your-app-password
   SMTP_FROM=noreply@velocart.com
   
   # Frontend
   FRONTEND_URL=http://localhost:3000
   ```

4. **Database Setup**
   ```bash
   # Create PostgreSQL database
   createdb velocart
   ```

5. **Run the application**
   ```bash
   # Development mode
   npm run start:dev
   
   # Production mode
   npm run build
   npm run start:prod
   ```

## API Endpoints

### Authentication
- `POST /auth/login` - User login
- `POST /auth/refresh` - Refresh access token

### Users
- `POST /users` - Create new user (registration)
- `GET /users` - Get all users (admin only)
- `GET /users/profile` - Get current user profile
- `GET /users/:id` - Get user by ID
- `PATCH /users/:id` - Update user
- `DELETE /users/:id` - Delete user
- `POST /users/verify-email/:token` - Verify email address
- `POST /users/forgot-password` - Request password reset
- `POST /users/reset-password/:token` - Reset password
- `POST /users/change-password` - Change password

## API Documentation

Once the server is running, visit:
- **Swagger UI**: http://localhost:3001/api
- **API Base URL**: http://localhost:3001

## Authentication Flow

1. **Registration**
   - User registers with email, password, and personal info
   - Verification email is sent automatically
   - Account status is 'pending' until email is verified

2. **Email Verification**
   - User clicks link in verification email
   - Account status changes to 'active'
   - User can now log in

3. **Login**
   - User provides email and password
   - JWT token is returned on successful authentication
   - Token is valid for 24 hours

4. **Password Reset**
   - User requests password reset via email
   - Reset link is sent to user's email
   - User can set new password using the link

## Development

### Available Scripts

```bash
# Development
npm run start:dev     # Start in watch mode
npm run start:debug   # Start with debugger

# Production
npm run build         # Build the application
npm run start:prod    # Start production server

# Testing
npm run test          # Run unit tests
npm run test:watch    # Run tests in watch mode
npm run test:e2e      # Run end-to-end tests

# Code Quality
npm run lint          # Run ESLint
npm run format        # Format code with Prettier
```

### Project Structure

```
src/
├── auth/                 # Authentication module
│   ├── dto/             # Data transfer objects
│   ├── guards/          # Authentication guards
│   ├── strategies/      # Passport strategies
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   └── auth.module.ts
├── users/               # Users module
│   ├── dto/             # Data transfer objects
│   ├── entities/        # Database entities
│   ├── users.controller.ts
│   ├── users.service.ts
│   └── users.module.ts
├── mail/                # Email module
│   ├── mail.service.ts
│   └── mail.module.ts
├── app.module.ts        # Root module
└── main.ts             # Application entry point
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DB_HOST` | Database host | localhost |
| `DB_PORT` | Database port | 5432 |
| `DB_USERNAME` | Database username | postgres |
| `DB_PASSWORD` | Database password | password |
| `DB_NAME` | Database name | velocart |
| `JWT_SECRET` | JWT signing secret | - |
| `SMTP_HOST` | SMTP server host | smtp.gmail.com |
| `SMTP_PORT` | SMTP server port | 587 |
| `SMTP_USER` | SMTP username | - |
| `SMTP_PASS` | SMTP password | - |
| `SMTP_FROM` | From email address | noreply@velocart.com |
| `FRONTEND_URL` | Frontend application URL | http://localhost:3000 |
| `NODE_ENV` | Environment mode | development |
| `PORT` | Application port | 3001 |

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the ISC License.
