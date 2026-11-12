# 💊 Medicine Finder

**A Dynamic Web-Based Medicine Management and Search Application**

Medicine Finder is a Python Flask-based web application designed to make medicine-related information easier to manage and access. It provides a platform for medical stores to manage their medicine records and allows users to explore available medical stores and medicine information.

The application includes separate functionality for administrators and medical-store users, with database-backed operations for managing records.

## 🚀 Features

- **User Authentication:** Login and registration functionality.
- **Admin Dashboard:** Manage medical-store information.
- **Medical Store Management:** View and manage registered medical stores.
- **Medicine Management:** Add, view, edit, and delete medicine records.
- **Medicine Information:** Store medicine names, company names, batch numbers, prices, and remarks.
- **Profile Management:** Update user profile information.
- **Profile Photo Upload:** Upload and manage profile pictures.
- **Database Integration:** Store and retrieve application data using MySQL/MariaDB.
- **Session Management:** Maintain user login sessions and role-based access.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Backend programming |
| Flask | Web application framework |
| HTML5 | Web page structure |
| CSS3 | Styling |
| JavaScript | Frontend functionality |
| MySQL / MariaDB | Database management |
| PyMySQL | Python-MySQL connectivity |
| Jinja2 | Dynamic HTML templates |

## 📂 Project Structure

```text
MedicineFinder/
│
├── app.py                  # Main Flask application
├── mylib.py                # Database connection and helper functions
├── medicine finder.sql     # Database structure and sample data
├── requirements.txt        # Python dependencies
├── Procfile                # Deployment configuration
│
├── static/
│   └── photos/             # Uploaded profile photos
│
├── templates/              # HTML templates
│
└── README.md               # Project documentation
```

## ⚙️ Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/govindsingh00/MedicineFinder.git
```

### 2. Navigate to the Project Directory

```bash
cd MedicineFinder
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it:

**Windows:**
```bash
venv\Scripts\activate
```

**Linux / macOS:**
```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install Flask PyMySQL
```

Install any additional dependencies required by your project.

### 5. Configure the Database

- Install MySQL or MariaDB.
- Open MySQL Workbench, phpMyAdmin, or another database management tool.
- Import the `medicine finder.sql` file.
- Configure the database connection environment variables.

Required environment variables:

```env
MYSQLHOST=localhost
MYSQLUSER=root
MYSQLPASSWORD=your_password
MYSQLPORT=3306
MYSQLDATABASE=govind
```

### 6. Run the Application

```bash
python app.py
```

Open your browser and visit:

```text
http://127.0.0.1:5000/
```

## 🗄️ Database

The application uses MySQL/MariaDB for storing application information.

The database includes tables for:

- Login information
- Administrator information
- Medical-store information
- Medicine records
- Profile photos
- Other supporting records

The database schema and sample records are provided in `medicine finder.sql`.

## 🔮 Future Enhancements

- Advanced medicine search and filtering.
- Improved user interface and responsive design.
- Medicine availability tracking.
- Medicine expiry-date notifications.
- Improved security and data validation.
- Integration with additional pharmacy services.

## 👨‍💻 Author

**Govind Singh Tanwar**

- GitHub: [@govindsingh00](https://github.com/govindsingh00)
- LinkedIn: [Govind Singh Tanwar](https://linkedin.com/in/govindsinghtanwar)

## 📄 License

This project is available for educational and learning purposes. Add an appropriate open-source license if you intend to permit reuse and redistribution.

---

⭐ If you find this project useful, consider giving the repository a star!
