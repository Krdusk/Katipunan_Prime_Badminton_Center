# Katipunan Prime Badminton Center
## Badminton Court Scheduling and Reservation System

Katipunan Prime Badminton Center is a web-based badminton court reservation system designed to simplify court booking for customers while giving administrators full control over court management, reservations, and reporting. The system ensures secure access, role-based dashboards, and conflict-free scheduling.

---

## Table of Contents:
1. [Project Overview](#project-overview)  
2. [Project Members](#project-members)  
3. [System Technologies](#system-technologies)  
4. [System Features](#system-features)  
5. [User Types and Access Control](#user-types-and-access-control)  
6. [Authentication Flow](#authentication-flow)  
7. [Customer Panel](#customer-panel)  
8. [Admin Panel](#admin-panel)  
9. [Database Design](#database-design)  
10. [Database Relationships](#database-relationships)  
11. [Double Booking Prevention](#double-booking-prevention)  
12. [Setup and Installation](#setup-and-installation)  
13. [Project Files](#project-files)

---

## Project Overview:

Katipunan Prime Badminton Center's Badminton Court Scheduling and Reservation System is a centralized platform that allows customers to reserve badminton courts online while enabling administrators to manage courts, reservations, users, and reports efficiently. The system is designed with role-based access control to ensure that users only access features appropriate to their role.

---

## Project Members and Contributions:

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin: 20px 0;">

### Project Head:
<div style="border: 2px solid #4CAF50; border-radius: 10px; padding: 20px; margin: 10px 0; background: linear-gradient(145deg, #ffffff, #f5f5f5); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">

**Castro, James Adrian**
> • Core Modules (Booking, Payment, Login, and Registration) 
> • Backend Logic and Database

</div>

### Development Team:
<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px;">

<div style="border: 2px solid #2196F3; border-radius: 10px; padding: 20px; background: linear-gradient(145deg, #ffffff, #f8f9fa); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">

**Amio, John**
> • Frontend (Profile Design)
> • Backend (Profile Page)

</div>

<div style="border: 2px solid #FF9800; border-radius: 10px; padding: 20px; background: linear-gradient(145deg, #ffffff, #f8f9fa); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">

**Cinco, Michaela**
> • Security Features (Email Encryption and Verification)
> • Backend

</div>

<div style="border: 2px solid #E91E63; border-radius: 10px; padding: 20px; background: linear-gradient(145deg, #ffffff, #f8f9fa); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">

**Santos, Samantha Lui**
> • Full-Stack Development 
> • Database and ERD Design 
> • UI Design
> • Presentation Materials

</div>

<div style="border: 2px solid #9C27B0; border-radius: 10px; padding: 20px; background: linear-gradient(145deg, #ffffff, #f8f9fa); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">

**Tarlac, Carlo Jose**
> • Backend (Admin and Forgot Password Functionality)  
> • ERD

</div>

---

## System Technologies:

The system uses the following technologies:  
- MySQL database for storing user, court, and reservation data.  
- HTML, CSS, and JavaScript for the user interface.  
- Backend logic using PHP.  
- Role-based access control for differentiating administrative and customer access.  

---

## System Features:

The system provides the following features:  
- Online badminton court reservations.  
- Secure user authentication.  
- Role-based dashboards for customers and administrators.  
- Real-time court availability checking.  
- Prevention of double-booking.  
- Administrative management and reporting.  
- Scalable database design.  

---

## User Types and Access Control:

The system has two main classifications of users:

**Customer**  
- Normal system user.  
- Can register and log in.  
- Can reserve badminton courts.  
- Can view and manage only their own reservations.  

**Admin**  
- Business owner or authorized staff.  
- Uses pre-created accounts.  
- Has full access to system management.  
- Can view, approve, and manage all reservations.  

User roles are determined using the `role` field stored in the database.  

---

## Authentication Flow:

The system verifies user roles using the following process:  
1. User logs in using their email address and password.  
2. The backend validates credentials against the Users table.  
3. If login is successful, the system reads the `role` column.  
4. Users are redirected based on their role:  
   - Admin users are directed to the Admin Dashboard.  
   - Customer users are directed to the Customer Dashboard.  

Customers cannot access admin pages even if they know the URL. Admin pages are fully secured through role verification.  

---

## Customer Panel:

**Registration Page**  
- Customers provide their full name, email address, and password.  
- Only customers can register through this page.  

**Login Page**  
- Email address and password.  
- The same login page is used by both customers and administrators.  

**Customer Dashboard**  
- View available badminton courts.  
- Quick access to court reservation.  

**Court Reservation Page**  
- Select a court and reservation date.  
- Select time slot.  
- Confirm reservation.  
- The system checks for time conflicts before confirming.  

**My Reservations Page**  
- View unique reservation ID, court name, date, time, and status.  
- Option to cancel reservation.  
- Customers can only view their own reservations.  

**Logout**  
- Ends the user session securely.  

---

## Admin Panel:

**Admin Dashboard Summary**  
- Total number of courts.  
- Total number of bookings.  
- Pending bookings.  
- Bookings for the current day.  

**Court Management**  
- Add, edit, or disable courts.  

**Reservation Management**  
- View all reservations.  
- Filter reservations by date or court.  
- View customer details.  

**Reports Module**  
- Daily and monthly reservation reports.  
- Revenue summaries.  

**User Management**  
- View all registered users.  

**Logout**  
- Securely ends the admin session.  

---

## Database Design:

**Database Name:** `katipunan_prime_db`  

**Users Table**  
- `id` (Primary Key)  
- `fullname`  
- `email`  
- `password`  
- `role` (admin or user)  

**Courts Table**  
- `id` (Primary Key)  
- `name`  

**Bookings Table**  
- `id` (Primary Key)  
- `user_id` (Foreign Key)  
- `court_id` (Foreign Key)  
- `booking_date`  
- `time_slot`  
- `payment_status`  

**Transactions Table**  
- `id` (Primary Key)  
- `user_id` (Foreign Key)  
- `amount`  
- `payment_method`  
- `status`  
- `created_at`  

---

## Database Relationships:

- One user can have many bookings.  
- One court can have many bookings.  
- One user can have many transactions.  

These relationships ensure data integrity, scalability, and efficient querying.  

---

## Double Booking Prevention:

The system prevents double booking by:  
- Checking court availability for selected time slots.  
- Validating overlapping time slots.  
- Rejecting reservations with scheduling conflicts.  

This guarantees accurate and conflict-free bookings.  

---

## Setup and Installation:

1. Clone the repository:
```bash
git clone <repository-url>
```

--- 

## Project Files:

All project materials, documentation, and media files are available in the Google Drive folder:

🔗 **[Click here to access project files](https://drive.google.com/drive/folders/1Xmlb_KAfOpZAlQC8_ktDsLDP2O8uB7Vb)**
