# Integrative Programming Lab Activity 1  
### User Registration and Authentication System (PHP + MySQL)

## 📌 Overview
This lab activity focuses on building a basic **User Authentication System** using PHP and MySQL. You will implement user registration, login, session management, and security practices such as password hashing and prepared statements.

---

## 🎯 Objectives
By completing this lab, you should be able to:

- Create and manage a MySQL database (`users` table)
- Connect PHP to MySQL using PDO
- Implement user registration and login functionality
- Securely hash and verify passwords
- Use PHP sessions for authentication
- Apply input validation and prevent SQL injection
- Protect restricted pages from unauthorized access

---

## 🛠️ Project Structure

```
integrative_lab/
│
├── config/
│   └── database.php
│
├── auth/
│   ├── register.php
│   ├── login.php
│   └── logout.php
│
├── dashboard.php
└── index.php
```

---

## ⚙️ Setup Instructions

### 1. Create the Database

```sql
CREATE DATABASE integrative_db;

USE integrative_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### 2. Configure Database Connection

```php
$host = "localhost";
$dbname = "integrative_db";
$username = "root";
$password = "";

try {
    $conn = new PDO("mysql:host=$host;dbname=$dbname", $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $e) {
    die("Database connection failed.");
}
```

---

## 🔐 Features to Implement

### 📝 User Registration
- Input validation (required fields, email format)
- Prevent duplicate email
- Password hashing using `password_hash()`

### 🔑 User Login
- Retrieve user by email
- Verify password using `password_verify()`

### 🧠 Session Management
```php
session_start();
$_SESSION['user_id'] = $user['id'];
```

### 🔒 Protect Pages
```php
if (!isset($_SESSION['user_id'])) {
    header("Location: auth/login.php");
    exit;
}
```

### 🚪 Logout
```php
session_start();
session_destroy();
header("Location: login.php");
exit;
```

---

## 🧪 Testing Checklist
- Empty input fields
- Invalid email format
- Duplicate email registration
- Incorrect login
- Successful login
- Unauthorized access protection
- Logout functionality

---

## 📦 Expected Output
- Functional registration and login
- Protected dashboard
- Secure password storage

---

## 📄 Deliverable
Submit a ZIP file containing:
- PHP source code
- SQL file
- README.md

---

## 👨‍💻 Academic Integrity
Use this as a guide. Ensure your final output is your own work.
