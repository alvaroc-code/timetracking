# TimeTrack

A time tracking application for managing employee work hours, time entries, and holiday requests.

## Features

- **Time Tracking**: Clock in/out, track work hours, break durations
- **Holiday Management**: Request and approve vacation days
- **User Management**: Admin panel for managing employees
- **Reports**: Monthly work hours and holiday summaries
- **Audit Log**: Track all changes for compliance
- **RGPD Compliance**: Data privacy consent management
- **RESTful API**: JSON API for integration

## Technology Stack

| Component | Technology |
|-----------|------------|
| Backend | Python 3 / Flask |
| Database | MySQL |
| Frontend | HTML5 / Jinja2 Templates |
| Containerization | Docker / Docker Compose |
| Web Server | Nginx (production) |
| Authentication | Session-based + Bearer Token (API) |

### Python Dependencies

- `flask` - Web framework
- `flask-cors` - CORS support for API
- `mysql-connector-python` - MySQL database driver
- `python-dotenv` - Environment variable management
- `bcrypt` - Password hashing

## Project Structure

```
timetracking/
├── app.py                 # Main Flask application
├── db.py                  # Database connection pool
├── requirements.txt       # Python dependencies
├── docker-compose.yml     # Docker orchestration
├── Dockerfile             # Application container
├── nginx.conf             # Nginx configuration
├── entrypoint.sh          # Container startup script
├── init.sql                # Database initialization
├── api/
│   └── __init__.py        # REST API blueprint
├── templates/              # HTML Jinja2 templates
│   ├── layout.html        # Base template
│   ├── login.html         # Login page
│   ├── dashboard.html     # User dashboard
│   ├── entries.html       # Time entries list
│   ├── holidays.html      # Holiday requests
│   ├── profile.html       # User profile
│   └── admin_*.html       # Admin panel templates
├── frontend/
│   └── install.html       # Installation page
└── backup/                # Database backups
```

## Quick Start

### Prerequisites

- Docker and Docker Compose
- (Optional) Python 3.8+ for local development

### Using Docker (Recommended)

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd timetracking
   ```

2. Create a `.env` file with your configuration:
   ```bash
   cp .env.example .env
   # Edit .env with your database credentials
   ```

3. Start the application:
   ```bash
   docker-compose up -d
   ```

4. Access the application at `http://localhost:8080`

### Local Development

1. Install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   # or: venv\Scripts\activate  # Windows
   pip install -r requirements.txt
   ```

2. Set up MySQL database and create `.env`:
   ```bash
   cp .env.example .env
   # Configure database connection in .env
   ```

3. Run the application:
   ```bash
   python app.py
   ```

4. Access at `http://localhost:8080`

## Default Credentials

After first run, use these credentials to log in:

| Role | Email | Password |
|------|-------|----------|
| Admin | admin@timetrack.es | admin123 |
| Employee | user@timetrack.es | user123 |

**Important**: Change these passwords immediately in production!

## API Documentation

### Authentication

```bash
# Login
POST /api/auth/login
Content-Type: application/json

{"email": "user@example.com", "password": "password"}

# Response
{"success": true, "data": {"user_id": 1, "token": "1:1234567890", ...}}
```

### Time Entries

```bash
# List entries
GET /api/entries?month=3&year=2026

# Clock in
POST /api/entries

# Clock out
POST /api/entries/1/clock-out
Content-Type: application/json
{"task_description": "Completed feature X"}

# Update entry
PUT /api/entries/1
Content-Type: application/json
{"start_time": "09:00", "end_time": "17:30", "break_duration": 30}

# Delete entry
DELETE /api/entries/1
```

### Holidays

```bash
# List holidays
GET /api/holidays

# Create request
POST /api/holidays
Content-Type: application/json
{"start_date": "2026-04-01", "end_date": "2026-04-05", "days_count": 5}
```

### Admin Endpoints

```bash
# Users
GET    /api/admin/users
POST   /api/admin/users
PUT    /api/admin/users/:id
DELETE /api/admin/users/:id

# Entries
GET    /api/admin/entries
PUT    /api/admin/entries/:id
POST   /api/admin/entries/:id/approve

# Holidays
GET    /api/admin/holidays
PUT    /api/admin/holidays/:id

# Reports
GET    /api/admin/reports?year=2026&month=3
```

## Configuration

Environment variables (see `.env`):

| Variable | Description | Default |
|----------|-------------|---------|
| `DB_HOST` | MySQL host | localhost |
| `DB_PORT` | MySQL port | 3306 |
| `DB_NAME` | Database name | timetrack |
| `DB_USER` | Database user | timetrack |
| `DB_PASSWORD` | Database password | - |
| `SECRET_KEY` | Flask secret key | timetrack-secret-key-change-in-production |
| `SESSION_COOKIE_SECURE` | Secure cookies (HTTPS) | False |

## License

MIT License

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=flat-square&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.0-000000?style=flat-square&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-24.0-2496ED?style=flat-square&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-1.24-009639?style=flat-square&logo=nginx&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=flat-square&logo=bootstrap&logoColor=white)
