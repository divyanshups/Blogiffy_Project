# Blogiffy 📝

> A blogging platform for learners and educators to share knowledge, insights, and ideas — freely and openly.

---

## 📌 About

Blogiffy is a full-stack blogging web application built with Flask and MySQL. It lets users register, write and manage blog posts by category, personalize their profiles, and engage with a community of knowledge-sharers. The project was developed as part of **Cloud Computing Project** and was deployed on AWS (EC2 + RDS).

---

## 🎯 Features

- **Registration & Authentication** — Sign up with username, email, and password; secure session-based login
- **Blog Creation & Management** — Write posts, select categories, and manage them from your personal dashboard
- **Account Personalization** — Update profile details and preferences at any time
- **Session Management** — Secure logout with automatic redirect to the login page

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, CSS, Jinja2 |
| Backend | Python 3, Flask |
| Database | MySQL |

---

## 🚀 Getting Started (Local Setup)

Follow these steps to run Blogiffy on your local machine.

### Prerequisites

Make sure you have the following installed:

- [Python 3.8+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/)
- [MySQL Server](https://dev.mysql.com/downloads/mysql/) (running locally)

---

### 1. Clone the Repository

```bash
git clone https://github.com/divyanshups/Blogiffy_Project.git
cd Blogiffy_Project
```

---

### 2. Create a Virtual Environment

```bash
# Create the environment
python -m venv venv

# Activate it — macOS/Linux
source venv/bin/activate

# Activate it — Windows
venv\Scripts\activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

> If a `requirements.txt` doesn't exist yet, install the core packages manually:
> ```bash
> pip install flask flask-mysqldb flask-login flask-wtf
> ```

---

### 4. Set Up the MySQL Database

Open your MySQL client (terminal or GUI like MySQL Workbench) and run:

```sql
CREATE DATABASE blogiffy;

USE blogiffy;

-- Users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Blog posts table
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    content TEXT NOT NULL,
    category VARCHAR(100),
    author_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES users(id)
);
```

> **Note:** Adjust the schema to match your actual models if they differ.

---

### 5. Configure Environment Variables

Create a `.env` file in the project root (never commit this file):

```env
SECRET_KEY=your_secret_key_here

MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=your_mysql_password
MYSQL_DB=blogiffy
```

Make sure your Flask app loads these — for example, using `python-dotenv`:

```bash
pip install python-dotenv
```

And in your `app.py` / `config.py`:

```python
from dotenv import load_dotenv
import os

load_dotenv()

app.config['SECRET_KEY'] = os.getenv('SECRET_KEY')
app.config['MYSQL_HOST'] = os.getenv('MYSQL_HOST')
app.config['MYSQL_USER'] = os.getenv('MYSQL_USER')
app.config['MYSQL_PASSWORD'] = os.getenv('MYSQL_PASSWORD')
app.config['MYSQL_DB'] = os.getenv('MYSQL_DB')
```

---

### 6. Run the Application

```bash
python app.py
```

The app will start at **http://127.0.0.1:5000** by default.

Open that URL in your browser to see Blogiffy running locally.

---

## 📁 Project Structure

```
Blogiffy_Project/
├── app.py               # Application entry point
├── config.py            # Configuration and env loading
├── requirements.txt     # Python dependencies
├── .env                 # Environment variables
├── .gitignore
├── static/
│   ├── css/             # Stylesheets
│   └── js/              # JavaScript files
└── templates/
    ├── index.html        # Home / blog feed
    ├── login.html        # Login page
    ├── register.html     # Registration page
    ├── create_blog.html  # Blog creation form
    ├── dashboard.html    # User account dashboard
    └── my_blogs.html     # Manage user's posts
```

> This is a suggested structure — adjust to match your actual layout.
