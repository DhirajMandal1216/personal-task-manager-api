# Personal Task Manager API

A REST API for managing personal tasks with user authentication,
role-based authorization, and full CRUD functionality.

## Features

- JWT-based authentication (register/login)
- Role-based authorization (admin vs user)
- Owner-based access control (users only access their own tasks)
- Task CRUD with status and priority filtering
- Input validation with Joi
- Security: Helmet, CORS, rate limiting
- Centralized error handling with custom error classes
- Environment-based error responses (development vs production)

## Tech Stack

- Node.js, Express 5
- MongoDB Atlas (Mongoose ODM)
- JWT (jsonwebtoken), bcrypt
- Joi (validation)
- Helmet, CORS, express-rate-limit (security)

## Project Structure

src/
├── server.js
├── app.js
├── config/
│ ├── db.js
│ └── cors.js
├── models/
│ ├── User.js
│ └── Task.js
├── routes/
│ ├── authRoutes.js
│ └── taskRoutes.js
├── controller/
│ ├── authController.js
│ └── taskController.js
├── service/
│ ├── authService.js
│ └── taskService.js
├── middleware/
│ ├── logger.js
│ ├── protect.js
│ ├── authorize.js
│ ├── validate.js
│ └── rateLimiter.js
├── validators/
│ ├── authValidator.js
│ └── taskValidator.js
└── errors/
└── AppError.js

## Environment Variables

Create a `.env` file in the project root with:

MONGO_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_jwt_secret
NODE_ENV=development
PORT=3000

**Never commit `.env` to version control.**

## Running Locally

```bash
npm install
npm run dev
```

## Deployment

Deployed on Render (free tier). Database hosted on MongoDB Atlas (free M0 tier).

Render automatically assigns PORT and sets NODE_ENV=production at runtime — these do not need to be set manually in Render's dashboard, only in local .env.

## Known Limitations

express-mongo-sanitize not used — incompatible with Express 5's read-only req.query.
Input safety currently relies on Joi validation only.
NoSQL-operator-shaped payloads (e.g. { "$gt": "" }) are not explicitly blocked.
Refresh tokens are implemented at a basic level (stateless, verified via jwt.verify() only). 
No database-tracked revocation or rotation yet — planned as a learning topic for a future project.
 
