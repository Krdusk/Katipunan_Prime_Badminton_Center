# Katipunan Prime Badminton Center Website Setup Guide (WAMP)
Foll
ow these steps to deploy the Katipunan Prime Badminton Center Booking system on your local machine using WAMP.

## 1. Prerequisites
- WAMP Server (Ensure it is installed and the icon in the taskbar is green)
- Code Editor (e.g., VS Code, Notepad++, or simply Notepad)

## 2. File Structure
In WAMP, the web directory is `www`. Create a folder named `katipunan-prime` inside `C:\wamp64\www\` and organize your files as follows:

C:\wamp64\www\katipunan-prime
├── db.php # Database connection settings
├── index.html # Login/Register page
├── auth.php # Authentication logic (Processes login/register)
├── home.php # Secure landing page (Slideshow)
├── dashboard.php # User booking dashboard
├── transactions.php # Payment history
├── logout.php # Ends the session
└── auth/
└── register.php # Registration processing


## 3. Database Configuration
1. Open phpMyAdmin by visiting `http://localhost/phpmyadmin/` in your browser
2. Login (Default WAMP username is `root`, password is blank)
3. Create a new database named `katipunan_prime_db`
4. Click the SQL tab and paste/run the following code:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    fullname VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    password VARCHAR(255),
    role ENUM('user', 'admin') DEFAULT 'user'
);

CREATE TABLE courts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE bookings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    court_id INT,
    booking_date DATE,
    time_slot VARCHAR(50),
    payment_status ENUM('pending', 'completed') DEFAULT 'pending',
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (court_id) REFERENCES courts(id)
);

CREATE TABLE transactions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    amount DECIMAL(10,2),
    payment_method VARCHAR(50),
    status VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

INSERT INTO courts (name) VALUES ('Court A'), ('Court B'), ('Court C');