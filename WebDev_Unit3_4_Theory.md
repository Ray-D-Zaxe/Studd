# Web Development Master's Syllabus - Final Exam Study Guide
## With Detailed Code Explanations & Theoretical Concepts

---

## UNIT III: PHP and MySQL

### **THEORETICAL CONCEPTS - UNIT III**

#### **What is PHP?**
**Definition**: PHP (Hypertext Preprocessor) is a server-side scripting language used to create dynamic web pages and web applications.

**How PHP Works**:
1. User requests a PHP file from web server (e.g., `www.example.com/index.php`)
2. Server receives request
3. Server executes PHP code (all processing happens on server)
4. PHP generates HTML/output based on logic
5. Server sends only HTML output to user's browser
6. Browser displays HTML (user never sees PHP code)

**Key Principle**: PHP code is NEVER sent to browser. Browser only sees the output (HTML).

**Why Server-Side Processing?**:
- **Security**: PHP code hidden from users (passwords, database logic protected)
- **Database Access**: Can connect to database on server
- **File System**: Can read/write files on server
- **Business Logic**: Complex computations on powerful server
- **Consistency**: Same behavior for all users regardless of browser

---

#### **Server-Side vs Client-Side Programming**

**Client-Side (JavaScript)**:
- Code executes in user's browser
- Source code visible to all users
- Access to: DOM, cookies, local storage, browser APIs
- NO access to: Database, server files, system resources
- Security Risk: User can modify JavaScript (no protection for sensitive logic)
- Use for: Form validation, UI animations, interactivity

**Server-Side (PHP)**:
- Code executes on web server machine
- Source code HIDDEN from users
- Access to: Database, files, server system, sensitive data
- NO direct access to: User's computer (can't access their hard drive)
- Secure: Logic/database credentials protected
- Use for: Authentication, database operations, business logic

**Example - User Login**:
```
JavaScript approach (INSECURE):
1. User enters username/password in form
2. JavaScript checks if "admin" == "admin" (code visible in browser)
3. Anyone can open browser console and modify this check
4. Someone can trick it to login without correct password

PHP approach (SECURE):
1. User enters username/password in form
2. JavaScript sends data to server via AJAX
3. Server (PHP) receives data
4. PHP queries database to verify credentials (code not visible)
5. Database only stores hashed passwords
6. Server sends response: "Login successful" or "Login failed"
7. Only server knows the actual passwords, users can't see verification logic
```

---

#### **Web Server Architecture**

**Three-Layer Web Architecture**:

1. **Presentation Layer (Client-Side)**:
   - HTML (structure)
   - CSS (styling)
   - JavaScript (interactivity)
   - Runs in browser
   - User can see/modify

2. **Application Layer (Server-Side)**:
   - PHP (business logic)
   - Server-side scripts
   - Authentication/authorization
   - Request processing
   - Hidden from user

3. **Data Layer (Backend)**:
   - MySQL database
   - Data persistence
   - Server-side storage
   - User cannot access directly

**Request-Response Cycle**:
```
Browser                           Server                    Database
  |                                 |                          |
  |---1. HTTP Request-------------->|                          |
  |   (GET /users.php?id=5)          |                          |
  |                                 |---2. Authenticate--------|
  |                                 |    (Check user login)   |
  |                                 |<--3. User Valid---------|
  |                                 |                          |
  |                                 |---4. Query--------+      |
  |                                 |    (SELECT *       |
  |                                 |     FROM users     |
  |                                 |     WHERE id=5)    |
  |                                 |<--5. Data---------+
  |                                 |    (user details)
  |                                 |
  |                                 |--6. Generate HTML---+
  |                                 |    (Process PHP)   |
  |                                 |
  |<--7. HTTP Response-------------|
  |   (200 OK + HTML)
  |
  |--8. Render Page-----+
  |   (Browser displays)|
  +----Display to user--+
```

---

#### **Database Concepts - Relational Databases**

**What is MySQL?**
- Relational Database Management System (RDBMS)
- Organizes data in structured tables (rows and columns)
- Fast queries using indexes
- ACID compliance (data integrity)
- Most widely used open-source database

