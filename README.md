# DriveCare – Vehicle Care Reminder System

A starter full-stack project for managing cars, maintenance reminders, service history, fuel records and expenses.

## Technology
- Frontend: HTML, CSS, JavaScript (hosted on Netlify)
- Backend: PHP 8+ JSON API
- Database: MySQL

## Project structure
- `database.sql` – creates the MySQL database and tables
- `api/index.php` – registration, login and CRUD API
- `api/config.php` – database connection configuration using environment variables
- `frontend/drivecare-api.js` – JavaScript helper for calling the API
- `README_SETUP.txt` – detailed local and hosting setup instructions

## Important before publishing
- Never commit real database passwords, API secrets, or production credentials.
- Keep the database on a PHP/MySQL hosting provider; Netlify hosts the frontend only.
- Configure `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASS`, and `FRONTEND_ORIGIN` as environment variables on the PHP host.
- Change `API_BASE` in `frontend/drivecare-api.js` to your actual HTTPS PHP API URL.
- This is a starter backend package. It has not yet been deployed or connected to the live Netlify site.

## Setup
See [`README_SETUP.txt`](README_SETUP.txt) for step-by-step instructions.
