# PulseMeet

PulseMeet is a web video-meeting application built with React, Express, Socket.IO, and MongoDB. It includes account registration and login, meeting rooms, meeting history, and in-call features such as chat and screen sharing.

## Requirements

- Node.js and npm
- MongoDB Community Server running locally, or a MongoDB Atlas cluster
- A modern browser with camera and microphone access for video calls

## Getting started

Install dependencies and start the backend and frontend in separate terminals.

### 1. Configure MongoDB

The backend connects to MongoDB in `backend/src/app.js`. Set the URI passed to `mongoose.connect(...)` to your database connection string before starting the backend.

For a local MongoDB Community Server using the default port, the URI can be:

```text
mongodb://127.0.0.1:27017/pulsemeet
```

For MongoDB Atlas, use the URI provided by Atlas. Keep database credentials private and do not commit them to source control. The backend currently reads the connection string directly from `app.js`; it does not load a `.env` file.

### 2. Start the backend

From the project directory:

```bash
cd backend
npm install
npm run dev
```

The backend listens on port `8000` by default. The `PORT` environment variable can be used to choose another port.

### 3. Start the frontend

Open another terminal in the project directory:

```bash
cd frontend
npm install
npm start
```

The React development server normally opens at [http://localhost:3000](http://localhost:3000). The frontend is configured to connect to the backend at `http://localhost:8000` in `frontend/src/environment.js`.

## Using the app

1. Open the frontend in your browser and register an account or log in.
2. Join a meeting using a meeting code.
3. Allow camera and microphone access when prompted. Use `localhost` or HTTPS for browser media permissions.
4. Use the meeting controls for available call features, including chat and screen sharing.
5. Open meeting history from the home screen to view saved meeting codes.

## Project structure

```text
PulseMeet/
├── backend/
│   ├── src/
│   │   ├── controllers/   # User endpoints and Socket.IO signaling
│   │   ├── models/        # MongoDB user and meeting models
│   │   ├── routes/        # Express API routes
│   │   └── app.js         # Express server and MongoDB connection
│   └── package.json
└── frontend/
    ├── public/
    ├── src/
    │   ├── contexts/      # Authentication and API state
    │   ├── pages/         # App pages and meeting interface
    │   └── environment.js # Backend URL
    └── package.json
```

## API routes

The backend mounts user routes at `/api/v1/users`:

| Method | Route | Purpose |
| --- | --- | --- |
| `POST` | `/login` | Log in with a username and password |
| `POST` | `/register` | Create an account |
| `POST` | `/add_to_activity` | Save a meeting code to user history |
| `GET` | `/get_all_activity` | Retrieve meeting history |

## Available scripts

Run these commands from the relevant package directory:

| Directory | Command | Purpose |
| --- | --- | --- |
| `backend` | `npm run dev` | Start the backend with automatic restart |
| `backend` | `npm start` | Start the backend |
| `frontend` | `npm start` | Start the React development server |
| `frontend` | `npm test` | Run frontend tests |
| `frontend` | `npm run build` | Create a production frontend build |
