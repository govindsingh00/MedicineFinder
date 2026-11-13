# Medicine Finder 💊

A web-based medicine discovery platform built with **Python, Flask, MySQL/MariaDB, and Bootstrap**. The application allows visitors to search medicines and view the medical stores associated with matching records. It also provides separate account areas for administrators and medical-store users to manage store information and medicine listings.

> **Project type:** Academic / learning project  
> **Backend:** Flask (Python)  
> **Database:** MySQL / MariaDB  
> **Frontend:** HTML, CSS, Bootstrap, JavaScript, jQuery

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [User Roles](#user-roles)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [How the Application Works](#how-the-application-works)
- [Database Design](#database-design)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Running the Project](#running-the-project)
- [Deployment](#deployment)
- [Security Notes](#security-notes)
- [Limitations and Future Improvements](#limitations-and-future-improvements)
- [Contributing](#contributing)
- [Author](#author)
- [License](#license)

---

## Overview

Medicine Finder is designed to make it easier to locate medicine listings available at registered medical stores. A visitor can search by medicine name and see matching medicine details along with the associated medical-store information.

The application has role-based areas for:

- **Administrators:** manage administrator and medical-store records, and access administrative functions.
- **Medical-store users:** manage their store profile and maintain their medicine listings.
- **Visitors:** search the available medicine records without signing in.

The project demonstrates server-side web development, database connectivity, session-based authentication, CRUD operations, file uploads, and server-rendered pages using Flask and Jinja templates.

## Features

### Public medicine search
- Search for medicines by name.
- Display matching medicine records.
- Show associated medical-store details for matching results.
- Display a message when no matching records are found.

### Authentication and sessions
- Login using an email address and password.
- Distinguish between administrator and medical-store accounts.
- Use Flask sessions to maintain the signed-in user's role and email.
- Logout and clear the active session.
- Restrict selected pages according to the signed-in user's role.

### Administrator area
- Administrator registration.
- View administrator records.
- View registered medical stores.
- Access an administrator dashboard.
- Edit administrator profile information.
- Change the administrator password.
- Upload or change an administrator profile photo.
- Manage medical-store records through the available edit and delete pages.

### Medical-store area
- Medical-store registration (through the administrator area).
- Access a medical-store dashboard.
- Edit store information.
- Change the medical-store account password.
- Upload or change the store photo.
- Add medicine records.
- View medicine listings.
- Edit and delete medicine records.

### Interface
- Flask/Jinja server-rendered HTML pages.
- Bootstrap-based styling and static CSS assets.
- JavaScript and jQuery assets for browser-side interactions.

## User Roles

| Role | Main capabilities |
|---|---|
| Visitor | Search medicines and view matching store information |
| Administrator | Access admin pages, manage store records, and maintain administrator profile details |
| Medical-store user | Maintain store details and manage medicine listings associated with the store |

Some management pages require an authenticated session and the appropriate account role.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Flask | Web application framework and routing |
| PyMySQL | Python-to-MySQL/MariaDB database connectivity |
| MySQL / MariaDB | Relational database |
| HTML5 | Page structure |
| CSS3 | Styling |
| Bootstrap | Responsive UI components and layout |
| JavaScript | Client-side interactions |
| jQuery | Browser-side scripting support |
| Jinja2 | Flask template rendering |
| Werkzeug | Secure filename utility for uploaded files |
| Gunicorn | WSGI server configuration for deployment |

## Project Structure

```text
MedicineFinder/
├── app.py                       # Flask application, routes, and request handling
├── mylib.py                     # Database connection and photo helper functions
├── requirements.txt             # Python dependencies
├── Procfile                     # Gunicorn start command for supported hosts
├── medicine finder.sql          # MySQL/MariaDB database schema and sample data
├── templates/                   # Jinja/HTML pages
│   ├── Home.html                 # Public home and medicine search page
│   ├── login.html                # Login page
│   ├── Admin*.html               # Administrator pages
│   ├── Medical*.html             # Medical-store pages
│   └── ...                       # Medicine, listing, edit, and status pages
└── static/
    ├── css/                      # Stylesheets and Bootstrap styles
    ├── jquery/                   # JavaScript libraries
    ├── images/                   # Interface images
    └── photos/                   # Uploaded administrator photos
```

The application also refers to `static/medicalphotos/` for medical-store photos. Create this directory before using medical-store photo uploads if it is not already present.

## How the Application Works

1. A visitor opens the home page and submits a medicine-name search.
2. Flask receives the search request and queries the `medicine_medical` database view.
3. The view combines medicine information with the medical store associated with each medicine record.
4. Matching records are passed to the relevant Jinja template and rendered in the browser.
5. An administrator or medical-store user signs in through the login page.
6. Flask checks the account record and stores the account email and user role in the session.
7. The user is redirected to the appropriate role-specific dashboard.
8. Authorized users can manage the records available to their role.

## Database Design

The supplied SQL script creates a database named **`govind`** and defines the following tables and view:

| Table / View | Purpose |
|---|---|
| `login_data` | Login email, password, and user type |
| `admin_data` | Administrator profile details |
| `medical_data` | Medical-store details and photo filename |
| `medicine_data` | Medicine name, company, batch/lot number, price, remarks, and store email |
| `photo_data` | Administrator photo information |
| `st_data` | Student data included in the supplied SQL dump |
| `medicine_medical` (view) | Joins medicine and medical-store data for search/display |

The `medicine_medical` view joins `medicine_data.email_medical` with `medical_data.email`. This allows medicine search results to include the store's details.

### Import the database

1. Start your MySQL or MariaDB server.
2. Open MySQL Workbench, phpMyAdmin, or a terminal client.
3. Import the supplied `medicine finder.sql` file.
4. Confirm that the `govind` database and its tables/view have been created.

Example using the MySQL command-line client:

```bash
mysql -u YOUR_DB_USER -p < "medicine finder.sql"
```

The SQL dump contains sample records. Review and replace those records with your own test data before publishing or deploying the project.

## Getting Started

### Prerequisites

Install the following before running the project:

- Python 3.9 or a compatible Python version.
- pip.
- MySQL or MariaDB.
- Git (optional, for cloning the repository).

### 1. Clone the repository

```bash
git clone https://github.com/govindsingh00/MedicineFinder.git
cd MedicineFinder
```

Alternatively, download and extract the project ZIP.

### 2. Create a virtual environment

**Windows (Command Prompt):**

```bat
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

The supplied `requirements.txt` includes packages beyond those directly imported by this application. For a smaller installation, the core runtime packages used by the current source are Flask, PyMySQL, and Werkzeug. Gunicorn is used by the included deployment `Procfile`.

### 4. Configure the database

The database helper in `mylib.py` reads these environment variables:

| Variable | Description | Example |
|---|---|---|
| `MYSQLHOST` | Database host | `localhost` |
| `MYSQLUSER` | Database username | `root` |
| `MYSQLPASSWORD` | Database password | `your_password` |
| `MYSQLPORT` | Database port | `3306` |
| `MYSQLDATABASE` | Database name | `govind` |

Set the values for your own local database. Do not commit real passwords to GitHub.

**Windows Command Prompt example:**

```bat
set MYSQLHOST=localhost
set MYSQLUSER=root
set MYSQLPASSWORD=your_password
set MYSQLPORT=3306
set MYSQLDATABASE=govind
```

**PowerShell example:**

```powershell
$env:MYSQLHOST="localhost"
$env:MYSQLUSER="root"
$env:MYSQLPASSWORD="your_password"
$env:MYSQLPORT="3306"
$env:MYSQLDATABASE="govind"
```

These commands configure the variables for the current terminal session. Set them again in a new terminal, or use a local environment-management approach that is excluded from version control.

### 5. Create the upload directory

Ensure the following directories exist:

```text
static/photos/
static/medicalphotos/
```

The first is used for administrator photos; the second is referenced by medical-store photo uploads.

### 6. Start the application

```bash
python app.py
```

Open the local address printed by Flask in your browser (typically `http://127.0.0.1:5000/`).

> If your local `app.py` does not contain an `app.run(...)` entry point, start it with:
>
> ```bash
> flask --app app run --debug
> ```

## Configuration

Database configuration is handled by `make_connection()` in `mylib.py`. Update the environment variables to match your MySQL/MariaDB installation.

Before deployment, configure a strong, private Flask secret key using an environment variable and update the application to read it from the environment. The current source contains a hard-coded development secret key.

Also review the password-change routes in `app.py`: they currently create a separate database connection using local hard-coded connection settings rather than the shared environment-based connection helper. Align these routes with `make_connection()` before running the application in a different environment.

## Running Tests

No automated test suite is included in the supplied project. You can manually verify the main workflows:

- Open the home page and search for a medicine that exists in the database.
- Search for a name that does not exist and confirm the no-results message.
- Sign in with a test administrator account and verify the administrator pages.
- Sign in with a test medical-store account and verify the store dashboard.
- Add, edit, view, and delete a test medicine record.
- Test profile and store photo uploads using non-sensitive sample images.
- Confirm that logout clears the session and protected pages require authentication.

Use test accounts and test data only.

## Deployment

A `Procfile` is included with this start command:

```text
web: gunicorn app:app
```

This tells a compatible hosting platform to serve the Flask application using Gunicorn.

For deployment:

1. Provision a MySQL-compatible database.
2. Import the schema and create fresh application accounts.
3. Configure the database environment variables on the hosting platform.
4. Configure a secure Flask secret key.
5. Ensure the photo-upload directories exist and that the application has permission to write to them.
6. Install dependencies and deploy the application.
7. Verify that the database, login, search, and upload workflows work in the deployed environment.

Uploaded files stored on a hosting instance may not persist across redeployments or work reliably across multiple instances. Use persistent/object storage for production deployments.

## Security Notes

**This repository should be treated as a learning project, not a production-ready medical or pharmacy system.** Review the following before making it publicly accessible:

- The supplied SQL dump includes sample login records and personal-looking contact details. Remove or anonymize these records before publishing the repository. Never publish real user data.
- The current login implementation stores and compares passwords as plain text. Use a password-hashing mechanism such as Werkzeug's password hashing utilities.
- Several SQL statements are assembled using string concatenation with form input. Replace them with parameterized queries to reduce SQL-injection risk.
- The Flask secret key is hard-coded in the current source. Load a strong secret from an environment variable.
- Some password-change routes use hard-coded local database connection settings. Use the shared environment-based connection helper instead.
- Add server-side validation for form fields and uploaded files, including file type and size restrictions.
- Review authorization checks on every route that reads or changes account-specific data.
- Use HTTPS and secure session-cookie settings when deploying.
- Do not use this project to make medical decisions. Search results are listings entered into the database and are not medical advice or confirmation of medicine availability.

## Limitations and Future Improvements

Possible next steps for the project include:

- Replace plain-text passwords with secure password hashing.
- Use parameterized SQL queries throughout the application.
- Add search filters for company, price, and medical-store location.
- Add pagination and sorting for large result sets.
- Add medicine availability and stock-quantity tracking.
- Improve form validation and user-friendly error handling.
- Add automated tests for authentication, search, and CRUD workflows.
- Move uploaded images to persistent storage.
- Add database migrations and a documented sample-data setup.
- Improve accessibility, mobile responsiveness, and interface consistency.

## Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes: `git commit -m "Add your feature"`.
4. Push the branch: `git push origin feature/your-feature`.
5. Open a Pull Request describing your changes.

Please do not include passwords, private database credentials, or real personal information in commits.

## Author

**Govind Singh Tanwar**

- GitHub: [@govindsingh00](https://github.com/govindsingh00)
- Project repository: [MedicineFinder](https://github.com/govindsingh00/MedicineFinder)

## License

No license file was present in the supplied project archive. Unless you add a license, the project is not explicitly licensed for reuse, modification, or redistribution. Add a `LICENSE` file if you want to grant others permission to use the code.
