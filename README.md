 Late Show API Challenge
A Flask REST API for managing a late night TV show system with guests, episodes, and appearances.

Features
JWT Authentication - Secure user registration/login

TV Show Management - Full CRUD for:

Guests

Episodes

Appearances (guest + episode combinations)

PostgreSQL - Robust database backend

Protected Routes - Token-based security for sensitive operations

Requirements
Python 3.8+

PostgreSQL (running locally)

Pipenv (recommended)

Project Structure
bash
.
├── server/
│   ├── app.py               # Main application
│   ├── config.py            # Configuration
│   ├── seed.py              # Database seeding
│   ├── models/              # Database models
│   │   ├── __init__.py
│   │   ├── guest.py
│   │   ├── episode.py
│   │   ├── appearance.py
│   │   └── user.py
│   └── controllers/         # Route controllers
│       ├── __init__.py
│       ├── guest_controller.py
│       ├── episode_controller.py
│       ├── appearance_controller.py
│       └── auth_controller.py
├── migrations/              # Database migrations
├── challenge-4-lateshow.postman_collection.json  # Postman tests
└── README.md
Deployment Guide
1. GitHub Setup
bash
git init
git remote add origin https://github.com/yourusername/late-show-api-challenge.git
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
2. Environment Setup
bash
# Install dependencies
pipenv install flask flask_sqlalchemy flask_migrate flask-jwt-extended psycopg2-binary
pipenv shell

# Create PostgreSQL database
psql -c "CREATE DATABASE late_show_db;"
3. Configuration
server/config.py

python
SQLALCHEMY_DATABASE_URI = "postgresql://yourusername:yourpassword@localhost:5432/late_show_db"
.env file

bash
echo "DATABASE_URL=postgresql://postgres:yourpassword@localhost:5432/late_show_db" > .env
echo "JWT_SECRET_KEY=your-unguessable-secret-key" >> .env
echo "FLASK_APP=server.app" >> .env
echo "FLASK_ENV=development" >> .env
4. Database Initialization
bash
flask db init
flask db migrate -m "initial migration"
flask db upgrade
python server/seed.py  # Optional seeding
5. Run the Server
bash
flask run --port 5555
Testing with Postman
Import the provided challenge-4-lateshow.postman_collection.json

Authentication Flow:

Register → Login → Use token for protected routes

Sample Requests:

json
// Registration
POST /register
{
  "username": "testuser",
  "password": "testpass123"
}

// Login
POST /login
{
  "username": "testuser",
  "password": "testpass123"
}

// Create Appearance (protected)
POST /appearances
{
  "rating": 4,
  "guest_id": 1,
  "episode_id": 1
}
Troubleshooting
Database Issues:

Verify PostgreSQL service is running

Double-check credentials in .env and config.py

Migrations:

Delete migrations folder and re-run flask db init if needed

Technologies Used
Python 3.8

Flask

PostgreSQL

Flask-JWT-Extended

SQLAlchemy
