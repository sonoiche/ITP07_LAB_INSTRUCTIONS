# Integrative Programming Lab Activity 2  
### REST API Development with Separate Server (PHP + MySQL + Security)

---

## 📌 Overview
This lab activity focuses on building a **RESTful API backend** using PHP and MySQL on a **separate server** and integrating it with your existing authentication system. You will create API endpoints that allow external applications to **retrieve, create, update, and delete data**, while applying **API security practices** such as token-based authentication.

---

## 🎯 Objectives
By completing this lab, you should be able to:

- Design and develop a RESTful API using PHP
- Handle HTTP methods (GET, POST, PUT, DELETE)
- Return structured JSON responses
- Connect to a MySQL database from an API server
- Implement CRUD operations through API endpoints
- Secure API access using token-based authentication
- Validate and sanitize API inputs
- Integrate API data into your existing PHP application

---

## 🏗️ System Architecture

```
[ Client App (Lab 1 PHP App) ]
            ↓
        (HTTP Request)
            ↓
[ API Server (Separate PHP Project) ]
            ↓
        [ MySQL Database ]
```

---

## 🛠️ Project Structure (API Server)

```
api_server/
│
├── config/
│   └── database.php
│
├── middleware/
│   └── auth.php
│
├── api/
│   └── users.php
│
└── .htaccess (optional for routing)
```

---

## ⚙️ Setup Instructions

### 1. Create a Separate Project Folder

Inside `htdocs`, create:

```
api_server/
```

---

### 2. Create the Database Table

```sql
CREATE TABLE api_data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### 3. Configure Database Connection

```php
$conn = new PDO("mysql:host=localhost;dbname=integrative_db", "root", "");
$conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

---

## 🔐 API Security (Token-Based Authentication)

```php
$valid_token = "SECRET123";

$headers = getallheaders();

if (!isset($headers['Authorization']) || $headers['Authorization'] !== $valid_token) {
    http_response_code(401);
    echo json_encode(["message" => "Unauthorized"]);
    exit;
}
```

All requests must include:

```
Authorization: SECRET123
```

---

## 🔄 API Endpoints

### GET
```
GET /api/users.php
```

### POST
```
POST /api/users.php
```

### PUT
```
PUT /api/users.php?id=1
```

### DELETE
```
DELETE /api/users.php?id=1
```

---

## 🧠 Handling HTTP Methods

```php
$method = $_SERVER['REQUEST_METHOD'];

switch ($method) {
    case 'GET':
        break;
    case 'POST':
        break;
    case 'PUT':
        break;
    case 'DELETE':
        break;
}
```

---

## 🔒 Best Practices

- Use prepared statements
- Sanitize inputs
- Return proper HTTP status codes
- Always return JSON responses

---

## 🔗 Integration with Lab Activity 1

```php
$response = file_get_contents("http://localhost/api_server/api/users.php");

$data = json_decode($response, true);
```

---

## 🧪 Testing Checklist

- Unauthorized access test
- CRUD operations test
- Input validation test

---

## 📦 Expected Output

- Working REST API
- Secure endpoints
- Integrated frontend (Lab 1)

---

## 📄 Deliverable

Submit a ZIP file containing:
- API source code
- SQL file
- README.md
- Screenshots

---

## 👨‍💻 Academic Integrity

Ensure your work is original. Use this as a guide only.
