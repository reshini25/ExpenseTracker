# ExpenseTracker

ExpenseTracker is a full-stack personal finance dashboard for recording income and expenses, reviewing spending trends, and keeping a clear view of your current financial position.

The project is split into a React/Vite frontend and a Node.js/Express API backed by MongoDB.

## Features

- Account registration and login with JWT authentication
- Protected dashboard with income, expense, balance, and savings summaries
- Add and delete income records
- Add and delete expense records with categories and emoji icons
- Recent transactions and last-30-days summaries
- Interactive charts for comparing income and expenses
- Profile image upload
- Excel downloads for income and expense records
- Responsive dashboard layout

## Tech Stack

### Frontend

- React 19
- Vite
- React Router
- Tailwind CSS
- Axios
- Recharts
- React Hot Toast

### Backend

- Node.js
- Express 5
- MongoDB with Mongoose
- JSON Web Tokens
- bcryptjs
- Multer for image uploads
- xlsx for spreadsheet exports

## Project Structure

```text
ExpenseTracker/
├── backend/
│   ├── config/          # Database connection
│   ├── controllers/     # Request handlers
│   ├── middleware/      # Authentication and upload middleware
│   ├── models/          # Mongoose models
│   ├── routes/          # API route definitions
│   └── server.js        # API entrypoint
├── frontend/
│   └── expense-tracker/ # React/Vite application
└── README.md
```

## Prerequisites

- Node.js 18 or newer
- npm
- MongoDB running locally or a MongoDB Atlas connection string

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/ExpenseTracker.git
cd ExpenseTracker
```

### 2. Configure the backend

```bash
cd backend
cp .env.example .env
npm install
```

On Windows PowerShell, use this instead of `cp`:

```powershell
Copy-Item .env.example .env
```

Update `.env` with your MongoDB connection string and a private JWT secret. The default API port is `8000`.

### 3. Configure the frontend

Open a second terminal from the repository root and install the frontend dependencies:

```bash
cd frontend/expense-tracker
npm install
```

The frontend is configured to call `http://localhost:8000` by default.

### 4. Run the applications

Start the backend:

```bash
cd backend
npm run dev
```

Start the frontend in a second terminal:

```bash
cd frontend/expense-tracker
npm run dev
```

Open the URL printed by Vite, usually `http://localhost:5173`.

For a production-style frontend build:

```bash
cd frontend/expense-tracker
npm run build
npm run preview
```

## Environment Variables

Create `backend/.env` from `backend/.env.example`:

| Variable | Required | Description |
| --- | --- | --- |
| `MONGO_URI` | Yes | MongoDB connection string |
| `JWT_SECRET` | Yes | Secret used to sign authentication tokens |
| `CLIENT_URL` | No | Frontend origin allowed by CORS; defaults to `*` |
| `PORT` | No | Backend port; defaults to `5000` in the server |

Do not commit `.env` files, database credentials, JWT secrets, or uploaded user files.

## API Overview

The API is served from the backend origin under `/api/v1`:

| Area | Base path | Purpose |
| --- | --- | --- |
| Authentication | `/api/v1/auth` | Register, login, user information, and image upload |
| Income | `/api/v1/income` | Create, list, delete, and export income |
| Expenses | `/api/v1/expense` | Create, list, delete, and export expenses |
| Dashboard | `/api/v1/dashboard` | Financial summaries and chart data |

Authenticated requests send the JWT in the `Authorization: Bearer <token>` header.

## Available Scripts

### Backend (`backend`)

- `npm start` starts the API with Node.js.
- `npm run dev` starts the API with Nodemon for development.

### Frontend (`frontend/expense-tracker`)

- `npm run dev` starts the Vite development server.
- `npm run build` creates a production build.
- `npm run preview` previews the production build locally.
- `npm run lint` runs ESLint.

## Troubleshooting

- **MongoDB connection failed:** confirm that MongoDB is running and `MONGO_URI` is correct.
- **Network error in the dashboard:** confirm the backend is running on port `8000`, or update the frontend API base URL in `frontend/expense-tracker/src/utils/apiPaths.js`.
- **CORS errors:** set `CLIENT_URL` to the exact frontend origin, such as `http://localhost:5173`.
- **Port already in use:** set a different `PORT` in `backend/.env` and update the frontend API base URL to match.

## Security Notes

This project is intended as a learning and portfolio application. Before deploying it publicly, add production-grade validation, rate limiting, secure cookie or token storage, stricter CORS configuration, request logging, and a managed file-storage strategy.

## License

No license has been selected for this project yet. Add a license file before accepting external contributions or redistributing the code.