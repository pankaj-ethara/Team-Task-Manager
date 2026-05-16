# Team Task Manager

A full-stack team task management web app with authentication, role-based access, projects, teams, task tracking, comments, notifications, activity history, dashboard analytics, calendar view, and user profile management.

## Features

- User registration and login with JWT authentication
- First registered user automatically becomes an admin
- Role-based access for admins and members
- Dashboard with project counts, task stats, charts, upcoming tasks, and recent activity
- Project management with members, status, priority, dates, progress, and project task boards
- Task management with Kanban and list views
- Task assignment, priorities, due dates, status updates, and comments
- Team management with team members and roles
- Global search for tasks, projects, and teams
- Notifications for assigned tasks
- Activity feed for key workspace events
- Calendar view for task due dates
- Profile editing, avatar color selection, and password updates
- Admin user management

## Tech Stack

- Backend: Node.js, Express
- Frontend: HTML, CSS, vanilla JavaScript
- Database: SQL.js persisted to `data/taskmanager.db`
- Authentication: JSON Web Tokens
- Security and middleware: Helmet, CORS, compression, rate limiting
- Charts: Chart.js

## Project Structure

```text
team-task-manager/
+-- data/
|   +-- taskmanager.db
+-- middleware/
|   +-- auth.js
+-- public/
|   +-- css/
|   |   +-- style.css
|   +-- js/
|   |   +-- app.js
|   |   +-- pages.js
|   +-- index.html
+-- routes/
|   +-- auth.js
|   +-- dashboard.js
|   +-- projects.js
|   +-- tasks.js
|   +-- teams.js
|   +-- users.js
+-- database.js
+-- package.json
+-- server.js
```

## Requirements

- Node.js 18 or newer
- npm

## Getting Started

Install dependencies:

```bash
npm install
```

Start the app:

```bash
npm start
```

Or:

```bash
node server.js
```

Open the app in your browser:

```text
http://localhost:3000
```

On Windows PowerShell, if `npm` is blocked by script execution policy, use:

```powershell
npm.cmd start
```

## Environment Variables

The app works without a `.env` file, but these values can be configured:

```text
PORT=3000
DB_PATH=./data/taskmanager.db
JWT_SECRET=replace-this-secret-in-production
```

Important: set a strong `JWT_SECRET` before using this app in a real environment.

## Database

The app uses SQL.js and persists the database file to:

```text
data/taskmanager.db
```

Tables are created automatically on startup if they do not already exist.

## Authentication and Roles

- Users register with name, email, and password.
- Passwords are hashed with bcrypt.
- JWT tokens are stored in browser local storage.
- The first registered user is assigned the `admin` role.
- Admin users can manage all users and see broader workspace data.
- Member users can access projects, teams, and tasks they are part of or created.

## Main API Routes

```text
POST   /api/auth/register
POST   /api/auth/login
GET    /api/auth/me
PUT    /api/auth/profile
PUT    /api/auth/password

GET    /api/dashboard/stats
GET    /api/dashboard/notifications
PUT    /api/dashboard/notifications/:id/read
PUT    /api/dashboard/notifications/read-all
GET    /api/dashboard/activity
GET    /api/dashboard/search
GET    /api/dashboard/calendar

GET    /api/projects
POST   /api/projects
GET    /api/projects/:id
PUT    /api/projects/:id
DELETE /api/projects/:id
POST   /api/projects/:id/members
DELETE /api/projects/:id/members/:userId
GET    /api/projects/:id/tasks

GET    /api/tasks
POST   /api/tasks
GET    /api/tasks/:id
PUT    /api/tasks/:id
DELETE /api/tasks/:id
GET    /api/tasks/:id/comments
POST   /api/tasks/:id/comments
DELETE /api/tasks/:id/comments/:commentId

GET    /api/teams
POST   /api/teams
GET    /api/teams/:id
PUT    /api/teams/:id
DELETE /api/teams/:id
POST   /api/teams/:id/members
DELETE /api/teams/:id/members/:userId

GET    /api/users
GET    /api/users/:id
PUT    /api/users/:id/role
DELETE /api/users/:id
```

## Health Check

```text
GET /health
```

Returns a simple JSON response confirming that the server is running.

## Notes

- This project serves the frontend from the `public` directory.
- The frontend is a single-page-style app rendered with vanilla JavaScript.
- The database file is local to the project and should be backed up before clearing the `data` folder.
- For production use, configure a strong `JWT_SECRET`, review CORS settings, and use a production-ready persistent database.