**Database Structure**:
```
Database Structure:
mydb (Database)
├── Table: users
│   ├── Columns (Schema):
│   │   ├── id (Primary Key, Auto-increment)
│   │   ├── username (Unique)
│   │   ├── email (Unique)
│   │   ├── password (Hashed)
│   │   ├── created_at (Timestamp)
│   │
│   └── Rows (Data):
│       ├── [1, 'john', 'john@email.com', '$2y$10$...hashed', '2024-01-15']
│       ├── [2, 'jane', 'jane@email.com', '$2y$10$...hashed', '2024-01-16']
│       └── [3, 'bob', 'bob@email.com', '$2y$10$...hashed', '2024-01-17']
│
├── Table: products
│   ├── Columns: id, name, price, category, stock
│   └── Rows: [1, 'Laptop', 999.99, 'Electronics', 50]
│
└── Table: orders
    ├── Columns: id, user_id (Foreign Key), product_id (FK), quantity, order_date
    └── Rows: [1, 1, 1, 2, '2024-01-18']
```

**Key Concepts**:
- **Table**: Collection of related data (e.g., users table stores all user records)
- **Row**: Single record (e.g., one user's information)
- **Column**: Field type (e.g., username, email)
- **Primary Key**: Unique identifier for each row (e.g., user ID)
- **Foreign Key**: Reference to another table's primary key (links data between tables)
- **Index**: Speed up queries (like book index for quick lookup)

**Why Databases?**:
- **Persistence**: Data survives server restart
- **Scalability**: Handle millions of records efficiently
- **Security**: Control who accesses what data
- **Integrity**: Ensure data accuracy (constraints, validations)
- **Concurrency**: Multiple users simultaneously

---

#### **SQL (Structured Query Language) Fundamentals**

**Definition**: Universal language for communicating with databases

**CRUD Operations**:
1. **CREATE (INSERT)**: Add new records to table
2. **READ (SELECT)**: Retrieve/query data
3. **UPDATE**: Modify existing records
4. **DELETE**: Remove records

**Basic Examples**:
```sql
-- CREATE: Insert new user
INSERT INTO users (username, email, password) 
VALUES ('john', 'john@email.com', SHA2('password123', 256));

-- READ: Get all users
SELECT * FROM users;

-- READ: Get specific user
SELECT id, username, email FROM users WHERE id = 1;

-- READ: Multiple conditions
SELECT * FROM users WHERE age > 18 AND country = 'USA';

-- UPDATE: Modify user
UPDATE users SET email = 'newemail@email.com' WHERE id = 1;

-- DELETE: Remove user
DELETE FROM users WHERE id = 5;
```

**WHERE Clause Operators**:
- `=`: Equal to
- `!=` or `<>`: Not equal to
- `>`: Greater than
- `<`: Less than
- `LIKE`: Pattern matching (% = any characters)
- `IN`: Match any in list
- `BETWEEN`: Range of values
- `AND`: Both conditions true
- `OR`: Either condition true

---

#### **SQL Joins - Combining Data from Multiple Tables**

**Why Joins?**
- Databases split data into multiple tables (normalization)
- Reduces redundancy (don't repeat data)
- Relationships connect tables
- Joins retrieve related data from multiple tables

**Types of Joins**:

**INNER JOIN**: Only matching records from both tables
```sql
SELECT users.name, orders.product 
FROM users 
INNER JOIN orders ON users.id = orders.user_id;

Result: Only users who have orders
┌──────────┬──────────┐
│ name     │ product  │
├──────────┼──────────┤
│ John     │ Laptop   │
│ Jane     │ Mouse    │
│ John     │ Monitor  │
└──────────┴──────────┘
(Bob has no orders, so not included)
```

**LEFT JOIN**: All from left table + matching from right
```sql
SELECT users.name, orders.product 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id;

Result: All users, with orders if they have them
┌──────────┬──────────┐
│ name     │ product  │
├──────────┼──────────┤
│ John     │ Laptop   │
│ Jane     │ Mouse    │
│ John     │ Monitor  │
│ Bob      │ NULL     │   (Bob has no orders)
└──────────┴──────────┘
```

**RIGHT JOIN**: All from right table + matching from left
```sql
SELECT users.name, orders.product 
FROM users 
RIGHT JOIN orders ON users.id = orders.user_id;

Result: All orders, even if user doesn't exist
(Rare in practice - usually means data integrity issues)
```

**FULL JOIN / UNION**: All records from both tables
```sql
SELECT users.name, orders.product 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id
UNION
SELECT users.name, orders.product 
FROM users 
RIGHT JOIN orders ON users.id = orders.user_id;

Result: All users AND all orders
```

**SELF JOIN**: Join table with itself
```sql
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.id;

Result: Each employee with their manager's name
┌──────────┬──────────┐
│ employee │ manager  │
├──────────┼──────────┤
│ John     │ Alice    │
│ Jane     │ Bob      │
│ Bob      │ Alice    │
└──────────┴──────────┘
```

**CROSS JOIN**: Cartesian product (all combinations)
```sql
SELECT * FROM sizes CROSS JOIN colors;
-- If sizes = [S, M, L] and colors = [Red, Blue]
-- Result: 3 × 2 = 6 combinations
-- (S-Red, S-Blue, M-Red, M-Blue, L-Red, L-Blue)
```

---

#### **Security in PHP - SQL Injection**

**SQL Injection Attack**:
```php
// VULNERABLE CODE - NEVER DO THIS
$id = $_GET['id'];  // User enters: 1' OR '1'='1
$query = "SELECT * FROM users WHERE id = " . $id;
// Query becomes: SELECT * FROM users WHERE id = 1' OR '1'='1
// This returns ALL users because '1'='1' is always true!
```

**Why It's Dangerous**:
```php
// Example: User login attack
$username = $_POST['username'];  // User enters: admin' --
$password = $_POST['password'];  // (anything)

// Vulnerable code
$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
// Query becomes: SELECT * FROM users WHERE username = 'admin' -- AND password = '...'
// The -- comments out the password check! Anyone logs in as admin!
```

**Solution - Prepared Statements**:
```php
// SECURE CODE - USE THIS
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute([':id' => $id]);
// :id is a placeholder
// $id is bound separately as data (not code)
// No matter what user enters, it's treated as data, not SQL
```

**Why Prepared Statements Work**:
1. SQL structure sent to database first (without data)
2. Database compiles/prepares the SQL
3. Data bound separately
4. Data cannot be interpreted as SQL code
5. Injection attempts treated as literal strings

---

#### **Password Security**

**Never Store Plain Passwords**:
```php
// BAD - stores actual password
$password = "mypassword123";
$sql = "INSERT INTO users (password) VALUES ('$password')";

// If database hacked, passwords exposed!
```

**Hash Passwords Before Storing**:
```php
// GOOD - stores hashed password
$password = "mypassword123";
$hashed = password_hash($password, PASSWORD_BCRYPT);
$sql = "INSERT INTO users (password) VALUES (:pwd)";
$stmt->execute([':pwd' => $hashed]);

// Hash: $2y$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcg7b3W9Dkhuyt3don7ZLBo4sDm
// Original password unrecoverable
// Even if hacked, attacker sees only hash

// To verify login:
$hash_from_db = // retrieve from database
if (password_verify($input_password, $hash_from_db)) {
    // Password correct
} else {
    // Password incorrect
}
```

**Why Hashing?**:
- One-way: Cannot reverse hash to get original password
- Salted: Extra random data added, same password creates different hashes
- Slow: Takes time to compute (slows down brute force attacks)
- Only way to verify: Hash input and compare with stored hash

---

#### **Sessions vs Cookies - Security Model**

**Cookies - Vulnerable to Tampering**:
```php
// Set cookie
setcookie("user_role", "admin", time() + 3600);

// Problem: User can:
// 1. Edit cookie in browser
// 2. Change "admin" to "superadmin"
// 3. Browser sends modified cookie
// 4. Your code trusts the cookie value
// 5. User becomes "superadmin"

// NEVER store sensitive data in cookies!
```

**Sessions - Server Controls Data**:
```php
// Start session
session_start();

// Store sensitive data
$_SESSION['user_id'] = 123;
$_SESSION['user_role'] = 'admin';
$_SESSION['is_logged_in'] = true;

// Only session ID stored in cookie
// Session data stays on server
// User cannot modify session data (data not in their browser)

// Verification on each request:
if (isset($_SESSION['user_id'])) {
    // User logged in (verified on server)
} else {
    // Not logged in
}
```

**Session Security Flow**:
```
1. User logs in with credentials
2. PHP verifies against database
3. PHP creates session: $_SESSION['user_id'] = 123
4. Server assigns session ID: abc123def456
5. Session ID sent in cookie to browser
6. Browser stores cookie (can't see $_SESSION data)
7. User visits next page
8. Browser sends session ID cookie
9. PHP uses ID to retrieve $_SESSION data from server
10. User recognized as logged in
11. Session expires after timeout or user logout
```

---

### **PHP Introduction - Practical**

#### **Installation and Configuration**
- Download from **php.net**
- Install XAMPP/WAMP/LAMP stack (bundles PHP, MySQL, Apache)
- Configure `php.ini` file (server settings)
- Restart Apache server
- Test: Create `info.php` with `<?php phpinfo(); ?>` and view in browser

