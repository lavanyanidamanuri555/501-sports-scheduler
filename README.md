# 501 Sports Scheduler

## About the Project
The **501 Sports Scheduler** is a web application designed to streamline sports session management. It allows users to register, create, join, and manage sports sessions efficiently. There are two primary user roles: **Admins** and **Players**. Admins can oversee sports activities, manage sessions, and analyze reports, while players can participate in available sessions. The platform is built with **Node.js, Express, PostgreSQL, and bcryptjs**, utilizing **EJS** for rendering dynamic web pages.

## Core Functionalities
- **User Registration & Authentication**: Secure login and account management.
- **Admin Dashboard**: Admins can manage sports, schedule sessions, and analyze participation reports.
- **Player Dashboard**: Players can view, join, and leave available sessions.
- **Session Management**: Admins can create, modify, or cancel sessions; players can enroll or withdraw.
- **Analytics & Reporting**: Admins gain insights into sports session participation.

## Technology Stack
- **Node.js** - Server-side JavaScript runtime.
- **Express.js** - Web application framework.
- **bcryptjs** - Password encryption for security.
- **PostgreSQL** - Relational database for storing sports and user data.
- **EJS** - Template engine for rendering dynamic HTML pages.
- **express-session** - User session management.

## How to Set Up

### Prerequisites
- Install **Node.js** (>=14.x)
- Install **npm** (Node Package Manager)
- Install **PostgreSQL** (>=12.x)

### Installation Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/lavanyanidamanuri555/501-sports-scheduler.git
   ```
2. Navigate to the project directory:
   ```bash
   cd 501-sports-scheduler
   ```
3. Install the required dependencies:
   ```bash
   npm install
   ```
4. Set up the PostgreSQL database:
   - Create a database (e.g., `sports_scheduler`).
   - Update database configurations in `database.js`.
   - Run the SQL schema setup:
   
   ```sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100) UNIQUE NOT NULL,
     password VARCHAR(255) NOT NULL,
     role VARCHAR(50) CHECK (role IN ('admin', 'player')) NOT NULL
   );

   CREATE TABLE sports (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100) NOT NULL
   );

   CREATE TABLE sessions (
     id SERIAL PRIMARY KEY,
     sport_id INT REFERENCES sports(id),
     creator_id INT REFERENCES users(id),
     team1 VARCHAR(100),
     team2 VARCHAR(100),
     additional_players INT DEFAULT 0,
     date TIMESTAMP,
     venue VARCHAR(255),
     cancelled BOOLEAN DEFAULT FALSE,
     cancellation_reason TEXT
   );

   CREATE TABLE session_players (
     session_id INT REFERENCES sessions(id),
     player_id INT REFERENCES users(id),
     PRIMARY KEY (session_id, player_id)
   );
   ```
5. Start the application:
   ```bash
   npm start
   ```
   The server will be accessible at `http://localhost:3000`.

## API Endpoints

- `GET /`: Home page
- `GET /login`: User login page
- `POST /login`: Authenticate user
- `GET /register`: Registration page
- `POST /register`: Create a new user account
- `GET /admin-dashboard`: Admin panel for sports and session management
- `POST /create-sport`: Admin action to add a new sport
- `POST /delete-session`: Remove a session
- `GET /player-dashboard`: View available sports sessions
- `POST /create-session`: Admin creates a sports session
- `POST /join-session`: Players join a session
- `POST /cancel-session`: Admin cancels a session
- `GET /reports`: View session participation statistics

## User Access Levels

### Admin Privileges:
- Create and modify sports sessions
- Generate reports on session popularity
- Cancel or delete sessions as needed

### Player Capabilities:
- Sign up and log in
- View available sports sessions
- Join or leave a session
- Check session details and participants

## Security Measures
- **Password Encryption**: Securely hashed with bcryptjs.
- **Session Management**: User authentication with express-session.

## Contribution Guidelines
We welcome contributions! Follow these steps to contribute:
- Fork the repository.
- Implement new features or bug fixes.
- Submit a pull request for review and potential integration.
